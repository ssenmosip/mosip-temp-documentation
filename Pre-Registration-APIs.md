This section details about the service APIs in the Pre-Registration modules

###### [2.7.1 Demographic Service APIs]()

###### [2.7.2 Document Service APIs]()

###### [2.7.3 Data sync Service APIs]()

###### [2.7.4 Booking Service APIs]()

Swagger link as below.


1.      https://dev.mosip.io/demographic/swagger-ui.html#/
2.      https://dev.mosip.io/document/swagger-ui.html#/
3.      https://dev.mosip.io/booking/swagger-ui.html#/
4.      https://dev.mosip.io/datasync/swagger-ui.html#/

Right now specifications are under review.

## 2.7.1 Demographic Service APIs
This service details used by Pre-Registration portal to create the demographic form by providing his/her basic demographic details.

### Host
##### Integration - `http://integ.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | True |
| DELETE | True |

#### Swagger API spec
##### Path - `mosip/docs/design/pre-registration/service/Demographic-Service-API-Spec.yaml`


#### 2.7.1.1 POST Operation
#### Path -  `/pre-registration/applications`
#### Summary
Create new pre-registration by demographic details or update demographic details by providing pre-registration id.


#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
preRegistrationId |Yes|Pre-registration id of the application| <ul><li>To create a new pre-registration don't assign any value (example: "")</li><li>To update the existing pre-registration assign pre-registration id (example: 46532058236716)</li></ul>
createdBy |Yes|created user of the application|987654321
createdDateTime |Yes|created Date & Time of the application|2019-01-17T17:05:48.492+0000
updatedBy |Yes|updated user of the application|<ul><li>To create a new pre-registration don't assign any value (example: "")</li><li>To update the existing pre-registration assign user id (example: 987654321)</li></ul>
updatedDateTime |Yes|updated Date & Time of the application|<ul><li>To create a new pre-registration don't assign any value (example: "")</li><li>To update the existing pre-registration assign updated Date & Time (example: 2019-01-18T17:05:48.492+0000)</li></ul>
langCode |Yes|primary language code| ENG
demographicDetails |Yes|demographicDetails of the applicant|
demographicDetails.identity |Yes|identity of the applicant|
demographicDetails.identity.gender |Yes|gender of the applicant|
demographicDetails.identity.city |Yes|city of the applicant|
demographicDetails.identity.mobileNumber |Yes|mobile number of the applicant|
demographicDetails.identity.fullName |Yes|full name of the applicant|
demographicDetails.identity.localAdministrativeAuthority |Yes|local Administrative Authority code of the application|
demographicDetails.identity.dateOfBirth |Yes|date of birth of the applicant|
demographicDetails.identity.email |Yes|email Id of the applicant|
demographicDetails.identity.province |Yes|province of the applicant|
demographicDetails.identity.postalCode |Yes|postal code of the applicant|
demographicDetails.identity.addressLine1 |Yes|address Line 1 of the applicant|
demographicDetails.identity.addressLine2 |Yes|address Line 2 of the applicant|
demographicDetails.identity.addressLine3 |Yes|address Line 3 of the applicant|
demographicDetails.identity.region |Yes|region of the applicant|
demographicDetails.identity.CNEOrPINNumber |Yes|CNE Number of the applicant|

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request:
```JSON
{  
   "preRegistrationId":"",
   "createdBy":"9900806068",
   "createdDateTime":"2019-01-08T17:05:48.492+0000",
   "updatedBy":"",
   "updatedDateTime":"",
   "langCode":"ENG",
   "demographicDetails":{  
      "identity":{  
         "dateOfBirth":"12/12/1992",
         "gender":[  
            {  
               "language":"ENG",
               "value":"Male"
            },
            {  
               "language":"arb",
               "value":"إناثا"
            }
         ],
         "addressLine1":[  
            {  
               "language":"ENG",
               "value":"20 AVENUE HASSAN"
            },
            {  
               "language":"arb",
               "value":"20 افينيو حسن"
            }
         ],
         "addressLine2":[  
            {  
               "language":"ENG",
               "value":""
            },
            {  
               "language":"arb",
               "value":""
            }
         ],
         "addressLine3":[  
            {  
               "language":"ENG",
               "value":""
            },
            {  
               "language":"arb",
               "value":""
            }
         ],
         "region":[  
            {  
               "language":"ENG",
               "value":"Beni Mellal-Khenifra"
            },
            {  
               "language":"arb",
               "value":"بني ملال خنيفرة"
            }
         ],
         "province":[  
            {  
               "language":"ENG",
               "value":"Azilal"
            },
            {  
               "language":"arb",
               "value":"أزيلال"
            }
         ],
         "postalCode":"570004",
         "localAdministrativeAuthority":[  
            {  
               "language":"ENG",
               "value":"Afourar"
            },
            {  
               "language":"arb",
               "value":"أفورار"
            }
         ],
         "email":"sano@gmail.com",
         "IDSchemaVersion":"1.0",
         "fullName":[  
            {  
               "language":"ENG",
               "value":"Sanober Noor"
            },
            {  
               "language":"arb",
               "value":"سانوبر نور"
            }
         ],
         "phone":"9887653767",
         "CNIENumber":"6789545678909"
      }
   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Demographic data successfully Created

```JSON
{  
   "response":[  
      {  
         "preRegistrationId":"46532058236716",
         "createdBy":"9900806068",
         "createdDateTime":"2019-01-08T17:05:48.492+0000",
         "updatedBy":null,
         "updatedDateTime":"2019-01-18T08:58:38.492+0000",
         "statusCode":"Pending_Appointment",
         "langCode":"ENG",
         "demographicDetails":{  
            "identity":{  
               "dateOfBirth":"12/12/1992",
               "gender":[  
                  {  
                     "language":"ENG",
                     "value":"Male"
                  },
                  {  
                     "language":"arb",
                     "value":"إناثا"
                  }
               ],
               "addressLine1":[  
                  {  
                     "language":"ENG",
                     "value":"20 AVENUE HASSAN"
                  },
                  {  
                     "language":"arb",
                     "value":"20 افينيو حسن"
                  }
               ],
               "addressLine2":[  
                  {  
                     "language":"ENG",
                     "value":""
                  },
                  {  
                     "language":"arb",
                     "value":""
                  }
               ],
               "addressLine3":[  
                  {  
                     "language":"ENG",
                     "value":""
                  },
                  {  
                     "language":"arb",
                     "value":""
                  }
               ],
               "region":[  
                  {  
                     "language":"ENG",
                     "value":"Beni Mellal-Khenifra"
                  },
                  {  
                     "language":"arb",
                     "value":"بني ملال خنيفرة"
                  }
               ],
               "province":[  
                  {  
                     "language":"ENG",
                     "value":"Azilal"
                  },
                  {  
                     "language":"arb",
                     "value":"أزيلال"
                  }
               ],
               "postalCode":"570004",
               "localAdministrativeAuthority":[  
                  {  
                     "language":"ENG",
                     "value":"Afourar"
                  },
                  {  
                     "language":"arb",
                     "value":"أفورار"
                  }
               ],
               "email":"sano@gmail.com",
               "IDSchemaVersion":"1.0",
               "fullName":[  
                  {  
                     "language":"ENG",
                     "value":"Sanober Noor"
                  },
                  {  
                     "language":"arb",
                     "value":"سانوبر نور"
                  }
               ],
               "phone":"9887653767",
               "CNIENumber":"6789545678909"
            }
         }
      }
   ]
}
```
##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`
      
###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_CORE_REQ_004|INVALID_REQUEST_BODY|Invalid or empty Request Body.
PRG_PAM_APP_001| PRG_PAM_APP_001 --> UNABLE_TO_CREATE_THE_PRE_REGISTRATION|Failed to create a pre-registration.
PRG_PAM_APP_012| PRG_PAM_APP_012 --> MISSING_REQUEST_PARAMETER|If created by/create date time/updated by/updated date time is empty while creating new pre-registration.
PRG_PAM_APP_005|PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID |Invalid pre-registration-id while updating the pre-registration.
PRG_PAM_APP_006|PRG_PAM_APP_006 --> UNABLE_TO_FETCH_THE_PRE_REGISTRATION|unable to fetch details based on pre-registration-id 
PRG_PAM_APP_008| PRG_PAM_APP_008  --> UNABLE_TO_UPDATE_THE_PRE_REGISTRATION| unable to update pre-registration demographic detials.

#### 2.7.1.2 PUT Operation
#### Path -  `/pre-registration/applications`
#### Summary
Update the pre-registration status by providing pre-registration id and valid status defined in pre-registration system in request parameter.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
pre_registration_id |Yes|pre-registration id of the application|46532058236716
status_code |Yes|status code of the application|BOOKED

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Pre-Registration Status successfully updated

```JSON
{
  "response": [
  "STATUS_UPDATED_SUCCESSFULLY"
  ]
}
```

##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`
###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_PAM_APP_005|PRG_PAM_APP_005 --> INVALID_STATUS_CODE| Invalid or empty status code
PRG_PAM_APP_005|PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID|Invalid or empty pre-registration id

