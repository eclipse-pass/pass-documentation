https://docs.google.com/document/d/1NO52smr8Uy2HNTM3Lk1RFJXjS5bV6i4ZsNshUiLZMAo/edit


PASS Submission.metadata schema

Overview

Submission Metadata

Basic format

Common section

Crossref section

Agent information section

Repository specific section

JScholarship ("id": "JScholarship")

PubMedCentral ("id": "pmc")

ERIC, DEC - the web linked repositories

Defining Repository Specific Metadata

Defining metadata using Repository.formSchema

Hardcoded additions to Repository specific metadata in Ember

Appendix A: Full Submission Metadata Example

Appendix B: Current Repository Metadata

Overview
This document describes the source, purpose, and scope of the contents of the Submission.metadata field. The Submission.metadata field contains a JSON array composed of metadata sections that have different purposes. The 4 kinds of metadata blocks that can be found in this array are:

Common elements (exactly 1, required).  A block of common metadata elements that can be populated for all Submissions. These “common” elements are built in to the Ember user interface and are associated with Submissions independent of which target repositories are selected. They cover typical manuscript metadata such as title and author.

CrossRef elements (exactly 1, optional). When a DOI is used, this section captures useful supplemental metadata fields retrieved from CrossRef that are not included in the common elements.

Agent information (exactly 1, required). A block of metadata appended to every Submission.metadata value by Ember that captures the user’s browser information..

Repository specific elements (1 or more, required). These can be configured extensively per Repository by populating the Repository.formSchema field with custom elements. This is formatted using a JSON schema specifically for configuring form elements (Alpaca.js). When configured these will be presented as a separate repository-specific form for the user - one for each repository selected. Note that in addition to this formSchema route for customization, some repository-specific metadata fields have been hard-coded into the Ember logic. For example, the Ember code skips the PMC form and there is an API lookup to retrieve the NLMTA value for PMC that happens without the User needing to enter it.


Submission Metadata
Basic format
The basic format of the Submission.metadata is shown below. It is essentially an array of data blocks, each with a corresponding “id”. Each block corresponds to a specific type of metadata. The rest of this document will explain the possible sections that appear in this array.  A full example can be seen in Appendix A


[{

  "id": "id_of_section_1",

  "data": {

    ...

  }

}, {

  "id": "id_of_section_2",

  "data": {

    ...

  }

}, {

<!-- other id/data sections-->

}]


Common section
The "common" metadata section is added to every Submission and reflects the main metadata form that is presented to all users. Fields are as follows, empty fields will be absent from the Submission.metadata JSON:


Field name

Type

Required

Description

title

string

yes

Title of manuscript/article

journal-title

string

yes

Title of journal

volume

string

no

Journal volume

issue

string

no

Journal issue

ISSN

string

no

One or more comma separated ISSNs e.g. 

"ISSN": "1234-5678,9876-543X"

publisher

string

no

Publisher name

publicationDate

string

no

Publication date, captured in exact format entered on the form e.g. “October 2017”, “Fall 2012” “12/20/2016”

abstract

string

no

Publication abstract

authors

array[author,orcid]

no

Array of author names and corresponding orcid IDs

"authors": [{

    "author": "Bob Author",

    "orcid": https://orcid.org/..."

  }, {

    "author": "Jane Writer",

    "orcid": https://orcid.org/..."

  }

]

under-embargo

boolean

no

true if publication is under embargo, absent if false

Embargo-end-date

date

no

Embargo date end e.g. 2018-09-12

