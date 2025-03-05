# Deposit Services - Next Steps / Institution Configuration

It is important to understand that the Deposit Service is not overly prescriptive. When PASS was developed, we did not
have a set of requirements for supporting a wide range of repositories, but we acknowledged that possibility existed. So
a balance was struck with the Deposit Service APIs: if they were over-specified, there may be use cases or repositories
that couldn't be accommodated later. If they were under-specified, then Deposit Services wouldn't be able to provide
value by sharing implementations or behaviors between repositories.

Since an exhaustive analysis of repository interfaces was impractical at the time, the idea was to provide general
interfaces that could accommodate almost any scenario. As more use cases, patterns, or abstractions were revealed (by
onboarding new institutions) they could be formalized (e.g. as Java interfaces).

Therefore, supporting new repositories or use cases requires novel code to be developed.

## Supporting a New Repository

### High Level Requirements

In order to support a new downstream repository (e.g. Dataverse, Islandora), there are four high-level requirements to
negotiate:

1. Repository protocol: the protocol used to transmit the bytes to the repository (e.g., SFTP, HTTP).
2. Custody transfer: mechanism used to determine whether a successful custody transfer took place.
3. Package spec: governs physical characteristics of the package (structure, pathing, naming), and required or optional
   metadata (e.g., NIH bulk package spec, BagIT).
4. Metadata mapping: maps elements of the PASS model to package metadata elements.

The philosophy of the Deposit Service is that these requirements are a negotiation. This is for a few reasons:

* PASS does not want to prescribe or dictate to a downstream repository what it must accept.
* Network effects are not in PASS's favor. A popular repository like DSpace is unlikely to change its package
  specifications to accommodate limitations in PASS.
* Requirements to accommodate limitations in PASS.

In order to satisfy their workflows, institutions will place requirements on packages, especially the metadata contained
in the package. Universities, the NIH, or the NSF are not going to change their package requirements to conform with 
PASS.

### Rationale for Packages

The package-oriented nature of the Deposit Service is the preferred way to send the files for a deposit. Sending a set
of files in a single archive is the most predictable transport approach for completing the transfer of custody. 

_It is also possible to send each file separately if the integration requires it, but the DS transport implementation 
must handle failure cases._ For example, if there is a failure in the middle of sending a set of file to the repository, 
when DS retries the failed Deposit, the transport needs to ensure the Deposit in the repository is in a "good state" 
before starting the transfer again.

### Interface Overview

If implementing a new repository the following interfaces will need to be implemented:

* Implementation of Assembler API
* Implementation of PackageProvider API
* Implementation of Transport API

### Downstream Requirements

If the downstream repository integration is receiving a single package, it must:

* Unpack the package,
* interpret its content,
* map it to the native repository model,
* and store the bytes of each file.

Ideally a downstream repository will have some mechanism to determine and expose the status of custody transfer (i.e. a
package has been accepted or rejected), but that is not a strict requirement. PASS will still function even if the
downstream repo doesn't expose the status of a deposit attempt.

If the downstream repository integration is receiving files separately, it is up to the DS Transport implementation to
make the appropriate calls as the repository API specifies.

### Repository Protocol

The repository protocol is primarily implemented by the Deposit Service Transport API. The Transport API is responsible
for using a given protocol to connect to the downstream repository, initiate a transfer of bytes (the package), and
interpret the response for success or failure. In some cases, the response carries valuable information that must be
persisted.

The transport implementation is also responsible for indicating the location of the package, e.g. the folder (SFTP) or
collection the package will be transferred to within the downstream repository. These transport hints are
supplied as key-value pairs to the underlying implementation.

If the repository protocol is DSpace API, SFTP, or InvenioRDM the existing implementation may be reused, otherwise write 
your own.

If the repository has a use case that is not handled by an existing implementation, it might be accommodated by
supporting new transport hints for an existing implementation rather than writing a novel implementation. Supporting an
additional transport hint involves:

* Adding and documenting the hint in the appropriate class.
* New logic to implement hint behavior.
* Writing tests for the new behavior.

### Custody Transfer

Determining the status of custody transfer depends on the transport.  For DSpace API and InvenioRDM transports, if the
deposit logic completes successfully, the custody transfer is considered completed.  For NIHMS transport, the NIHMS 
repository workflow is a long workflow taking several days to complete.  The `NihmsReceiveMailService` reads emails 
from NIHMS with status updates for deposits made to NIHMS and updates the associated Deposit accordingly. 
`NihmsReceiveMailService` is a job that runs on a periodic basis.

In the future, if the DSpace API or InvenioRDM transports require Deposit status updates after the initial deposit, it 
is recommended to use a factory pattern to implement the needed logic to get the deposit status from the downstream
repository. This logic could be added to the `DepositUpdater` that is already invoked from a job to retry failed
Deposits.

If the downstream repository rejects custody of the package, the only recourse is for the end user to perform another
submission that addresses the reason(s) for the rejection. The reasons for rejecting a package may not be communicated.

In practice, a faculty member would need to:
1. understand that their submission has been rejected
2. know who to reach out to, e.g. a support interface or phone number
3. work with PASS support staff to initiate a new submission that addresses the reasons for rejection

PASS support staff would need to comb through logs, contact the downstream repository administrator, or take other
action to determine the cause of the rejection.  PASS has no support for remediating submissions that failed because
the downstream repository workflow rejected it.

### Package Specification

For implementations of the DS `Assembler` and `Package Provider API`, if the packaging spec is NIHMS or BagIT, reuse
existing implementations. If the packaging spec is DSpace METS, reuse existing implementation, and provide a metadata
mapping in a package provider. If a new specification is being supported, write a new implementation of the `Assembler`,
using shared implementations like `AbstractAssembler` and `ArchivingPackageStream`.

Concrete subclasses of `AbstractAssembler` are responsible for implementing the `PackageProvider` interface.

The complexity of creating a stream is encapsulated in `ArchivingPackageStream`, which is shared across all Assemblers
that produce a single archive file. They allow for the generation of packages for BagIt, DSpace METS, NIHMS, along with
simple package formats used for integration tests.

#### Important Concepts in the Assembler API:

* Custodial content: content supplied by the end user in a PASS Submission; these are PASS File entities.
* Supplemental files: not to be confused with the PASS File role option of the same name; these are files that are
  generated by the Assembler, usually to comply with a package specification. E.g. a manifest of files and their
  checksums, or a file containing metadata for the package. End users do not upload supplemental files. They are 
  supplied by the Assembler implementation.
* Package Provider (discussed in the next topic): responsible for producing the supplemental files included in a package
* Packages are streams, and are designed to be relatively performant. For example, a client of the Assembler API can 
  open a PackageStream and begin reading from it right away, and the stream won't block as long as the implementation 
  continues to supply bytes.

#### Important Abstractions in the Assembler API

* `Resource` and `ResourceBuilder`: A Resource carries metadata about an individual file in a package: its size, media type,
  file name, and checksums. The ResourceBuilder allows a Resource to be built as the PackageStream is written, and
  different components may contribute to a Resource during this process. For example, one component determines the
  media type of `Resource` and must be invoked at the beginning of streaming the resource (typically the first 
  512 bytes are used). Another component may be invoked after streaming the resource to calculate its checksum. The
  ResourceBuilder allows different components to contribute to the Resource state without sharing the concrete
  implementation.
* `MetadataBuilder` and `Metadata`: Metadata and MetadataBuilder are similar to Resource and ResourceBuilder, except 
that they provide for the package metadata, as opposed to individual files within the package.
* `StreamWriter` and `DefaultStreamWriterImpl`: Uses the factory pattern to instantiate a new `ResourceBuilder` for each 
resource being streamed. The `DefaultStreamWriterImpl` is responsible for handling the process of writing and packaging 
the files associated with a `DepositSubmission`, and is one implementation of the `StreamWriter`. If you need to support
a new packaging format that `DefaultStreamWriterImpl` doesn't handle (e.g., a different type of archive format or a 
custom packaging scheme), creating a new class that implements `StreamWriter` would be a preferred method to add 
different behavior to streaming resources.

#### Metadata Mapping

Implementation of the Deposit Service Package Provider API. Specifically the generation of Supplemental Resources;
metadata files that are generated by the Deposit Service, not submitted by the end user. Examples of supplemental
resources include:
* BagIt
  * bagit.txt: a required file in BagIt packages identifying its version and encoding
  * manifests: a required file in BagIt packages listing the contents and their checksum
  * bag-info.txt: an optional file in BagIt (though often required by institutional profiles) that provides descriptive
      metadata about the package; this is the volatile section of BagIt