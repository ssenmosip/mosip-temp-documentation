This section details about the service APIs in the Pre-Registration modules

###### [2.7.1 Demographic Service APIs]()

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
#### Path -  ` /pre-registration/applications`
#### Summary
Create new pre-registration by demographic details or update demographic details by providing pre-registration id.


#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
preRegistrationId |Yes|Pre-registration id of the application| <ul><li>To create a new pre-registration dont assign any value (example: "")</li><li>To update the exisiting pre-registration assign pre-registration id (example: 46532058236716)</li></ul>
createdBy |Yes|created user of the application|987654321
createdDateTime |Yes|created Date & Time of the application|2019-01-17T17:05:48.492+0000
updatedBy |Yes|updated user of the application|<ul><li>To create a new pre-registration dont assign any value (example: "")</li><li>To update the exisiting pre-registration assign user id (example: 987654321)</li></ul>
updatedDateTime |Yes|updated Date & Time of the application|<ul><li>To create a new pre-registration dont assign any value (example: "")</li><li>To update the exisiting pre-registration assign updated Date & Time (example: 2019-01-18T17:05:48.492+0000)</li></ul>
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
#### Path -  ` /pre-registration/applications`
#### Summary
Update the pre-registration status by providing pre-registration id and vaild status defined in pre-registration system in request parameter.

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
  "STATUS_UPDATED_SUCESSFULLY"
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
#### Path -  ` /pre-registration/applications`
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
      "deletedDateTime": "2019-01-18T04:57:15.196Z"
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
#### Path -  ` /pre-registration/applications`
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
#### Path -  ` /pre-registration/applicationStatus`
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
#### Path -  ` /pre-registration/applicationDataByDateTime`
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
#### Path -  ` /pre-registration/applicationData`
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
         "createdDateTime":"2019-01-11T11:01:21.947Z",
         "updatedBy":null,
         "updatedDateTime":"2019-01-15T14:25:56.512Z",
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


