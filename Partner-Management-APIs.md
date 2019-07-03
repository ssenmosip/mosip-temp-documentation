This section details about the service API in the Partner Management module.

* [User Management Service](#user-management-service)

# User Management Service
This service is used to authenticate MOSIP Admin and management of MISP(MOSIP Infrastructure Service Provider).

* [POST /misp](#post-misp)
* [PUT /misp/{mispId}](#put-mispmispid)
* [PUT /misp/license/{mispId}](#put-misplicensemispid)
* [GET /misp](#get-misp)

### POST /misp
This request will send the MOSIP Admin credentials and misp details to get registered

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misp</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.misp.create
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-07-02T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|admin
request.adminCredential.password|Yes|admin password|admin
request.mispDetails.organizationName|Yes|MISP organization name|telecom
request.mispDetails.contactNumber|Optional|MISP contact number|9876998888
request.mispDetails.emailId|Optional|MISP emailId|"prm@telecom.com
request.mispDetails.address|Optional|MISP address|india

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.create",
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "request": {
    "adminCredential": {
      "username": "admin",
      "password": "admin"
    },
    "mispDetails": {
      "organizationName": "telecom",
      "contactNumber": 9876998888,
      "emailId": "prm@telecom.com",
      "address": "india"
    }
  }
}

```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: MISP successfully created
```JSON
{
  "id": "mosip.partnermanagement.misp.create",
  "version": "1.0",
  "responsetime": "2019-05-20T09:48:43.394Z",
  "response": {
    "mispId": "64269837502851",
    "mispStatus": "Active",
    "mispLicenseKey": "fa604-affcd-33201-04770",
    "mispLicenseKeyExpiry": "2022-12-31",
    "mispLicenseKeyStatus": "Active"
  },
  "errors": null
}

```

##### Failure Response:
###### Status code: '200'
###### Description: MISP already registered

```JSON
{
  "id": "mosip.partnermanagement.misp.create",
  "version": "1.0",
  "responsetime": "2019-05-14T16:46:39.582Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MISP_003",
      "message": "A MISP is already registered with name - organizationName"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MISP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation

### PUT /misp/{mispId}
This request to update MISP with the parameters.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misp/{mispId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispId |Yes| id of the misp|64269837502851

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.misp.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-07-02T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|admin
request.adminCredential.password|Yes|admin password|admin
request.mispDetails.organizationName|Optional|MISP organization name|telecom
request.mispDetails.contactNumber|Optional|MISP contact number|9876998888
request.mispDetails.emailId|Optional|MISP emailId|prm@telecom.com
request.mispDetails.address|Optional|MISP address|india

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.update",
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "request": {
    "adminCredential": {
      "username": "admin",
      "password": "admin"
    },
    "mispDetails": {
      "organizationName": "telecom",
      "contactNumber": 9876998888,
      "emailID": "prm@telecom.com",
      "address": "india"
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
  "id": "mosip.partnermanagement.misp.update",
  "version": "1.0",
  "responsetime": "2019-06-03T06:47:10.838Z",
  "response": {
    "mispDetails": {
      "id": "64269837502851",
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailID": "prm@telecom.com",
      "address": "india"
    }
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: MISP Organization Name, MISP Contact Number, MISP Email ID, MISP Address - None available in request
```JSON
{
  "id": "mosip.partnermanagement.misp.update",
  "version": "1.0",
  "responsetime": "2019-06-03T18:03:12.305Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MISP_007",
      "message": "No information provided for update"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MISP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MISP_008|MISP ID does not exist|MISP ID not available in database

### PUT /misp/license/{mispId}
This request will deactivate/suspend MISPs (update MISP License Key Status)

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misp/license/{mispId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispId |Yes| id of the misp|64269837502851


#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.misp.license.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|admin
request.adminCredential.password|Yes|admin password|admin
request.mispDetails.mispStatus|Optional|MISP organization name|telecom
request.mispDetails.mispLicenseKey|Optional|MISP contact number|
request.mispDetails.mispLicenseKeyStatus|Optional|MISP emailId|

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.license.update",
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "request": {
    "adminCredential": {
      "username": "admin",
      "password": "admin"
    },
    "mispDetails": {
      "mispStatus": "Active",
      "mispLicenseKey": "fa604-affcd-33201-04770",
      "mispLicenseKeyStatus": "Deactive"
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
  "id": "mosip.partnermanagement.misp.license.update",
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
  "id": "mosip.partnermanagement.misp.license.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MISP_007",
      "message": "No information provided for update"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MISP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MISP_008|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
PMS_MISP_009|MISP License key not associated to MISP ID|MISP License key not associated to MISP in the input


### GET /misp
This request will retrieve MISP ID, MISP status, MISP Organization Name,MISP Contact Number, MISP Email ID, MISP Address,MISP License Key, MISP License Key expiry, MISP License key status for all the MISPs retrieved for the requested MISP.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misp</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.misp.retrieve
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.adminCredential.username|Yes|admin username|admin
request.adminCredential.password|Yes|admin password|admin
request.mispOrganizationName|Optional|MISP organization name|telecome

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.reterive",
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "request": {
    "adminCredential": {
      "username": "admin",
      "password": "admin"
    },
    "mispOrganizationName": "telecom"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Config parameter retrieved sucessfully 
```JSON
{
  "id": "mosip.partnermanagement.misp.reterive",
  "version": "1.0",
  "responsetime": "2019-05-14T16:01:20.534Z",
  "response": {
    "mispDetails": {
      "id": "64269837502851",
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailID": "prm@telecom.com",
      "address": "india",
      "status": "Active",
      "licenseKey": "fa604-affcd-33201-04770",
      "licenseKeyExpiry": "2022-12-31",
      "licenseKeyStatus": "Active"
    }
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No MISP found for the organization
```JSON
{
  "id": "mosip.partnermanagement.misp.license.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MISP_009",
      "message": "No MISP found for the organization"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MISP_001|MOSIP Admin does not exist|Un-authorised MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation