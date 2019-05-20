This section details about the service API in the Pre-Registration modules.


* [Login Service](#login-service-public)

* [Demographic Service](#demographic-service-public)

* [Document Service](#document-service-public)

* [DataSync Service](#datasync-service-external)

* [Booking Service](#booking-service-public)

* [BatchJob Service](#batchjob-service-private)

* [Generate QR code service](#generate-qr-code-service-public)

* [Notification Service](#notification-service-public)

* [Transliteration Service](#transliteration-service-public)

**Note**: id, version and requesttime in request and responsetime in response bodies are optional fields and not consumed by pre registration application unless defined. Though we need to pass these as part of the request, it should not be tested.
Few of the error messages are intended for API consumer, who are mostly SI and developers. User friendly messages need to be mapped in the UI reference implementation. 

API testing Prerequisites
~~~
1. Generate a Authorization Token by using following Kernel AuthManager APIs
     a. To send an OTP [/authmanager/sendOTPUsingPOST](https://github.com/mosip/mosip/wiki/AuthN-&-AuthZ-APIs#post-v10authenticatesendotp)
     b. To validate the OTP [/authmanager/userIdOTPUsingPOST](https://github.com/mosip/mosip/wiki/AuthN-&-AuthZ-APIs#post-v10authenticateuseridotp)
   Once OTP get validate successfully you will get the Authorization token. 
2. Use this Authorization token in the every request header of all pre-registration APIs.
~~~
***

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


#### Request:
```JSON
{
	"id": "mosip.pre-registration.login.sendotp",
	"version": "1.0",
	"requesttime": "2019-05-14T07:24:47.605Z",
	"request": {	
		"userId": "8907654778"
	}
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: OTP sent successfully to specified channel
```JSON
{
  "id": "mosip.pre-registration.login.sendotp",
  "version": "1.0",
  "responsetime": "2019-05-14T07:25:00.803Z",
  "response": {
    "message": "Email Request submitted",
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
  "id": "mosip.pre-registration.login.sendotp",
  "version": "1.0",
  "responsetime": "2019-05-14T16:46:39.582Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PRG_AUTH_001",
      "message": "OTP failed to send through a specified channel"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_LGN_008|	Invalid Request userId received|	If requested userId is invalid
PRG_PAM_CORE_001|   Request id is invalid|  Invalid or empty Request Id
PRG_PAM_CORE_002 |   Request version is invalid |Invalid or empty Request version
PRG_PAM_CORE_003    | Request timestamp is invalid |Invalid or empty Request time
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
	"requesttime": "2019-03-15T08:28:04.783Z",
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
  "responsetime": "",
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
  "responsetime": "2019-05-14T18:03:12.305Z",
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
KER-OTV-003 |	OTP can't be empty or null.	|   If otp field is null
KER-OTV-004 |   OTP consists of only numeric characters. No other characters is allowed. | If otp contains character other than numeric
KER-OTV-005|Validation can't be performed against this key. Generate OTP first.|If validation has already done against the generated otp
PRG_AUTH_002    |   Authentication failed   | If userId field is null or invalid
PRG_PAM_CORE_001|   Request id is invalid|  Invalid or empty Request Id
PRG_PAM_CORE_002 |   Request version is invalid |Invalid or empty Request version
PRG_PAM_CORE_003    | Request timestamp is invalid |Invalid or empty Request time
PRG_CORE_REQ_013  | Request date should be current date | If the date is not current date
PRG_PAM_LGN_013|	OTP_EXPIRED|	If otp expired
PRG_PAM_LGN_008 |   Invalid Request userId received | if request id is invalid or empty

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
  "responsetime": "2019-05-14T18:14:25.546Z",
  "response": null,
  "errors": [
    {
      "errorCode": "KER-ATH-005",
      "message": "Token is not present in cookies"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
KER-ATH-007| Token is not present in datastore,Please try with new token | If token is not present in database

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


# Demographic Service (public)
This service details used by Pre-Registration portal to maintain the demographic data by providing his/her basic details.

* [POST /applications](#post-applications)
* [PUT /applications/{preRegistrationId}](#put-applicationspreRegistrationid)
* [GET /applications/{preRegistrationId}](#get-applicationspreRegistrationid)
* [GET /applications/status/{preRegistrationId}](#get-applicationsstatuspreRegistrationid)
* [GET /applications](#get-applications)
* [DELETE /applications/{preRegistrationId}](#delete-applicationspreRegistrationid)

### POST /applications
This request is used to create new pre-registration with demographic details, which generates pre-registration id and associates it with demographic details.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.demographic.create
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.langCode |Yes|primary language code|  value will be derived from UI
request.demographicDetails |Yes|demographicDetails of the applicant|
request.demographicDetails.identity |Yes|identity of the applicant|
request.demographicDetails.identity.gender |Yes|gender of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.city |Yes|city of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.phone |Yes|mobile number of the applicant|
request.demographicDetails.identity.IDSchemaVersion|Yes|id schema version|1
request.demographicDetails.identity.fullName |Yes|full name of the applicant|
request.demographicDetails.identity.localAdministrativeAuthority |Yes|local Administrative Authority code of the application| value will be derived from the domain metadata
request.demographicDetails.identity.dateOfBirth |Yes|date of birth of the applicant|
request.demographicDetails.identity.email |Yes|email Id of the applicant|
request.demographicDetails.identity.province |Yes|province of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.postalCode |Yes|postal code of the applicant|
request.demographicDetails.identity.addressLine1 |Yes|address Line 1 of the applicant|
request.demographicDetails.identity.addressLine2 |Yes|address Line 2 of the applicant|
request.demographicDetails.identity.addressLine3 |Yes|address Line 3 of the applicant|
request.demographicDetails.identity.region |Yes|region of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.residenceStatus|Yes|residence status of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.CNIENumber|Yes|CNIE Number of the applicant|

#### Request:
```JSON
{
  "id": "mosip.pre-registration.demographic.create",
  "version": "1.0",
  "requesttime": "2019-05-20T07:22:57.086Z",
  "request":{
      "langCode":"fra",
      "demographicDetails":{
         "identity":{
            "IDSchemaVersion":1,
            "fullName":[
               {
                  "language":"fra",
                  "value":"Shashank"
               },
               {
                  "language":"ara",
                  "value":"سهَسهَنك "
               }
            ],
            "dateOfBirth":"1993/12/12",
            "gender":[
               {
                  "language":"fra",
                  "value":"MLE"
               },
               {
                  "language":"ara",
                  "value":"MLE"
               }
            ],
            "addressLine1":[
               {
                  "language":"fra",
                  "value":"005-DS Max Silicon"
               },
               {
                  "language":"ara",
                  "value":"٠٠٥-دس مَكس سِلِكُن"
               }
            ],
            "residenceStatus":[
               {
                  "language":"fra",
                  "value":"NFR"
               },
               {
                  "language":"ara",
                  "value":"NFR"
               }
            ],
            "addressLine2":[
               {
                  "language":"fra",
                  "value":"Global Village"
               },
               {
                  "language":"ara",
                  "value":"گلُبَل ڤِللَگِ"
               }
            ],
            "addressLine3":[
               {
                  "language":"fra",
                  "value":"Karnataka"
               },
               {
                  "language":"ara",
                  "value":"كَرنَتَكَ"
               }
            ],
            "region":[
               {
                  "language":"fra",
                  "value":"RSK"
               },
               {
                  "language":"ara",
                  "value":"RSK"
               }
            ],
            "province":[
               {
                  "language":"fra",
                  "value":"KTA"
               },
               {
                  "language":"ara",
                  "value":"KTA"
               }
            ],
            "city":[
               {
                  "language":"fra",
                  "value":"BNMR"
               },
               {
                  "language":"ara",
                  "value":"BNMR"
               }
            ],
            "localAdministrativeAuthority":[
               {
                  "language":"fra",
                  "value":"14022"
               },
               {
                  "language":"ara",
                  "value":"14022"
               }
            ],
            "postalCode":"56059",
            "phone":"8680958812",
            "email":"shashank@gmail.com",
            "CNIENumber":"9182345678456"
         }
      }
   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Pre-Registration successfully Created
```JSON
{
    "id": "mosip.pre-registration.demographic.create",
    "version": "1.0",
    "responsetime": "2019-05-20T05:51:41.253Z",
    "response": {
        "preRegistrationId": "37149356189473",
        "createdDateTime": "2019-05-20T05:51:41.085Z",
        "statusCode": "Pending_Appointment",
        "langCode": "fra",
        "demographicDetails": {
            "identity": {
                "CNIENumber": "9182345678456",
                "gender": [
                    {
                        "language": "fra",
                        "value": "MLE"
                    },
                    {
                        "language": "ara",
                        "value": "MLE"
                    }
                ],
                "city": [
                    {
                        "language": "fra",
                        "value": "BNMR"
                    },
                    {
                        "language": "ara",
                        "value": "BNMR"
                    }
                ],
                "postalCode": "56059",
                "fullName": [
                    {
                        "language": "fra",
                        "value": "Shashank"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "localAdministrativeAuthority": [
                    {
                        "language": "fra",
                        "value": "14022"
                    },
                    {
                        "language": "ara",
                        "value": "14022"
                    }
                ],
                "dateOfBirth": "1993/12/12",
                "IDSchemaVersion": 1,
                "province": [
                    {
                        "language": "fra",
                        "value": "KTA"
                    },
                    {
                        "language": "ara",
                        "value": "KTA"
                    }
                ],
                "phone": "8680958812",
                "addressLine1": [
                    {
                        "language": "fra",
                        "value": "005-DS Max Silicon"
                    },
                    {
                        "language": "ara",
                        "value": "٠٠٥-دس مَكس سِلِكُن"
                    }
                ],
                "residenceStatus": [
                    {
                        "language": "fra",
                        "value": "NFR"
                    },
                    {
                        "language": "ara",
                        "value": "NFR"
                    }
                ],
                "addressLine2": [
                    {
                        "language": "fra",
                        "value": "Global Village"
                    },
                    {
                        "language": "ara",
                        "value": "گلُبَل ڤِللَگِ"
                    }
                ],
                "addressLine3": [
                    {
                        "language": "fra",
                        "value": "Karnataka"
                    },
                    {
                        "language": "ara",
                        "value": "كَرنَتَكَ"
                    }
                ],
                "region": [
                    {
                        "language": "fra",
                        "value": "RSK"
                    },
                    {
                        "language": "ara",
                        "value": "RSK"
                    }
                ],
                "email": "shashank@gmail.com"
            }
        }
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: invalid or empty request id
```JSON
{
    "id": "mosip-registration.demographic.create",
    "version": "1.0",
    "responsetime": "2019-05-20T05:52:20.435Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_CORE_001",
            "message": "Request id is invalid"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime
PRG_CORE_REQ_013|Request date should be current date|when the date is not current or future date
PRG_CORE_REQ_014|Lang code is invalid|when language code is invalid or empty
PRG_PAM_CORE_011|encryption failed|encryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed
PRG_PAM_CORE_010|hashing failed|demographic data hashing failed
PRG_PAM_CORE_012|decryption failes|decryption of demographic data failed

### PUT /applications/{preRegistrationId}
This request is used to update pre-registration's demographic details by providing pre-registration id in the path parameter and updated demographic details in request body.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/{preRegistrationId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|pre-registration id of the application|64269837502851

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.demographic.create
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.langCode |Yes|primary language code|  value will be derived from UI
request.demographicDetails |Yes|demographicDetails of the applicant|
request.demographicDetails.identity |Yes|identity of the applicant|
request.demographicDetails.identity.gender |Yes|gender of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.city |Yes|city of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.phone |Yes|mobile number of the applicant|
request.demographicDetails.identity.IDSchemaVersion|Yes|id schema version|1
request.demographicDetails.identity.fullName |Yes|full name of the applicant|
request.demographicDetails.identity.localAdministrativeAuthority |Yes|local Administrative Authority code of the application| value will be derived from the domain metadata
request.demographicDetails.identity.dateOfBirth |Yes|date of birth of the applicant|
request.demographicDetails.identity.email |Yes|email Id of the applicant|
request.demographicDetails.identity.province |Yes|province of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.postalCode |Yes|postal code of the applicant|
request.demographicDetails.identity.addressLine1 |Yes|address Line 1 of the applicant|
request.demographicDetails.identity.addressLine2 |Yes|address Line 2 of the applicant|
request.demographicDetails.identity.addressLine3 |Yes|address Line 3 of the applicant|
request.demographicDetails.identity.region |Yes|region of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.residenceStatus|Yes|residence status of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.CNIENumber|Yes|CNIE Number of the applicant|

#### Request:
```JSON
{
  "id": "mosip.pre-registration.demographic.update",
  "version": "1.0",
  "requesttime": "2019-05-20T07:22:57.086Z",
  "request":{
      "langCode":"fra",
      "demographicDetails":{
         "identity":{
            "IDSchemaVersion":1,
            "fullName":[
               {
                  "language":"fra",
                  "value":"Rakesh P"
               },
               {
                  "language":"ara",
                  "value":"سهَسهَنك "
               }
            ],
            "dateOfBirth":"1993/12/12",
            "gender":[
               {
                  "language":"fra",
                  "value":"MLE"
               },
               {
                  "language":"ara",
                  "value":"MLE"
               }
            ],
            "addressLine1":[
               {
                  "language":"fra",
                  "value":"005-DS Max Silicon"
               },
               {
                  "language":"ara",
                  "value":"٠٠٥-دس مَكس سِلِكُن"
               }
            ],
            "residenceStatus":[
               {
                  "language":"fra",
                  "value":"NFR"
               },
               {
                  "language":"ara",
                  "value":"NFR"
               }
            ],
            "addressLine2":[
               {
                  "language":"fra",
                  "value":"Global Village"
               },
               {
                  "language":"ara",
                  "value":"گلُبَل ڤِللَگِ"
               }
            ],
            "addressLine3":[
               {
                  "language":"fra",
                  "value":"Karnataka"
               },
               {
                  "language":"ara",
                  "value":"كَرنَتَكَ"
               }
            ],
            "region":[
               {
                  "language":"fra",
                  "value":"RSK"
               },
               {
                  "language":"ara",
                  "value":"RSK"
               }
            ],
            "province":[
               {
                  "language":"fra",
                  "value":"KTA"
               },
               {
                  "language":"ara",
                  "value":"KTA"
               }
            ],
            "city":[
               {
                  "language":"fra",
                  "value":"BNMR"
               },
               {
                  "language":"ara",
                  "value":"BNMR"
               }
            ],
            "localAdministrativeAuthority":[
               {
                  "language":"fra",
                  "value":"14022"
               },
               {
                  "language":"ara",
                  "value":"14022"
               }
            ],
            "postalCode":"56059",
            "phone":"9680958812",
            "email":"rak@gmail.com",
            "CNIENumber":"9182345678456"
         }
      }
   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Pre-Registration demographic details successfully updated
```JSON
{
    "id": "mosip.pre-registration.demographic.update",
    "version": "1.0",
    "responsetime": "2019-05-20T06:30:38.091Z",
    "response": {
        "preRegistrationId": "32042841521591",
        "updatedDateTime": "2019-05-20T06:25:00.262Z",
        "statusCode": "Pending_Appointment",
        "langCode": "fra",
        "demographicDetails": {
            "identity": {
                "CNIENumber": "9182345678456",
                "gender": [
                    {
                        "language": "fra",
                        "value": "MLE"
                    },
                    {
                        "language": "ara",
                        "value": "MLE"
                    }
                ],
                "city": [
                    {
                        "language": "fra",
                        "value": "BNMR"
                    },
                    {
                        "language": "ara",
                        "value": "BNMR"
                    }
                ],
                "postalCode": "56059",
                "fullName": [
                    {
                        "language": "fra",
                        "value": "Rakesh P"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "localAdministrativeAuthority": [
                    {
                        "language": "fra",
                        "value": "14022"
                    },
                    {
                        "language": "ara",
                        "value": "14022"
                    }
                ],
                "dateOfBirth": "1993/12/12",
                "IDSchemaVersion": 1,
                "province": [
                    {
                        "language": "fra",
                        "value": "KTA"
                    },
                    {
                        "language": "ara",
                        "value": "KTA"
                    }
                ],
                "phone": "9680958812",
                "addressLine1": [
                    {
                        "language": "fra",
                        "value": "005-DS Max Silicon"
                    },
                    {
                        "language": "ara",
                        "value": "٠٠٥-دس مَكس سِلِكُن"
                    }
                ],
                "residenceStatus": [
                    {
                        "language": "fra",
                        "value": "NFR"
                    },
                    {
                        "language": "ara",
                        "value": "NFR"
                    }
                ],
                "addressLine2": [
                    {
                        "language": "fra",
                        "value": "Global Village"
                    },
                    {
                        "language": "ara",
                        "value": "گلُبَل ڤِللَگِ"
                    }
                ],
                "addressLine3": [
                    {
                        "language": "fra",
                        "value": "Karnataka"
                    },
                    {
                        "language": "ara",
                        "value": "كَرنَتَكَ"
                    }
                ],
                "region": [
                    {
                        "language": "fra",
                        "value": "RSK"
                    },
                    {
                        "language": "ara",
                        "value": "RSK"
                    }
                ],
                "email": "rak@gmail.com"
            }
        }
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid preregistration id or data is not found for that preregistration id.
```JSON
{
    "id": "mosip.pre-registration.demographic.update",
    "version": "1.0",
    "responsetime": "2019-05-20T06:31:35.160Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No data found for the requested pre-registration id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime
PRG_CORE_REQ_013|Request date should be current date|when the date is not current or future date
PRG_PAM_CORE_011|encryption failed|encryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed
PRG_PAM_CORE_010|hashing failed|demographic data hashing failed
PRG_PAM_CORE_012|decryption failes|decryption of demographic data failed

### GET /applications/{preRegistrationId}
This request is used to retrieve Pre-Registration demographic data by pre-Registration id provided in request path parameter.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/{preRegistrationId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|32042841521591

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Demographic data successfully retrieved
```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.details",
    "version": "1.0",
    "responsetime": "2019-05-20T06:33:08.516Z",
    "response": {
        "preRegistrationId": "32042841521591",
        "createdBy": "8754462073",
        "createdDateTime": "2019-05-20T06:25:00.262Z",
        "updatedBy": "8754462073",
        "updatedDateTime": "2019-05-20T06:30:37.900Z",
        "statusCode": "Pending_Appointment",
        "langCode": "fra",
        "demographicDetails": {
            "identity": {
                "CNIENumber": "9182345678456",
                "gender": [
                    {
                        "language": "fra",
                        "value": "MLE"
                    },
                    {
                        "language": "ara",
                        "value": "MLE"
                    }
                ],
                "city": [
                    {
                        "language": "fra",
                        "value": "BNMR"
                    },
                    {
                        "language": "ara",
                        "value": "BNMR"
                    }
                ],
                "postalCode": "56059",
                "fullName": [
                    {
                        "language": "fra",
                        "value": "Rakesh P"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "localAdministrativeAuthority": [
                    {
                        "language": "fra",
                        "value": "14022"
                    },
                    {
                        "language": "ara",
                        "value": "14022"
                    }
                ],
                "dateOfBirth": "1993/12/12",
                "IDSchemaVersion": 1,
                "province": [
                    {
                        "language": "fra",
                        "value": "KTA"
                    },
                    {
                        "language": "ara",
                        "value": "KTA"
                    }
                ],
                "phone": "9680958812",
                "addressLine1": [
                    {
                        "language": "fra",
                        "value": "005-DS Max Silicon"
                    },
                    {
                        "language": "ara",
                        "value": "٠٠٥-دس مَكس سِلِكُن"
                    }
                ],
                "residenceStatus": [
                    {
                        "language": "fra",
                        "value": "NFR"
                    },
                    {
                        "language": "ara",
                        "value": "NFR"
                    }
                ],
                "addressLine2": [
                    {
                        "language": "fra",
                        "value": "Global Village"
                    },
                    {
                        "language": "ara",
                        "value": "گلُبَل ڤِللَگِ"
                    }
                ],
                "addressLine3": [
                    {
                        "language": "fra",
                        "value": "Karnataka"
                    },
                    {
                        "language": "ara",
                        "value": "كَرنَتَكَ"
                    }
                ],
                "region": [
                    {
                        "language": "fra",
                        "value": "RSK"
                    },
                    {
                        "language": "ara",
                        "value": "RSK"
                    }
                ],
                "email": "rak@gmail.com"
            }
        }
    },
    "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id.
```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.details",
    "version": "1.0",
    "responsetime": "2019-05-20T06:35:18.678Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No data found for the requested pre-registration id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_010|hashing failed|demographic data hashing failed
PRG_PAM_CORE_012|decryption failes|decryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed

### GET /applications/status/{preRegistrationId}
This request is used to retrieve pre-registration application status by providing the pre-registration id in request path parameter.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/status/{preRegistrationId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameter
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|62076019780925

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications status fetched successfully

```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.status",
    "version": "1.0",
    "responsetime": "2019-05-14T16:17:19.601Z",
    "response": {
        "preRegistartionId": "29810389154051",
        "statusCode": "Pending_Appointment"
    },
    "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id.
```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.status",
    "version": "1.0",
    "responsetime": "2019-05-14T16:17:34.330Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No data found for the requested pre-registration id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_010|hashing failed|demographic data hashing failed

### GET /applications
This request is used to retrieve all Pre-Registration id, Full name in both language, Status Code and Appointment details and Postal Code by user id from authorization token.

### Without pagination
if pageIndex parameter is not passed as query param, then all the demographic data for the user will be retrieved without applying pagination mechanism.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications</div>

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
    "id": "mosip.pre-registration.demographic.retrieve.basic",
    "version": "1.0",
    "responsetime": "2019-05-20T07:10:24.850Z",
    "response": {
        "basicDetails": [
            {
                "preRegistrationId": "32042841521591",
                "fullname": [
                    {
                        "language": "fra",
                        "value": "Rakesh P"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "statusCode": "Pending_Appointment",
                "bookingRegistrationDTO": null,
                "postalCode": "56059"
            },
            {
                "preRegistrationId": "38469435683243",
                "fullname": [
                    {
                        "language": "fra",
                        "value": "Shashank"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "statusCode": "Pending_Appointment",
                "bookingRegistrationDTO": null,
                "postalCode": "56059"
            }
        ],
        "totalRecords": "2",
        "noOfRecords": "0",
        "pageIndex": "0"
    },
    "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No record found for the requested user id.
```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.basic",
    "version": "1.0",
    "responsetime": "2019-05-20T07:12:37.316Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No record found for the requested user id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_010|hashing failed|demographic data hashing failed
PRG_PAM_CORE_012|decryption failed|decryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed

### With pagination
if pageIndex parameter is passed as query param, then all the demographic data for the user will be retrieved in terms of pages.
pageSize parameter is configurable.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications?pageIndex=0</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameter
Name | Required | Description | Comment
-----|----------|-------------|--------
pageIndex |Yes|page index of the application|0

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications fetched successfully
```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.basic",
    "version": "1.0",
    "responsetime": "2019-05-20T07:14:18.868Z",
    "response": {
        "basicDetails": [
            {
                "preRegistrationId": "38469435683243",
                "fullname": [
                    {
                        "language": "fra",
                        "value": "Shashank"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "statusCode": "Pending_Appointment",
                "bookingRegistrationDTO": null,
                "postalCode": "56059"
            },
            {
                "preRegistrationId": "32042841521591",
                "fullname": [
                    {
                        "language": "fra",
                        "value": "Rakesh P"
                    },
                    {
                        "language": "ara",
                        "value": "سهَسهَنك "
                    }
                ],
                "statusCode": "Pending_Appointment",
                "bookingRegistrationDTO": null,
                "postalCode": "56059"
            }
        ],
        "totalRecords": "2",
        "noOfRecords": "2",
        "pageIndex": "0"
    },
    "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No record found for the requested user id.
```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.basic",
    "version": "1.0",
    "responsetime": "2019-05-20T07:12:37.316Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No record found for the requested user id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_APP_016|no record found for the requested page index|if no demographic data found for the requested page index
PRG_PAM_APP_015|Page size must be greater than zero|if page size is defined 0 or less than 0 in config
PRG_PAM_CORE_010|hashing failed|demographic data hashing failed
PRG_PAM_CORE_012|decryption failed|decryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed

### DELETE /applications/{preRegistrationId}
This request is used to discard the entire pre-registration details based pre-registration id provided in request path parameter.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/{preRegistrationId}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|pre-registration id of the application|29605371807216

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Deletion of individual is successfully

```JSON
{
    "id": "mosip.pre-registration.demographic.delete",
    "version": "1.0",
    "errors": null,
    "responsetime": "2019-05-20T10:28:37.488Z",
    "response": [
        {
            "preRegistrationId": "29605371807216",
            "deletedBy": "9886442073",
            "deletedDateTime": "2019-05-20T10:28:37.485+0000"
        }
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id
```JSON
{
    "id": "mosip.pre-registration.demographic.delete",
    "version": "1.0",
    "responsetime": "2019-05-20T07:25:04.305Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No data found for the requested pre-registration id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_APP_003|delete operation is not allowed|Deletion of Preregistration fails if its status is neither pending appointment nor booked
PRG_PAM_APP_014|Document service rest call failed|When rest call to document service fails
PRG_PAM_DOC_016|failed to delete the booking|If Booking data is failed to delete
PRG_PAM_APP_004|failed to delete the pre-registration data|If Preregistration data is failed to delete

# Document Service (public)
This service enables Pre-Registration portal to request for uploading the document for a particular pre-registration.

* [POST /documents/:preRegistrationId](#post-documentspreregistrationid)
* [PUT /documents/:preRegistrationId](#put-documentspreregistrationid)
* [GET /documents/preregistration/:preRegistrationId](#get-documentspreregistrationpreregistrationid)
* [GET /documents/:documentId?preRegistrationId=:preRegistrationId](#get-documentsdocumentidpreregistrationidpreregistrationid)
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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date
PRG_CORE_REQ_011|encryption failed|encryption of document data failed
PRG_PAM_APP_007|json parsing is failed|document request json parsing failed
PRG_CORE_REQ_010|hashing failed|document data hashing failed
PRG_PAM_DOC_010|Document virus scan failed|virus scan of uploaded document is failed
PRG_PAM_DOC_007|Document exceeding permitted size|when uploaded document size is exceeding the configured size
PRG_PAM_DOC_018|Document Category code is invalid|empty document category code
PRG_PAM_DOC_018|Document type code is invalid|empty document type code
PRG_PAM_DOC_018|Language code is invalid|If language code is empty
PRG_PAM_DOC_020|Demographic record failed to fetch|when rest call to demographic service fails
PRG_PAM_APP_005|No data found for the requested pre-registration id|invalid preregistration id or data is not found for that preregistration id
PRG_PAM_DOC_012|Document table not accessible|access to document table fails
PRG_PAM_DOC_009|Document upload failed|if the document & document details are failed to store

### PUT /documents/:preRegistrationId
This request used to copy the document from source pre-registration id to destination pre-registration id with the specified document category code.

#### Resource URL
<div>https://mosip.io/preregistration/v1/documents/:preRegistrationId?catCode=:doc_cat_code&sourcePreId=:preRegistrationId</div>

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

### GET /documents/preregistration/:preRegistrationId
This request used to retrieve all documents metadata associated with particular pre-registration.

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

### GET /documents/:documentId?preRegistrationId=:preRegistrationId
This request used to retrieve the document for a particular document id from the File System server.

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
###### Description: Document successfully retrieved
```JSON
{
   "id": "mosip.pre-registration.document.fetch.content",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response":{
      "document": ByteArray
    },
   "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If the document is not found for the preregistration id and document id
```JSON
{
   "id": "mosip.pre-registration.document.fetch.content",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
      {
         "errorCode": "PRG_PAM_DOC_005",
         "message": "document is not found for the requested pre-registration id and document id"
      }
   ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_DOC_012|Document table not accessible|access to document table fails
PRG_PAM_DOC_005|Failed to fetch from File System server|if the document is failed to be fetched from file system
PRG_CORE_REQ_012|decryption failed|decryption of document data failed
PRG_CORE_REQ_010|hashing failed|document data hashing failed

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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_DOC_006|Documents failed to delete|if the document & document details are failed to delete
PRG_PAM_DOC_012|Document table not accessible|access to document table fails

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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_DOC_022|DocumentId is not belongs to the pre-registration Id|If the requested document id is not stored with respect to the requested preregistration id
PRG_PAM_DOC_006|Documents failed to delete|if the document & document details are failed to delete
PRG_PAM_DOC_012|Document table not accessible|access to document table fails


# DataSync Service (External)
This service enables Pre-Registration to a registration client, request to retrieve all pre-registration ids based on registration client id, appointment date and an user type.

* [POST /sync](#post-sync)
* [POST /sync/consumedPreRegIds](#post-consumedpreRegIds)
* [GET /sync/:preRegistrationId](#get-syncpreregistrationid)

### POST /sync
This request is used by registration client to retrieve all the pre-registration Ids by date range.

#### Resource URL
<div>https://mosip.io/preregistration/v1/sync</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.datasync
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.registrationCenterId|Yes|Registration Center Id for which the data is required|10001
request.fromDate |Yes|From date of the application|2019-02-09
request.toDate |Yes|To date of the application|2019-02-12

#### Request:
```JSON
{
  "id": "mosip.pre-registration.datasync.fetch.ids",
  "version": "1.0",
  "requesttime": "2019-05-16T06:57:29.969Z",
  "request": {
    "registrationCenterId":"10001",
    "fromDate":"2019-05-09",
    "toDate":"2019-05-20"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All Pre-Registration Ids fetched successfully
```JSON
{
    "id": "mosip.pre-registration.datasync.fetch.ids",
    "version": "1.0",
    "responsetime": "2019-05-16T08:34:01.315",
    "response": {
        "transactionId": "5afbfbae-77b5-11e9-8dea-e342188bfd4e",
        "countOfPreRegIds": "2",
        "preRegistrationIds": {
            "47184958619749": "2019-05-15T11:44:28.966",
            "76426186439718": "2019-05-16T05:54:01.999"
        }
    },
    "errors": null
}

```
##### Failure Response:
###### Status code: '200'
###### Description: If appointment is not booked under the registration center and requested date range.

```JSON
{
    "id": "mosip.pre-registration.datasync.fetch.ids",
    "version": "1.0",
    "responsetime": "2019-05-16T08:32:19.732Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_BOOK_RCI_032",
            "message": "Record not found for date range and reg center id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_DATA_SYNC_009|registration center id is invalid|Empty registration center Id
PRG_CORE_REQ_013|Request date should be current date|Invalid or empty from date or to date
PRG_DATA_SYNC_007|Demographic record failed to fetch|when rest service to demographic service fails
PRG_DATA_SYNC_016|booking data not found|when rest service to booking service fails

### POST /sync/consumedPreRegIds
This request is used by registration processor, to retrieve all processed pre-registration ids and store in pre-registration database and delete records from main table and move to history table.

#### Resource URL
<div>https://mosip.io/preregistration/v1/sync/consumedPreRegIds</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.datasync.store
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationIds |Yes|List of Preregistration Ids|42973267563920

#### Request:
```JSON
{
  "id": "mosip.pre-registration.datasync.store",
  "version": "1.0",
  "requesttime": "2019-02-11T07:05:08.850Z",
  "request": {
    "preRegistrationIds": [
      "94625367217037",
      "43526512857302"
    ]
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Consumed Pre-Registrations saved
```JSON
{
   "id": "mosip.pre-registration.datasync.store",
   "version" : "1.0",
   "responsetime": "2019-02-16T17:31:04.021Z",
   "response": {
       "transactionId": "26fde349-0e56-11e9-99e1-f7683fbbce99",
       "countOfPreRegIds": "2",
       "preRegistrationIds": "2"
    },
    "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No pre-registration ids passed in request body or all the preregistration ids are invalid
```JSON
{
    "id": "mosip.pre-registration.datasync.store",
    "version": "1.0",
    "responsetime": "2019-05-16T08:41:48.546Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_DATA_SYNC_011",
            "message": "requested preregistration ids are not valid"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_CORE_REQ_013|Request date should be current date|Invalid or empty requesttime
PRG_DATA_SYNC_007|Demographic record failed to fetch|when rest service to demographic service fails

### GET /sync/:preRegistrationId
This request is used by registration client to retrieve particular pre-registration data based on a pre-registration id.

Note: ID.json will include both demographic and uploaded document metadata content

#### Resource URL
<div>https://mosip.io/preregistration/v1/sync/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Pre Registration id|41342175487213

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Data Sync records fetched

```JSON
{
    "id": "mosip.pre-registration.datasync.fetch",
    "version": "1.0",
    "responsetime": "2019-05-16T08:34:56.440",
    "response": {
        "pre-registration-id": "47184958619749",
        "registration-client-id": "10001",
        "appointment-date": "2019-05-17",
        "from-time-slot": "09:00",
        "to-time-slot": "09:15",
        "zip-filename": "47184958619749",
        "zip-bytes": ByteCode
    },
    "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data exist for the requested pre-registration id
```JSON
{
    "id": "mosip.pre-registration.datasync.fetch",
    "version": "1.0",
    "responsetime": "2019-05-16T08:35:37.021Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No data found for the requested pre-registration id"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_013|booking data not found|If appointment is not booked against the preregistration id
PRG_DATA_SYNC_007|Demographic record failed to fetch|when rest service to demographic service fails
PRG_DATA_SYNC_016|booking data not found|when rest service to booking service fails
PRG_DATA_SYNC_005|Unable to create zip file|If any error occurs while creating the zip file bytes
PRG_DATA_SYNC_014|file IO exception|File system exception
PRG_DATA_SYNC_006|unable to fetch the document|when rest service to document service fails

# Booking Service (Public)
This service details used by Pre-Registration portal to book an appointment by providing his/her basic appointment details.

* [GET appointment/availability/sync](#get-appointmentavailabilitysync)
* [POST /appointment/:preRegistrationId](#post-appointmentpreregistrationid)
* [POST /appointment](#post-appointment)
* [PUT /appointment/:preRegistrationId](#put-appointmentpreregistrationid)
* [GET /appointment/:preRegistrationId](#get-appointmentpreregistrationid)
* [GET /appointment/availability/:registrationCenterId](#get-appointmentavailabilityregistrationcenterid)
* [GET /appointment/preRegistrationId/:registrationCenterId?from_date=:date&to_date=:date](#get-appointmentpreregistrationidregistrationcenteridfrom_datedateto_datedate)

### GET /appointment/availability/sync
This request is used to synchronize booking slots availability table with master data.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/availability/sync</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Master Data Sync is successful

```JSON
{
    "id": "mosip.pre-registration.appointment.availability",
    "version": "1.0",
    "responsetime": "2019-05-15T08:47:25.523Z",
    "response": "MASTER_DATA_SYNCED_SUCCESSFULLY",
    "errors":null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_015|No available slots found for specified registration center| If no slots are available in the specified registration center
### POST /appointment/:preRegistrationId
This request is used to book an registration center. If the appointment data exists for the requested pre-registration id, it will cancel it and update the new appointment data. If no appointment data then it will book an appointment for specified registration center and time slot.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegsitrationId |Yes|pre-registration id of the application|37802950913289

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.registration_center_id |Yes|Registration center Id |10005
request.appointment_date |Yes|Date of the appointment|2019-01-19
request.time_slot_from |Yes|Time Slot From|12:15:00
request.time_slot_from |Yes|Time Slot To|12:28:00

#### Request:
```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "version": "1.0",
  "requesttime": "2019-05-16T15:31:32.957Z",
  "request": {
        "registration_center_id": "10001",
        "appointment_date": "2019-05-17",
        "time_slot_from": "09:30:00",
        "time_slot_to": "09:45:00"
   }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment booked successfully
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-05-16T09:57:38.433Z",
    "response": {
        "bookingMessage": "Appointment booked successfully"
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid Pre Registration Id.
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-05-16T09:58:41.110Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_PAM_APP_005",
            "message": "No data found for the requested pre-registration id"
        }
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Slot availability not found for selected time.
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-05-15T10:12:07.623Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_BOOK_RCI_002",
            "message": "Availability not found for the selected time"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime 
PRG_CORE_REQ_013|Request date should be current date| when the date is not current date
PRG_BOOK_RCI_002|Availability not found for the selected time|When availability not found for the requested registration center id or appointment date or time slot
PRG_BOOK_RCI_003|User has not selected time slot|If from time slot or to time slot is empty
PRG_BOOK_RCI_005|Booking table not found|access to appointment table fails
PRG_BOOK_RCI_007|Registration center id not entered|If registration center id is empty
PRG_BOOK_RCI_008|Booking date time not selected|If appointment date is empty
PRG_BOOK_RCI_009|INVALID_DATE_TIME_FORMAT|If the appointment date is in invalid format
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service is failed to update the status of the preregistration
PRG_BOOK_RCI_012|Demographic service call failed|when rest call to demographic service is failed to retrieve the demographic data
PRG_BOOK_RCI_013|Booking data not found|while rebooking, when the preregistration status is booked but appointment data not found in the db
PRG_BOOK_RCI_016|Availablity table not accessible|access to availability table fails
PRG_BOOK_RCI_024|Availablity update failed|when appointment availability is failed to update
PRG_BOOK_RCI_026|Booking status cannot be altered|when we tend to modify the appointment details after the configured time span for rebook
PRG_BOOK_RCI_028|Failed to delete the pre registration record|while rebooking, failed to delete old appointment details

### POST /appointment
This request is used to book mulitple registration centers. If the appointment data exists for the requested pre-registration ids, it will cancel it and update the new appointment data. If no appointment data then it will book an appointment for specified registration center and time slot.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationid|Yes|Preregistration Id|51489749326453
request.registration_center_id |Yes|Registration center Id |10001
request.appointment_date |Yes|Date of the appointment|2019-04-22
request.time_slot_from |Yes|Time Slot From|15:30:00
request.time_slot_from |Yes|Time Slot To|15:45:00

#### Request:
```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "version": "1.0",
  "requesttime": "2019-05-15T10:52:04.737Z",
  "request": {
    "bookingRequest": [
      {
        "preRegistrationId": "20167403769842",
        "registration_center_id": "10001",
        "appointment_date": "2019-04-22",
        "time_slot_from": "15:30:00",
        "time_slot_to": "15:45:00"
      },
      {
        "preRegistrationId": "94625367217037",
        "registration_center_id": "10008",
        "appointment_date": "2019-04-23",
        "time_slot_from": "15:30:00",
        "time_slot_to": "15:45:00"
      }
    ]
  }
}

```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment booked successfully
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-05-15T10:58:35.546Z",
    "response": {
        "bookingStatusResponse": [
            {
                "bookingMessage": "Appointment booked successfully"
            },
            {
                "bookingMessage": "Appointment booked successfully"
            }
        ]
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid Pre Registration Id.
```JSON
{
   "id": "mosip.pre-registration.booking.book",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_PAM_APP_006",
            "message": "No data found for the requested pre-registration id"
         }
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Slot availability not found for selected time.
```JSON
{
   "id": "mosip.pre-registration.booking.book",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_BOOK_RCI_002",
            "message": "Availability not found for the selected time"
         }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date
PRG_BOOK_RCI_007|Registration center id not entered|If registration center id is empty
PRG_BOOK_RCI_008|Booking date time not selected|If appointment date is empty
PRG_BOOK_RCI_009|INVALID_DATE_TIME_FORMAT|If the appointment date is in invalid format
PRG_BOOK_RCI_002|Availability not found for the selected time|When availability not found for the requested registration center id or appointment date or time slot
PRG_BOOK_RCI_012|Demographic service call failed|when rest call to demographic service is failed to retrieve the demographic data
PRG_BOOK_RCI_016|Availability table not accessible|access to availability table fails
PRG_BOOK_RCI_005|Booking table not found|access to appointment table fails
PRG_BOOK_RCI_024|Availability update failed|when appointment availability is failed to update
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service is failed to update the status of the preregistration
PRG_BOOK_RCI_013|Booking data not found|while rebooking, when the preregistration status is booked but appointment data not found in the database
PRG_BOOK_RCI_026|Booking status cannot be altered|when we tend to modify the appointment details after the configured time span for rebook
PRG_BOOK_RCI_028|Failed to delete the pre registration record|while rebooking, failed to delete old appointment details
PRG_PAM_APP_017|Requested preregistration id does not belong to the user|If the preregistration id does not belongs to the user

### PUT /appointment/:preRegistrationId
This request used to cancel the appointment. Which will retrieve the appointment details for the specified pre-registration id,if appointment data exists update the availability for the slot by increasing the value and delete the record from the table and update the demographic record status "Pending_Appointment".

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment cancelled successfully

```JSON
{
    "id": "mosip.pre-registration.appointment.cancel",
    "version": "1.0",
    "responsetime": "2019-05-15T11:04:41.312Z",
    "response": {
        "transactionId": "3ce712c7-7701-11e9-967a-530860351daf",
        "message": "Appointment cancelled successfully"
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Appointment cancellation failed.
```JSON
{
    "id": "mosip.pre-registration.appointment.cancel",
    "version": "1.0",
    "responsetime": "2019-05-15T11:05:30.680Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_BOOK_RCI_018",
            "message": "Appointment cannot be canceled"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_013|Booking data not found|if appointment is not booked against the requested preregistration id
PRG_BOOK_RCI_016|Availability table not accessible|access to availability table fails
PRG_BOOK_RCI_005|Booking table not found|access to appointment table fails
PRG_BOOK_RCI_024|Availability update failed|when appointment availability is failed to update
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service fails
PRG_BOOK_RCI_026|Booking status cannot be altered|when we tend to cancel the appointment details after the configured time span for cancel
PRG_BOOK_RCI_018|Appointment cannot be canceled|If status is other than booked
PRG_PAM_APP_005 |No data found for the requested pre-registration id | If no data found for the requested preregistration id
### GET /appointment/:preRegistrationId
This request is to retrieve Pre-Registration appointment details by pre-Registration id.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|37802950913289

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment details successfully retrieved
```JSON
{
   "id": "mosip.pre-registration.appointment.fetch",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
    "registration_center_id": "10005",
    "appointment_date": "2019-02-13",
    "time_slot_from": "16:10",
    "time_slot_to": "16:23"
  },
  "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No Appointment record found for the specified pre-registration id
```JSON
{
   "id": "mosip.pre-registration.appointment.fetch",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_BOOK_RCI_013",
            "message": "Booking data not found"
         }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_013|Booking data not found|if appointment is not booked against the requested preregistration id
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service fails

### GET /appointment/availability/:registrationCenterId
This request is used to retrieve all appointment slots available for booking based on the specified registration center id.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/availability/:registrationCenterId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
registrationCenterId |Yes|Registration Center Id|10004

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Availability details fetched successfully
```JSON
{
   "id": "mosip.pre-registration.appointment.availability",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
        "regCenterId": "10004",
        "centerDetails": [
         {
            "date": "2019-02-13",
            "timeSlots": [
              {
                "fromTime": "09:00:00",
                "toTime": "09:15:00",
                "availability": 4
              },
             {
               "fromTime": "09:15:00",
               "toTime": "09:30:00",
                "availability": 3
             }
             ],
            "holiday": false
         },
        {
            "date": "2019-02-14",
            "timeSlots": [
              {
                "fromTime": "09:00:00",
                "toTime": "09:15:00",
                "availability": 4
              },
             {
               "fromTime": "09:15:00",
               "toTime": "09:30:00",
                "availability": 3
             }
             ],
            "holiday": false
         }
    ]
  },
  "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No available slots found for specified registration center.
```JSON
{
   "id": "mosip.pre-registration.appointment.availability",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_BOOK_RCI_015",
            "message": "No available slots found for specified registration center"
         }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_016|Availability table not accessible|access to availability table fails

### GET /appointment/preRegistrationId/:registrationCenterId?from_date=:Date&to_date=:Date
This request is used to retrieve all pre-registration ids available for specified registration center and date range.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/preRegistrationId/:registrationCenterId?from_date=:Date&to_date=:Date</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
registrationCenterId |Yes|Registration Center Id|10002

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
fromDate |Yes|From Date | 2019-02-12
toDate |Yes|To Date | 2019-06-15

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Availability details fetched successfully
```JSON

{
    "id": "mosip.pre-registration.appointment.ids",
    "version": "1.0",
    "responsetime": "2019-05-15T11:21:39.328Z",
    "response": {
        "registration_center_id": "10002",
        "pre_registration_ids": [
            "76426186439718"
        ]
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No available slots found for specified registration center with date range.
```JSON
{
   "id": "mosip.pre-registration.appointment.ids",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_BOOK_RCI_032",
            "message": "Record not found for date range and reg center id"
         }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_005|Booking table not found|access to appointment table fails

# BatchJob Service (Private)
This service is used by Pre-Registration portal to update an expired pre registration id  and consumed pre registration id.

* [PUT batch/expiredStatus](#put-expiredstatus)
* [PUT batch/consumedStatus](#put-consumedstatus)

### PUT /expiredStatus
This request is used to update status of appointment expired pre-registration ids to expired status in database.

#### Resource URL
<div>https://mosip.io/preregistration/v1/batch/expiredStatus</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Expired status updated successfully
```JSON
{
   "id": "mosip.pre-registration.batchjob.service.expired",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
        "message": "Registration appointment status updated to expired successfully"
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No pre registration record found to update expired status
```JSON
{
   "id": "mosip.pre-registration.batchjob.service.expired",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_PAM_BAT_001",
            "message": "No pre registration id found to update status"
         } 
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_BAT_004|Demographic table not accessible|If data is not found found  for preRegistrationId
PRG_PAM_BAT_005|Reg appointment table not accessible|If Reg appointment table not accessible

### PUT /consumedStatus
This request is used to update the consumed status for all pre-Registration ids given by registration processor.

#### Resource URL
<div>https://mosip.io/preregistration/v1/batch/consumedStatus</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Consumed status updated successfully
```JSON
{
   "id": "mosip.pre-registration.batchjob.service.consumed",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
        "message":  "Demographic status to consumed updated successfully"
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No pre registration record found to update consumed status
```JSON
{
  "id": "mosip.pre-registration.batchjob.service.consumed",
  "version": "1.0",
  "responsetime": "2019-05-14T12:15:53.753Z",
  "response": null,
  "errors": [
    {
      "errorCode": "PRG_PAM_BAT_001",
      "message": "No pre registration id found to update status"
    }
  ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_BAT_004	|Demographic table not accessible|If data is not found for preRegistrationId
PRG_PAM_BAT_005	|Reg appointment table not accessible|If Reg appointment table not accessible
PRG_PAM_BAT_006|Processed prereg list table not accessible|If Processed prereg list table not accessible
PRG_PAM_BAT_007	|Document table not accessible|	If document table not accessible
PRG_PAM_BAT_008	|Reg appointment consumed table not accessible|If Reg appointment consumed table not accessible
PRG_PAM_BAT_009|Demographic consumed table not accessible|If Demographic consumed table not accessible
PRG_PAM_BAT_010	|Document consumed table not accessible|If document consumed table not accessible

# Generate QR code service (public)
This service details used by Pre-Registration portal to generate QR Code.

* [POST qrCode/generate](#post-qrcodegenerate)

### POST qrCode/generate
This request is used to generate QR Code for the pre-registration acknowledgement.

#### Resource URL
<div>https://mosip.io/preregistration/v1/qrCode/generate</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.qrcode.generate
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.name |Yes|user name of the application|Sanober Noor
request.preRegistrationId|Yes|Pre Registration of the application|37802950913289
request.appointmentDate|Yes| Booking appointment date|2019-01-18
request.appointmentTime| Yes|Booking appointment time| 12:02
request.mobNum|  Yes| applicant mobile number |9480456789
request.emailID| Yes|applicant email Id |`sanober@gmail.com`
request.multipart file| Yes| pdf file of acknowledgment page|37802950913289.pdf
request.LangCode| Yes| language code whatever user choose while login|eng

#### Request:
```JSON
{
  "id": "mosip.pre-registration.qrcode.generate",
  "version": "1.0",
  "requesttime": "2019-01-09T15:31:32.957Z",
  "request": {
	"name": "sanober noor",
	"preRegistrationId": "37802950913289",
	"appointmentDate": "2019-01-22",
	"appointmentTime": "22:57",
	"mobNum": "9748107386",
	"emailID": "sanober.noor2@mindtree.com"
   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: QR Code generated  successfully
```JSON
{
   "id": "mosip.pre-registration.notification.qrCode",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
	"qrcode":{ByteCode}
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Failed to generate QR code
```JSON
{
   "id": "mosip.pre-registration.notification.qrCode",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
    	    "errorCode": "PRG_QRC_002",
    	    "message": " Failed to generate QR code"
	 }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id 
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date 
PRG_QRC_001|	File input output exception|	when there is any input / output file operation issues

# Notification Service (public)
This service details used by Pre-Registration portal to trigger notification via SMS or email.

* [POST notification/notify](#post-notificationnotify)

### POST notification/notify
This request is used to notify the pre-registration acknowledgement via Email and SMS.

#### Resource URL
<div>https://mosip.io/preregistration/v1/notification/notify</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Part (NotificationRequestDTO) Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.notification.notify
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.name |Yes|user name of the application|Sanober Noor
request.preRegistrationId|Yes|Pre Registration of the application|37802950913289
request.appointmentDate|Yes| Booking appointment date|2019-01-18
request.appointmentTime| Yes|Booking appointment time| 12:02
request.mobNum|  Yes| applicant mobile number |9480456789
request.emailID| Yes|applicant email Id |`sanober@gmail.com`

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
attachment| Yes| pdf file of acknowledgment page|37802950913289.pdf
langCode| Yes| language code whatever user choose while login|eng

#### Request:
```JSON
{
  "id": "mosip.pre-registration.notification.notify",
  "version": "1.0",
  "requesttime": "2019-01-09T15:31:32.957Z",
  "request": {
	"name": "sanober noor",
	"preRegistrationId": "37802950913289",
	"appointmentDate": "2019-01-22",
	"appointmentTime": "22:57",
	"mobNum": "9748107386",
	"emailID": "sanober.noor2@mindtree.com",
         "additionalRecipient":"true"

   }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Email and sms request successfully submitted
```JSON
{
   "id": "mosip.pre-registration.notification.notify",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
      "message": "Email and sms request successfully submitted"
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Mobile number or Email Id is missing
```JSON
{
   "id": "mosip.pre-registration.notification.notify",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_ACK_001",
            "message": "Mobile number or Email Id is missing"
         }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id 
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date 
PRG_ACK_002|Incorrect mandatory Fields|	If any of the request is null

# Transliteration Service (Public)
This service is used by Pre-Registration portal to transliterate given value from one language to another language. In this API transliteration is using IDB ICU4J library , so accuracy will be less.

* [POST /transliteration/transliterate](#post-transliterationtransliterate)

###  POST /transliteration/transliterate
This request is used to transliterate from_Field_value to to_field_value based on given valid from_lang_code to to_lang_code.

#### Resource URL
<div>https://mosip.io/preregistration/v1/transliteration/transliterate</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.transliteration.transliterate
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.from_field_lang|Yes|From language code|eng
request.from_field_value |Yes|From field value |Kishan
request.to_field_lang |Yes|To language code|ara

#### Request:
```JSON
{
  "id": "mosip.pre-registration.transliteration.transliterate",
  "version": "1.0",
  "requesttime": "2019-01-09T15:31:32.957Z",
  "request": {
    "from_field_lang": "eng",
    "from_field_value": "Kishan",
    "to_field_lang": "ara"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Given key is transliterated successfully
```JSON
{
   "id": "mosip.pre-registration.transliteration.transliterate",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
    "from_field_lang": "eng",
    "from_field_value": "Kishan",
    "to_field_lang": "ara",
    "to_field_value": "كِسهَن"
  },
  "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Failed to transliterate
```JSON
{
   "id": "mosip.pre-registration.transliteration.transliterate",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[
         {
            "errorCode": "PRG_TRL_APP_001",
            "message": "Failed to transliterate"
         }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id 
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date 
PRG_TRL_APP_008|Unsupported language|If langCode is other than ara,eng and fra
PRG_TRL_APP_002|Incorrect mandatory Fields|If any of the request is null
