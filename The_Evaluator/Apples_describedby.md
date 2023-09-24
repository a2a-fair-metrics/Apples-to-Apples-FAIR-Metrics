# TITLE:  FAIR Maturity Indicator Apples_describedby

## Authors: 
Mark D Wilkinson: 0000-0001-6960-357X

#### Publication Date: 2022-03-21
#### Last Edit: 2022-03-21
#### Accepted: pending


### Maturity Indicator Identifier: Apples_describedby [https://w3id.org/fair/maturity_indicator/Apples/Apples_describedby](https://w3id.org/fair/maturity_indicator/Apples/Apples_describedby)

### Maturity Indicator Name:   Headers or Link HTML elements include describedby link

The landing page should point to one or more metadata records using the `describedby` link.This should be accomplished 
using the `describedby` Link Header type [https://www.rfc-editor.org/rfc/rfc8574.html](https://www.rfc-editor.org/rfc/rfc8574.html) or the equivalent HTML `describedby` link.
The value of this link should be an absolute URL. The link must also have a `type` attribute indicating the MIME type of the Accept headers when resolving the link, that will result in retrieval of the metadata.

### To which principle does it apply?
F2 - data is described by rich metadata

### What is being measured?

The existence of a describedby link, absolute URL, and including a type attribute, that resolves

### Why should we measure it?

The ability to discover structured metadata in a predictable manner is core to the 'Apples to apples' signposting approach.  This includes giving 
an agent all of the information it requires to make a successful call for metadata retrieval.

### What must be provided for the measurement?
A GUID that resolves (after following all redirects) to the landing page of a data record, or to a data record that has these link headers.


### How is the measurement executed?

ALL OF THE FOLLOWING MUST BE TRUE TO PASS THIS METRIC

   * HTTP GET calls, using Accept `*/*` content type, are made on the provided GUID, and any 300-range redirects are followed.  
   * When there are no more redirects, the HTTP headers of the last call are examined for the presence of a `link` header of type `describedby`, 
   and similarly `link` elements in the HTML (if the record is HTML) are examined for the existence of a `rel="describedby"` link.  
   * In both cases, the `type` element of that `describedby` link must exist and have a valid content-type.  This is tested by executing an HTTP GET call on the link, with the indicated type as the Accept headers for the call
   * After following all 300-range redirects, should end with an HTTP 200 success, 
   * The repoted Content-type of the final response should be the same as the value reported in the `type` element

### What is/are considered valid result(s)?
the workflow described above results in a document with the correct `content-type`

### For which digital resource(s) is this relevant? (or 'all')
All

### Examples of good practices (that would score well on this assessment)


### Comments
