This section details about the service API in the Partner Management module.

#### Note:
If you want to access rest apis, access token is required from authmanager.
1. Authenticate through client-id/Secret or User Id/Password having respective roles assigned.
2. After successful authentication access token will set as Authorization cookies.
3. Access API through postman by passing the access token in cookies.

#### Admin Token
 url- https://dev.mosip.io/v1/authmanager/authenticate/useridPwd

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
#

* [MISP Management Service](#misp-management-service)

# MISP Management Service
This service is used to authenticate MOSIP Admin and management of MISP(MOSIP Infrastructure Service Provider).

* [POST /misps](#post-misps)
* [POST /misps/{mispId}](#put-mispsmispid)
* [POST /misps/{mispId}/licenseKey](#post-mispsmispidlicensekey)
* [PUT /misps/{mispId}](#put-mispsmispid)
* [PUT /misps/{mispId}/licenseKey](#put-mispsmispidlicensekey)
* [GET /misps/{mispOrgName}](#get-mispsmispOrgName)
* [GET /misps/{mispId}/licenseKey](#get-mispsmispidlicensekey)

### POST /misps
This request will send the MOSIP Admin credentials and misp details to get registered

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
request.address|Yes|MISP address|india

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
      "address": "india"
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
PMS_MISP_003|A MISP is already registered with name - organizationName|If MISP is already registered with organizationName
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation

### POST /misps/{mispId}
This request to update MISP with the parameters.

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
request.address|Optional|MISP address|india

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.update",
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "organizationName": "telecom",
      "contactNumber": "9876998888",
      "emailID": "prm@telecom.com",
      "address": "india"
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
      "address": "india"
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
PMS_MISP_007|No information provided for update|No information provided for update
PMS_MISP_008|MISP ID does not exist|MISP ID not available in database


### POST /misps/{mispId}/licenseKey
This request will validate MISPs LK - 
   1. Validate LK pattern.
   2. Validate LK is associated with the requested MISP id.
   3. Validate LK is active or not.

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
  "ver": "1.0",
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
      "errorCode": "PMS_MISP_010",
      "message": "MISP License key not valid"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MISP_001|MOSIP Admin does not exist|Un-authorized MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MISP_008|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
PMS_MISP_009|MISP License key not associated to MISP ID|MISP License key not associated to MISP in the input
PMS_MISP_010|MISP License key not valid|MISP License key not valid


### PUT /misps/{mispId}
This request to update MISP status.

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
request.msipStatus|Yes|MISP status|Deactive

#### Request:
```JSON
{
  "id": "mosip.partnermanagement.misp.status.update",
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "msipStatus": "Deactive"
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
      "message": "MISP deactived successfully"
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
      "errorCode": "PMS_MISP_011",
      "message": "Failed to update MISP status"
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
PMS_MISP_007|No information provided for update|No information provided for update
PMS_MISP_008|MISP ID does not exist|MISP ID not available in database
PMS_MISP_011|Failed to update MISP status|Failed to update the MISP status
PMS_MISP_012|MISP status already in the requested status|MISP status already in the requested status

### PUT /misps/{mispId}/licenseKey
This request will activate/deactivate MISPs LK (update MISP License Key Status)

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
  "ver": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "mispStatus": "Active",
      "mispLicenseKey": "fa604-affcd-33201-04770",
      "mispLicenseKeyStatus": "Deactive"
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
PMS_MISP_001|MOSIP Admin does not exist|Un-authorized MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MISP_007|No information provided for update|No information provided for update
PMS_MISP_008|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
PMS_MISP_009|MISP License key not associated to MISP ID|MISP License key not associated to MISP in the input


### GET /misps/{mispOrgName}
This request will retrieve the MISPs details
1. If MISP organitaion name present, then reterive all msip details for matching organization name.
2. If MISP organitaion name not present, then reterive all msip details. 

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
  "id": "mosip.partnermanagement.misp.reterive",
  "version": "1.0",
  "responsetime": "2019-05-14T16:01:20.534Z",
  "response": {
     "telecom": {
        "id": "64269837502851",
        "organizationName": "telecom",
        "contactNumber": "9876998888",
        "emailID": "prm@telecom.com",
        "address": "india",
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
        "address": "india",
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
  "id": "mosip.partnermanagement.misp.reterive",
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
PMS_MISP_001|MOSIP Admin does not exist|Un-authorized MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MISP_009|No MISP found for the organization|No MISP found for the organization

### GET /misps/{mispId}/licenseKey
This request download MISPs LK. If LK is expired then generate a new LK and associate with MISP ID and return.

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
  "id": "mosip.partnermanagement.misp.license.reterive",
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
  "id": "mosip.partnermanagement.misp.license.reterive",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_MISP_008",
      "message": "MISP ID/MISP License Key does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MISP_001|MOSIP Admin does not exist|Un-authorized MOSIP Admin- UserName not available in database
PMS_MISP_002|Mismatch of the MOSIP Admin Credentials|User Name and Password of the Admin does not match
PMS_MISP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MISP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MISP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation
PMS_MISP_008|MISP ID/MISP License Key does not exist|MISP ID/MISP License Key not available in database