#### 2.7.1.3 DELETE Operation
#### Path -  `/pre-registration/applications`
#### Summary 
Discard the entire pre-registration details based pre-registration id provided in request parameter.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
pre_registration_id |Yes|pre-registration id of the application|46532058236716

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Deletion of individual is successfully

```JSON
{
  "response": [
    {
      "pre_registration_id": "96157107249860",
      "deletedBy": "9900806068",
      "deletedDateTime": "2019-01-18T04:57:15.196+000"
    }
  ]
}
```

##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`
###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_PAM_APP_005|PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID|Invalid or empty pre-registration id
PRG_PAM_APP_003|PRG_PAM_APP_003 --> DELETE_OPERATION_NOT_ALLOWED| delete operation not allowed based on  roles allowed.
PRG_PAM_APP_004|PRG_PAM_APP_004 --> FAILED_TO_DELETE_THE_PRE_REGISTRATION_RECORD| failed to delete the pre-registration record.

#### 2.7.1.4 GET Operation
#### Path -  `/pre-registration/applications`
#### Summary
Retrieve All Pre-Registration id, Full name, Status and Appointment details by user id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
userId |Yes|User Id of the application|rajath@gmail.com

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications fetched successfully

```JSON
{
   "response":[  
      {  
         "preId":"50490792462164",
         "fullname":"Habiba",
         "statusCode":"Pending_Appointment",
         "appointmentDetails":null
      },
      {  
         "preId":"65490792462164",
         "fullname":"Imane",
         "statusCode":"Booked",
         "appointmentDetails":{  
            "registration_center_id":"RCG-RC-01",
            "appointment_date":"2018-01-17",
            "time_slot_from":"09:00:00",
            "time_slot_to":"09:30:00"
         }
      }
   ]
}
```

##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`

###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_PAM_APP_005|PRG_PAM_APP_005 --> NO_RECORD_FOUND_FOR_USER_ID|Unable to fetch the pre-Registration demographic data

#### 2.7.1.5 GET Operation
#### Path -  `/pre-registration/applications/status`
#### Summary
Retrieve pre-registration application status by providing the pre-registration id in request parameter.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|50490792462164

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications status fetched successfully

```JSON
{
  "response": [
    {
      "statusCode": "Pending_Appointment",
      "preRegistrationId": "50490792462164"
    }
  ]
}
```
##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`
###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_PAM_APP_005|PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID|Invalid or empty pre-registration id.

#### 2.7.1.6 GET Operation
#### Path -  `/pre-registration/applications/byDateTime`
#### Summary 
Retrieve pre-registration ids between created from and to dates provided in request parameters.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
from_date |Yes|From date|2019-01-15 07:22:57.086
to_date |Yes|To date|2019-01-19 07:22:57.086

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications status fetched successfully

```JSON
{
  "response": [
    "91793240270548",
    "89470382513069",
    "38417530829462"
  ]
}
```

##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`

###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_CORE_REQ_003|PRG_CORE_REQ_003 --> INVALID_REQUEST_DATETIME_FORMAT -->  yyyy-MM-dd HH:mm:ss |Invalid requested date formats.
PRG_PAM_APP_010|PRG_PAM_APP_010 --> RECORD_NOT_FOUND_FOR_DATE_RANGE| no record found between date range.

#### 2.7.1.7 GET Operation
#### Path -  `/pre-registration/applications/details`
#### Summary
Retrieve Pre-Registration demographic data by pre-Registration id provided in request parameter.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|82986390537094

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Demographic data successfully retrieved

```JSON
{
   "response":[
      {
         "preRegistrationId":"20180396713560",
         "createdBy":"9900806086",
         "createdDateTime":"2019-01-11T11:01:21.947+000",
         "updatedBy":null,
         "updatedDateTime":"2019-01-15T14:25:56.512+000",
         "statusCode":"Pending_Appointment",
         "langCode":"ENG",
         "demographicDetails":{
         "identity":{
            "dateOfBirth":"12/12/1992",
            "gender":[
               {
                  "language":"ENG",
                  "value":"Male"
               },
               {
                  "language":"arb",
                  "value":"إناثا"
               }
            ],
            "addressLine1":[
               {
                  "language":"ENG",
                  "value":"20 AVENUE HASSAN"
               },
               {
                  "language":"arb",
                  "value":"20 افينيو حسن"
               }
            ],
            "addressLine2":[
               {
                  "language":"ENG",
                  "value":""
               },
               {
                  "language":"arb",
                  "value":""
               }
            ],
            "addressLine3":[
               {
                  "language":"ENG",
                  "value":""
               },
               {
                  "language":"arb",
                  "value":""
               }
            ],
            "region":[
               {
                  "language":"ENG",
                  "value":"Beni Mellal-Khenifra"
               },
               {
                  "language":"arb",
                  "value":"بني ملال خنيفرة"
               }
            ],
            "province":[
               {
                  "language":"ENG",
                  "value":"Azilal"
               },
               {
                  "language":"arb",
                  "value":"أزيلال"
               }
            ],
            "postalCode":"570004",
            "localAdministrativeAuthority":[
               {
                  "language":"ENG",
                  "value":"Afourar"
               },
               {
                  "language":"arb",
                  "value":"أفورار"
               }
            ],
            "email":"sano@gmail.com",
            "IDSchemaVersion":"1.0",
            "fullName":[
               {
                  "language":"ENG",
                  "value":"Sanober Noor"
               },
               {
                  "language":"arb",
                  "value":"سانوبر نور"
               }
            ],
            "phone":"9887653767",
            "CNIENumber":"6789545678909"
         }
      }
   ]
}
```

##### Failure Response:
###### Failure Status code: '200'
###### Failure Response Structure:
###### Path -  `mosip/docs/design/pre-registration/service/Pre-Registration-error-response.json`
###### Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_PAM_APP_005|PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID | Invalid or empty pre-registration id.
PRG_PAM_APP_006|PRG_PAM_APP_006 --> UNABLE_TO_FETCH_THE_PRE_REGISTRATION_DEMOGRAPHIC_DATA | unable to fetch the details by pre-registration id.

## 2.7.2 Document Service APIs
This service enables Pre-Registration portal to request for uploading the document for a particular pre-registration.

### Host
##### Integration - `http://integ.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | False |
| DELETE | True |

#### 2.7.2.1 POST Operation
#### Path -  ` /pre-registration/documents`
#### Summary
Upload document for a pre-registration Id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.document.upload
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.pre_registration_id |Yes|Pre-registration id of the application|49158360813920
request.doc_cat_code |Yes|Document category code|POI
request.doc_typ_code |Yes|Document type code|address
request.doc_file_format |Yes|Document file format|pdf
request.status_code |Yes|Status of the application|Pending_Appoinment
request.upload_by |Yes|Document Uploaded user Id|9480548558
request.upload_date_time |Yes|Document Uploaded date & time|2019-01-09T07:22:57.086Z
request.lang_code |Yes|Language code of the application|ENG

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document uploaded successfully
```JSON
{
  "status": true,
  "timestamp": "2019-01-16T16:41:06.659+000",
  "response": [
    {
      "preRegsitrationId": "49158360813920",
      "documnetId": "2c979c01680905860168091c21970001",
      "documentName": "passport.PDF",
      "documentCat": "POI",
      "documentType": "identity",
      "resMsg": "DOCUMENT_UPLOAD_SUCCESSFUL"
    }
  ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: if the document size is more than the specified limit
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:36:40.763+000",
  "err": {
    "code": "PRG_PAM_DOC_007",
    "message": "DOCUMENT_EXCEEDING_PERMITTED_SIZE"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid document format
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:25:21.352+000",
  "err": {
    "code": "PRG_PAM_DOC_004",
    "message": "DOCUMENT_INVALID_FORMAT"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: When preregistration data is not found for the preregistration id in the DB
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:26:56.177+000",
  "err": {
    "code": "PRG_PAM_APP_005",
    "message": "PRG_PAM_APP_005 --> PRG_PAM_APP_005 --> UNABLE_TO_FETCH_THE_PRE_REGISTRATION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If preregistration id, status code, document category code or preregistration data is empty
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:49:10.286+000",
  "err": {
    "code": "PRG_PAM_DOC_014",
    "message": "MANDATORY_FIELD_NOT_FOUND"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If the document & document details are failed to store in the db
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:49:10.286+000",
  "err": {
    "code": "PRG_PAM_DOC_009",
    "message": "DOCUMENT_FAILED_TO_UPLOAD"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Document virus scan failed
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:49:10.286+000",
  "err": {
    "code": "PRG_PAM_DOC_010",
    "message": "DOCUMENT_FAILED_IN_VIRUS_SCAN"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Retrieval of preregistration data failed
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000",
  "err": {
    "code": "PRG_PAM_DOC_020",
    "message": "DEMOGRAPHIC_GET_RECORD_FAILED"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Copied document & the details are failed to store in the db
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T10:49:10.286+000",
  "err": {
    "code": "PRG_PAM_DOC_011",
    "message": "DOCUMENT_FAILED_TO_COPY"
  }
}
```
#### 2.7.2.2 POST Operation
#### Path -  ` /pre-registration/copyDocuments`
#### Summary
This service enables Pre-Registration portal to request for copy the document from one pre-registration id to another.


