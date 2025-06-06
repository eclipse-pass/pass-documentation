## Release v2.2.0
### Date: May 28, 2025

Release Manager: Jared Galanis, JHU

This release includes a refactoring of the way metadata schemas are processed and handled in pass-ui. This was a broad refactor that improved and simplified metadata state management and processing in pass-ui, replaced an outdated library (alpaca.js) in pass-ui that previously handled metadata forms with a more modern JavaScript library (survey.js), and moved the metadata schema service from pass-core into pass-ui. This release also removed support for the pass demo site, updating documentation and shutting down AWS resources that served the demo site. This release additionally resolved intermittent failures in  pass-acceptance-testing CI runs and improved the documentation around the release process itself. During this release cycle the team also investigated and supported the migration from Sonatype OSSRH (being deprecated at the end of June) to Central Portal for publishing artifacts to Maven central.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/35?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/2.2.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/2.2.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/2.2.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/2.2.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/2.2.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/2.2.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/2.2.0)

## Release v2.1.1
### Date: May 6, 2025

Release Manager: Mark Patton, JHU

This is a patch release to fix a bug viewing the submission details page and fix a bug that prevented submissions with an embargo to DSpace from working.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/37?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/2.1.1)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/2.1.1)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/2.1.1)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/2.1.1)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/2.1.1)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/2.1.1)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/2.1.1)

## Release v2.1.0
### Date: April 30, 2025

Release Manager: Jared Galanis, JHU

This release introduces support in pass-core for Spring Cloud AWS to connect to S3 for reading config files. It also addresses technical debt in pass-support, includes test cleanup, and removes the MD5 checksum option in deposit services. Additionally, it resolves a page reload bug and a submit confirmation bug in pass-ui, along with refactoring the logic for submission file state management. Finally, documentation for SonarQube and JaCoCo has been added in this release.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/34?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/2.1.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/2.1.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/2.1.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/2.1.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/2.1.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/2.1.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/2.1.0)

## Release v2.0.0
### Date: March 27, 2025

Release Manager: Tim Sanders, JHU

This is a major release of PASS, marking the transition from the 1.x series to 2.x. It includes important security updates, new tools for improving code quality, and removed SWORD deposits. A research spike was also conducted to explore removing AlpacaJS. We had our first pull request from an external contributor with the [Pass-Docker InvenioRDM update](https://github.com/eclipse-pass/pass-docker/pull/389)!

Highlights

* Removed SWORD Support: SWORD deposit support has been removed.

* Security Fixes: Updated dependencies identified with CVEs, improving the security posture of the PASS user interface. Strengthened Content Security Policy (CSP) headers to mitigate risks such as cross-site scripting (XSS) and content injection attacks.

* Code Coverage Setup: Configured SonarQube to ingest JaCoCo reports, providing real-time code coverage status checks for pull requests.

* Remove Alpaca Analysis: Investigated the feasibility of removing AlpacaJS from the metadata step, exploring potential improvements and simplifications for dynamic form generation.

Additional Changes

* Bug Fix: Addressed an issue with the proxy search dialog displaying at the top of the page rather than in its intended dialog.
* Cleanup Documentation: Archived out-dated documentation.
* Pass-Docker InvenioRDM: Update InvenioRDM to v12 in local docker environment.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/32?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/2.0.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/2.0.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/2.0.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/2.0.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/2.0.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/2.0.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/2.0.0)

## Release v1.15.0
### Date: February 27, 2025

Release Manager: Mark Patton, JHU

This release adds support for transforming JATS XML abstracts imported from a DOI to HTML for better display in a repository. Dependencies have been updated to address security problems found by an analysis of SBOMs. Fixes were made handling cleanup of test deposits which use the DSpace API.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/30?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.15.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.15.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.15.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.15.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.15.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.15.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/1.15.0)

## Release v1.14.1
### Date: February 12, 2025

Release Manager: Russ Poetker, JHU

This release is a patch release to fix a bug in notification services that was not allowing emails to be sent. This release also contains the new DSpace API transport in deposit services which is the new way to perform deposits into DSpace. The DSpace API transport will eventually replace the SWORD transport for DSpace deposits. Additionally, pass-docker was changed so that test PKI files are generated as needed on startup for the test IDP and InvenioRDM containers.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/31?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.14.1)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.14.1)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.14.1)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.14.1)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.14.1)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.14.1)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/1.14.1)

## Release v1.14.0
### Date: January 29, 2025

Release Manager: Russ Poetker, JHU

