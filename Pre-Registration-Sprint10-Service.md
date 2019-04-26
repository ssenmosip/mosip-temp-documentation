This section details about the service API in the Pre-Registration Document service.
* [Login Service](#login-service-public)
* [Demographic Service](#demographic-service-public)
* [Document Service](#document-service-public)
* [Booking Service](#booking-service-public)
* [DataSync Service](#datasync-service-external)

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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id 
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date 
PRG_PAM_LGN_008|	Invalid Request userId received|	If otp field is null or invalid
PRG_AUTH_011|	Error while Parsing the kernel response	|failed to parse kernel response 

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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id 
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date 
PRG_AUTH_002|	Authentication failed	|If userId field is null or invalid
KER-OTV-003|	OTP can't be empty or null.	|If otp field is null
KER-OTV-004|	OTP consists of only numeric characters. No other characters is allowed.|	If otp contains character other than numeric
PRG_AUTH_011	|Error while Parsing the kernel response|	failed to parse kernel response 
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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_AUTH_012	|Config file not found in the config server|	If config file not found in the config server

# Demographic Service (public)
This service details used by Pre-Registration portal to maintain the demographic data by providing his/her basic details.

* [POST /applications](#post-applications)
* [PUT /applications/:preRegistrationId](#put-applicationspreRegistrationid)
* [GET /applications/:preRegistrationId](#get-applicationspreRegistrationid)
* [GET /applications/status/:preRegistrationId](#get-applicationsstatuspreRegistrationid)
* [GET /applications](#get-applications)
* [DELETE /applications/:preRegistrationId](#delete-applicationspreRegistrationid)

### POST /applications
This request will used to create new pre-registration with demographic details, which generate pre-registration id and associate with demographic details.

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
request.demographicDetails.identity.gender |Yes|gender of the applicant|
request.demographicDetails.identity.city |Yes|city of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.mobileNumber |Yes|mobile number of the applicant|
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
request.demographicDetails.identity.CNEOrPINNumber |Yes|CNE Number of the applicant|

#### Request:
```JSON
{
   "id":"mosip.pre-registration.demographic.create",
   "version":"1.0",
   "requesttime":"2019-04-24T07:22:57.086Z",
   "request":{
      "langCode":"fra",
      "demographicDetails":{
         "identity":{
            "IDSchemaVersion":1,
            "fullName":[
               {
                  "language":"fra",
                  "value":"Shashank Agrawal"
               },
               {
                  "language":"ara",
                  "value":"سهَسهَنك َگرَوَل"
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
            "email":"test@gmail.com",
            "CNIENumber":"1234567845678"
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
   "id":"mosip.pre-registration.demographic.create",
   "version":"1.0",
   "responsetime":"2019-04-24T08:08:13.246Z",
   "response":{  
      "preRegistrationId":"64269837502851",
      "createdDateTime":"2019-01-08T17:05:48.953Z",
      "statusCode":"Pending_Appointment",
      "langCode":"fra",
      "demographicDetails":{  
         "identity":{  
            "IDSchemaVersion":1,
            "fullName":[  
               {  
                  "language":"fra",
                  "value":"Shashank Agrawal"
               },
               {  
                  "language":"ara",
                  "value":"سهَسهَنك َگرَوَل"
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
            "postalCode":"560059",
            "phone":"8680958812",
            "email":"test@gmail.com",
            "CNIENumber":"1234567845678"
         }
      }
   },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Failed to create the pre-registration with demographic data provided. 
```JSON
{
  "id": "mosip.pre-registration.demographic.create",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": {
	   "errorCode": "PRG_PAM_APP_001",
	   "message": "Failed to create the pre-registration with demographic data provided"
	}
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date
PRG_PAM_APP_014|email failed for the regex ^[\\w-\\+]+(\\.[\\w]+)*@[\\w-]+(\\.[\\w]+)*(\\.[a-z]{2,})$|invalid email id format
PRG_PAM_APP_014|phone failed for the regex ^([6-9]{1})([0-9]{9})$|invalid phone number format
PRG_PAM_APP_014|dateOfBirth failed for the regex ^\\d{4}/([0]\\d1[0-2])/([0-2]\\d3[01])$|invalid data of birth format
PRG_PAM_APP_014|CNIENumber failed for the regex ^([0-9]{10,30})$|invalid CNIENumber format
PRG_PAM_APP_014|postalCode failed for the regex ^[(?i)A-Z0-9]{5}$|Invalid postal code format
PRG_CORE_REQ_011|encryption failed|encryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed
PRG_CORE_REQ_010|hashing failed|demographic data hashing failed
PRG_CORE_REQ_012|decryption failes|decryption of demographic data failed

### PUT /applications/:preRegistrationId
This request used to update pre-registration's demographic details by providing pre-registration id in the path parameter and updated demographic details in request body.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/:preRegistrationId</div>

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
id |Yes|Id of the application|mosip.pre-registration.demographic.update
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.langCode |Yes|primary language code|  value will be derived from UI
request.demographicDetails |Yes|demographicDetails of the applicant|
request.demographicDetails.identity |Yes|identity of the applicant|
request.demographicDetails.identity.gender |Yes|gender of the applicant|
request.demographicDetails.identity.city |Yes|city of the applicant| value will be derived from the domain metadata
request.demographicDetails.identity.mobileNumber |Yes|mobile number of the applicant|
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
request.demographicDetails.identity.CNEOrPINNumber |Yes|CNE Number of the applicant|

#### Request:
```JSON
{
  "id": "mosip.pre-registration.demographic.update",
  "version": "1.0",
  "requesttime": "2019-04-24T07:22:57.086Z",
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
            "email":"test@gmail.com",
            "CNIENumber":"1234567845678"
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
   "responsetime": "2019-03-15T08:08:13.246Z",
   "response": {
      "preRegistrationId": "64269837502851",
      "updatedDateTime": "2019-02-11T13:37:37.215Z",
      "statusCode": "Pending_Appointment",
      "langCode": "fra",
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
            "postalCode":"560059",
            "phone":"8680958812",
            "email":"test@gmail.com",
            "CNIENumber":"1234567845678"
         }
      }
   },
  "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Failed to update the pre-registration demographic details. 
```JSON
{
  "id": "mosip.pre-registration.demographic.update",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
        {
	   "errorCode": "PRG_PAM_APP_008",
	   "message": "Failed to update the pre-registration demographic details"
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
PRG_PAM_APP_005|No data found for the requested pre-registration id|invalid preregistration id or data is not found for that preregistration id
PRG_PAM_APP_014|email failed for the regex ^[\\w-\\+]+(\\.[\\w]+)*@[\\w-]+(\\.[\\w]+)*(\\.[a-z]{2,})$|invalid email id
PRG_PAM_APP_014|phone failed for the regex ^([6-9]{1})([0-9]{9})$|invalid phone number
PRG_PAM_APP_014|dateOfBirth failed for the regex ^\\d{4}/([0]\\d1[0-2])/([0-2]\\d3[01])$|invalid data of birth format
PRG_PAM_APP_014|CNIENumber failed for the regex ^([0-9]{10,30})$|invalid CNIENumber
PRG_PAM_APP_014|postalCode failed for the regex ^[(?i)A-Z0-9]{5}$|Invalid postal code
PRG_CORE_REQ_011|encryption failed|encryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed
PRG_CORE_REQ_010|hashing failed|demographic data hashing failed
PRG_CORE_REQ_012|decryption failes|decryption of demographic data failed


### GET /applications/:preRegistrationId
This request is used to retrieve Pre-Registration demographic data by pre-Registration id provided in request path parameter.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|64269837502851

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Demographic data successfully retrieved
```JSON
{
  "id": "mosip.pre-registration.demographic.retrieve.details",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response":{
           "preRegistrationId": "20180396713560",
            "createdBy": "9886442073",
            "createdDateTime": "2019-04-24T09:42:03.883Z",
            "updatedBy": "9886442073",
            "updatedDateTime": "2019-04-24T09:47:10.591Z",
            "statusCode": "Pending_Appointment",
            "langCode": "fra",
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
            "email":"test@gmail.com",
            "CNIENumber":"1234567845678"
         }
      },
 "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id.
```JSON
{
    "id": null,
    "version": null,
    "errors": {
        "errorCode": "PRG_PAM_APP_005",
        "message": "No data found for the requested pre-registration id"
    },
    "responsetime": "2019-04-24T09:51:46.563Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_CORE_REQ_010|hashing failed|demographic data hashing failed
PRG_CORE_REQ_012|decryption failes|decryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed

### GET /applications/status/:preRegistrationId
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
preRegistrationId |Yes|Id of the application|29605371807216

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications status fetched successfully

```JSON
{
    "id": "mosip.pre-registration.demographic.retrieve.status",
    "version": "1.0",
    "errors": null,
    "responsetime": "2019-04-24T10:20:55.821Z",
    "response": [
        {
            "preRegistartionId": "29605371807216",
            "statusCode": "Pending_Appointment"
        }
    ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id.
```JSON
{
    "id": null,
    "version": null,
    "errors": {
        "errorCode": "PRG_PAM_APP_005",
        "message": "No data found for the requested pre-registration id"
    },
    "responsetime": "2019-04-24T10:21:30.952Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_CORE_REQ_010|hashing failed|demographic data hashing failed

### GET /applications
This request is used to retrieve all Pre-Registration id, Full name in both language, Status Code and Appointment details and Postal Code by user id from authorization token.

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
  "errors": null,
  "responsetime": "2019-04-24T10:24:10.253Z",
  "response": [
    {
      "preRegistrationId": "36019326031045",
      "fullname": [
        {
          "language": "fra",
          "value": "Rakesh Palani"
        },
        {
          "language": "ara",
          "value": "سهَسهَنك َگرَوَل"
        }
      ],
      "statusCode": "Pending_Appointment",
      "bookingRegistrationDTO": null,
      "postalCode": "56086"
    },
    {
      "preRegistrationId": "32963146892458",
      "fullname": [
        {
          "language": "fra",
          "value": "Ravi"
        },
        {
          "language": "ara",
          "value": "سهَسهَنك َگرَوَل"
        }
      ],
      "statusCode": "Booked",
      "appointmentDetails": {
        "registration_center_id": "RCG-RC-01",
        "appointment_date": "2018-01-17",
        "time_slot_from": "09:00:00",
        "time_slot_to": "09:30:00"
      },
      "postalCode": "56086"
    },
    {
      "preRegistrationId": "29605371807216",
      "fullname": [
        {
          "language": "fra",
          "value": "Ashish Ras"
        },
        {
          "language": "ara",
          "value": "سهَسهَنك َگرَوَل"
        }
      ],
      "statusCode": "Pending_Appointment",
      "bookingRegistrationDTO": null,
      "postalCode": "56086"
    }
  ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No record found for the requested user id.
```JSON
{
  "id": "mosip.pre-registration.demographic.retrieve.basic",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": {
	    "errorCode": "PRG_PAM_APP_005",
	    "message": "No record found for the requested user id"
	}
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_CORE_REQ_010|hashing failed|demographic data hashing failed
PRG_CORE_REQ_012|decryption failes|decryption of demographic data failed
PRG_PAM_APP_007|json parsing is failed|demographic json parsing failed


### DELETE /applications/:preRegistrationId
This request is used to discard the entire pre-registration details based pre-registration id provided in request path parameter.

#### Resource URL
<div>https://mosip.io/preregistration/v1/applications/:preRegistrationId</div>

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
    "responsetime": "2019-04-24T10:28:37.488Z",
    "response": [
        {
            "preRegistrationId": "29605371807216",
            "deletedBy": "9886442073",
            "deletedDateTime": "2019-04-24T10:28:37.485+0000"
        }
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id
```JSON
{
    "id": null,
    "version": null,
    "errors": {
        "errorCode": "PRG_PAM_APP_005",
        "message": "No data found for the requested pre-registration id"
    },
    "responsetime": "2019-04-24T10:29:23.507Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_APP_003|delete operation is not allowed|Deletion of Preregistration fails if its status is neither pending appointment nor booked
PRG_PAM_APP_014|Document service rest call failed|When rest call to document service fails
PRG_PAM_DOC_016|failed to delete the booking|If Booking data is failed to delete
PRG_PAM_APP_004|failed to delete the pre-registration data|If Preregistration data is failed to delete

##### Failure Response:
###### Status code: '200'
###### Description: failed to delete the pre-registration record.
```JSON
{
  "id": "mosip.pre-registration.demographic.delete",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": {
	  "errorCode": "PRG_PAM_APP_004",
	  "message": "Failed to delete data for the requested pre-registration id"
	}
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
    "version": "1.0",
    "errors": null,
    "responsetime": "2019-04-25T12:43:04.432Z",
    "response": [
        {
            "preRegistrationId": "48064860942061",
            "documentId": "e7bc9ebb-6755-11e9-875d-dd2016b322c2",
            "docName": "Passport.pdf",
            "docCatCode": "POA",
            "docTypCode": "adress",
            "docFileFormat": "pdf"
        }
    ]
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
PRG_PAM_DOC_007|Document exceeding permited size|when uploaded document size is exceeding the configured size
PRG_PAM_DOC_018|Document Catagory code is invalid|empty document category code
PRG_PAM_DOC_018|Document type code is invalid|empty document type code
PRG_PAM_DOC_018|Language code is invalid|If language code is empty
PRG_PAM_DOC_020|Demographic record failed to fetch|when rest call to demographic service failes
PRG_PAM_APP_005|No data found for the requested pre-registration id|invalid preregistration id or data is not found for that preregistration id
PRG_PAM_DOC_012|Document table not accessible|access to document table failes
PRG_PAM_DOC_009|Document upload failed|if the document & document details are failed to store

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
    "version": "1.0",
    "errors": null,
    "responsetime": "2019-04-25T12:30:47.893Z",
    "response": [
        {
            "preRegistrationId": "36019326031045",
            "documentId": "7a16d909-6746-11e9-875d-4f4ef38bd2a2",
            "docName": "Passport.pdf",
            "docCatCode": "POA",
            "docTypCode": "adress",
            "docFileFormat": "pdf"
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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_CORE_REQ_001|request parameter is missing|If source preregistration id or destination preregistration id is empty
PRG_PAM_DOC_018|Catagory code is invalid|if document category code is not POA
PRG_PAM_APP_005|No data found for the requested pre-registration id|If source preregistration id or destination preregistration id is invalid or no preregistration data found for any of the preregistration id
PRG_PAM_DOC_005|Documents is not found for the requested pre-registration id|when document is not found for the requested source preregistration id
PRG_PAM_DOC_012|Document table not accessible|access to document table failes
PRG_PAM_DOC_009|Document upload failed|if the document & document details are failed to store
PRG_PAM_DOC_011|Document copy failed from source to destination|when document is not copied from source to destination preregistration id
PRG_CORE_REQ_010|hashing failed|document data hashing failed






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
    "version": "1.0",
    "errors": null,
    "responsetime": "2019-04-24T11:30:00.880Z",
    "response": [
        {
            "docName": "Passport.pdf",
            "documentId": "a147e0a2-6680-11e9-875d-7742f86a7d68",
            "docCatCode": "POA",
            "docTypCode": "passport",
            "multipartFile": "ByteCode"
		}
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Document is not found for the requested pre-registration id
```JSON
{
    "id": null,
    "version": "1.0",
    "errors": {
        "errorCode": "PRG_PAM_DOC_005",
        "message": "DOCUMENT_IS_MISSING"
    },
    "responsetime": "2019-04-25T11:00:45.744Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_DOC_012|Document table not accessible|access to document table failes
PRG_PAM_DOC_005|Failed to fetch from File System server|if the document is failed to be fetched from file system
PRG_CORE_REQ_012|decryption failes|decryption of document data failed
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
    "id": null,
    "version": "1.0",
    "errors": {
        "errorCode": "PRG_PAM_DOC_005",
        "message": "DOCUMENT_IS_MISSING"
    },
    "responsetime": "2019-04-24T11:44:34.422Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_DOC_006|Documents failed to delete|if the document & document details are failed to delete
PRG_PAM_DOC_012|Document table not accessible|access to document table failes


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
    "id": null,
    "version": "1.0",
    "errors": {
        "errorCode": "PRG_PAM_DOC_005",
        "message": "DOCUMENT_IS_MISSING"
    },
    "responsetime": "2019-04-24T11:42:11.449Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_DOC_022|DocumentId is not belongs to the pre-registration Id|If the requested document id is not stored with respect to the requested preregistration id
PRG_PAM_DOC_006|Documents failed to delete|if the document & document details are failed to delete
PRG_PAM_DOC_012|Document table not accessible|access to document table failes


# Booking Service (Public)
This service details used by Pre-Registration portal to book an appointment by providing his/her basic appointment details.

* [POST /appointment/:preRegistrationId](#post-appointmentpreregistrationid)
* [POST /appointment](#post-appointment)
* [PUT /appointment/:preRegistrationId](#put-appointmentpreregistrationid)
* [GET /appointment/:preRegistrationId](#get-appointmentpreregistrationid)
* [GET /appointment/availability/:registrationCenterId](#get-appointmentavailabilityregistrationcenterid)
* [GET /appointment/preRegistrationId/:registrationCenterId?from_date=:date&to_date=:date](#get-appointmentpreregistrationidregistrationcenteridfrom_datedateto_datedate)

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
  "requesttime": "2019-01-09T15:31:32.957Z",
  "request": [{
        "registration_center_id": "10005",
        "appointment_date": "2019-02-13",
        "time_slot_from": "15:31:00",
        "time_slot_to": "15:44:00"
   }]
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
    "responsetime": "2019-04-23T15:18:29.974Z",
    "response": {
        "preRegistrationId": "65340187513461",
        "bookingStatus": "Booked",
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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date
PRG_BOOK_RCI_003|User has not selected time slot|If from time slot or to time slot is empty
PRG_BOOK_RCI_007|Registration center id not entered|If registration center id is empty
PRG_BOOK_RCI_008|Booking date time not selected|If appointment date is empty
PRG_BOOK_RCI_009|INVALID_DATE_TIME_FORMAT|If the appointment date is in invalid format
PRG_BOOK_RCI_002|Availability not found for the selected time|When availability not found for the requested registration center id or appointment date or time slot
PRG_BOOK_RCI_012|Demographic service call failed|when rest call to demographic service is failed to retrieve the demographic data
PRG_BOOK_RCI_016|Availablity table not accessible|access to availibility table fails
PRG_BOOK_RCI_005|Booking table not found|acess to appointment table fails
PRG_BOOK_RCI_024|Availablity update failed|when appointment availability is failed to update
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service is failed to update the status of the preregistration
PRG_BOOK_RCI_013|Booking data not found|while rebooking, when the preregistration status is booked but appointment data not found in the db
PRG_BOOK_RCI_026|Booking status cannot be altered|when we tend to modify the appointment details after the configured time span for rebook
PRG_BOOK_RCI_028|Failed to delete the pre registration record|while rebooking, falled to delete old appointment details

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
  "requesttime": "2019-04-22T15:31:32.957Z",
  "request": [{
  		"preRegistrationId":"36019326031045",
        "registration_center_id": "10001",
        "appointment_date": "2019-04-22",
        "time_slot_from": "15:30:00",
        "time_slot_to": "15:45:00"
   },
   {
  		"preRegistrationId":"94625367217037",
        "registration_center_id": "10008",
        "appointment_date": "2019-04-23",
        "time_slot_from": "15:30:00",
        "time_slot_to": "15:45:00"
   }]
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
    "responsetime": "2019-04-23T15:16:42.010Z",
    "response": [
        {
            "preRegistrationId": "29487243023716",
            "bookingStatus": "Booked",
            "bookingMessage": "Appointment booked successfully"
        },
        {
            "preRegistrationId": "65340187513461",
            "bookingStatus": "Booked",
            "bookingMessage": "Appointment booked successfully"
        }
    ],
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
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_PAM_CORE_001|Request id is invalid|Invalid or empty Request Id
PRG_PAM_CORE_002|Request version is invalid|Invalid or empty Request Version
PRG_PAM_CORE_003|Request timestamp is invalid|Invalid or empty Request DateTime and when the date is not current or future date
PRG_BOOK_RCI_003|User has not selected time slot|If from time slot or to time slot is empty
PRG_BOOK_RCI_007|Registration center id not entered|If registration center id is empty
PRG_BOOK_RCI_008|Booking date time not selected|If appointment date is empty
PRG_BOOK_RCI_009|INVALID_DATE_TIME_FORMAT|If the appointment date is in invalid format
PRG_BOOK_RCI_002|Availability not found for the selected time|When availability not found for the requested registration center id or appointment date or time slot
PRG_BOOK_RCI_012|Demographic service call failed|when rest call to demographic service is failed to retrieve the demographic data
PRG_BOOK_RCI_016|Availablity table not accessible|access to availibility table fails
PRG_BOOK_RCI_005|Booking table not found|acess to appointment table fails
PRG_BOOK_RCI_024|Availablity update failed|when appointment availability is failed to update
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service is failed to update the status of the preregistration
PRG_BOOK_RCI_013|Booking data not found|while rebooking, when the preregistration status is booked but appointment data not found in the db
PRG_BOOK_RCI_026|Booking status cannot be altered|when we tend to modify the appointment details after the configured time span for rebook
PRG_BOOK_RCI_028|Failed to delete the pre registration record|while rebooking, falled to delete old appointment details

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
    "id": null,
    "version": null,
    "responsetime": "2019-04-24T11:24:51.920Z",
    "response": {
        "transactionId": "93df61b6-6683-11e9-a334-0fb6535e5ce8",
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
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:25:33.606Z",
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
PRG_BOOK_RCI_016|Availablity table not accessible|access to availibility table fails
PRG_BOOK_RCI_005|Booking table not found|acess to appointment table fails
PRG_BOOK_RCI_024|Availablity update failed|when appointment availability is failed to update
PRG_BOOK_RCI_011|Demographic service call failed|when rest call to demographic service fails
PRG_BOOK_RCI_026|Booking status cannot be altered|when we tend to cancel the appointment details after the configured time span for cancel

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
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:13:58.911Z",
    "response": {
        "registration_center_id": "10001",
        "appointment_date": "2019-04-22",
        "time_slot_from": "15:30",
        "time_slot_to": "15:45"
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No Appointment record found for the specified pre-registration id
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:15:22.904Z",
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
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:17:25.799Z",
    "response": {
        "regCenterId": "10001",
        "centerDetails": [
            {
                "date": "2019-04-26",
                "timeSlots": [
                    {
                        "fromTime": "09:00:00",
                        "toTime": "09:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:15:00",
                        "toTime": "09:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:30:00",
                        "toTime": "09:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:45:00",
                        "toTime": "10:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:00:00",
                        "toTime": "10:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:15:00",
                        "toTime": "10:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:30:00",
                        "toTime": "10:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:45:00",
                        "toTime": "11:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:00:00",
                        "toTime": "11:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:15:00",
                        "toTime": "11:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:30:00",
                        "toTime": "11:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:45:00",
                        "toTime": "12:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:00:00",
                        "toTime": "12:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:15:00",
                        "toTime": "12:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:30:00",
                        "toTime": "12:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:45:00",
                        "toTime": "13:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:00:00",
                        "toTime": "14:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:15:00",
                        "toTime": "14:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:30:00",
                        "toTime": "14:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:45:00",
                        "toTime": "15:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:00:00",
                        "toTime": "15:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:15:00",
                        "toTime": "15:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:30:00",
                        "toTime": "15:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:45:00",
                        "toTime": "16:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:00:00",
                        "toTime": "16:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:15:00",
                        "toTime": "16:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:30:00",
                        "toTime": "16:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:45:00",
                        "toTime": "17:00:00",
                        "availability": 3
                    }
                ],
                "holiday": false
            },
            {
                "date": "2019-04-27",
                "timeSlots": [
                    {
                        "fromTime": "09:00:00",
                        "toTime": "09:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:15:00",
                        "toTime": "09:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:30:00",
                        "toTime": "09:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:45:00",
                        "toTime": "10:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:00:00",
                        "toTime": "10:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:15:00",
                        "toTime": "10:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:30:00",
                        "toTime": "10:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:45:00",
                        "toTime": "11:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:00:00",
                        "toTime": "11:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:15:00",
                        "toTime": "11:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:30:00",
                        "toTime": "11:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:45:00",
                        "toTime": "12:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:00:00",
                        "toTime": "12:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:15:00",
                        "toTime": "12:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:30:00",
                        "toTime": "12:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:45:00",
                        "toTime": "13:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:00:00",
                        "toTime": "14:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:15:00",
                        "toTime": "14:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:30:00",
                        "toTime": "14:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:45:00",
                        "toTime": "15:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:00:00",
                        "toTime": "15:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:15:00",
                        "toTime": "15:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:30:00",
                        "toTime": "15:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:45:00",
                        "toTime": "16:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:00:00",
                        "toTime": "16:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:15:00",
                        "toTime": "16:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:30:00",
                        "toTime": "16:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:45:00",
                        "toTime": "17:00:00",
                        "availability": 3
                    }
                ],
                "holiday": false
            },
            {
                "date": "2019-04-28",
                "timeSlots": [
                    {
                        "fromTime": "09:00:00",
                        "toTime": "09:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:15:00",
                        "toTime": "09:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:30:00",
                        "toTime": "09:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:45:00",
                        "toTime": "10:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:00:00",
                        "toTime": "10:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:15:00",
                        "toTime": "10:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:30:00",
                        "toTime": "10:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:45:00",
                        "toTime": "11:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:00:00",
                        "toTime": "11:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:15:00",
                        "toTime": "11:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:30:00",
                        "toTime": "11:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:45:00",
                        "toTime": "12:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:00:00",
                        "toTime": "12:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:15:00",
                        "toTime": "12:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:30:00",
                        "toTime": "12:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:45:00",
                        "toTime": "13:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:00:00",
                        "toTime": "14:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:15:00",
                        "toTime": "14:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:30:00",
                        "toTime": "14:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:45:00",
                        "toTime": "15:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:00:00",
                        "toTime": "15:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:15:00",
                        "toTime": "15:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:30:00",
                        "toTime": "15:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:45:00",
                        "toTime": "16:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:00:00",
                        "toTime": "16:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:15:00",
                        "toTime": "16:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:30:00",
                        "toTime": "16:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:45:00",
                        "toTime": "17:00:00",
                        "availability": 3
                    }
                ],
                "holiday": false
            },
            {
                "date": "2019-04-29",
                "timeSlots": [
                    {
                        "fromTime": "09:00:00",
                        "toTime": "09:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:15:00",
                        "toTime": "09:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:30:00",
                        "toTime": "09:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:45:00",
                        "toTime": "10:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:00:00",
                        "toTime": "10:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:15:00",
                        "toTime": "10:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:30:00",
                        "toTime": "10:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:45:00",
                        "toTime": "11:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:00:00",
                        "toTime": "11:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:15:00",
                        "toTime": "11:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:30:00",
                        "toTime": "11:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:45:00",
                        "toTime": "12:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:00:00",
                        "toTime": "12:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:15:00",
                        "toTime": "12:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:30:00",
                        "toTime": "12:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:45:00",
                        "toTime": "13:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:00:00",
                        "toTime": "14:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:15:00",
                        "toTime": "14:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:30:00",
                        "toTime": "14:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:45:00",
                        "toTime": "15:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:00:00",
                        "toTime": "15:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:15:00",
                        "toTime": "15:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:30:00",
                        "toTime": "15:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:45:00",
                        "toTime": "16:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:00:00",
                        "toTime": "16:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:15:00",
                        "toTime": "16:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:30:00",
                        "toTime": "16:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:45:00",
                        "toTime": "17:00:00",
                        "availability": 3
                    }
                ],
                "holiday": false
            },
            {
                "date": "2019-04-30",
                "timeSlots": [
                    {
                        "fromTime": "09:00:00",
                        "toTime": "09:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:15:00",
                        "toTime": "09:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:30:00",
                        "toTime": "09:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "09:45:00",
                        "toTime": "10:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:00:00",
                        "toTime": "10:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:15:00",
                        "toTime": "10:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:30:00",
                        "toTime": "10:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "10:45:00",
                        "toTime": "11:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:00:00",
                        "toTime": "11:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:15:00",
                        "toTime": "11:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:30:00",
                        "toTime": "11:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "11:45:00",
                        "toTime": "12:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:00:00",
                        "toTime": "12:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:15:00",
                        "toTime": "12:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:30:00",
                        "toTime": "12:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "12:45:00",
                        "toTime": "13:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:00:00",
                        "toTime": "14:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:15:00",
                        "toTime": "14:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:30:00",
                        "toTime": "14:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "14:45:00",
                        "toTime": "15:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:00:00",
                        "toTime": "15:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:15:00",
                        "toTime": "15:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:30:00",
                        "toTime": "15:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "15:45:00",
                        "toTime": "16:00:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:00:00",
                        "toTime": "16:15:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:15:00",
                        "toTime": "16:30:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:30:00",
                        "toTime": "16:45:00",
                        "availability": 3
                    },
                    {
                        "fromTime": "16:45:00",
                        "toTime": "17:00:00",
                        "availability": 3
                    }
                ],
                "holiday": false
            }
        ]
    },
    "errors": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No available slots found for specified registration center.
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:18:00.802Z",
    "response": null,
    "errors": [
        {
            "errorCode": "PRG_BOOK_RCI_015",
            "message": "PRG_BOOK_RCI_015 --> No time slots assigned to that reg center"
        }
    ]
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_016|Availablity table not accessible|access to availibility table fails

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
registrationCenterId |Yes|Registration Center Id|10004

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
fromDate |Yes|From Date | 2019-02-12
toDate |Yes|To Date | 2019-02-14

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Availability details fetched successfully
```JSON
{
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:20:15.696Z",
    "response": {
        "registration_center_id": "10001",
        "pre_registration_ids": [
            "51648718735821",
            "43069587924925",
            "26957245731486",
            "56418391827315",
            "36825069830953",
            "26046130437504",
            "80784057109835",
            "41941685249147",
            "58720860169859",
            "64096148729540",
            "58051460264028",
            "37430651935864",
            "47369847260278",
            "25046285490872",
            "35975403619830",
            "32963146892458"
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
    "id": "mosip.pre-registration.booking.book",
    "version": "1.0",
    "responsetime": "2019-04-24T11:20:50.434Z",
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
PRG_BOOK_RCI_005|Booking table not found|access to appointment table fails

# DataSync Service (External)
This service enables Pre-Registration to a registration client, request to retrieve all pre-registration ids based on registration client id, appointment date and an user type.

* [POST /sync](#post-sync)
* [POST /sync/consumedPreRegIds](#post-syncconsumedpreregids)
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
  "requesttime": "2019-02-11T06:57:29.969Z",
  "request": {
    "registrationCenterId":"10001",
    "fromDate":"2019-02-09",
    "toDate":"2019-02-12"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All Pre-Registration Ids fetched successfully
```JSON
{
    "id": null,
    "version": null,
    "responsetime": "2019-04-24T13:13:15.429Z",
    "response": {
        "transactionId": "b844b66d-6692-11e9-9e21-a96692193955",
        "countOfPreRegIds": "16",
        "preRegistrationIds": {
            "21728945805937": "2019-04-22T13:09:38.182",
            "57128359318508": "2019-04-22T13:45:51.029",
            "27807168975134": "2019-04-22T07:13:19.696",
            "48156207857649": "2019-04-23T13:25:32.195",
            "47619536407427": "2019-04-23T07:33:29.495",
            "31805269138406": "2019-04-21T13:49:45.607",
            "37025075316953": "2019-04-23T12:47:14.395",
            "36058368043843": "2019-04-23T05:19:50.163",
            "25104860854153": "2019-04-23T13:29:42.664",
            "25742948395781": "2019-04-23T08:52:19.487",
            "63196106573148": "2019-04-22T08:42:32.458",
            "45746897093203": "2019-04-22T05:29:19.288",
            "83154079450486": "2019-04-22T09:52:37.834",
            "60597241326438": "2019-04-21T16:54:21.695",
            "40572697835643": "2019-04-22T10:22:31.634",
            "29708209769312": "2019-04-22T09:44:02.757"
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
    "id": null,
    "version": null,
    "errors": {
        "errorCode": "PRG_BOOK_RCI_032",
        "message": "Record not found for date range and reg center id"
    },
    "responsetime": "2019-04-24T13:33:50.237Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_DATA_SYNC_009|INVALID_REGISTRATION_CENTER_ID|Empty registration center Id
PRG_DATA_SYNC_010|INVALID_REQUESTED_DATE|Invalid or empty from date or to date
PRG_DATA_SYNC_007|DEMOGRAPHIC_GET_RECORD_FAILEDwhen rest service to demographic service fails
PRG_DATA_SYNC_016|BOOKING_NOT_FOUND|when rest service to booking service fails

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
    "id": null,
    "version": null,
    "responsetime": "2019-04-24T13:24:14.781Z",
    "response": {
        "transactionId": "4145fefe-6694-11e9-9e21-c39e2258fc31",
        "countOfStoredPreRegIds": "1",
        "preRegistrationIds": [
            "41342175487213"
        ]
    },
    "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No pre-registration ids passed in request body
```JSON
{
    "id": null,
    "version": null,
    "errors": {
        "errorCode": "PRG_DATA_SYNC_011",
        "message": "INVALID_REQUESTED_PRE_REG_ID_LIST"
    },
    "responsetime": "2019-04-24T13:23:17.378Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
- -|FAILED_TO_STORE_PRE_REGISTRATION_IDS|access to sync tables fail

### GET /sync/:preRegistrationId
This request is used by registration client to retrieve particular pre-registration data based on a pre-registration id.

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
    "id": null,
    "version": null,
    "responsetime": "2019-04-24T12:46:18.335Z",
    "response": {
        "pre-registration-id": "41342175487213",
        "registration-client-id": "10008",
        "appointment-date": "2019-04-26",
        "from-time-slot": "12:00",
        "to-time-slot": "12:15",
        "zip-filename": "41342175487213",
        "zip-bytes":"{ByteCode}"
   },
   "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data exist for the requested pre-registration id
```JSON
{
    "id": null,
    "version": null,
    "errors": {
        "errorCode": "PRG_PAM_APP_005",
        "message": "No data found for the requested pre-registration id"
    },
    "responsetime": "2019-04-24T12:14:38.607Z",
    "response": null
}
```
#### Other Failure details
Error Code | Error Message | Error Description
-----|----------|-------------
PRG_BOOK_RCI_013|Booking data not found|If appointment is not booked against the preregistration id
PRG_DATA_SYNC_007|DEMOGRAPHIC_GET_RECORD_FAILED|when rest service to demographic service fails
PRG_DATA_SYNC_016|BOOKING_NOT_FOUND|when rest service to booking service fails
PRG_DATA_SYNC_005|FAILED_TO_CREATE_A_ZIP_FILE|If any error occurs while creating the zip file bytes
PRG_DATA_SYNC_014|FILE_IO_EXCEPTION|File system exception
PRG_DATA_SYNC_006|FAILED_TO_FETCH_DOCUMENT|when rest service to document service fails