#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
catCode|Yes|Document category code|POA
destinationPreId |Yes|Destination Pre-registration id of the application|67531403498547
sourcePrId |Yes|Source Pre-registration id of the application|97285429827016

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document successfully copied
```JSON
{
  
  "status": true,
  "timestamp": "2019-01-17T11:18:43.889+000",
  "response": [
    {
      "sourcePreRegId": "97285429827016",
      "sourceDocumnetId": "4028abea68334b510168334e62060001",
      "destPreRegId": "67531403498547",
      "destDocumnetId": "2c9180836833aa3101685b88e12f0016"
    }
  ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Document not found for the source pre-registration Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:09:33.258+000",
  "err": {
    "code": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Source preregistration id or Destination preregistration id is empty or invalid
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:22:26.321+000",
  "err": {
    "code": "PRG_PAM_DOC_018",
    "message": "INVALID_REQUEST_PARAMETER"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: ceph exception
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:22:26.321+000",
  "err": {
    "code": "PRG_PAM_DOC_009",
    "message": "DOCUMENT_FAILED_TO_UPLOAD"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: if the copied document & document details are failed to store in the db
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:22:26.321+000",
  "err": {
    "code": "PRG_PAM_DOC_011",
    "message": "DOCUMENT_FAILED_TO_COPY"
  }
}
```

#### 2.7.2.3 GET Operation
#### Path -  ` /pre-registration/getDocument`
#### Summary
This service enables Pre-Registration portal request to retrieve all document associated with particular pre-registration.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
pre_registration_id |Yes|Pre-registration id of the application|97285429827016

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Documents retrieved successfully
```JSON
{
  
  "status": true,
  "timestamp": "2019-01-17T11:31:44.994+000",
  "response": [
    {
      "pre_registration_id": "97285429827016",
      "doc_name": "morethan1mb.PDF",
      "doc_id": "4028abea68334b510168334e62060001",
      "doc_cat_code": "POA",
      "doc_typ_code": "address",
      "doc_file_format": "pdf",
      "multipartFile": "{ByteCode}"
    },
    {
      "prereg_id": "97285429827016",
      "doc_name": "Doc.pdf",
      "doc_id": "2c979ec9683c5aaf01683c7807110000",
      "doc_cat_code": "POB",
      "doc_typ_code": "address",
      "doc_file_format": "pdf",
      "multipartFile": "{ByteCode}"
    },
    {
      "prereg_id": "97285429827016",
      "doc_name": "Address.pdf",
      "doc_id": "2c979ec9683c5aaf01683c7892bc0001",
      "doc_cat_code": "POI",
      "doc_typ_code": "address",
      "doc_file_format": "",
      "multipartFile": "{ByteCode}"
    }
  ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty pre-registration Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:38:13.866+000",
  "err": {
    "code": "PRG_PAM_DOC_018",
    "message": "INVALID_REQUEST_PARAMETER"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If the document is not found in the db for the preregistration id
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:47:37.773+000",
  "err": {
    "code": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description:  ceph exception
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:09:33.258+000",
  "err": {
    "code": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_FAILED_TO_FETCH"
  }
}
```

#### 2.7.2.4 DELETE Operation
#### Path -  ` /pre-registration/deleteDocument`
#### Summary
This service enables Pre-Registration portal, request to delete the document for a particular document id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
documentId |Yes|document id of the application|2c9180836833aa31016837aac4c40012

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document successfully deleted
```JSON
{
  "status": true,
  "timestamp": "2019-01-17T11:46:49.220+000",
  "response": [
    {
      "documnet_Id": "2c9180836833aa31016837aac4c40012",
      "resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If the document is not found in the db for the preregistration id
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:47:37.773+000",
  "err": {
    "code": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: ceph exception
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:52:51.433+000",
  "err": {
    "code": "PRG_PAM_DOC_006",
    "message": "DOCUMENT_FAILED_TO_DELETE"
  }
}
```
#### 2.7.2.5 DELETE Operation
#### Path -  ` /pre-registration/deleteAllByPreRegId`
#### Summary
This service enables Pre-Registration portal, request to delete all the document for a particular pre-registration id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
pre_registration_id |Yes|pre-registration id of the application|2c9180836833aa31016837aac4c40012

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Documents successfully deleted
```JSON
{
  "status": true,
  "timestamp": "2019-01-17T11:52:22.165+000",
  "response": [
    {
      "documnet_Id": "2c9180836833aa31016833b242c50000",
      "resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty pre-registration Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:51:31.071+000",
  "err": {
    "code": "PRG_PAM_DOC_018",
    "message": "INVALID_REQUEST_PARAMETER"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: if the document & document details are failed to delete from the db
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:52:51.433+000",
  "err": {
    "code": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: ceph exception
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T11:52:51.433+000",
  "err": {
    "code": "PRG_PAM_DOC_006",
    "message": "DOCUMENT_FAILED_TO_DELETE"
  }
}
```