This release adds SonarQube Cloud for pass-core, pass-support, and pass-ui for Static Code Analysis to improve code quality and security (badges have been added to each project showing SonarQube Quality Gate status). The pass-core and pass-support projects now produce JaCoCo code coverage metrics. In a near-term future release, code coverage reports will be generated on SonarQube Cloud. The failed deposit retry rule has changed so that a failed deposit is only automatically retried if the target repository was unreachable. The release workflow has been updated to release the pass-documentation project. Various code cleanups and dependency updates have been made to the project.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/29?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.14.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.14.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.14.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.14.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.14.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.14.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/1.14.0)

## Release v1.13.0
### Date: December 9, 2024

Release Manager: Mark Patton, JHU

This release added SBOM creation to our release process. GitHub repository documentation now points to the new documentation site. Various code cleanups and dependency updates have been made to the Java backend. In addition work has started on support for direct deposit with the DSpace REST API.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/28?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.13.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.13.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.13.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.13.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.13.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.13.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/1.13.0)

## Release v1.12.0
### Date: October 31, 2024

Release Manager: Tim Sanders, JHU

With this version, we’ve implemented improvements in security, documentation, and fixed some minor bugs. The DOI service now avoids returning entries that lack a URL, and it provides more reliable functionality for retrieving filenames from URLs. Security enhancements include a review of security alerts, the removal of stack trace outputs on the 404 page, and the elimination of default values from sensitive application properties. Additionally, a new AWS feature allows application properties to be optionally loaded from the AWS SSM Parameter Store. Our documentation revamp is complete and accessible on our [new documentation site](https://docs.eclipse-pass.org)!

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/27?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.12.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.12.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.12.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.12.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.12.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.12.0)
* [pass-documentation](https://github.com/eclipse-pass/pass-documentation/releases/tag/1.12.0)

## Release v1.11.0
### Date: September 30, 2024

Release Manager: Mark Patton, JHU

This release fixed a few small bugs around retrieving and displaying manuscripts associated with a DOI, added the ability to display a failure message from a repository to a user and refreshed the Shibboleth setup of the local development environment. Work on enhancing our documentation and moving it to Gitbook is ongoing.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/26?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.11.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.11.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.11.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.11.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.11.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.11.0)

## Release v1.10.0
### Date: August 28, 2024

Release Manager: Russ Poetker, JHU

This release focused on a new Deposit Services repository integration, NIHMS Data Loader automation, and Release process and Documentation improvements. Deposit services has been enhanced to be able to deposit into InvenioRDM. This can also be tested locally with pass-docker being able to start a local instance of InvenioRDM. There is a new automation available in NIHMS Data Loader for refreshing the NIHMS API Token. We made a change to the pass-core/pass-support releases to align the maven repackage plugin configuration with its latest recommendations. As part of this change, the repackaged jar file is no longer deployed to Maven Central during release. The team continued work on overhauling and improving the existing documentation.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/24?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.10.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.10.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.10.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.10.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.10.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.10.0)

## Release v1.9.1
### Date: August 1, 2024

Release Manager: Russ Poetker, JHU

This release fixes a bug with the layout of some of the pages in the UI.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/25?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.9.1)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.9.1)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.9.1)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.9.1)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.9.1)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.9.1)

## Release v1.9.0
### Date: July 31, 2024

Release Manager: Russ Poetker, JHU

This release focused on improving deployment tests, addressing technical debt, and improving documentation. Deployment tests were updated to make deposits into downstream repositories optional. If a deployment test deposit is made into a downstream DSpace repository, it will be automatically deleted after the test completes. More deprecations in pass-ui were fixed which allowed pass-ui to be upgraded to Ember v5.8. The pass-ui module now uses Embroider and pnpm for building. The team continued work on overhauling the existing documentation.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/23?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.9.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.9.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.9.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.9.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.9.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.9.0)

## Release v1.8.0
### Date: July 1, 2024

Release Manager: Jared Galanis, JHU

This release focused on improving documentation, addressing technical debt, and fixing bugs. CSRF protection was added to several PASS components. An optional InvenioRDM instance was added to pass-docker. Many deprecations that were preventing an upgrade of pass-ui to Ember v5.x were addressed. The IDP configuration was reworked to be loaded more dynamically via a url instead of a file. The team advanced an overhaul of existing documentation, where many older sources of documentation were reviewed for accuracy, relevance and categorization, and some of which were subsequently synthesized into new forms of documentation.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/22?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.8.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.8.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.8.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.8.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.8.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.8.0)

## Release v1.7.0
### Date: May 30, 2024

Release Manager: Russ Poetker, JHU

