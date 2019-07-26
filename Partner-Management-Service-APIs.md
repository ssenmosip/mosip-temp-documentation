This section details about the service API in the Partner Management module.

#### Note:
For securely accessing any API in MOSIP, you must gain auth token from kernel authmanager
1. Authenticate through client-id/Secret or User Id/Password having respective roles assigned in IAM.
2. After successful authentication access token will set as Authorization cookies.
3. Access API through postman by passing the access token in cookies.

#### Auth Token
 url- https://mosip.io/v1/authmanager/authenticate/useridPwd

```
{
  "id": "string",
  "version": "string",
  "requesttime": "2018-12-10T06:12:52.994Z",
  "metadata": {},
  "request": {
     "appId": "admin",
     "password": "admin",
     "userName": "admin"
  }
}
```
After hitting api, you will get the Authorization token in the cookie. 

#### Prerequisite for Partner Management Module:
1. Digital certificate sharing between MOSIP and Partners
2. MISP (MOSIP Infrastructure Service Provider) Creation
3. Master data related to Partner Management - like Policy Groups, Partner Manager mappings to Policy Groups, Policy Manager mappings to Policy Groups, Master policy for the country

# Partner Management APIs are categorized into following services

* [MISP Management Service](#misp-management-service)
* [Policy Management Service](#policy-management-service)
* [Partner Management Service](#partner-management-service)

## MISP Management Service
This service would be used by MOSIP admin for MISP(MOSIP Infrastructure Service Provider) management.

* [POST /misps](#post-misps)
* [POST /misps/{mispId}](#put-mispsmispid)
* [POST /misps/{mispId}/licenseKey](#post-mispsmispidlicensekey)
* [PUT /misps/{mispId}](#put-mispsmispid)
* [PUT /misps/{mispId}/licenseKey](#put-mispsmispidlicensekey)
* [GET /misps/{mispId}](#get-mispsmispId)
* [GET /misps/{mispOrgName}](#get-mispsmispOrgName)
* [GET /misps/{mispId}/licenseKey](#get-mispsmispidlicensekey)


### POST /misps
MOSIP Admin would be able to create MISP using this API. At the time of creation of MISP, MISP ID and MISP License Key are generated,mapped and shared back in response. Post successful MISP creation, by default MISP is set to active status,  MISP License key is to active status. MISP License key is configurable and set to expire in 3 months, 6 months OR any configurable period.  

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps</div>

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
request.organizationName|Yes|MISP organization name|telecom
request.contactNumber|Optional|MISP contact number|9876998888
request.emailId|Yes|MISP emailId|prm@telecom.com
request.address|Yes|MISP address|India

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.create",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailId": "prm@telecom.com",
      "address": "India"
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
      "errorCode": "PMS_MSP_003",
      "message": "A MISP is already registered with name - organizationName"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_003|A MISP is already registered with name - organizationName|If MISP is already registered with organizationName
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### POST /misps/{mispId}
This request would be used to update MISP for given mispID.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispId |Yes| id of the misp|64269837502851

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.misp.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-07-02T05:23:08.019Z
request |Yes|Request for the application|
request.organizationName|Optional|MISP organization name|telecom
request.contactNumber|Optional|MISP contact number|9876998888
request.emailId|Optional|MISP emailId|prm@telecom.com
request.address|Optional|MISP address|India

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.update",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailID": "prm@telecom.com",
      "address": "India"
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
      "id": "64269837502851",
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailID": "prm@telecom.com",
      "address": "India"
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
      "errorCode": "PMS_MSP_004",
      "message": "No information provided for update"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_004|No information provided for update|No information provided for update
PMS_MSP_005|MISP ID does not exist|MISP ID not available in database
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### POST /misps/{mispId}/licenseKey
This request would be used for validating MISPs license key- 
   1. Validate license key pattern.
   2. Validate license key is associated with the requested MISP id.
   3. Validate license key is Active or not.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispId}/licenseKey</div>

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
id |Yes|id |mosip.partnermanagement.misp.license.validate
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-05-20T09:48:43.394Z
request |Yes|Request for the application|
request.mispLicenseKey|Yes|MISP license key|fa604-affcd-33201-04234


#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.license.validate",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "mispLicenseKey": "fa604-affcd-33201-04234"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: MISP License validated successfully
```JSON
{
  "id": "mosip.partnermanagement.misp.license.validate",
  "version": "1.0",
  "responsetime": "2019-05-20T09:48:43.395Z",
  "response": {
    "message": "MISP License key is valid",
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: MISP ID/MISP License Key not available in database
```JSON
{
  "id": "mosip.partnermanagement.misp.license.validate",
  "version": "1.0",
  "responsetime": "2019-05-20T09:48:43.395Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSP_008",
      "message": "MISP License key not valid"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_006|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
PMS_MSP_007|MISP License key not associated to MISP ID|MISP License key not associated to MISP in the input
PMS_MSP_008|MISP License key not valid|MISP License key not valid
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error


### PUT /misps/{mispId}
This API would be used update MISP status.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispId |Yes| id of the misp|64269837502851

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.misp.status.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-07-02T05:23:08.019Z
request |Yes|Request for the application|
request.mispStatus|Yes|MISP status|De-Active

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.status.update",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "mispStatus": "De-Active"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: sms sent successfully
```JSON
{
  "id": "mosip.partnermanagement.misp.status.update",
  "version": "1.0",
  "responsetime": "2019-06-03T06:47:10.838Z",
  "response": {
      "message": "MISP deactivated successfully"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: MISP Organization Name, MISP Contact Number, MISP Email ID, MISP Address - None available in request
```JSON
{
  "id": "mosip.partnermanagement.misp.status.update",
  "version": "1.0",
  "responsetime": "2019-06-03T18:03:12.305Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSP_009",
      "message": "Failed to update MISP status"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_004|No information provided for update|No information provided for update
PMS_MSP_005|MISP ID does not exist|MISP ID not available in database
PMS_MSP_009|Failed to update MISP status|Failed to update the MISP status
PMS_MSP_010|MISP status already in the requested status|MISP status already in the requested status
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### PUT /misps/{mispId}/licenseKey
This API would be used to activate/deactivate MISPs License Key (update MISP License Key Status)

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispId}/licenseKey</div>

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
request.mispStatus|Optional|MISP status|Active
request.mispLicenseKey|Optional|MISP license Key|fa604-affcd-33201-04770
request.mispLicenseKeyStatus|Optional|MISP license Key Status|Active


#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.license.update",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "mispStatus": "Active",
      "mispLicenseKey": "fa604-affcd-33201-04770",
      "mispLicenseKeyStatus": "De-Active"
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
    "status": "De-Active"
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
      "errorCode": "PMS_MSP_004",
      "message": "No information provided for update"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_004|No information provided for update|No information provided for update
PMS_MSP_006|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
PMS_MSP_007|MISP License key not associated to MISP ID|MISP License key not associated to MISP in the input
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error


### GET /misps/{mispId}
This API would be used to retrieve the MISPs details based on given misp id.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispId |Yes| id of the misp|64269837502851

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Responses:
##### Success Response:
###### Status code: '200'

```JSON
{
  "id": "mosip.partnermanagement.misp.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-03T06:47:10.838Z",
  "response": {
      "id": "64269837502851",
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailID": "prm@telecom.com",
      "address": "India"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: MISP ID does not exist
```JSON
{
  "id": "mosip.partnermanagement.misp.status.update",
  "version": "1.0",
  "responsetime": "2019-06-03T18:03:12.305Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSP_005",
      "message": "MISP ID does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_005|MISP ID does not exist|MISP ID not available in database
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /misps/{mispOrgName}
This API would retrieve MISPs details based on given name
1. If MISP organization name present, then retrieve all misp details for matching organization name.
2. If MISP organization name not present, then retrieve all misp details. 

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispOrgName}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispOrgName|Yes|MISP organization name|telecome

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Config parameter retrieved successfully 
```JSON
{
  "id": "mosip.partnermanagement.misp.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-14T16:01:20.534Z",
  "response": {
     "telecom": {
        "id": "64269837502851",
        "organizationName": "telecom",
        "contactNumber": "9876998888",
        "emailID": "prm@telecom.com",
        "address": "India",
        "status": "Active",
        "licenseKey": "fa604-affcd-33201-04770",
        "licenseKeyExpiry": "2022-12-31",
        "licenseKeyStatus": "Active"
     },
     "telecomIndia": {
        "id": "93469837502851",
        "organizationName": "telecomIndia",
        "contactNumber": "9876995433",
        "emailID": "srs@telecomInd.com",
        "address": "India",
        "status": "Active",
        "licenseKey": "ty604-affcd-33201-04770",
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
  "id": "mosip.partnermanagement.misp.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSP_009",
      "message": "No MISP found for the organization"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_011|No MISP found for the organization|No MISP found for the organization
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /misps/{mispId}/licenseKey
This API would be used by MISP Admin / MOSIP Admin for download MISPs license key. In case where license key got expired then user would be able to get a new license key. New license key thus generated would be mapped with given MISP ID . Older license keys would be updated with inactive status. 

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/misps/{mispId}/licenseKey</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
mispId |Yes| id of the misp|64269837502851


#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: MISP License retrieved successfully
```JSON
{
  "id": "mosip.partnermanagement.misp.license.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-16T09:37:04.941Z",
  "response": {
    "mispLicenseKey": "fa604-affcd-33201-04770",
    "mispLicenseKeyExpiry": "2022-12-31",
    "mispLicenseKeyStatus": "Active"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: MISP status,  MISP License key status - None available in request
```JSON
{
  "id": "mosip.partnermanagement.misp.license.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MSP_006",
      "message": "MISP ID/MISP License Key does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSP_001|MOSIP Admin does not exist|Unauthorized MOSIP Admin- UserName not available in database
PMS_MSP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MSP_006|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error


## Policy Management Service
This service would be used by Policy Manager to manage policies for his Policy Group.

* [POST /policies](#post-policies)
* [POST /policies/{policyID}](#post-policiespolicyid)
* [PUT /policies/{policyID}](#put-policiespolicyid)
* [GET /policies](#get-policies)
* [GET /policies/{policyID}](#get-policiespolicyid)
* [GET /policies/{PartnerAPIKey}](#get-policiespartnerapikey)

### POST /policies
This API would be used to create new Policy for policy group

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.policy.create
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.name|Yes|name of the policy|Insurance Policy
request.desc|Yes|description of the policy|Desc about policy
request.policies|Yes|policy file|JSON
request.policies.authPolicies|Yes|auth details|Array of JSON
request.policies.allowedKycAttributes|Yes|eKYC details|Array of JSON


#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.policy.create",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
       "name": "Insurance Policy",
       "desc": "Desc about policy",
       "policies": {
            "authPolicies": [ 	
				{"authType": "otp","mandatory": true},
				{"authType": "demo","mandatory": false},
				{"authType": "bio","authSubType": "FINGER","mandatory": true},
				{"authType": "bio","authSubType": "IRIS","mandatory": false},
				{"authType": "bio","authSubType": "FACE","mandatory": false},
				{"authType": "kyc","mandatory": false}
		    ],
            "allowedKycAttributes": [  
				{"attributeName": "fullName","required": true},
				{"attributeName": "dateOfBirth","required": true},
				{"attributeName": "gender","required": true},
				{"attributeName": "phone","required": true},
				{"attributeName": "email","required": true},
				{"attributeName": "addressLine1","required": true},
				{"attributeName": "addressLine2","required": true},
				{"attributeName": "addressLine3","required": true},
				{"attributeName": "location1","required": true},
				{"attributeName": "location2","required": true},
				{"attributeName": "location3","required": true},
				{"attributeName": "postalCode","required": false},
				{"attributeName": "photo","required": true}
			]
        }
    }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: create new Policy for policy group is successful
```JSON
{
  "id": "mosip.partnermanagement.policy.create",
  "version": "1.0",
  "responsetime": "2019-05-14T16:01:20.534Z",
  "response": {
       "policies": [
          {
            "id": "32058251034176",
            "name": "Insurance Policy",
            "desc": "Desc about policy",
            "is_Active": true,
            "cr_by": "MOSIP",
            "cr_dtimes": "2019-05-14T16:01:20.534Z",
            "up_by": null,
            "upd_dtimes": null
          }
        ]
   },
  "errors": null
}
```


##### Failure Response:
###### Status code: '200'
###### Description: If policy name already exists in the policy group
```JSON
{
  "id": "mosip.partnermanagement.policy.create",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_004",
      "message": "Policy Name already exists in the policy Group"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_004|Policy Name already exists in the policy Group|If Policy Name already exists in the policy Group
PMS_POL_005|Unsupported KYC attribute in the Policy File|If any unsupported KYC attribute in the Policy File
PMS_POL_006|Unsupported Authentication Type in the Policy File|If any unsupported Authentication Type in the Policy File
PMS_POL_007|eKYC attribute missing in the policy file|If any eKYC attribute missing in the policy file
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### POST /policies/{policyID}
This request is used to update existing policy for a policy group

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/{policyID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
policyID |Yes| policyID |45678451034176

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.policy.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.name|Yes|name of the policy|Insurance Policy
request.desc|Yes|description of the policy|Desc about policy
request.policies|Yes|policy file|JSON
request.policies.authPolicies|Yes|auth details|Array of JSON
request.policies.allowedKycAttributes|Yes|eKYC details|Array of JSON

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.policy.update",
  "version": "1.0",
  "requesttime": "2019-05-15T16:01:20.534Z",
  "metadata": {},
  "request": {
      "name": "Loan Policy",
      "desc": "Desc about policy",
      "policies": {
            "authPolicies": [ 	
					{"authType": "otp","mandatory": true},
					{"authType": "demo","mandatory": false},
					{"authType": "bio","authSubType": "FINGER","mandatory": true},
					{"authType": "bio","authSubType": "IRIS","mandatory": true},
					{"authType": "bio","authSubType": "FACE","mandatory": false},
					{"authType": "kyc","mandatory": false}
			],
            "allowedKycAttributes": [  
					{"attributeName": "fullName","required": true},
					{"attributeName": "dateOfBirth","required": true},
					{"attributeName": "gender","required": true},
					{"attributeName": "phone","required": true},
					{"attributeName": "email","required": true},
					{"attributeName": "addressLine1","required": true},
					{"attributeName": "addressLine2","required": true},
					{"attributeName": "addressLine3","required": true},
					{"attributeName": "location1","required": true},
					{"attributeName": "location2","required": true},
					{"attributeName": "location3","required": true},
					{"attributeName": "postalCode","required": false},
					{"attributeName": "photo","required": true}
			]
        }
    }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: update existing policy for policy group is successful
```JSON
{
  "id": "mosip.partnermanagement.policy.update",
  "version": "1.0",
  "responsetime": "2019-05-15T16:01:20.534Z",
  "response":{
        "id": "45678451034176",
        "name": "Loan Policy",
		"desc": "Desc about policy",
		"is_Active": true,
		"cr_by": "MOSIP",
		"cr_dtimes": "2019-05-14T16:01:20.534Z",
		"up_by": "MOSIP",
		"upd_dtimes": "2019-05-15T16:01:20.534Z"
	},
  "errors": null
}
```


##### Failure Response:
###### Status code: '200'
###### Description: If policy ID does not exist
```JSON
{
  "id": "mosip.partnermanagement.policy.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_008",
      "message": "Policy ID does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_004|Policy Name already exists in the policy Group|If Policy Name already exists in the policy Group
PMS_POL_005|Unsupported KYC attribute in the Policy File|If any unsupported KYC attribute in the Policy File
PMS_POL_006|Unsupported Authentication Type in the Policy File|If any unsupported Authentication Type in the Policy File
PMS_POL_007|eKYC attribute missing in the policy file|If any eKYC attribute missing in the policy file
PMS_POL_008|Policy ID does not exist|If Policy ID does not exist
PMS_POL_009|No information provided for update|if no information provided for update
PMS_POL_010|Policy Manager is denied permission to update the policy|if the policy manager is denied permission to update the policy
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### PUT /policies/{policyID}
This API would be used to update the existing policy status.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/{policyID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
policyID |Yes| policyID |45678451034176

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.policy.update.status
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.status|Yes|status of the policy that needs to update|De-Active

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.policy.update.status",
  "version": "1.0",
  "requesttime": "2019-05-15T16:01:20.534Z",
  "metadata": {},
  "request": {
		"status":"De-Active"
   }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: update the existing policy status successful
```JSON
{
  "id": "mosip.partnermanagement.policy.update.status",
  "version": "1.0",
  "responsetime": "2019-05-15T16:01:20.534Z",
  "response":{
        "message" : "status updated successfully"
   },
  "errors": null
}
```


##### Failure Response:
###### Status code: '200'
###### Description: If policy ID does not exist
```JSON
{
  "id": "mosip.partnermanagement.policy.update.status",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_008",
      "message": "Policy ID does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_004|Policy Name already exists in the policy Group|If Policy Name already exists in the policy Group
PMS_POL_008|Policy ID does not exist|If Policy ID does not exist
PMS_POL_012|Policy Manager is denied permission to update the policy status|if the policy manager is denied permission to update the policy status
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /policies
Policy manager would require this service to get details for the policies in the policy group he belongs to. All the policy groups are required to be back filled in the partner management database through an offline process based on country specific requirements. Partner Manager and Policy Manager assigned for the Policy group are also required to be back filled along with creation of the policy group. Partner management would depend on Kernel IAM module services for all user management related activities. User ID and Password are shared using off-line process.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: retrieve the policies available for my policy group successful
```JSON
{
  "id": "mosip.partnermanagement.partner.policies",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response": {
     "policies": [
	   {
		"id": "32058251034176",
		"name": "Insurance Policy",
		"desc": "Desc about policy",
		"is_Active": true,
		"policyManagerId": "898778899",
		"cr_by": "MOSIP",
		"cr_dtimes": "2019-05-14T16:01:20.534Z",
		"up_by": null,
		"upd_dtimes": null,
		"policies": {
            "authPolicies": [ 	
					{"authType": "otp","mandatory": true},
					{"authType": "demo","mandatory": false},
					{"authType": "bio","authSubType": "FINGER","mandatory": true},
					{"authType": "bio","authSubType": "IRIS","mandatory": false},
					{"authType": "bio","authSubType": "FACE","mandatory": false},
					{"authType": "kyc","mandatory": false}
			],
            "allowedKycAttributes": [  
					{"attributeName": "fullName","required": true},
					{"attributeName": "dateOfBirth","required": true},
					{"attributeName": "gender","required": true},
					{"attributeName": "phone","required": true},
					{"attributeName": "email","required": true},
					{"attributeName": "addressLine1","required": true},
					{"attributeName": "addressLine2","required": true},
					{"attributeName": "addressLine3","required": true},
					{"attributeName": "location1","required": true},
					{"attributeName": "location2","required": true},
					{"attributeName": "location3","required": true},
					{"attributeName": "postalCode","required": false},
					{"attributeName": "photo","required": true}
			 ]
          }
       },
       {
		"id": "45678451034176",
		"name": "Loan Policy",
		"desc": "Desc about policy",
		"is_Active": true,
		"policyManagerId": "898778899",
		"cr_by": "MOSIP",
		"cr_dtimes": "2019-05-14T16:01:20.534Z",
		"up_by": "MOSIP",
		"upd_dtimes": "2019-05-15T16:01:20.534Z",
		"policies": {
            "authPolicies": [ 	
					{"authType": "otp","mandatory": true},
					{"authType": "demo","mandatory": false},
					{"authType": "bio","authSubType": "FINGER","mandatory": true},
					{"authType": "bio","authSubType": "IRIS","mandatory": true},
					{"authType": "bio","authSubType": "FACE","mandatory": false},
					{"authType": "kyc","mandatory": false}
			],
            "allowedKycAttributes": [  
					{"attributeName": "fullName","required": true},
					{"attributeName": "dateOfBirth","required": true},
					{"attributeName": "gender","required": true},
					{"attributeName": "phone","required": true},
					{"attributeName": "email","required": true},
					{"attributeName": "addressLine1","required": true},
					{"attributeName": "addressLine2","required": true},
					{"attributeName": "addressLine3","required": true},
					{"attributeName": "location1","required": true},
					{"attributeName": "location2","required": true},
					{"attributeName": "location3","required": true},
					{"attributeName": "postalCode","required": false},
					{"attributeName": "photo","required": true}
			]
        }
       }
     ]
	},
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No Active policy available in the Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partner.policies",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_003",
      "message": "No Active policy available in the Policy Group"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_003|No Active policy available in the Policy Group|No Active policies exist in the policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /policies/{policyID}
This API would be used to retrieve existing policy for a policy group based on the policy id.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/{policyID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
policyID |Yes| policyID |45678451034176

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: policy retrieved successfully
```JSON
{
  "id": "mosip.partnermanagement.policy.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-15T16:01:20.534Z",
  "response":{
		"id": "45678451034176",
		"name": "Loan Policy",
		"desc": "Desc about policy",
		"is_Active": true,
		"cr_by": "MOSIP",
		"cr_dtimes": "2019-05-14T16:01:20.534Z",
		"up_by": "MOSIP",
		"upd_dtimes": "2019-05-15T16:01:20.534Z",
		"policies": {
            "authPolicies": [ 	
					{"authType": "otp","mandatory": true},
					{"authType": "demo","mandatory": false},
					{"authType": "bio","authSubType": "FINGER","mandatory": true},
					{"authType": "bio","authSubType": "IRIS","mandatory": false},
					{"authType": "bio","authSubType": "FACE","mandatory": false},
					{"authType": "kyc","mandatory": false}
			],
            "allowedKycAttributes": [  
					{"attributeName": "fullName","required": true},
					{"attributeName": "dateOfBirth","required": true},
					{"attributeName": "gender","required": true},
					{"attributeName": "phone","required": true},
					{"attributeName": "email","required": true},
					{"attributeName": "addressLine1","required": true},
					{"attributeName": "addressLine2","required": true},
					{"attributeName": "addressLine3","required": true},
					{"attributeName": "location1","required": true},
					{"attributeName": "location2","required": true},
					{"attributeName": "location3","required": true},
					{"attributeName": "postalCode","required": false},
					{"attributeName": "photo","required": true}
			]
        }
	},
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If policy ID does not exist
```JSON
{
  "id": "mosip.partnermanagement.policy.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_008",
      "message": "Policy ID does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_004|Policy Name already exists in the policy Group|If Policy Name already exists in the policy Group
PMS_POL_008|Policy ID does not exist|If Policy ID does not exist
PMS_POL_011|Policy Manager is denied permission to retrieve the policy|if the policy manager is denied permission to retrieve the policy
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /policies/{PartnerAPIKey}
This request will retrieve the partner policy details for given PartnerAPIKey. 

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/fa604-affcd-33201-04770</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
PartnerAPIKey|Yes| PartnerAPIKey | fa604-affcd-33201-04770

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: retrieve the partner policy details for given PartnerAPIKey successful
```JSON
{
  "id": "mosip.partnermanagement.policies.retrieve.partnerAPIKey",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
		"id": "32058251034176",
		"name": "Insurance Policy",
		"desc": "Desc about policy",
		"is_Active": true,
		"cr_by": "MOSIP",
		"cr_dtimes": "2019-05-14T16:01:20.534Z",
		"up_by": null,
		"upd_dtimes": null,
		"policies": {
            "authPolicies": [ 	
					{"authType": "otp","mandatory": true},
					{"authType": "demo","mandatory": false},
					{"authType": "bio","authSubType": "FINGER","mandatory": true},
					{"authType": "bio","authSubType": "IRIS","mandatory": false},
					{"authType": "bio","authSubType": "FACE","mandatory": false},
					{"authType": "kyc","mandatory": false}
			],
            "allowedKycAttributes": [  
					{"attributeName": "fullName","required": true},
					{"attributeName": "dateOfBirth","required": true},
					{"attributeName": "gender","required": true},
					{"attributeName": "phone","required": true},
					{"attributeName": "email","required": true},
					{"attributeName": "addressLine1","required": true},
					{"attributeName": "addressLine2","required": true},
					{"attributeName": "addressLine3","required": true},
					{"attributeName": "location1","required": true},
					{"attributeName": "location2","required": true},
					{"attributeName": "location3","required": true},
					{"attributeName": "postalCode","required": false},
					{"attributeName": "photo","required": true}
			]
        }
	},
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No policy available for given PartnerAPIKey
```JSON
{
  "id": "mosip.partnermanagement.policies.retrieve.partnerAPIKey",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_013",
      "message": "No policy available for given PartnerAPIKey"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_013|No policy available for given PartnerAPIKey|No policy available for given PartnerAPIKey
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

## Partner Management Service
This service enables partner managers to manage respective partners, manage partner API Key requests, manage PartnerAPIKeys to Policies mappings.

* [POST /pmpartners/{partnerID}/{PartnerAPIKey}](#post-pmpartnerspartneridpartnerapikey)
* [PUT /pmpartners/{partnerID}](#put-pmpartnerspartnerid)
* [PUT /pmpartners/{partnerID}/{PartnerAPIKey}](#put-pmpartnerspartneridpartnerapikey)
* [PUT /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}](#put-pmpartnerspartnerapikeyrequestsapikeyreqid)
* [GET /pmpartners](#get-pmpartners)
* [GET /pmpartners/{partnerID}](#get-pmpartnerspartnerid)
* [GET /pmpartners/{partnerID}/{PartnerAPIKey}](#get-pmpartnerspartneridpartnerapikey)
* [GET /pmpartners/PartnerAPIKeyRequests](#get-pmpartnerspartnerapikeyrequests)
* [GET /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}](#get-pmpartnerspartnerapikeyrequestsapikeyreqid)


### POST /pmpartners/{partnerID}/{PartnerAPIKey}
This API would be used by partner Manager, to update Partner api key to Policy Mappings.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/{partnerID}/{PartnerAPIKey}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
partnerID |Yes| partnerID |65432345634232
PartnerAPIKey|Yes| PartnerAPIKey | fa604-affcd-33201-04770

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.partners.policy.mapping
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.oldPolicyID|Yes|old Policy ID|54662345634232
request.newPolicyID|Yes|new Policy ID|45662345639999

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.policy.mapping",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
     "oldPolicyID":"54662345634232", 
	 "newPolicyID":"45662345639999"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Partner api key to Policy Mappings updated successfully.
```JSON
{
  "id": "mosip.partnermanagement.partners.policy.mapping",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "message": "Partner api key to Policy Mappings updated successfully"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: old/new Policy %d does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.policy.mapping",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_014",
      "message": "Policy %d does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_008|Partner api key is not assigned to” + old policy ID+ “ hence cannot be updated with new policy|Partner api key is not assigned to old policy ID hence cannot be updated with new policy
PMS_PMP_009|Partner api key does not belong to the Policy Group of the Partner Manger|Partner api key does not belong to the Policy Group of the Partner Manger
PMS_PMP_010|Policy does not belong to the Policy Group of the Partner Manger|Policy does not belong to the Policy Group of the Partner Manger
PMS_PMP_011|Partner api key Request ID does not exist|Partner api key Request ID does not exist
PMS_PMP_014|Policy %d does not exist|Policy does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### PUT /pmpartners/{partnerID}
This API would be used to activate/deactivate Auth/E-KYC Partners

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/{partnerID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
partnerID |Yes| partnerID |65432345634232

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.partners.status.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.status|Yes|status of the partner that needs to update|DeActive

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.status.update",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "status": "De-Active"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Partner status updated successfully.
```JSON
{
  "id": "mosip.partnermanagement.partners.status.update",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "message": "Partner status updated successfully"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Requested partner ID does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.status.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_005",
      "message": "Partner ID %d does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_005|Partner ID %d does not exist|Requested Partner ID does not exist
PMS_PMP_006|Partner Manager is denied permission to activate/deactivate Partner|Partner Manager is denied permission to activate/deactivate Partner
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### PUT /pmpartners/{partnerID}/{PartnerAPIKey}
Partner Manager would be using this API to activate OR de-activate PartnerAPIKey for given partner.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/{partnerID}/{PartnerAPIKey}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
partnerID |Yes| partnerID |65432345634232
PartnerAPIKey|Yes| PartnerAPIKey | fa604-affcd-33201-04770

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.partners.apikeystatus.update
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.status|Yes|status of the partnerAPI that needs to update|Active

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.apikeystatus.update",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "status": "Active"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: PartnerAPIKey status updated successfully.
```JSON
{
  "id": "mosip.partnermanagement.partners.apikeystatus.update",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "message": "Partner API Key status updated successfully"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Requested Partner API Key does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.apikeystatus.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_007",
      "message": "Partner API Key does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_005|Partner ID %d does not exist|Requested Partner ID does not exist
PMS_PMP_006|Partner Manager is denied permission to activate/deactivate Partner|Partner Manager is denied permission to activate/deactivate Partner
PMS_PMP_007|Partner API Key does not exist|Requested Partner API Key does not exist
PMS_PMP_008|Partner api key is not assigned to” + old policy ID+ “ hence cannot be updated with new policy|Partner api key is not assigned to old policy ID hence cannot be updated with new policy
PMS_PMP_009|Partner api key does not belong to the Policy Group of the Partner Manger|Partner api key does not belong to the Policy Group of the Partner Manger
PMS_PMP_010|Policy does not belong to the Policy Group of the Partner Manger|Policy does not belong to the Policy Group of the Partner Manger
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### PUT /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}
Partner Manager would be using this API to approve OR reject partner API key requests based on API key request id. During approval process of the request unique PartnerAPI Key is generated in Partner Management module, which is mapped to requested policies. Partner API Key would be having default active status, expiry of which would configurable.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
APIKeyReqID |Yes| APIKey Request ID |65432345634232

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.partnermanagement.partners.apikey.approval
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.status|Yes|status of the partner API Key that needs to update|Approved

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.approval",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "status": "Approved"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: PartnerAPIKey approved successfully.
```JSON
{
  "id": "mosip.partnermanagement.partners.apikeystatus.update",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "message": "PartnerAPIKey approved successfully"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Requested Partner API Key Request ID does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.apikeystatus.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_007",
      "message": "Partner api key Request ID does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_011|Partner api key Request ID does not exist|Partner api key Request ID does not exist
PMS_PMP_012|Partner Manager is denied permission to approve or reject the request|Partner Manager is denied permission to approve or reject the request
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /pmpartners
This API would be used to retrieve all Auth/E-KYC Partners for the policy group.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: retrieve the partner details for the particular policy group.
```JSON
{
  "id": "mosip.partnermanagement.partners.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
         "partners" : [
		    {
			   "partnerID":"65432345634232", 
		       "status":"Active", 
		       "organizationName":"telecomAirtel",
		       "contactNumber":"9876545654", 
		       "emailID":"telecomAirtel@gmail.com", 
		       "address":"India"
			},
			{
			   "partnerID":"87652345634232", 
		       "status":"Active", 
		       "organizationName":"telecomJio",
		       "contactNumber":"9988774654", 
		       "emailID":"telecomJio@gmail.com", 
		       "address":"India"
			}
		]	
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No partner Registered in the policy Group
```JSON
{
  "id": "mosip.partnermanagement.partners.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_004",
      "message": "No partner Registered in the policy Group"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_004|No Partners are registered in the Policy Group|No partner Registered in the policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /pmpartners/{partnerID}
This request will retrieve particular Auth/E-KYC Partners. pattern validation for partner id taken care internally.
#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/{partnerID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
partnerID |Yes| Partner ID|87652345634232

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: retrieve the partner details for the particular policy group.
```JSON
{
  "id": "mosip.partnermanagement.partners.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "partnerID":"87652345634232", 
		"status":"Active", 
		"organizationName":"telecomJio",
		"contactNumber":"9988774654", 
		"emailID":"telecomJio@gmail.com", 
		"address":"India"	
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Requested partner does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_013",
      "message": "Partner does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_013|Partner does not exist|Requested partner does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /pmpartners/{partnerID}/{PartnerAPIKey}
Partner managers would be using this request to retrieve the Partner API key to Policy Mappings. Partner management system would be able to validate Partner API Key pattern, validate expiry for Partner API Key and status details in background, while fetching Policy to Partner API mappings.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/{partnerID}/{PartnerAPIKey}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
partnerID |Yes| partnerID |87652345634232
PartnerAPIKey|Yes|PartnerAPIKey|fa604-affcd-33201-04770


#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: successfully retrieved the Partner API key to Policy Mappings.
```JSON
{
  "id": "mosip.partnermanagement.partners.retrieve.policy",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "partnerID":"87652345634232",
        "policyId":"77862345634232"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Requested partner does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.retrieve.policy",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_009",
      "message": "Partner api key does not belong to the Policy Group of the Partner Manger"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_007|Partner API Key does not exist|Requested Partner API Key does not exist
PMS_PMP_009|Partner api key does not belong to the Policy Group of the Partner Manger|Partner api key does not belong to the Policy Group of the Partner Manger
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /pmpartners/PartnerAPIKeyRequests
This request will retrieve all the Partner API key to Policy Mappings requests.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/PartnerAPIKeyRequests</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: successfully retrieved the Partner API key to Policy Mappings.
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.request.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "apikeyRequests" : [
	     {
			"partnerID":"87652345634232", 
			"status":"Active", 
			"organizationName":"telecomJio",
			"policyName": "Insurance Policy",
			"policyDesc": "Desc about policy",
			"apiKeyReqNo":"873276828663"
		 },
		 {
			"partnerID":"67678856342329", 
			"status":"Active", 
			"organizationName":"airtelInd",
			"policyName": "Banking Policy",
			"policyDesc": "Desc about policy",
			"apiKeyReqNo":"903276828609"
		 }
       ]	  
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No Partner api key requests for the Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.request.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_015",
      "message": "No Partner api key requests for the Policy Group"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_015|No Partner api key requests for the Policy Group|No Partner api key requests for the Policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error

### GET /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}
This request will retrieve the particular Partner API key to Policy Mappings request.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
APIKeyReqID |Yes| APIKey Request ID|873276828663

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: successfully retrieved the Partner API key requests for the partner manager.
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.requests.retrieve",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
			"partnerID":"87652345634232", 
			"status":"Active", 
			"organizationName":"telecomJio",
			"policyName": "Insurance Policy",
			"policyDesc": "Desc about policy",
			"apiKeyReqNo":"873276828663"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No Partner api key requests for the Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.request.retrieve",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PMP_015",
      "message": "No Partner api key requests for the Policy Group"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PMP_001|Partner Manager does not exist|Not a authorized Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Password of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_015|No Partner api key requests for the Policy Group|No Partner api key requests for the Policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_COR_003|Could not process the request|Any Internal Error