## 2.7.3  Data sync Service APIs
This service enables Pre-Registration to a registration client , request to retrieve all pre-registration ids based on registration client id, appointment date and an user type.

### Host
##### Integration - `http://integ.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | False |
| DELETE | False |

#### 2.7.3.1 POST Operation
#### Path -  ` pre-registration/data-sync/retrieveAllPreRegIds`
#### Summary
Retrieve all the pre-registration Ids by date range and registration center Id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.datasync
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.registration-client-id |Yes|Registration center Id of the application|12
request.from-date |Yes|From date of the application|2019-01-01 00:00:00
request.to-date |Yes|To date of the application|2019-01-31 00:00:00
request.user-id |Yes|user Id of the application|Officer

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All Pre-Registration Ids fetched successfully
```JSON
{ 
  "status": true,
  "timestamp": "2019-01-10T13:24:53.427+000",
  "response": {
    "transactionId": "03a0acf4-14ad-11e9-b7b7-09819c6c033b",
    "countOfPreRegIds": "4",
    "preRegistrationIds": {
      "42973267563920": "2019-01-10T13:24:53.419+000",
      "56014280251746": "2019-01-10T13:24:51.665+000",
      "63470164572136": "2019-01-10T13:24:52.203+000",
      "25368956035901": "2019-01-10T13:24:52.753+000"
    }
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Empty registration center Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_DATA_SYNC_009",
    "message":"INVALID_REGISTRATION_CENTER_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty from-date or to-date
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_DATA_SYNC_010",
    "message":"INVALID_REQUESTED_DATE"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Empty user id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_DATA_SYNC_003",
    "message":"INVALID_USER_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If appointment is not booked under the registration center Id for the preregistration id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000",
  "err": {
    "code": "PRG_BOOK_RCI_013",
    "message": "BOOKING_DATA_NOT_FOUND"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If retrieval of booking data fails
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000",
  "err": {
    "code": "PRG_DATA_SYNC_013",
    "message": "FAILED_TO_GET_PRE_REG_ID_BY_REG_CLIENT_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If retrieval of preregistration data fails 
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000",
  "err": {
    "code": "PRG_DATA_SYNC_007",
    "message": "DEMOGRAPHIC_GET_RECORD_FAILED"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If no preregistration data created within the from date & to date
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:42:35.401+000",
  "err": {
    "code": "PRG_PAM_APP_005",
    "message": "PRG_PAM_APP_005 --> RECORD_NOT_FOUND_FOR_DATE_RANGE"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If retrieval of preregistration data fails 
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000",
  "err": {
    "code": "PRG_DATA_SYNC_007",
    "message": "DEMOGRAPHIC_GET_RECORD_FAILED"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If writing and reading of files fail
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000",
  "err": {
    "code": "PRG_DATA_SYNC_014",
    "message": "FILE_IO_EXCEPTION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: When demographic JSON file & documents are not zipped
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:25:46.359+000"
  "err": {
    "code": "PRG_DATA_SYNC_005",
    "message": "FAILED_TO_CREATE_A_ZIP_FILE"
  }
}
```

