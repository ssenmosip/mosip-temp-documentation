This section details about the service API in the Partner Management module.

* [User Management Service](#user-management-service)


# User Management Service
This service used to authenticate MOSIP Admin and management of MISP(MOSIP Infrastructure Service Provider).

* [POST /msip](#post-msip)
* [PUT /msip](#put-msip)
* [PUT /msip/license](#post-msiplicense)
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

#### Request Part Parameters
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
###### For SMS:

```JSON
{
    "id":"mosip.partnermanagement.msip.create",
    "ver":"1.0",
    "requesttime":"2019-05-20T09:48:43.394Z",
    "request" :
    {
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
        "mispStatus":"String",//encrypt
        "mispLicenseKey":"String",
        "mispLicenseKeyExpiry":LocalDate,//regex
        "mispLicenseKeyStatus":"String"//regex
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
      "errorCode": "PMS_MSIP_001",
      "message": "MOSIP Admin does not exist"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PMS_MSIP_002|Mismatch of the MOSIP Admin Credentials|User Name and Passoword of the Admin does not match
PMS_MSIP_003|A MISP is already registered with name MISP Organization Name|MISP already registered
PMS_MSIP_004|Missing Input Parameter - %d|Missing Input Parameter - for all mandatory attributes
PMS_MSIP_005|Invalid Input Parameter - %d |Invalid Input Parameter - for all attributes not as per defined data definition
PMS_MSIP_006|Could not process the request|Internal Error due to MISP ID/MISP License Key Generation

### PUT /msip
This request to update MISP with the parameters.

#### Resource URL
<div>https://mosip.io/partnermanagement/v1/msip</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
  "requesttime": "2019-06-03T08:28:04.783Z",
  "request": {
    "otp": "345674",
    "userId": "8907654778"
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
  "responsetime": "2019-06-03T06:47:10.838Z",
  "response": {
    "message": "VALIDATION_SUCCESSFUL",
    "status": "success"
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
      "errorCode": "KER-OTV-005",
      "message": "Validation can't be performed against this key. Generate OTP first."
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
KER-ATH-003|User Detail doesn't exist.|If userId is empty or invalid
KER-OTV-003|OTP can't be empty or null.|  If otp field is empty or null
KER-OTV-004|OTP consists of only numeric characters. No other characters is allowed|If otp contains character other than numeric
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request version
PRG_PAM_CORE_003|Invalid request time |Empty Request time
PRG_CORE_REQ_013|Request date should be current date|If request date is not current date
PRG_PAM_LGN_013|VALIDATION_UNSUCCESSFUL|If incorrect otp is entered
PRG_PAM_LGN_014|Token is not present in the header |When token does not come from kernel service in the header

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
  "id": "mosip.pre-registration.login.invalidate",
  "version": "1.0",
  "responsetime": "2019-05-16T09:37:04.941Z",
  "response": {
    "message": "Token has been invalidated successfully",
    "status": "success"
  },
  "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Token is not present in cookies
```JSON
{
  "id": "mosip.pre-registration.login.invalidate",
  "version": "1.0",
  "responsetime": "2019-06-14T08:41:17.156Z",
  "response": null,
  "errors": [
    {
      "errorCode": "KER-ATH-007",
      "message": "Token is not present in cookies"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
KER-ATH-007|Token is not present in datastore,Please try with new token|If token is not present in datastore
KER-ATH-006|Cookies are empty|When no Cookie is passed in the header

### GET /login/config
This request will load the configuration parameters while loading the pre-registration portal page.

##### Note: All the values are retrieving from the pre-registration config properties file. If any value get changed in the config properties file it will get reflected in the response of this API. Following mentioned response is the sample of that.

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
  "id": "mosip.pre-registration.login.config",
  "version": "1.0",
  "responsetime": "2019-05-14T16:01:20.534Z",
  "response": {
    "mosip.kernel.otp.default-length": "6",
    "mosip.id.validation.identity.postalCode": "^[(?i)A-Z0-9]{5}$",
    "mosip.left_to_right_orientation": "eng,fra",
    "preregistration.recommended.centers.locCode": "5",
    "mosip.kernel.otp.validation-attempt-threshold": "10",
    "mosip.country.code": "MOR",
    "mosip.primary-language": "fra",
    "preregistration.timespan.cancel": "1",
    "mosip.default.dob.month": "01",
    "mosip.preregistration.auto.logout.timeout": "60",
    "preregistration.availability.noOfDays": "5",
    "mosip.kernel.otp.expiry-time": "180",
    "mosip.id.validation.identity.dateOfBirth": "^\\d{4}/([0]\\d|1[0-2])/([0-2]\\d|3[01])$",
    "mosip.supported-languages": "eng,ara,fra",
    "preregistration.workflow.documentupload": "true/false",
    "preregistration.workflow.demographic": "true/false",
    "preregistration.documentupload.allowed.file.nameLength": "50",
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
    "preregistration.workflow.booking": "true/false",
    "mosip.preregistration.auto.logout.ping": "30 ",
    "mosip.id.validation.identity.CNIENumber.length": "30",
    "mosip.id.validation.identity.fullName.[*].value": "^(?=.{0,50}$).*",
    "mosip.id.validation.identity.addressLine1.[*].value": "^(?=.{0,50}$).*",
    "mosip.login.mode": "email,mobile",
    "mosip.id.validation.identity.phone.length": "10",
    "mosip.preregistration.auto.logout.idle": "180",
    "preregistration.auto.logout": "10",
    "mosip.secondary-language": "ara",
    "preregistration.nearby.centers": "2000",
    "preregistration.documentupload.allowed.file.size": "1000000",
    "mosip.default.dob.day": "01",
    "preregistration.booking.offset": "1",
    "preregistration.documentupload.allowed.file.type": "application/pdf,image/jpeg,image/png,image/gif"
  },
  "errors": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_AUTH_012|	Config file not found in the config server|	If config file is missing in the config server
