This section details about the service API in the Pre-Registration modules

* [Login Service](#login-service-public)

* [Demographic Service](#demographic-service-public)

* [Document Service](#document-service-public)

* [DataSync Service](#datasync-service-external)

* [Booking Service](#booking-service-public)

* [BatchJob Service](#batchjob-service-private)

* [Generate QR code service](#generate-qr-code-service-public)

* [Notification Service](#notification-service-public)

* [Transliteration Service](#transliteration-service-public)

**Note**: id,version and requesttime, responsetime in request and response bodies are optional fields and not consumed by pre registration application unless defined. Though we need to pass these as part of the request, it should not be tested.
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
request.langcode|Yes|The preferred language code |fra

#### Request:
```JSON
{
	"id": "mosip.pre-registration.login.sendotp",
	"version": "1.0",
	"requesttime": "2019-03-15T07:24:47.605Z",
	"request": {
		"langCode": "fra",
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
	"responsetime": "2019-03-15T07:24:50.246Z",
	"response": {
		"message": "OTP sent successfully to specified channel"
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
		"OTP": "345674",
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
    "responsetime": "2019-03-15T08:08:13.246Z",
    "response": {
	  "message": "OTP Validated Successfully"
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
    "responsetime": "2019-03-27T06:22:19.673Z",
    "response": null,
    "errors": [
        {
            "errorCode": "KER-OTV-005",
            "message": "Validation can't be performed against this key. Generate OTP first."
        }
    ]
}
```
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
    "responsetime": "2019-03-27T06:22:19.673Z",
    "response": {
         "message": "Token has been invalidated successfully"
    },
    "errors": null
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
    "id": "mosip.pre-registration.login.config",
    "version": "1.0",
    "responsetime": "2019-03-27T06:22:19.673Z",
    "response": {
         "mosip.kernel.OTP.default-length": "6",
         "mosip.id.validation.identity.postalCode": "^[(?i)A-Z0-9]{6}$",
         "mosip.left_to_right_orientation": "eng,fra",
         "preregistration.recommended.centers.locCode": "4",
         "mosip.kernel.OTP.validation-attempt-threshold": "3",
         "mosip.primary-language": "ara",
         "preregistration.timespan.cancel": "24",
         "mosip.default.dob.month": "01",
         "preregistration.availability.noOfDays": "7",
         "mosip.kernel.OTP.expiry-time": "120",
         "mosip.id.validation.identity.dateOfBirth": "^\\d{4}/([0]\\d|1[0-2])/([0-2]\\d|3[01])$",
         "mosip.supported-languages": "eng,ara,fra",
         "preregistration.workflow.demographic": "true/false ",
         "preregistration.workflow.documentupload": "true/false ",
         "mosip.id.validation.identity.postalCode.length": "6",
         "mosip.kernel.sms.number.length": "10",
         "preregistration.availability.sync": "9",
         "mosip.id.validation.identity.email.length": "50",
         "preregistration.timespan.rebook": "24",
         "mosip.id.validation.identity.email": "^[\\w-\\+]+(\\.[\\w]+)*@[\\w-]+(\\.[\\w]+)*(\\.[a-z]{2,})$",
         "mosip.id.validation.identity.CNIENumber": "^([0-9]{10,30})$",
         "mosip.right_to_left_orientation": "ara",
         "mosip.kernel.pin.length": "6",
         "mosip.id.validation.identity.phone": "^([6-9]{1})([0-9]{9})$",
         "preregistration.workflow.booking": "true/false ",
         "mosip.id.validation.identity.CNIENumber.length": "30",
         "mosip.login.mode": "email,mobile",
         "mosip.id.validation.identity.phone.length": "10",
         "preregistration.auto.logout": "10",
         "mosip.secondary-language": "fra",
         "preregistration.nearby.centers": "2000",
         "mosip.default.dob.day": "01",
         "preregistration.booking.offset": "2"
      },
      "errors": null
}
```
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
   "requesttime":"2019-01-22T07:22:57.086Z",
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
            "postalCode":"560059",
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
   "responsetime":"2019-03-15T08:08:13.246Z",
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
  "errors": [
        {
	   "errorCode": "PRG_PAM_APP_001",
	   "message": "Failed to create the pre-registration with demographic data provided"
	}
   ]
}
```
###### Other Failure Details:
Error Code|Message Code|Description
-----|----------|-------------
PRG_CORE_REQ_004|INVALID_REQUEST_BODY|Invalid or empty Request Body.
PRG_PAM_APP_001|UNABLE_TO_CREATE_THE_PRE_REGISTRATION|Failed to create the pre-registration with demographic data provided.

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
  "requesttime": "2019-01-22T07:22:57.086Z",
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
            "postalCode":"560059",
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
###### Other Failure Details:
Error Code|Message Code|Description
-----|----------|-------------
PRG_CORE_REQ_004|INVALID_REQUEST_BODY|Invalid or empty Request Body.
PRG_PAM_APP_006|UNABLE_TO_FETCH_THE_PRE_REGISTRATION|unable to fetch details based on pre-registration-id.

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
  "id": "mosip.pre-registration.demographic.fetch.details",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response":{
         "preRegistrationId":"20180396713560",
         "createdBy":"9900806086",
         "createdDateTime":"2019-01-11T11:01:21.947Z",
         "updatedDateTime":"2019-01-15T14:25:56.512Z",
         "statusCode":"Pending_Appointment",
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
            "postalCode":"560059",
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
  "id": "mosip.pre-registration.demographic.fetch.details",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response":null,
  "errors": [
	{
	   "errorCode": "PRG_PAM_APP_006",
	   "message": "No data found for the requested pre-registration id"
        }
   ]
}
```
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
preRegistrationId |Yes|Id of the application|62076019780925

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All applications status fetched successfully

```JSON
{
  "id": "mosip.pre-registration.demographic.fetch.status",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response":{
      "statusCode": "Pending_Appointment",
      "preRegistrationId": "62076019780925"
    },
  "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id.
```JSON
{
  "id": "mosip.pre-registration.demographic.fetch.status",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
	{
	    "errorCode": "PRG_PAM_APP_006",
	    "message": "No data found for the requested pre-registration id"
	}
   ]
}
```

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
  "id": "mosip.pre-registration.demographic.fetch.basic",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response":{
       "basicDetails":[
        {
         "preRegistrationId":"62076019780925",
         "fullname":[
            {
               "language":"fra",
               "value":"ashish"
            },
            {
               "language":"ara",
               "value":"َسهِسه"
            }
         ],
         "statusCode":"Pending_Appointment",
         "appointmentDetails":null,
         "postalCode":"767882"
      },
      {
         "preRegistrationId":"64269837502851",
         "fullname":[
            {
               "language":"fra",
               "value":"ashish"
            },
            {
               "language":"ara",
               "value":"َسهِسه"
            }
         ],
         "statusCode":"Booked",
         "appointmentDetails":{
            "registration_center_id":"RCG-RC-01",
            "appointment_date":"2018-01-17",
            "time_slot_from":"09:00:00",
            "time_slot_to":"09:30:00"
         },
        "postalCode":"767882"
      }
    ]
   },
   "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No record found for the requested user id.
```JSON
{
  "id": "mosip.pre-registration.demographic.fetch.basic",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
	{
	    "errorCode": "PRG_PAM_APP_005",
	    "message": "No record found for the requested user id"
	}
   ]
}
```
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
preRegistrationId |Yes|pre-registration id of the application|64269837502851

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Deletion of individual is successfully

```JSON
{
  "id": "mosip.pre-registration.demographic.delete",
  "version":"1.0",
  "responsetime": "2019-02-11T07:15:18.565Z",
  "response":{
      "preRegistrationId": "64269837502851",
      "deletedBy": "9876453738",
      "deletedDateTime": "2019-02-11T07:15:18.549Z"
   },
  "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No data found for the requested pre-registration id
```JSON
{
  "id": "mosip.pre-registration.demographic.delete",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
	{
           "errorCode": "PRG_PAM_APP_006",
	   "message": "No data found for the requested pre-registration id"
	}
    ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: failed to delete the pre-registration record.
```JSON
{
  "id": "mosip.pre-registration.demographic.delete",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
	{
	  "errorCode": "PRG_PAM_APP_004",
	  "message": "Failed to delete data for the requested pre-registration id"
	}
    ]
}
```

# Document Service (public)
This service enables Pre-Registration portal to request for uploading the document for a particular pre-registration.

* [POST /documents/:preRegistrationId](#post-documentspreregistrationid)
* [PUT /documents/:preRegistrationId](#put-documentspreregistrationid)
* [GET /documents/:preRegistrationId](#get-documentspreregistrationid)
* [GET /documents/:documentId?preRegistrationId=:preRegistrationId](#get-documentsdocumentidpreregistrationidpreregistrationid)
* [DELETE /documents/preregistration/:preRegistrationId](#delete-documentspreregistrationpreregsitrationid)
* [DELETE /documents/:documentId?preRegistrationId=:preRegistrationId](#delete-documentsdocumentidpreregistrationidpreregistrationid)


### POST /documents/:preRegistrationId
This request is used to upload document with the metadata which include document cateogry code, document type code and document format for a pre-registration Id.

#### Resource URL
<div>https://mosip.io/preregistration/v1/douments/:preRegistrationId</div>

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

##### Failure Response:
###### Status code: '200'
###### Description: Document virus scan failed
```JSON
{ 
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
	{
	   "errorCode": "PRG_PAM_DOC_010",
	   "message": "Document virus scan failed"
	}
    ]
}
```

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
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response": {
    "documnetsMetaData":[
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
      "multipartFile": :ByteArray
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
##### Failure Response:
###### Status code: '200'
###### Description: Failed to fetch from File System server
```JSON
{
   "id": "mosip.pre-registration.document.fetch.content",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
      {
        "errorCode": "PRG_PAM_DOC_006",
        "message": "Failed to fetch from File System server"
     }
  ]
}
```
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
    	    "errorCode": "PRG_PAM_DOC_006",
    	    "message": "Documents failed to delete"
         }
    ]
}
```
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
##### Failure Response:
###### Status code: '200'
###### Description: Failed to delete from file system server
```JSON
{
   "id": "mosip.pre-registration.document.delete.specific",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
      {
         "errorCode": "PRG_PAM_DOC_006",
         "message": "Failed to delete from file system server"
     }
  ]
}
```
# DataSync Service (External)
This service enables Pre-Registration to a registration client, request to retrieve all pre-registration ids based on registration client id, appointment date and an user type.

* [POST /sync](#post-sync)
* [POST /sync/consumedPreRegIds](#post-consumedpreRegIds)
* [GET /sync/:preRegistrationId](#get-syncpreregistrationid)

### POST /sync
This request is used by registration client to retrieve all the pre-registration Ids by date range.

#### Resource URL
<div>https://mosip.io/preregistration/v1/datasync/sync/</div>

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
   "id": "mosip.pre-registration.datasync.fetch.ids",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response":{
    "transactionId": "aee82061-2dcb-11e9-b69e-b1fffe7cd4d7",
    "countOfPreRegIds": "3",
    "preRegistrationIds": {
      "69032701821381": "2019-02-09T06:07:24.500Z",
      "42839738507687": "2019-02-10T07:07:24.612Z",
      "45219759079506": "2019-02-11T08:07:24.662Z",
    }
  },
  "errors":null
}

```
##### Failure Response:
###### Status code: '200'
###### Description: No Records found for the date range
```JSON
{
   "id": "mosip.pre-registration.datasync.fetch.ids",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
        {
    	   "errorCode": "PRG_DATA_SYNC_001",
    	   "message": "No Records found for the date range"
	}
    ]
}
```
### POST /sync/consumedPreRegIds
This request is used by registration processor, to retrieve all processed pre-registration ids and store in pre-registration database and delete records from main table and move to history table.

#### Resource URL
<div>https://mosip.io/preregistration/v1/datasync/sync/consumedPreRegIds</div>

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
###### Description: No pre-registration ids passed in request body
```JSON
{
   "id": "mosip.pre-registration.datasync.store",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         { 
            "errorCode": "PRG_DATA_SYNC_011",
            "message": "No pre-registration ids passed in request body"
	 }
    ]
}
```
### GET /sync/:preRegistrationId
This request is used by registration client to retrieve particular pre-registration data based on a pre-registration id.

#### Resource URL
<div>https://mosip.io/preregistration/v1/datasync/sync/:preRegistrationId</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Pre Registration id|94625367217037

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Data Sync records fetched
```JSON
{
   "id": "mosip.pre-registration.datasync.fetch",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
    "registrationCenterId": "10005",
    "appointmentDate": "2019-02-13",
    "fromTimeSlot": "09:00",
    "toTimeSlot": "09:15",
    "zipFilename": "94625367217037",
    "zipBytes": "{ByteCode}"
   },
   "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No data exist for the requested pre-registration id
```JSON
{
   "id": "mosip.pre-registration.datasync.fetch.ids",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_DATA_SYNC_002",
            "message": "No data exist for the requested pre-registration id"
         }
   ]
}
```

# Booking Service (Public)
This service details used by Pre-Registration portal to book an appointment by providing his/her basic appointment details.

* [POST /appointment/:preRegistrationId](#post-appointmentpreregistrationid)
* [PUT /appointment/:preRegistrationId](#put-appointmentpreregistrationid)
* [GET /appointment/:preRegistrationId](#get-appointmentpreregistrationid)
* [GET /appointment/availability/:registrationCenterId](#get-appointmentavailabilityregistrationcenterid)
* [GET /appointment/:registrationCenterId?fromDate=:date&toDate=:date](#get-appointmentregistrationcenteridfromdatedatetodatedate)

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
  "request": {
        "registration_center_id": "10005",
        "appointment_date": "2019-02-13",
        "time_slot_from": "15:31:00",
        "time_slot_to": "15:44:00"
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
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
      "message": "Appointment booked successfully"
    },
   "errors":null
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
            "message": "Slot availability not found for selected time"
         }
    ]
}
```
### PUT /appointment/:preRegistrationId
This request used to retrieve the appointment details for the specified pre-registration id,
if exist update the availability for the slot and delete the record from the table and update the demographic record status "Pending_Appointment".

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
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response":{
        "message":"Appointment cancelled successfully"
    },
    "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Appointment cancellation failed.
```JSON
{
   "id": "mosip.pre-registration.appointment.cancel",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors": [
          {
             "errorCode": "PRG_BOOK_RCI_015",
             "message": "Appointment cancellation failed"
          }
    ] 
}
```
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
            "message": "No Appointment record found for the specified pre-registration id"
         }
    ]
}
```
### GET /appointment/availability/:registrationCenterId
This request is used to retrieve all appointment slots available for booking based on the specified registration center id.

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
        "registrationCenterId": "10004",
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
### GET /appointment/:registrationCenterId?fromDate=:Date&toDate=:Date
This request is used to retrieve all pre-registration ids available for specified registration center and date range.

#### Resource URL
<div>https://mosip.io/preregistration/v1/appointment/:registrationCenterId?fromDate=:Date&toDate=:Date</div>

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
   "id": "mosip.pre-registration.appointment.ids",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
        "preRegistrationIds": [
                       "94625367217037",
                       "43526512857302"
         ]
    },
    "errors":null
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
            "errorCode": "PRG_BOOK_RCI_016",
            "message": "No available slots found for specified registration center with date range"
         }
    ]
}
```
# BatchJob Service (Private)
This service is used by Pre-Registration portal to update an expired pre registration id  and consumed pre registration id and master data sync for availability.

* [PUT batch/expiredApplication](#put-expiredapplication)
* [PUT batch/consumedApplication](#put-consumedapplication)
* [PUT batch/availabilitySync](#put-availabilitysync)

### PUT /expiredApplication
This request is used to update status of appointment expired pre-registration ids to expired status in database.

#### Resource URL
<div>https://mosip.io/preregistration/v1/batch/expiredApplication</div>

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
   "id": "mosip.pre-registration.batchjob.expired",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
        "message": "Expired status updated successfully"
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No pre registration record found to update expired status
```JSON
{
   "id": "mosip.pre-registration.booking.book",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_PAM_BAT_001",
            "message": "No pre registration record found to update expired status"
         } 
    ]
}
```
### PUT /consumedApplication
This request is used to update the consumed status for all pre-Registration ids given by registration processor.

#### Resource URL
<div>https://mosip.io/preregistration/v1/batch/consumedApplication</div>

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
   "id": "mosip.pre-registration.batchjob.expired",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
        "message":  "Consumed status updated successfully"
    },
   "errors":null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No pre registration record found to update consumed status
```JSON
{
   "id": "mosip.pre-registration.booking.book",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": null,
   "errors":[ 
         {
            "errorCode": "PRG_PAM_BAT_002",
            "message": "No pre registration record found to update consumed status"
         }
    ]
}
```

### PUT /availabilitySync
This request is used to synchronize booking slots availability table with master data.

#### Resource URL
<div>https://mosip.io/preregistration/v1/batch/availabilitySync</div>

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
   "id": "mosip.pre-registration.batchjob.sync",
   "version" : "1.0",
   "responsetime": "2019-01-16T17:31:04.021Z",
   "response": {
      "message": "Master Data Sync is successful"
   },
   "errors":null
}
```
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
    	    "errorCode": "PRG_PAM_ACK_006",
    	    "message": " Failed to generate QR code"
	 }
    ]
}
```

# Notification Service (public)
This service details used by Pre-Registration portal to trigger notification via SMS or email and get QRCode.

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

#### Request Part Parameters
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
request.multipart file| Yes| pdf file of acknowledgment page|37802950913289.pdf
request.LangCode| Yes| language code whatever user choose while login|eng

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
	"emailID": "sanober.noor2@mindtree.com"
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
            "errorCode": "PRG_PAM_ACK_001",
            "message": "Mobile number or Email Id is missing"
         }
    ]
}
```

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
    "to_field_lang": "ara",
    "to_field_value": ""
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Given key is translitrated successfully
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
            "errorCode": "PRG_PAM_TRL_002",
            "message": "Failed to transliterate"
         }
    ]
}
```