#### 2.7.3.2 GET Operation
#### Path -  ` pre-registration/data-sync/datasync`
#### Summary
This service enables Pre-Registration to a registration client , request to retrieve particular pre-registration data based on a pre-registration id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
pre_registration_id |Yes|Pre Registration id|86710482195706

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Data Sync records fetched
```JSON
{ 
  "status": true,
  "timestamp": "2019-01-02T11:49:57.139+000",
  "response": {
    "pre-registration-id": "86710482195706",
    "registration-client-id": "1",
    "appointment-date": "2018-12-16",
    "from-time-slot": "10:05",
    "to-time-slot": "10:18",
    "zip-filename": "86710482195706",
    "zip-bytes": "{ByteCode}"
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If data does not exists for the preregistration id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:50:08.286+000",
  "err": {
    "code": "PRG_PAM_APP_005",
    "message": "PRG_PAM_APP_005 --> UNABLE_TO_FETCH_THE_PRE_REGISTRATION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If document is not uploaded for the preregistration id
```JSON
{
  "status": false,
  "timestamp": "2019-01-02T12:32:27.955+000",
  "err": {
    "message": "FAILED_TO_FETCH_DOCUMENT",
    "code": "PRG_DATA_SYNC_006"
  }
}
```
#### 2.7.3.3 POST Operation
#### Path -  ` pre-registration/data-sync/reverseDataSync`
#### Summary
This service enables Pre-Registration to a registration processor , request to retrieve all processed pre-registration ids and store in pre-registration database and update the status code in main table.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.datasync
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.createdBy |Yes|Created user of the application|5766477466
request.createdDateTime |Yes|Created date & time of the application|2019-01-16T06:15:25.721Z
request.langCode |Yes|Language of the application|AR
request.preRegistrationIds |Yes|List of Preregistration Ids|42973267563920
request.updateBy |Yes|Updated user of the application|5766477466
request.updateDateTime |Yes|Updated date & time of the application|2019-01-16T06:15:25.721Z

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Consumed Pre-Registrations saved
```JSON
{
  "status": true,
  "timestamp": "2019-01-02T11:47:59.566+000",
  "response": {
    "transactionId": "26fde349-0e56-11e9-99e1-f7683fbbce99",
    "countOfStoredPreRegIds": "1",
    "alreadyStoredPreRegIds": "1"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If there are no preregistration ids passed in request body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_DATA_SYNC_011",
    "message":"INVALID_REQUESTED_PRE_REG_ID_LIST"
  }
}
```
## 2.7.4 Booking Service APIs
This service details used by Pre-Registration portal to book an appointment by providing his/her basic appointment details.

### Host
##### Integration - `http://integ.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | True |
| DELETE | False |

#### 2.7.4.1 GET Operation
#### Path -  ` pre-registration/booking/appointmentDetails`
#### Summary
Retrieve Pre-Registration appointment details by pre-Registration id.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|37802950913289

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment details successfully retrieved

```JSON
{
  "status": true,
  "timestamp": "2019-01-17T13:28:44.595+000",
  "response": {
    "registration_center_id": "1",
    "appointment_date": "2019-01-18",
    "time_slot_from": "12:02",
    "time_slot_to": "12:15"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Unable to fetch the pre-Registration demographic data
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T13:29:15.247+000",
  "err": {
    "code": "PRG_BOOK_RCI_013",
    "message": "BOOKING_DATA_NOT_FOUND"
  }
}
```
#### 2.7.4.2 GET Operation
#### Path -  ` pre-registration/booking/availability`
#### Summary
Retrieve Pre-Registration appointment slots available for booking.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
registration_center_id |Yes|Registration Center Id|1

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Availability details fetched successfully

```JSON
{
  "status": true,
  "timestamp": "2019-01-17T13:32:51.866+000",
  "response": {
    "regCenterId": "1",
    "centerDetails": [
      {
        "date": "2019-01-19",
        "timeSlots": [
          {
            "fromTime": "12:15:00",
            "toTime": "12:28:00",
            "availability": 1
          },
          {
            "fromTime": "12:41:00",
            "toTime": "13:00:00",
            "availability": 4
          },
          {
            "fromTime": "14:00:00",
            "toTime": "14:13:00",
            "availability": 3
          }
        ],
        "holiday": false
      }
    ]
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Unable to fetch available slots.
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T13:33:33.098+000",
  "err": {
    "code": "PRG_BOOK_RCI_015",
    "message": "PRG_BOOK_RCI_015 --> NO_TIME_SLOTS_ASSIGNED_TO_THAT_REG_CENTER"
  }
}
```
#### 2.7.4.3 POST Operation
#### Path -  ` pre-registration/booking/book`
#### Summary
This service enables by Pre-Registration to book an registration center, request to book and re-book an appointment with a selected registration center and time slot. After successful booking update the status code Booked in main table.

#### Parameters for book
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationId|Yes|pre Registration Id|37802950913289
request.newBookingDetails.registration_center_id |Yes|Registration center Id of the application|1
request.newBookingDetails.appointment_date |Yes|Date of the appointment|2019-01-19
request.newBookingDetails.time_slot_from |Yes|Time Slot From|12:15:00
request.newBookingDetails.time_slot_from |Yes|Time Slot To|12:28:00
request.oldBookingDetail|No

