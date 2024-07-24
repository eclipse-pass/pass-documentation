
(This is the old documentation that needs to be updated.)

Purpose

Ultimately, we want a user of PASS to be informed of open access manuscripts that already exist on the web and be able to use those copies in their PASS submission, instead of having to manually upload the manuscript file(s). To accomplish this we propose an Open Access Download service that will have two functions.
lookup
The service will fetch a set of open access manuscripts available on the web. In response, the service will send a list of files and relevant metadata back to the Ember client. Initial implementation will only check Unpaywall, but future iterations could include other sources such as OpenAccessButton.

This function will be used to drive the UI and provide enough information for the UI to make a request to this service to download a file. Initial implementation will return only one file, though it could be expanded to return an array of file metadata in the future
Request:
GET: <service_url>?doi=10.1086/307800
Response:
  {
    “url”: “http://example.com/moo.pdf”,
    “name”: “moo.pdf”,
    “type”: “application/pdf”,
    “source”: “Unpaywall”,
    “repositoryLabel”: “J10P”,
    “repositoryUrl”: “http://J10P.example.com/”
  }

url
Download URL for the file
name
(OPTIONAL) File name
type
(OPTIONAL) MIME type
source
(OPTIONAL) Where did we find the file (Unpaywall, UAB, etc)
repositoryLabel
(OPTIONAL) User readable label for the repository where the file can be downloaded
repositoryUrl
(OPTIONAL) URL of the repository


If no files are found to be associated with the provided DOI, the service should return an empty array. 
Question: If the client provides an invalid DOI or one that does not exist, should we return status 404? <404 error response is fine>
download
Once the client has a list of files to present to the user, we want to let them select one to attach to the submission. Because of browser interactions and CORS, the browser cannot treat these files in a similar way as direct uploads. Instead, we need this function to download the file for us. By providing the submission’s DOI, the service can validate the provided file download URL before actually downloading the file. Given the file URL and the DOI, the service should:

Validate file URL against the provided DOI
Example: make sure the provided file URL is among the data provided by Unpaywall
If DOI is invalid or otherwise not found, return status 404 with a message describing this
If validation fails, return status 400 with an appropriate error message?
Attempt to download the file
File bits should be saved in Fedora, the URL of the resting place should be added to the response
If the file download fails in any way, the error status and message can be added to the service response. In this case, url, name, mimeType, description should not appear in the response.

Initial implementation will be done sequentially with a known timeout and act only on a single file URL.
Request:
POST: <base_url>/download?doi=<some_doi>&url=<file_download_url>

doi
DOI associated with a submission, used for validation
url
File download URL


In the future, if we want to support multiple files, we would move the URL query parameters to the HTTP request body.
Response
Our first implementation of this will only allow the handling of a single file URL. In the future, if we want to support multiple files, this response can be expanded  to a map, mapping file URLs to associated metadata. 

{
  “fileUrl”: “<url_of_bits_in_Fedora>”
}

fileUrl
URL of the file bits in Fedora

