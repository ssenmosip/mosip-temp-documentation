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
* [Policy Management Service](#policy-management-service)
* [Partner Management Service](#partner-management-service)
* [Partner Service](#partner-service)

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
  "version": "1.0",
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
  "version": "1.0",
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
  "version": "1.0",
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


## Policy Management Service
This service is used to manage policies.

* [POST /policies](#post-policies)
* [POST /policies/{policyID}](#post-policiespolicyid)
* [PUT /policies/{policyID}](#put-policiespolicyid)
* [GET /policies](#get-policies)
* [GET /policies/{policyID}](#get-policiespolicyid)
* [GET /policies/{PartnerAPIKey}](#get-policiespartnerapikey)

### POST /policies
This request is used to create new Policy for policy group

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
            "is_active": true,
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

### POST /policies/{policyID}
This request is used to update existing policy for a policy group

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/45678451034176</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
		"is_active": true,
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

### PUT /policies/{policyID}
This request is used to update the existing policy status.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/45678451034176</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
		"status":"Deactive"
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
        "message" : "status updated sucessfully"
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

### GET /policies
This request will retrieve the policies available for my policy group so that he/she can place a request for a partner api key. 

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
		"name": "Insurence Policy",
		"desc": "Desc about policy",
		"is_active": true,
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
		"is_active": true,
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
###### Description: No active policy available in the Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partner.policies",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_POL_003",
      "message": "No active policy available in the Policy Group"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_POL_001|Policy Manager does not exist|If Policy Manager does not exist
PMS_POL_002|Mismatch of Policy Manager Credentials|If any mismatch of Policy Manager Credentials
PMS_POL_003|No active policy available in the Policy Group|No active policies exist in the policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /policies/{policyID}
This request is used to reterive existing policy for a policy group based on the policy id.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/45678451034176</div>

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
###### Description: policy reterived successfully
```JSON
{
  "id": "mosip.partnermanagement.policy.reterive",
  "version": "1.0",
  "responsetime": "2019-05-15T16:01:20.534Z",
  "response":{
		"id": "45678451034176",
		"name": "Loan Policy",
		"desc": "Desc about policy",
		"is_active": true,
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
  "id": "mosip.partnermanagement.policy.reterive",
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
PMS_POL_011|Policy Manager is denied permission to reterive the policy|if the policy manager is denied permission to reterive the policy
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /policies/{PartnerAPIKey}
This request will retrieve the partner policy details for given PartnerAPIKey. 

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/policies/fa604-affcd-33201-04770</div>

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
###### Description: retrieve the partner policy details for given PartnerAPIKey successful
```JSON
{
  "id": "mosip.partnermanagement.policies.reterive.partnerAPIKey",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
		"id": "32058251034176",
		"name": "Insurence Policy",
		"desc": "Desc about policy",
		"is_active": true,
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
  "id": "mosip.partnermanagement.policies.reterive.partnerAPIKey",
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


## Partner Management Service
This service enables partner managers to manage respective partners, manage partner API Key requests, manage PartnerAPIKeys to Policies mappings.

* [POST /pmpartners/{partnerID}/{PartnerAPIKey}](#post-pmpartnerspartneridpartnerapikey)
* [PUT /pmpartners/{partnerID}](#put-pmpartnerspartnerid)
* [PUT /pmpartners/{partnerID}/{PartnerAPIKey}](#put-pmpartnerspartneridpartnerapikey)
* [PUT /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}](#put-pmpartnerspartnerapikeyrequestapikeyreqid)
* [GET /pmpartners](#get-pmpartners)
* [GET /pmpartners/{partnerID}](#get-pmpartnerspartnerid)
* [GET /pmpartners/{partnerID}/{PartnerAPIKey}](#get-pmpartnerspartneridpartnerapikey)
* [GET /pmpartners/PartnerAPIKeyRequests](#get-pmpartnerspartnerapikeyrequest)
* [GET /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}](#get-pmpartnerspartnerapikeyrequestapikeyreqid)


### POST /pmpartners/{partnerID}/{PartnerAPIKey}
This request is used by partner Manager, to update Partner api key to Policy Mappings.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/65432345634232/fa604-affcd-33201-04770</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_008|Partner api key is not assigned to” + old policy ID+ “ hence cannot be updated with new policy|Partner api key is not assigned to old policy ID hence cannot be updated with new policy
PMS_PMP_009|Partner api key does not belong to the Policy Group of the Partner Manger|Partner api key does not belong to the Policy Group of the Partner Manger
PMS_PMP_010|Policy does not belong to the Policy Group of the Partner Manger|Policy does not belong to the Policy Group of the Partner Manger
PMS_PMP_011|Partner api key Request ID does not exist|Partner api key Request ID does not exist
PMS_PMP_014|Policy %d does not exist|Policy does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition



### PUT /pmpartners/{partnerID}
This request used to activate/deactivate Auth/E-KYC Partners

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/65432345634232</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
      "status": "Deactive"
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_005|Partner ID %d does not exist|Requested Partner ID does not exist
PMS_PMP_006|Partner Manager is denied permission to activate/deactivate Partner|Partner Manager is denied permission to activate/deactivate Partner
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### PUT /pmpartners/{partnerID}/{PartnerAPIKey}
This request used by the partner Manager, to update Partner api key to Policy Mappings

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/65432345634232/fa604-affcd-33201-04770</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_005|Partner ID %d does not exist|Requested Partner ID does not exist
PMS_PMP_006|Partner Manager is denied permission to activate/deactivate Partner|Partner Manager is denied permission to activate/deactivate Partner
PMS_PMP_007|Partner API Key does not exist|Requested Partner API Key does not exist
PMS_PMP_008|Partner api key is not assigned to” + old policy ID+ “ hence cannot be updated with new policy|Partner api key is not assigned to old policy ID hence cannot be updated with new policy
PMS_PMP_009|Partner api key does not belong to the Policy Group of the Partner Manger|Partner api key does not belong to the Policy Group of the Partner Manger
PMS_PMP_010|Policy does not belong to the Policy Group of the Partner Manger|Policy does not belong to the Policy Group of the Partner Manger
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### PUT /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}
This request used by the partner Manager, to approve/reject Partner api key requests based on api key request id.


#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/PartnerAPIKeyRequests/65432345634232</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.approvel",
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_011|Partner api key Request ID does not exist|Partner api key Request ID does not exist
PMS_PMP_012|Partner Manager is denied permission to approve or reject the request|Partner Manager is denied permission to approve or reject the request
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /pmpartners
This request will retrieve all Auth/E-KYC Partners for the particular policy group.

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
  "id": "mosip.partnermanagement.partners.reterive",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
         "partners" : [
		    {
			   "partnerID":"65432345634232", 
		       "status":"active", 
		       "organizationName":"telecomAirtel",
		       "contactNumber":"9876545654", 
		       "emailID":"telecomAirtel@gmial.com", 
		       "address":"India"
			},
			{
			   "partnerID":"87652345634232", 
		       "status":"active", 
		       "organizationName":"telecomJio",
		       "contactNumber":"9988774654", 
		       "emailID":"telecomJio@gmial.com", 
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
  "id": "mosip.partnermanagement.partners.reterive",
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_004|No Partners are registered in the Policy Group|No partner Registered in the policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /pmpartners/{partnerID}
This request will retrieve particular Auth/E-KYC Partners.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/87652345634232</div>

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
  "id": "mosip.partnermanagement.partners.reterive",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "partnerID":"87652345634232", 
		"status":"active", 
		"organizationName":"telecomJio",
		"contactNumber":"9988774654", 
		"emailID":"telecomJio@gmial.com", 
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
  "id": "mosip.partnermanagement.partners.reterive",
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_013|Partner does not exist|Requested partner does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /pmpartners/{partnerID}/{PartnerAPIKey}
This request will retrieve the Partner API key to Policy Mappings.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/87652345634232/fa604-affcd-33201-04770</div>

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
  "id": "mosip.partnermanagement.partners.reterive.policy",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
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
  "id": "mosip.partnermanagement.partners.reterive.policy",
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_007|Partner API Key does not exist|Requested Partner API Key does not exist
PMS_PMP_009|Partner api key does not belong to the Policy Group of the Partner Manger|Partner api key does not belong to the Policy Group of the Partner Manger
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

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
  "id": "mosip.partnermanagement.partners.apikey.request.reterive",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "apikeyRequests" : [
	     {
			"partnerID":"87652345634232", 
			"status":"active", 
			"organizationName":"telecomJio",
			"policyName": "Insurence Policy",
			"policyDesc": "Desc about policy",
			"apiKeyReqNo":"873276828663"
		 },
		 {
			"partnerID":"67678856342329", 
			"status":"active", 
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
  "id": "mosip.partnermanagement.partners.apikey.request.reterive",
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_015|No Partner api key requests for the Policy Group|No Partner api key requests for the Policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

### GET /pmpartners/PartnerAPIKeyRequests/{APIKeyReqID}
This request will retrieve the perticular Partner API key to Policy Mappings request.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/pmpartners/PartnerAPIKeyRequests/873276828663</div>

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
###### Description: successfully retrieved the Partner API key requests for the partner manager.
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.requests.reterive",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
			"partnerID":"87652345634232", 
			"status":"active", 
			"organizationName":"telecomJio",
			"policyName": "Insurence Policy",
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
  "id": "mosip.partnermanagement.partners.apikey.request.reterive",
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
PMS_PMP_001|Partner Manager does not exist|Not a authorised Partner Manager- UserName not available in database
PMS_PMP_002|Mismatch of the Partner Manager Credentials|User Name and Passoword of the Partner Manager does not match
PMS_PMP_003|Your password has expired. Please reset your password|Password expired
PMS_PMP_015|No Partner api key requests for the Policy Group|No Partner api key requests for the Policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

## Partner Service
This service enables partners to do self registration, submit request for respective authentication policies, sharing of digital certificate for secure communication: 

* [POST /partners](#post-partners)
* [POST /partners/{partnerID}/partnerAPIKeyRequest}](#post-partnerspartneridpartnerapikeyrequest)
* [POST /partners/{partnerID}/partnerAPIKeyRequest/{RequestID}](#post-partnerspartneridpartnerapikeyrequestrequestid)
* [POST /partners/digitalcertificate](#post-partnersdigitalcertificate)
* [PUT /partners/{partnerID}](#put-partnerspartnerid)
* [PUT /partners/digitalcertificate](#get-partnersdigitalcertificate)
* [GET /partners/{partnerID}](#post-partnerspartnerid)
* [GET /partners/{partnerID}/partnerAPIKeyRequest}](#get-partnerspartneridpartnerapikeyrequest)
* [GET /partners/{partnerID}/partnerAPIKeyRequest/{RequestID}](#get-partnerspartneridpartnerapikeyrequestrequestid)
* [GET /partners/digitalcertificate](#get-partnersdigitalcertificate)


### POST /partners
This request is used to create Auth/E-KYC Partners.

<div>https://mosip.io/partnermanagement/v1/partners</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.create",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "organizationName":"airtelInd", 
	  "contactNumber":"9886779980", 
	  "emailID":"airtelInd@gmail.com", 
	  "address":"INDIA",
	  "policyGroup":"Banking"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Partner successfully created.
```JSON
{
  "id": "mosip.partnermanagement.partners.create",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "partnerID":"6565655443544", 
	   "status":"active"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: A Partner is already registered with name ”+ Partner Organization Name+ “ in the policy Group +Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partners.create",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_001",
      "message": "A Partner is already registered with name 'airtelInd' in the policy Group 'Banking'.
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_001|A Partner is already registered with name %d in the policy Group %d|A Partner is already registered with name ”+ Partner Organization Name+ “ in the policy Group +Policy Group
PMS_PRT_002|Policy Group does not exist|Policy Group does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

### POST /partners/{partnerID}/partnerAPIKeyRequest
This request is used to submit Partner api key request.

<div>https://mosip.io/partnermanagement/v1/partners/6565655443544/partnerAPIKeyRequest</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partnerAPIKeyRequest.create",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
		"policyName":"airtelIndPolicy", 
		"useCaseDescription":"Need to submit the payment"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: partnerAPIKeyRequest successfully created.
```JSON
{
  "id": "mosip.partnermanagement.partnerAPIKeyRequest.create",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "apiRequestId":"873276828663",
       "message":"partnerAPIKeyRequest successfully created"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: A Partner is already registered with name ”+ Partner Organization Name+ “ in the policy Group +Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partnerAPIKeyRequest.create",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_001",
      "message": "A Partner is already registered with name 'airtelInd' in the policy Group 'Banking'.
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_001|A Partner is already registered with name %d in the policy Group %d|A Partner is already registered with name ”+ Partner Organization Name+ “ in the policy Group +Policy Group
PMS_PRT_002|Policy Group does not exist|Policy Group does not exist
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition



### POST /partners/{partnerID}/partnerAPIKeyRequest/{RequestID}
This request is used to download Partner API key for the given RequestID

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/6565655443544/partnerAPIKeyRequest/873276828663</div>

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
###### Description: successfully retrieved the partnerAPIKey.
```JSON
{
  "id": "mosip.partnermanagement.partnerAPIKey.download",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "partnerAPIKey":"fa604-affcd-33201-04770"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: RequestID does not exist
```JSON
{
  "id": "mosip.partnermanagement.partnerAPIKey.download",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_005",
      "message": "RequestID does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_PRT_006|RequestID does not exist|RequestID does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### POST /partners/digitalcertificate
This request used to upload partner's digital certificate.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/digitalcertificate</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.certificate.upload",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "partnerCertificate":"MIIFtjCCA56gAwIBAgIJAP1p0BePP1CFMA0GCSqGSIb3DQEBCwUAMHAxCzAJBgNV
                            UUTHNkNaMRcwFQYDVQQIDA5DemVjaCBSZXB1YmxpYzELMAkGA1UEBwwCQ0IxITAf
                            BgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDEYMBYGA1UEAwwPUkVTVCBB
                            UEkgU0VSVkVSMB4XDTE4MTAwNjIxMTQyMVoXDTI4MTAwMzIxMTQyMVowcDELMAkG
                            A1UEBhMCQ1oxFzAVBgNVBAgMDkN6ZWNoIFJlcHVibGljMQswCQYDVQQHDAJDQjEh
                            MB8GA1UECgwYSW50ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMRgwFgYDVQQDDA9SRVNU
                            IEFQSSBTRVJWRVIwggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQDF0BqJ
                            htgl5JJZM3zwDNN5l7rWcnN0Gp0A0fKY/rfyuSR/mQJ2W2DkX2ISvvRHaNsVwpVb
                            9Z1T0Dqa3RxgaGbgdc1AtTAAMzHWiPzCNtU="
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: successfully uploaded partner's digital certificate
```JSON
{
  "id": "mosip.partnermanagement.partners.certificate.upload",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "message":"successfully uploaded partner's digital certificate"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Partner digital certificate is not valid
```JSON
{
  "id": "mosip.partnermanagement.partners.reterive",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_007",
      "message": "Partner digital certificate is not valid"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_PRT_007|Partner digital certificate is not valid|Partner digital certificate is not valid
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

### PUT /partners/{partnerID}
This request is used to update Auth/E-KYC Partners.

<div>https://mosip.io/partnermanagement/v1/partners/6565655443544</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.update",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "organizationName":"airtelInd", 
	  "contactNumber":"9886779980", 
	  "emailID":"airtelInd@gmail.com", 
	  "address":"Bangalore,INDIA",
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Partner successfully updated.
```JSON
{
  "id": "mosip.partnermanagement.partners.update",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "partnerID":"6565655443544", 
	   "status":"active"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: A Partner is already registered with name ”+ Partner Organization Name+ “ in the policy Group +Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partners.update",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_001",
      "message": "A Partner is already registered with name 'airtelInd' in the policy Group 'Banking'.
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_001|A Partner is already registered with name %d in the policy Group %d|A Partner is already registered with name ”+ Partner Organization Name+ “ in the policy Group +Policy Group
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

### PUT /partners/digitalcertificate
This request used to validate partner's digital certificate.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/digitalcertificate</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Header 
Name | Required | Description | Comment
-----|----------|-------------|--------
Authorization | Yes | authentication token | Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYXZpLmJhbGFqaUBtaW5kdHJlZS5jb20iLCJtb2JpbGUiOiIiLCJtYWlsIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwicm9sZSI6IklORElWSURVQUwiLCJuYW1lIjoicmF2aS5iYWxhamlAbWluZHRyZWUuY29tIiwiaXNPdHBSZXF1aXJlZCI6dHJ1ZSwiaXNPdHBWZXJpZmllZCI6dHJ1ZSwiaWF0IjoxNTYyNTgwMzg0LCJleHAiOjE1NjI1ODYzODR9.eycrDnzPFBnx57wp6v-iXHtFnRxPgOysG3QETnElSswBUH5ojUUCLsn6SeYukIy-rEZ0SOdr9jkLE6A8tNkj4w


#### Request:
```JSON
{
  "id": "mosip.partnermanagement.partners.certificate.validate",
  "version": "1.0",
  "requesttime": "2019-05-20T09:48:43.394Z",
  "metadata": {},
  "request": {
      "partnerCertificate":"MIIFtjCCA56gAwIBAgIJAP1p0BePP1CFMA0GCSqGSIb3DQEBCwUAMHAxCzAJBgNV
                            UUTHNkNaMRcwFQYDVQQIDA5DemVjaCBSZXB1YmxpYzELMAkGA1UEBwwCQ0IxITAf
                            BgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDEYMBYGA1UEAwwPUkVTVCBB
                            UEkgU0VSVkVSMB4XDTE4MTAwNjIxMTQyMVoXDTI4MTAwMzIxMTQyMVowcDELMAkG
                            A1UEBhMCQ1oxFzAVBgNVBAgMDkN6ZWNoIFJlcHVibGljMQswCQYDVQQHDAJDQjEh
                            MB8GA1UECgwYSW50ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMRgwFgYDVQQDDA9SRVNU
                            IEFQSSBTRVJWRVIwggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQDF0BqJ
                            htgl5JJZM3zwDNN5l7rWcnN0Gp0A0fKY/rfyuSR/mQJ2W2DkX2ISvvRHaNsVwpVb
                            9Z1T0Dqa3RxgaGbgdc1AtTAAMzHWiPzCNtU="
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: successfully validated partner's digital certificate
```JSON
{
  "id": "mosip.partnermanagement.partners.certificate.upload",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "message":"successfully validated partner's digital certificate"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Partner digital certificate is not valid
```JSON
{
  "id": "mosip.partnermanagement.partners.reterive",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_007",
      "message": "Partner digital certificate is not valid"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_PRT_007|Partner digital certificate is not valid|Partner digital certificate is not valid
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /partners/{partnerID}
This request should be able to retrieve Auth/E-KYC Partners.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/6565655443544</div>

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
###### Description: successfully retrieved the Partner details.
```JSON
{
  "id": "mosip.partnermanagement.partners.reterive",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "partnerID":"6565655443544", 
		"status":"active", 
		"organizationName":"airtelInd", 
	    "contactNumber":"9886779980", 
	    "emailID":"airtelInd@gmail.com", 
	    "address":"INDIA",
	    "policyGroup":"Banking"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Partner does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.reterive",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_005",
      "message": "Partner does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

### GET /partners/{partnerID}/partnerAPIKeyRequest
This request should be able to retrieve policies available for my policy group so that i can place a request for a partner api key.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/6565655443544/partnerAPIKeyRequest</div>

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
###### Description: successfully retrieved all active policies available for my policy group.
```JSON
{
  "id": "mosip.partnermanagement.partners.reterive.policies",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
       "policies": [
	      {
			"id": "32058251034176",
			"name": "Insurence Policy",
			"desc": "Desc about policy",
			"is_active": true,
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
			"is_active": true,
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
###### Description: No active policy available in the Policy Group
```JSON
{
  "id": "mosip.partnermanagement.partners.reterive.policies",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_008",
      "message": "No active policy available in the Policy Group"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_PRT_008|No active policy available in the Policy Group|No active policy available in the Policy Group
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

### GET /partners/{partnerID}/partnerAPIKeyRequest/{RequestID}
This request is used to view Partner api key/partner api key request status

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/6565655443544/partnerAPIKeyRequest/873276828663</div>

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
###### Description: successfully reterived Partner api key/partner api key request status
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.status",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "apiKeyRequestStatus":"approved", 
		"partnerApiKey":"fa604-affcd-33201-04770",
		"validityTill":"2019-11-01"
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: RequestID does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.apikey.status",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_006",
      "message": "RequestID does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_PRT_006|RequestID does not exist|RequestID does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition


### GET /partners/digitalcertificate
This request used to reterive MOSIP digital certificate.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/partners/digitalcertificate</div>

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
###### Description: successfully reterived mosip digital certificate
```JSON
{
  "id": "mosip.partnermanagement.partners.mosip.certificate.download",
  "version": "1.0",
  "responsetime": "2019-05-16T16:01:20.534Z",
  "response":{
        "moispCertificate":"MIIFtjCCA56gAwIBAgIJAP1p0BePP1CFMA0GCSqGSIb3DQEBCwUAMHAxCzAJBgNV
                            UUTHNkNaMRcwFQYDVQQIDA5DemVjaCBSZXB1YmxpYzELMAkGA1UEBwwCQ0IxITAf
                            BgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDEYMBYGA1UEAwwPUkVTVCBB
                            UEkgU0VSVkVSMB4XDTE4MTAwNjIxMTQyMVoXDTI4MTAwMzIxMTQyMVowcDELMAkG
                            A1UEBhMCQ1oxFzAVBgNVBAgMDkN6ZWNoIFJlcHVibGljMQswCQYDVQQHDAJDQjEh
                            MB8GA1UECgwYSW50ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMRgwFgYDVQQDDA9SRVNU
                            IEFQSSBTRVJWRVIwggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQDF0BqJ
                            htgl5JJZM3zwDNN5l7rWcnN0Gp0A0fKY/rfyuSR/mQJ2W2DkX2ISvvRHaNsVwpVb
                            9Z1T0Dqa3RxgaGbgdc1AtTAAMzHWiPzCNtU="
  },
  "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Partner does not exist
```JSON
{
  "id": "mosip.partnermanagement.partners.mosip.certificate.download",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PMS_PRT_005",
      "message": "Partner does not exist"
    }
  ]
}
```

#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_PRT_003|Mismatch of the Partner Credentials|User Name and Passoword of the Admin does not match
PMS_PRT_004|Your password has expired. Please reset your password|Password expired
PMS_PRT_005|Partner does not exist|Partner does not exist
PMS_COR_001|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_COR_002|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition

