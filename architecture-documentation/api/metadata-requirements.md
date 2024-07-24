Dump of table from: https://docs.google.com/document/d/1j3tAT6cU2jz746c3NzABVRrv8VqrX7vZa1dhy_-7tcQ/edit


Global name
Data type
Description
NIH
J10P
Where this information come from 
DOI
string
Digital identifier assigned to published  article of the manuscript
Optional
Optional 
User
title
string
Title of manuscript/article
Required
Required
User, DOI lookup
journal-title
string
Title of journal
Optional
Required
User, DOI lookup
volume
string
Journal volume
Optional
Optional
User, DOI lookup
issue
string
Journal issue
Optional
Optional
User, DOI lookup
ISSN
string
One or more comma separated ISSNs e.g. 
"ISSN": "1234-5678,9876-543X"
Required
Optional
User, DOI lookup
NLMTA
string
National Library of Medicines Title Abbreviation
Required IF ISSN is not available
n/a
Look up via NCBI service
publisher
string
Publisher name
Optional
Optional
User, DOI lookup
publicationDate
string
Publication date, captured in exact format entered on the form e.g. “October 2017”, “Fall 2012” “12/20/2016”
Optional
Optional
User, DOI lookup
abstract
string
Publication abstract
Optional
Optional
User, DOI lookup
authors
array[author,orcid]
Array of author names and corresponding orcid IDs
"authors": [{
    "author": "Bob Author",
    "orcid": https://orcid.org/..."
  }, {
    "author": "Jane Writer",
    "orcid": https://orcid.org/..."
  }
]
Optional
Required
User, DOI lookup
corrpi-name
string
Name of corresponding pi, who can approve NIHMS processing of the manuscript
Required
Optional
Can be found on associated grant  from user’s input
corrpi-email
string
Email of corresponding pi who can approve NIHMS processing of the manuscript
Required
Optional
Can be found on associated grant
under-embargo
boolean
true if publication is under embargo, absent if false
Optional
Optional
User
embargo-end-date
date
Embargo date end e.g. 2018-09-12
Optional
Optional
User