Example when all fields populated:
{

    "id": "common",

    "data": {

      "title": "The title of the article",

      "journal-title": "A Terrific Journal",

      "volume": "2",

      "issue": "4",

      "ISSN": "1234-5678,9876-543X",

      "publisher": "Journal Publisher Inc",

      "publicationDate": "Summer 2018",

      "abstract": "This is the abstract of the article.",

      "authors": [{

          "author": "Bob Author"

        }, {

          "author": "Jane Writer",

          "orcid": https://orcid.org/1234-5678-9087-4453"

        }

      ],

      "under-embargo": "true",

      "Embargo-end-date": "2019-01-18"

  }

Crossref section
The "crossref" metadata section is included if a DOI is entered. It includes:


Field name

Type

Required

Description

doi

string

no

DOI of article

publisher

string

no

Publisher from CrossRef

journal-title-short

string

no

Short journal title from CrossRef

Example when all fields populated:
{

    "id": "crossref",

    "data": {

      "doi": "10.19999/124kjd923",

      "publisher": "Journal Publisher Inc",

      "journal-title-short": "Terrif Jour."

    }

}

Agent information section
The "agent_information" metadata section is added to every Submission. It captures some information about the browser used to create the Submission that can be used for troubleshooting issues. In this case the data section contains a single property, "information" which contains two browser properties:


Field name

Type

Required

Description

information.name

string

yes

Browser name

information.version

string

yes

Browser version

Example when all fields populated:
{

    "id": "agent_information",

    "data": {

      "information": {

        "name": "Chrome",

        "version": "70"

      }

    }

}

Repository specific section
Below is a summary of the current Repository-specific metadata

JScholarship ("id": "JScholarship")
Field name

Type

Required

Description

authors

array[string]

yes

Array of author names 

embargo

string

yes

Text of agreement that was agreed to, derived from Repository.agreementText. 

agreement-to-deposit

string

yes

“true” indicates the agreement text was agreed to.

Example when all fields populated:
{

    "id": "JScholarship",

    "data": {

      "authors": [{

          "author": "Bob Author"

        }, {

          "author": "Jane Writer"

        }

      ],

      "embargo": "NON-EXCLUSIVE LICENSE FOR USE OF MATERIALS This non-exclusive license defines..."

      "agreement-to-deposit": "true"

    }

}

PubMedCentral ("id": "pmc")
Field name

Type

Required

Description

nlmta

string

yes

NLMTA of journal. This is required by PMC, but is populated automatically by Ember without the user needing to do anything.

Example when all fields populated:
{

    "id": "pmc",

    "data": {

      "nlmta": "Terrif Journ"

    }

}

ERIC, DEC - the web linked repositories
No repository-specific metadata captured

Defining Repository Specific Metadata
The custom repository-specific metadata sections of Submission.metadata are:

Defined via Repository.formSchema, and/or

Added to by hard-coding into Ember

Defining metadata using Repository.formSchema
Metadata that is specifically required by a Repository can be configured in the Repository.formSchema field. The field uses the Alpaca JS format for configuring form fields and behavior as JSON.  The JSON consists of 3 properties: 

id - a unique id within the scope of PASS for the template

schema - Alpaca JS uses JSON Schema to define the properties and types contained in the form

options - further defines additional options/behavior of the form fields defined in the schema. The Alpaca JS website has documentation for these options.


The JSON is formatted as follows:

{

  "id": "repository-key",

  "schema": {

      <!--form fields configured using Alpaca http://alpacajs.org/documentation.html-->

  }, 

  "options": {

      <!--form field options configured using Alpaca http://alpacajs.org/docs/fields/optiontree.html-->

  }

}


The “id” should correspond to a unique repositoryKey for the repository correspond to the unique repositoryKey for the repository. 

This “schema” and “options” sections follow the format defined on http://alpacajs.org/documentation.html. To see the current data for each repository view Appendix B: Current data.


{

  "id": "repositoryKeyX",

  "schema": {

    "title": "Displayed as page title on metadata form. Can be formatted with HTML",

    "type": "object",

    "properties": {

      "example_fld_name": {

        "title": "Field name to be displayed can be formatted with HTML",

        "type": "text"

        <!--other format configurations as needed-->

        }

      }

    }

  },

  "options": {

    "fields": {

      <!--use documentation at http://alpacajs.org/docs/fields/optiontree.html e.g.]-->

      "example_fld_name": {

        "hidden": "false"

      }       

    }

  }

}

Hardcoded additions to Repository specific metadata in Ember
There are currently several instances in which metadata is added to the Repository specific sections of the Submission.metadata block via hard-coded logic in Ember :

The “NLMTA” tag required for PubMedCentral. In the case of NLMTA tag, there is an API lookup to retrieve this information from the NLM Entrez APIs. The Repository.formSchema does list the field as "journal-NLMTA-ID" but it is not displayed as a form element for the user to enter. Instead it is added as “nlmta”: to the PubMedCentral Submission.metadata.

