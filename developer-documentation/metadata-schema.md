# Metadata Schema Handling

PASS needs to handle the different metadata requirements that repositories place on a submission. When submitting to multiple repositories, PASS figures out the metadata needed by all of them and makes sure the user does not have to enter information more than once.

## Schemas

A PASS [repository](/developer-documentation/pass-core/model/Repository.md) entity represents a target repository where submissions may be submitted. Each repository may have one or more schemas that define the repository's metadata requirements. PASS combines all the schemas dynamically.

## Schema service

The pass-ui metadata schema service creates a schema that describes the metadata for a set of repositories. It does this by resolving the schema identifiers from the repositories and combining the resulting schemas.
That schema is displayed to the user, filled in by the user, validated and saved to the submission metadata field as a JSON blob.

A schema specifies how metadata fields are shown to the user, saved in the metadata blob. and validated.

PASS has a common schema with properties common to all the repositories and per repository schemas, each with properties unique to a particular repository. A particular repositories specifies the common schema along with its own schema.

The metadata schema service uses [SurveyJS](https://surveyjs.io/). A SurveyJS specific configuration file describes all of the possible metadata fields. A separate configuration file maps PASS schema identifiers to a set the set of metadata fields. The service then dynamically produces a SurveyJS configuration file from a set of PASS schema identifiers.

## Metadata blob documentation

The metadata blob is a JSON object stored as a string in the Submission metadata field.


| Key               | Type   | Description                                                                                                                 | 
|-------------------|--------|-----------------------------------------------------------------------------------------------------------------------------|
| DOI               | string | Digital identifier assigned to published  article of the manuscript                                                         |
| title             | string | Title of manuscript/article                                                                                                 |
| journal-title     | string | Title of journal                                                                                                            |
| volume            | string | Journal volume                                                                                                              |
| issue             | string | Journal issue                                                                                                               |
| issns             | array  | array[issn,pubType] where issn is International Standard Serial Number and pubType is Print or Online                       |
| journal-NLMTA-ID  | string | National Library of Medicines Title Abbreviation                                                                            |
| publisher         | string | Publisher name                                                                                                              |
| publicationDate   | string | Publication date in ISO local date format                                                                                   |
| embargo-End-Date  | string | Embargo end date in ISO local date format                                                                                   |
| abstract          | string | Publication abstract                                                                                                        |
| authors           | array  | array[author,orcid] Array of author names and corresponding orcid IDs                                                       |
| agent_information | object | Information about the browser                                                                                               |
| agreements        | array  | Array of objects which reprents ageements. Each object has a key with the repository name and a value of the agreement text |
| under-embargo     | string | Should be "true" or "false" indicating whether or not the submission is under an embargo                                    |

Example of authors field:

```JSON
[{
    "author": "Bob Author",
    "orcid": "https://orcid.org/..."
  }, {
    "author": "Jane Writer",
    "orcid": "https://orcid.org/..."
  }]
```

Example of issn field:

```JSON
[{
  "issn": "0031-9023",
  "pubType": "Print"
  },
  {
  "issn": "1538-6724",
  "pubType": "Online"
  }]
```
