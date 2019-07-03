This section details about the service API in the Partner Management module.

* [User Management Service](#user-management-service)


# User Management Service
This service used to authenticate MOSIP Admin and management of MISP(MOSIP Infrastructure Service Provider).

* [POST /msip](#post-msip)
* [PUT /msip/{msipId}](#put-msipmsipid)
* [PUT /msip/license/{msipId}](#post-msiplicensemsipid)
* [GET /msip](#get-msip)

### POST /msip
This request will send the MOSIP Admin credentials and msip details to get register

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/msip</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.pre-registration.login.sendotp
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|
request.adminCredential.password|Yes|admin password|
request.msipDetails.organizationName|Yes|MISP organization name|
request.msipDetails.contactNumber|Yes|MISP contact number|
request.msipDetails.emailId|Yes|MISP emailId|
request.msipDetails.address|Yes|MISP address|

#### Request:
```JSON
{
    "id":"mosip.partnermanagement.msip.create",
    "ver":"1.0",
    "requesttime":"2019-05-20T09:48:43.394Z",
    "request" : {
       "adminCredential":{
	       "username":"admin",
	       "password":"admin"
	    },
       "msipDetails":{
	       "organizationName":"telecom",
	       "contactNumber":9876998888,
	       "emailId":"prm@telecom.com",
	       "address":"india"
	    }
    }
}

```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: MSIP successfully created
```JSON
{
    "id":"mosip.partnermanagement.msip.create",
    "version":"1.0",
    "responsetime":"2019-05-20T09:48:43.394Z",
    "response": {
        "mispId":"String",
        "mispStatus":"String",
        "mispLicenseKey":"String",
        "mispLicenseKeyExpiry":LocalDate,
        "mispLicenseKeyStatus":"String"
    },
    "errors": null 
}

```

##### Failure Response:
###### Status code: '200'
###### Description: Not a authorised MOSIP Admin- UserName not available in database
```JSON
{
  "id": "mosip.partnermanagement.msip.create",
  "version": "1.0",
  "responsetime": "2019-05-14T16:46:39.582Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSIP_003",
      "message": "A MISP is already registered with name MISP Organization Name"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSIP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MSIP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MSIP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MSIP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MSIP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation

### PUT /msip/{msipId}
This request to update MISP with the parameters.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/msip/{msipId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
msipId |Yes| id of the misp|64269837502851

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.msip.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|
request.adminCredential.password|Yes|admin password|
request.msipDetails.organizationName|Yes|MISP organization name|
request.msipDetails.contactNumber|Yes|MISP contact number|
request.msipDetails.emailId|Yes|MISP emailId|
request.msipDetails.address|Yes|MISP address|

#### Request:
```JSON
{
    "id":"mosip.partnermanagement.msip.update",
    "ver":"1.0",
    "requesttime":"2019-05-20T09:48:43.394Z",
    "request" : {
        "adminCredential":{
	       "username":"admin",
	       "password":"admin"
	    },	
       "mispDetails":{
           "organizationName":"string",
           "contactNumber":"string",
           "emailID":"string",
           "address":"string"
		}
   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: sms sent successfully
```JSON
{
  "id": "mosip.partnermanagement.msip.update",
  "version": "1.0",
  "responsetime": "2019-06-03T06:47:10.838Z",
  "response": {
      "mispDetails":{  
		   "id":"string",
           "organizationName":"string",
           "contactNumber":"string",
           "emailID":"string",
           "address":"string"
	   }
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
  "responsetime": "2019-06-03T18:03:12.305Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSIP_007",
      "message": "No information provided for update"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSIP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MSIP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MSIP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MSIP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MSIP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MSIP_008|MISP ID does not exist|Internal Error due to Updating

### PUT /msip/license/{msipId}
This request will invalidate the authorization token when force logout is done.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/msip/license/{msipId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
msipId |Yes| id of the misp|64269837502851


#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.msip.license.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|
request.adminCredential.password|Yes|admin password|
request.msipDetails.mispStatus|Yes|MISP organization name|
request.msipDetails.mispLicenseKey|Yes|MISP contact number|
request.msipDetails.mispLicenseKeyStatus|Yes|MISP emailId|

#### Request:
```JSON
{
    "id":"mosip.partnermanagement.msip.license.update",
    "ver":"1.0",
    "requesttime":"2019-05-20T09:48:43.394Z",
    "request" : {
        "adminCredential":{
	       "username":"admin",
	       "password":"admin"
	    },	
       "mispDetails":{
           "mispStatus":"Active",
           "mispLicenseKey":"fa604-affcd-33201-04770",
           "mispLicenseKeyStatus":"Deactive"
		}
   }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: MISP License updated successfully
```JSON
{
  "id": "mosip.partnermanagement.msip.license.update",
  "version": "1.0",
  "responsetime": "2019-05-16T09:37:04.941Z",
  "response": {
    "status": "Active"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: MISP status,  MISP License key status - None available in request
```JSON
{
  "id": "mosip.partnermanagement.msip.license.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSIP_007",
      "message": "No information provided for update"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSIP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MSIP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MSIP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MSIP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MSIP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MSIP_008|MISP ID does not exist|Internal Error due to Updating


### GET /msip
This request will load the configuration parameters while loading the pre-registration portal page.

##### Note: All the values are retrieving from the pre-registration config properties file. If any value get changed in the config properties file it will get reflected in the response of this API. Following mentioned response is the sample of that.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/msip</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.msip.reterive
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|
request.adminCredential.password|Yes|admin password|
request.msipDetails.mispStatus|Yes|MISP organization name|
request.msipDetails.mispLicenseKey|Yes|MISP contact number|
request.msipDetails.mispLicenseKeyStatus|Yes|MISP emailId|

#### Request:
```JSON
{
    "id":"mosip.partnermanagement.msip.reterive",
    "ver":"1.0",
    "requesttime":"2019-05-20T09:48:43.394Z",
    "request" : {
        "adminCredential":{
	       "username":"admin",
	       "password":"admin"
	    },	
       "msipOrganizationName":"telecom"
   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Config parameter retrieved sucessfully 
```JSON
{
  "id": "mosip.partnermanagement.msip.reterive",
  "version": "1.0",
  "responsetime": "2019-05-14T16:01:20.534Z",
  "response": {
     "mispDetails":{
		"id":"String",
		"organizationName":"string",
        "contactNumber":"string",
        "emailID":"string",
        "address":"string"
        "status":"String",
        "licenseKey":"String",
        "licenseKeyExpiry":LocalDate,
        "licenseKeyStatus":"Active"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No MSIP found for the organization
```JSON
{
  "id": "mosip.partnermanagement.msip.license.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSIP_009",
      "message": "No MSIP found for the organization"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSIP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MSIP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MSIP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MSIP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MSIP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation