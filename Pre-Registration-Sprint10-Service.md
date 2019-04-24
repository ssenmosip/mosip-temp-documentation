This section details about the service API in the Pre-Registration Document service.
* [Login Service](#login-service-public)
* [Document Service](#document-service-public)

# Login Service (Public)
This service details used by Pre-Registration portal to authenticate user by sending OTP to the user, validating with userid and OTP.

* [POST /login/sendOtp](#post-loginsendotp)
* [POST /login/validateOtp](#post-loginvalidateotp)
* [POST /login/invalidateToken](#post-logininvalidatetoken)
* [GET /login/config](#get-loginconfig)

### POST /login/sendOtp
This request will send the OTP to the requested user in the preferred channel(sms/email)

#### Resource URL
<div>https://mosip.io/preregistration/v1/login/sendOtp</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.pre-registration.login.sendotp
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.userid |Yes|user id of the applicant(mobile number/email address)|8907654778
request.langcode|Yes|The preferred language code |fra

#### Request:
```JSON
{
	"id": "mosip.pre-registration.login.sendotp",
	"version": "1.0",
	"requesttime": "2019-04-24T07:24:47.605Z",
	"request": {
		"langCode": "eng",
		"userId": "akshay.jain@mindtree.com"
	}
}
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Email Request submitted
```JSON
{
  "id": "mosip.pre-registration.login.sendotp",
  "version": "1.0",
  "responsetime": "2019-04-24T09:29:13.546Z",
  "response": {
    "message": "Email Request submitted"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid parameters
```JSON
{
	"id": "mosip.pre-registration.login.sendotp",
	"version": "1.0",
	"responsetime": "2019-03-15T08:09:42.327Z",
	"response": null,
	"errors": [
		{
		 "errorCode": "PRG_PAM_LGN_001",
		 "message": "OTP failed to send through a specified channel"
		}
	]	
}
```

### POST /login/validateOtp
This request will validate the OTP with respect to userid and provide the authorize token in the browser cookies.

#### Resource URL
<div>https://mosip.io/preregistration/v1/login/validateOtp</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.pre-registration.login.useridotp
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.userid |Yes|user id of the applicant (mobile number/email address)|8907654778
request.OTP|Yes| received OTP  |345674

#### Request:
```JSON
{
  "id": "mosip.pre-registration.login.useridotp",
  "version": "1.0",
  "requesttime": "2019-04-24T07:24:47.605Z",
  "request": {
    "otp": "854406",
    "userId": "akshay.jain@mindtree.com"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: sms sent successfully
```JSON
{
  "id": "mosip.pre-registration.login.useridotp",
  "version": "1.0",
  "responsetime": "2019-04-24T09:42:01.741Z",
  "response": {
    "message": "VALIDATION_SUCCESSFUL"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid parameters
```JSON
{
  "id": "mosip.pre-registration.login.useridotp",
  "version": "1.0",
  "responsetime": "2019-04-24T09:43:20.359Z",
  "response": null,
  "errors": [
    {
      "errorCode": "KER-OTV-005",
      "message": "Validation can't be performed against this key. Generate OTP first."
    }
  ]
}
```
### POST /login/invalidateToken
This request will invalidate the authorization token when force logout is done.

#### Resource URL
<div>https://mosip.io/preregistration/v1/login/invalidateToken</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Token invalidated successfully
```JSON
{
  "message": "Token has been invalidated successfully"
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Token is not present in cookies
```JSON
{
  "timestamp": "2019-04-24T09:45:07.972+0000",
  "status": 500,
  "error": "Internal Server Error",
  "message": "No message available",
  "path": "/preregistration/v1/login/invalidateToken"
}
```
### GET /login/config
This request will load the configuration parameters while loading the pre-registration portal page.

#### Resource URL
<div>https://mosip.io/preregistration/v1/login/config</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Config parameter retrieved sucessfully 
```JSON
{
  "id": null,
  "version": null,
  "responsetime": "2019-04-24T09:46:38.188Z",
  "response": {
    "mosip.kernel.otp.default-length": "6",
    "mosip.id.validation.identity.postalCode": "^[(?i)A-Z0-9]{5}$",
    "mosip.left_to_right_orientation": "eng,fra",
    "preregistration.recommended.centers.locCode": "5",
    "mosip.kernel.otp.validation-attempt-threshold": "3",
    "mosip.country.code": "MOR",
    "mosip.primary-language": "fra",
    "preregistration.timespan.cancel": "1",
    "mosip.default.dob.month": "01",
    "preregistration.availability.noOfDays": "4",
    "mosip.preregistration.auto.logout.timeout": "60",
    "mosip.kernel.otp.expiry-time": "120",
    "mosip.id.validation.identity.dateOfBirth": "^\\d{4}/([0]\\d|1[0-2])/([0-2]\\d|3[01])$",
    "mosip.supported-languages": "eng,ara,fra",
    "preregistration.workflow.demographic": "true/false",
    "preregistration.documentupload.allowed.file.nameLength": "50",
    "preregistration.workflow.documentupload": "true/false",
    "mosip.id.validation.identity.postalCode.length": "5",
    "mosip.kernel.sms.number.length": "10",
    "preregistration.availability.sync": "6",
    "mosip.id.validation.identity.email.length": "50",
    "preregistration.timespan.rebook": "1",
    "mosip.id.validation.identity.email": "^[\\w-\\+]+(\\.[\\w]+)*@[\\w-]+(\\.[\\w]+)*(\\.[a-z]{2,})$",
    "mosip.id.validation.identity.age": "^(150|1[0-4][0-9]|[1-9]?[0-9])$",
    "mosip.id.validation.identity.CNIENumber": "^([0-9]{10,30})$",
    "mosip.right_to_left_orientation": "ara",
    "mosip.kernel.pin.length": "6",
    "mosip.id.validation.identity.phone": "^([6-9]{1})([0-9]{9})$",
    "preregistration.workflow.booking": "true/false ",
    "mosip.preregistration.auto.logout.ping": "30",
    "mosip.id.validation.identity.CNIENumber.length": "30",
    "mosip.id.validation.identity.fullName.[*].value": "^(?=.{0,50}$).*",
    "mosip.id.validation.identity.addressLine1.[*].value": "^(?=.{0,50}$).*",
    "mosip.login.mode": "email,mobile",
    "mosip.id.validation.identity.phone.length": "10",
    "mosip.preregistration.auto.logout.idle": "180",
    "preregistration.auto.logout": "2",
    "mosip.secondary-language": "ara",
    "preregistration.documentupload.allowed.file.size": "1000000",
    "preregistration.nearby.centers": "2000",
    "mosip.default.dob.day": "01",
    "preregistration.booking.offset": "2",
    "preregistration.documentupload.allowed.file.type": "application/pdf,image/jpeg,image/png,image/gif"
  },
  "errors": null
}
```

# Document Service (public)
This service enables Pre-Registration portal to request for uploading the document for a particular pre-registration.

* [POST /documents/:preRegistrationId](#post-documentspreregistrationid)
* [PUT /documents/:preRegistrationId](#put-documentspreregistrationid)
* [GET /documents/:preRegistrationId](#get-documentspreregistrationid)
* [DELETE /documents/preregistration/:preRegistrationId](#delete-documentspreregistrationpreregsitrationid)
* [DELETE /documents/:documentId?preRegistrationId=:preRegistrationId](#delete-documentsdocumentidpreregistrationidpreregistrationid)


### POST /documents/:preRegistrationId
This request is used to upload document with the metadata which include document category code, document type code and document format for a pre-registration Id.

#### Resource URL
<div>https://mosip.io/preregistration/v1/documents/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Pre-registration id of the application|36732486130976

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
file |Yes|Document which we need to upload|

#### Request Part (Document request) Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.document.upload
version |Yes|version of the application|1.0
requesttime |Yes|Request tme of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.docCatCode |Yes|Document category code|POI
request.docTypCode |Yes|Document type code|address
request.langCode |Yes|Language code of the application|ENG

#### Request:
```JSON
{
    "id": "mosip.pre-registration.document.upload",
    "version" : "1.0",
    "requesttime" : "2019-03-13T07:22:57.086Z",
    "request" : {
	"docCatCode" : "POI",
	"docTypCode" : "identity",
	"langCode" : "fra"
     }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document uploaded successfully
```JSON
{
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T16:41:06.659Z",
  "response": {
      "preRegsitrationId": "36732486130976",
      "docId": "01964111-4fc0-11e9-ae3b-7d108980d190",
      "docName": "passport.PDF",
      "docCatCode": "POI",
      "docTypCode": "identity",
      "docFileFormat": "pdf"
  },
  "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid document format supported
```JSON
{ 
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
	{
	   "errorCode": "PRG_PAM_DOC_004",
	   "message": " Invalid document format supported"
	}
    ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Document virus scan failed
```JSON
{ 
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
	{
	   "errorCode": "PRG_PAM_DOC_010",
	   "message": "Document virus scan failed"
	}
    ]
}
```

### PUT /documents/:preRegistrationId
This request used to copy the document from source pre-registration id to destination pre-registration id with the specified document category code.

#### Resource URL
<div>https://mosip.io/preregistration/v1/douments/:preRegistrationId?catCode=:doc_cat_code&sourcePreId=:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Destination Pre-registration id of the application|67531403498547

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
catCode|Yes|Document category code|POA
sourcePreId |Yes|Source Pre-registration id of the application|97285429827016

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document successfully copied
```JSON
{
  "id": "mosip.pre-registration.document.copy",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response": {
      "preRegsitrationId": "67531403498547",
      "docId": "8196222-5fb0-11e9-rg3b-7d108980f456",
      "docName": "address.pdf",
      "docCatCode": "POA",
      "docTypCode": "address",
      "docFileFormat": "pdf"
  },
  "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Document not found for the source pre-registration Id
```JSON
{
  "id": "mosip.pre-registration.document.copy",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
        {
	   "errorCode": "PRG_PAM_DOC_005",
	   "message": "Document not found for the source pre-registration Id"
        }
   ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Document copy failed from source to destination
```JSON
{
  "id": "mosip.pre-registration.document.copy",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
	{
	   "errorCode": "PRG_PAM_DOC_011",
	   "message": "Document copy failed from source to destination"
        }
   ]
}
```

### GET /documents/:preRegistrationId
This request used to retrieve all documents metadata associated with particular pre-registration.

#### Resource URL
<div>https://mosip.io/preregistration/v1/documents/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Pre-registration id of the application|97285429827016

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Documents retrieved successfully
```JSON
{
  "id": "mosip.pre-registration.document.fetch.metadata",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response": {
    "documentsMetaData":[
    {
      "docName": "morethan1mb.pdf",
      "docId": "06896ba0-4fa8-11e9-ae3b-0d644a9860e6",
      "docCatCode": "POA",
      "docTypeCode": "address"
    },
    {
      "docName": "Doc.pdf",
      "docId": "0748c439-4f83-11e9-ae3b-7b0aa1318f48",
      "docCatCode": "POB",
      "docTypeCode": "dateOfBirth"
    },
    {
      "docName": "Address.pdf",
      "docId": "1093758a-4f83-11e9-ae3b-cdfde9d4aaca",
      "docCatCode": "POI",
      "docTypeCode": "identity"
    }
  ]
  },
  "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Document is not found for the requested pre-registration id
```JSON
{
   "id": "mosip.pre-registration.document.fetch.metadata",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response":null,
   "errors": [
  	{
    	    "errorCode": "PRG_PAM_DOC_005",
    	    "message": "Documents is not found for the requested pre-registration id"
        }
    ]
}
```
### DELETE /documents/preregistration/:preRegsitrationId
This request used to delete all the documents which are associated with requested pre-registration id.

#### Resource URL
<div>https://mosip.io/preregistration/v1/documents/preregistration/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegsitrationId |Yes|pre-registration id of the application|37802950913289

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Documents successfully deleted
```JSON
{
   "id": "mosip.pre-registration.document.delete",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
       "message": "All documents assosiated with requested pre-registration id deleted sucessfully"
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty pre-registration Id
```JSON
{
   "id": "mosip.pre-registration.document.delete",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
    	    "errorCode": "PRG_PAM_DOC_005",
    	    "message": "Documents is not found for the requested pre-registration id"
         }
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty pre-registration Id
```JSON
{
   "id": "mosip.pre-registration.document.delete",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
    	    "errorCode": "PRG_PAM_DOC_006",
    	    "message": "Documents failed to delete"
         }
    ]
}
```
### DELETE /documents/:documentId?preRegistrationId=:preRegistrationId
This request used to delete the document for a particular document id from database and File System server.

#### Resource URL
<div>https://mosip.io/preregistration/v1/documents/:documentId?preRegistrationId=:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
documentId |Yes|document id of the application|0748c439-4f83-11e9-ae3b-7b0aa1318f48

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|pre registration id of the application|74843948119371

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document successfully deleted
```JSON
{
   "id": "mosip.pre-registration.document.delete.specific",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
      "message": "Document successfully deleted"
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Document is not found for the pre-registration id and document id
```JSON
{
   "id": "mosip.pre-registration.document.delete.specific",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_PAM_DOC_005",
            "message": "Document is not found for the pre-registration id and document id"
         }
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Failed to delete from file system server
```JSON
{
   "id": "mosip.pre-registration.document.delete.specific",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
      {
         "errorCode": "PRG_PAM_DOC_006",
         "message": "Failed to delete from file system server"
     }
  ]
}
```