Repository.agreementText. If a Repository has an agreementText value, this gets appended to the repository-specific metadata like this to indicate what text was agreed to and that it was indeed agreed to:

"embargo": "NON-EXCLUSIVE LICENSE FOR USE OF MATERIALS This non-exclusive license defines..."

       "agreement-to-deposit": "true"


Hardcoded additions to this should generally be reserved for highly unusual cases. 



________________________________________________________________________________________________________

Appendix A: Full Submission Metadata Example
[{

    "id": "JScholarship",

    "data": {

      "authors": [{

          "author": "Bob Author"

        }, {

          "author": "Jane Writer"

        }

      ],

      "embargo": "NON-EXCLUSIVE LICENSE FOR USE OF MATERIALS This non-exclusive license defines..."

      "agreement-to-deposit": "true"

    }

  }, {

    "id": "common",

    "data": {

      "title": "The title of the article",

      "journal-title": "A Terrific Journal",

      "volume": "2",

      "issue": "4",

      "ISSN": "1234-5678,9876-543X",

      "publisher": "Journal Publisher Inc",

      "abstract": "This is the abstract of the article.",

      "authors": [{

          "author": "Bob Author"

        }, {

          "author": "Jane Writer"

        }

      ]

    }

  }, {

    "id": "crossref",

    "data": {

      "doi": "10.1039/c7fo01251a",

      "publisher": "Journal Publisher Inc",

      "journal-title-short": "Terrif Jour."

    }

  }, {

    "id": "pmc",

    "data": {

      "nlmta": "Terrif Jour"

    }

  }, {

    "id": "agent_information",

    "data": {

      "information": {

        "name": "Chrome",

        "version": "70"

      }

    }

  }

]



________________________________________________________________________________________________________

Appendix B: Current Repository Metadata
JScholarship
{

  "id": "JScholarship",

  "schema": {

    "title": "Johns Hopkins - JScholarship <br><p class='lead text-muted'>Deposit requirements for JH's institutional repository JScholarship.</p>",

    "type": "object",

    "properties": {

      "authors": {

        "title": "<div class='row'><div class='col-6'>Author(s) <small class='text-muted'>(required)</small></div><div class='col-6 p-0'></div></div>",

        "type": "array",

        "uniqueItems": true,

        "items": {

          "type": "object",

          "properties": {

            "author": {

              "type": "string",

              "fieldClass": "body-text col-6 pull-left pl-0"

            }

          }

        }

      }

    }

  },

  "options": {

    "fields": {

      "authors": {

        "hidden": false

      }

    }

  }

}

DEC
{

  "id": "dec",

  "schema": {

    "title": "United States Agency for International Development - DEC <br><small>Requires deposit to the Development Experience Clearinghouse (DEC).</small><br><br><p class='lead text-muted'>Automatic submission from PASS to ERIC is not available at this time. Instead, submission to DEC will be prompted before this submission is finalized in PASS. The publication information collected so far can be used to complete the submission via the DEC website.</p>",

    "type": "object",

    "properties": {}

  },

  "options": {

    "fields": {}

  }

}

ERIC
{

  "id": "eric",

  "schema": {

    "title": "Department of Education - ERIC <br><small>Requires deposit to Education Resource Information Center (ERIC).</small><br><br><p class='lead text-muted'>Automatic submission from PASS to ERIC is not available at this time. Instead, submission to ERIC will be prompted before this submission is finalized in PASS. The publication information collected so far can be used to complete the submission via the ERIC website.</p>",

    "type": "object",

    "properties": {}

  },

  "options": {

    "fields": {}

  }

}


NIH

{

  "id": "nih",

  "data": {},

  "schema": {

    "title": "NIH Manuscript Submission System (NIHMS) <br><p class='lead text-muted'>The following metadata fields will be part of the NIHMS submission.</p>",

    "type": "object",

    "properties": {

      "journal-NLMTA-ID": {

        "type": "string"

      }

    }

  },

  "options": {

    "fields": {

      "journal-NLMTA-ID": {

        "type": "text",

        "label": "Journal NLMTA ID",

        "placeholder": ""

      }

    }

  }

}