#### Parameters for rebook
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationId|Yes|pre Registration Id|37802950913289
request.oldBookingDetails.registration_center_id |Yes|Registration center Id of the application|1
request.oldBookingDetails.appointment_date |Yes|Date of the appointment|2019-01-19
request.oldBookingDetails.time_slot_from |Yes|Time Slot From|12:15:00
request.oldBookingDetails.time_slot_from |Yes|Time Slot To|12:28:00
request.newBookingDetails.registration_center_id |Yes|Registration center Id of the application|1
request.newBookingDetails.appointment_date |Yes|Date of the appointment|2019-01-20
request.newBookingDetails.time_slot_from |Yes|Time Slot From|12:28:00
request.newBookingDetails.time_slot_from |Yes|Time Slot To|12:41:00

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment booked successfully

```JSON
{ 
  "status": true,
  "timestamp": "2019-01-17T13:42:32.427+000",
  "response": [
    {
      "preRegistrationId": "37802950913289",
      "bookingStatus": "Booked",
      "bookingMessage": "APPOINTMENT_SUCCESSFULLY_BOOKED"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid Pre Registration Id.
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T13:43:59.434+000",
  "err": {
    "code": "PRG_PAM_APP_005",
    "message": "PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Availability not found for selected time.
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T13:46:03.002+000",
  "err": {
    "code": "PRG_BOOK_RCI_002",
    "message": "AVAILABILITY_NOT_FOUND_FOR_THE_SELECTED_TIME"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  }
}
```
#### 2.7.4.4 PUT Operation
#### Path -  ` pre-registration/booking/book`
#### Summary
This service enables by Pre-Registration to cancel an appointment booking, request to cancel an booked appointment with a selected registration center and time slot. After successful canceling an booking update the status code Canceled in appointment table.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationId|Yes|pre Registration Id|37802950913289
request.registration_center_id |Yes|Registration center Id of the application|1
request.appointment_date |Yes|Date of the appointment|2019-01-19
request.time_slot_from |Yes|Time Slot From|12:15:00
request..time_slot_from |Yes|Time Slot To|12:28:00


#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment canceled successfully

```JSON
{ 
  "status": true,
  "timestamp": "2019-01-17T13:42:32.427+000",
  "response": [
    {
      "preRegistrationId": "37802950913289",
      "bookingStatus": "Booked",
      "bookingMessage": "APPOINTMENT_SUCCESSFULLY_CANCELED"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid Pre Registration Id for registration center.
```JSON
{
  "status": false,
  "timestamp": "2019-01-17T14:00:13.103+000",
  "err": {
    "code": "PRG_PAM_APP_005",
    "message": "PRG_PAM_APP_005 --> INVALID_PRE_REGISTRATION_ID"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:31:04.021+000",
  "err": {
    "code": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  }
}
```
#### 2.7.4.5 POST Operation
#### Path -  ` pre-registration/booking/bookedPreIdsByRegId`
#### Summary
Retrieve Pre-Registration appointment details by pre-Registration id and registration center id for the use of Data sync service.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
ver |Yes|version of the application|1.0
reqTime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.registration_center_id|Yes|Registration Center Id|1
request.preRegistrationId|Yes|pre Registration Id|37802950913289,..

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Retrieved all pre-registration ids successfully.

```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "ver": "1.0",
  "reqTime": "2019-01-17T12:48:30.416+000",
  "request": {
    "registration_center_id": "1",
    "pre_registration_ids": [
      "37802950913289"
    ]
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Unable to fetch.
```JSON
{
  "err": {
    "code": "PRG_BOOK_RCI_013",
    "message": "BOOKING_DATA_NOT_FOUND"
  },
  "status": false,
  "timestamp": "2019-01-17T14:09:27.310+000",
  
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_001",
    "message":"INVALID_REQUEST_ID"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty request version
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T17:32:35.658+000",
  "err": {
    "code": "PRG_CORE_REQ_002",
    "message":"INVALID_REQUEST_VERSION"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_003",
    "message":"INVALID_REQUEST_DATETIME"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "status": false,
  "timestamp": "2019-01-16T15:15:05.467+000",
  "err": {
    "code": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  }
}
```
#### 2.7.4.6 PUT Operation
#### Path -  ` pre-registration/booking/master-sync`
#### Summary
Synchronize booking slots availability table with master data.

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment details successfully retrieved

```JSON
{
  "status": true,
  "timestamp": "2019-01-06T15:56:35.398+000",
  "response": {
    "message":"Master Data Sync is successful"
   }
}
```