This release focused on adding a GitHub workflow that will complete the release of all PASS components. The pass-core metadata schema service was changed as a first step in supporting InvenioRDM integration. There were several documentation tasks completed such as a Review Manual, Style Guide, and first round of reviews. There has been steps made to eventually add IaC for PASS. OpenTofu has been selected as the IaC tool; developing the terraform modules is in progress. A few smaller bugs were also fixed.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/21?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.7.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.7.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.7.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.7.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.7.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.7.0)

## Release v1.6.1
### Date: May 7, 2024

Release Manager: Mark Patton, JHU

This release fixes a bug which may prevent login and tweaks timeouts for monitoring NIHMS email.

Tickets Completed:
* [930](https://github.com/eclipse-pass/main/issues/930)
* [974](https://github.com/eclipse-pass/main/issues/974)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.6.1)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.6.1)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.6.1)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.6.1)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.6.1)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.6.1)

## Release v1.6.0
### Date: April 30, 2024

Release Manager: Mark Patton, JHU

This release focused on simplifying authentication support, writing documentation to make collaboration easier, and automated testing against a live PASS instance. The pass-core component took over the responsibility for authentication and mediating access to pass-ui resources. This allowed us to remove the no longer needed pass-auth component. The deposit services now also cleanup after the new automated tests.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/20?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.6.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.6.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.6.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.6.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.6.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.6.0)

## Release v1.5.0
### Date: March 28, 2024

Release Manager: Timothy Sanders, JHU

This release focused on use cases for the planned Admin UI, documentation for the PASS Welcome Guide, and enhancements to the grant and nihms data loaders. We added updated parameters to the nihms loader for scheduled environments, and revised the nihms email processing. The grant loader had updates to its aggregation rules, CSV ingest, and extended test coverage. We simplified our CI/CD pipeline by creating a single action to deploy all PASS components to a specified environment. Began consolidating the authentication process to integrate Spring Security into pass-core, enhancing flexibility and security.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/19?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.5.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.5.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.5.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.5.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.5.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/1.5.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.5.0)

## Release v1.4.0
### Date: February 28, 2024

Release Manager: Russ Poetker, JHU

This release focused on updating dependency versions and enforcing clean dependency management in the PASS backend repositories. The required configuration architecture was simplified for the nihms and grant data loaders by making these Spring applications. We began working on a new documentation repository supported by GitBook, more to come on this in the near future. We improved the file delete action on the UI by deleting such files from the backend.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/18?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.4.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.4.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.4.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.4.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.4.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/1.4.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.4.0)

## Release v1.3.0
### Date: January 31, 2024

Release Manager: Mark Patton, JHU

This release focused on updating the interactions with NIHMS. A service was added to handle email messages from NIHMS about submission status. We made GitHub actions for Java snapshot and release builds consistent and more robust. We switched the grant loader to a CSV format which will make it easier to import grant data from other systems. For the UI, we improved the accessibility of the UI and the interaction with external links in the workflow.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/17?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.3.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.3.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.3.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.3.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.3.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/1.3.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.3.0)

## Release v1.2.0
### Date: November 30, 2023

Release Manager: Timothy Sanders, JHU

This release focused on increasing the security of PASS and making interactions with external services more robust, notably the interface with NIHMS. Parameterized queries were added to the grant loader to enhance security. We've made substantial upgrades to the NIHMS data transfer within our Deposit Services and enhancements to the NIHMS loader. Updates were made to the data model documentation and client-side pagination support has been added in the UI.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/16?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.2.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.2.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.2.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.2.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.2.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/1.2.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.2.0)

## Release v1.1.0
### Date: October 26, 2023

Release Manager: Mark Patton, JHU

This release focused on getting PASS ready for deployment in production. We did a great deal of testing of the user interface, backend services, and interactions with repositories. We found and fixed a large number of bugs. We significantly improved the performance of grant loading. We made accessibility improvements to the user interface.  In addition, we added support for depositing to repositories without requiring a journal be entered by the user.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/15?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.1.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.1.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.1.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.1.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.1.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/1.1.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.1.0)

## Release v1.0.0
### Date: September 29, 2023

Release Manager: Jared Galanis, JHU

This release focused on setting up a PASS for production readiness. We resolved a large number of bugs in the user interface and the API / backend services. We added optimistic locking to Submission and Deposit entities to ensure more expected behavior when users edit a shared resource. We also did work on tooling for data migration and remediation.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/12?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/1.0.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/1.0.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/1.0.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/1.0.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/1.0.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/1.0.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/1.0.0)

## Release v0.9.0
### Date: August 30, 2023

Release Manager: John Abrahams, JHU

This release focused on setting up a staging environment for the PASS application. We deployed PASS to the new environment, integrated single sign-on and the data loaders, and fixed a number of bugs that were discovered in the refactored codebase.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/13?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.9.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.9.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.9.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.9.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.9.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.9.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.9.0)

## Release v0.8.0
### Date: July 28, 2023

Release Manager: Mark Patton, JHU

This release introduces updated Java implementations of pass-deposit-services. All of the major functionality of PASS has now been ported to the new framework. In addition more testing was added to the pass-core file service and support for the file service was added to pass-data-client.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/11?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.8.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.8.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.8.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.8.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.8.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.8.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.8.0)

Release Manager: Mark Patton, JHU

## Release v0.7.0
### Date: June 29, 2023

Release Managers: Christopher Shannon, JHU and Russell Poetker, JHU

This release introduces updated java implementations of the pass-nihms-loader and pass-notification-services projects. This release also introduces support for sending submission and deposit JMS message from pass-core, adds access control to the file-service, removes pass-ui-public from pass-docker, and cleans up the SAML configuration in pass-auth.

[Tickets Completed](https://github.com/eclipse-pass/main/milestone/10?closed=1)

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.7.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.7.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.7.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.7.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.7.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.7.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.7.0)

## Release v0.6.0
### Date: May 31, 2023

Release Manager: Jared Galanis, JHU

This release introduces java implementations of the pass-journal-loader, pass-grant-loader and submission status service. This release also introduces support for user token authentication, updates to use of Java 17 in several repositories, converts pass-auth to TypeScript, integrates the user interface with the API for the policy service, introduces a simplified branding strategy along with default branding fallbacks to enable organization specific look and feel, and provides an action for publishing to an AWS SNS (Simple Notification Service) topic to facilitate deploying to AWS infrastructure.

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.6.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.6.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.6.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.6.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.6.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.6.0)
* [pass-ui-public](https://github.com/eclipse-pass/pass-ui-public/releases/tag/0.6.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.6.0)

## Release v0.5.0
### Date: April 27, 2023

Release Manager: Timothy Sanders, JHU

This release introduces the Metadata Schema Service and the Policy Service API. The Metadata Schema Service provides JSON schemas for repository metadata requirements.
The Policy Service API determines the policies applicable to a given Submission, as well as the repositories that a Submission must be deposited into.
Release Automation has been expanded to include [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing) and [pass-docker](https://github.com/eclipse-pass/pass-docker).

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.5.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.5.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.5.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.5.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.5.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.5.0)
* [pass-ui-public](https://github.com/eclipse-pass/pass-ui-public/releases/tag/0.5.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.5.0)

## Release v0.4.0
### Date: March 30, 2023

Release Managers: John Abrahams, JHU and Christopher Shannon, JHU

This release introduces a new user service and access control. The release also upgraded ember to the latest LTS Ember 4.

* Updated Ember packages and 3rd party dependencies
* Fixed styling post Ember 4 upgrade
* Introduces User Service Integration
* Introduces Access Control
* Standardized the entrypoint of dockerfiles to point at an entrypoint.sh file

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.4.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.4.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.4.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.4.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.4.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.4.0)
* [pass-ui-public](https://github.com/eclipse-pass/pass-ui-public/releases/tag/0.4.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.4.0)

## Release v0.3.0
### Date: February 28, 2023

Release Manager: John Abrahams, JHU

This release introduces a new file handling service for dealing with file uploads in PASS. Releases are now largely automated using GitHub workflows.

* Release automations using GitHub workflows. Snapshot versions are published automatically and releases can be triggered manually in the GitHub UI
* Add file API to pass-core for handling file related create, read, and delete operations
* Add service to pass-core to look for publicly available manuscripts for a given DOI

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.3.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.3.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.3.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.3.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.3.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/0.3.0)
* [pass-ui-public](https://github.com/eclipse-pass/pass-ui-public/releases/tag/0.3.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.3.0)

## Release v0.2.0
### Date: January 18, 2023

Release Manager: Jim Martino, JHU

Release 0.2.0 provides a major upgrade to the backend architecture of the PASS application.
The Fedora Repository has been replaced with a completely new REST API built using Elide and backed by
Postgres. This change allows the PASS API to be tailored more directly to the purposes of the PASS
application, provides considerable performance enhancements, and reduces maintenance burden.
The structure of the projects making up the PASS application have also been streamlined to simplify
release and deployment procedures. These changes require updates to be made across the application,
such as replacing all uses of the Fedora API within PASS with calls to the new API. For 0.2.0,
this work is completed sufficiently to provide a demonstration of PASS application capabilities,
but certain parts of the application are currently mocked. Full functionality
will be restored in a future release.

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.2.0)
* [pass-core](https://github.com/eclipse-pass/pass-core/releases/tag/0.2.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.2.0)
* [pass-acceptance-testing](https://github.com/eclipse-pass/pass-acceptance-testing/releases/tag/0.2.0)
* [pass-support](https://github.com/eclipse-pass/pass-support/releases/tag/0.2.0)
* [pass-auth](https://github.com/eclipse-pass/pass-auth/releases/tag/v0.2.0)
* [pass-ui-public](https://github.com/eclipse-pass/pass-ui-public/releases/tag/v0.2.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/0.2.0)

Some major changes for v0.2.0 are:

* Replacement of Fedora storage with Elide / postgres.
* Creation of a pass-core repository which contains REST services previously in separate projects/images
* Elimination of functionality written in Go in previous releases. These have
either been implemented in Java or eliminated
* Refactoring of authorization functionality in javascript closer to the UI

## Release v0.1.0
### Date: August 3, 2022

Release Manager: John Abrahams, JHU

This is the initial release of the Eclipse PASS codebase. The following changes were made to the code after completing the transition to Eclipse:

Naming changes - updating code to transition to the Eclipse PASS name
Version alignment - ensuring all project components utilize a consistent versioning scheme
Data model alignment - ensuring all project components utilize the same version of the data model
Adjustments to release process - updates to allow release of Java components to Maven Central with a new groupId
Introduction of code style guide - ensuring code conforms to consistent guidelines
Adjustments to testing methods - transitioning to the use of GitHub Actions for the execution of unit and integration testing
Initial documentation - providing a starting point for development and deployment documentation

Release Components:
* [main](https://github.com/eclipse-pass/main/releases/tag/0.1.0)
* [pass-ui-public](https://github.com/eclipse-pass/pass-ui-public/releases/tag/v0.1.0)
* [pass-ui](https://github.com/eclipse-pass/pass-ui/releases/tag/v0.1.0)
* [pass-ember-adapter](https://github.com/eclipse-pass/pass-ember-adapter/releases/tag/v0.1.0)
* [pass-java-client](https://github.com/eclipse-pass/pass-java-client/releases/tag/0.1.0)
* [pass-authz](https://github.com/eclipse-pass/pass-authz/releases/tag/0.1.0)
* [pass-deposit-services](https://github.com/eclipse-pass/pass-deposit-services/releases/tag/0.1.0)
* [pass-messaging-support](https://github.com/eclipse-pass/pass-messaging-support/releases/tag/0.1.0)
* [pass-notification-services](https://github.com/eclipse-pass/pass-notification-services/releases/tag/0.1.0)
* [pass-package-providers](https://github.com/eclipse-pass/pass-package-providers/releases/tag/0.1.0)
* [pass-doi-service](https://github.com/eclipse-pass/pass-doi-service/releases/tag/0.1.0)
* [pass-download-service](https://github.com/eclipse-pass/pass-download-service/releases/tag/0.1.0)
* [pass-policy-service](https://github.com/eclipse-pass/pass-policy-service/releases/tag/0.1.0)
* [pass-indexer-checker](https://github.com/eclipse-pass/pass-indexer-checker/releases/tag/0.1.0)
* [pass-indexer](https://github.com/eclipse-pass/pass-indexer/releases/tag/0.1.0)
* [pass-journal-loader](https://github.com/eclipse-pass/pass-journal-loader/releases/tag/0.1.0)
* [pass-nihms-loader](https://github.com/eclipse-pass/pass-nihms-loader/releases/tag/0.1.0)
* [pass-grant-loader](https://github.com/eclipse-pass/pass-grant-loader/releases/tag/0.1.0)
* [pass-fcrepo-jsonld](https://github.com/eclipse-pass/pass-fcrepo-jsonld/releases/tag/0.1.1)
* [pass-fcrepo-jms](https://github.com/eclipse-pass/pass-fcrepo-jms/releases/tag/0.1.0)
* [pass-docker](https://github.com/eclipse-pass/pass-docker/releases/tag/0.1.0)

These repositories were involved in the release, but do not have a `0.1.0` release:
* [pass-fcrepo-module-auth-rbacl](https://github.com/eclipse-pass/pass-fcrepo-module-auth-rbacl)
* [modeshape](https://github.com/eclipse-pass/modeshape)
