This section details about the service API in the Pre-Registration modules

## Content
<!--ts-->
 [Auth Service APIs](#auth-service-apis)

 [Demographic Service APIs](#demographic-service-apis)

 [Document Service APIs](#document-service-apis)

 [Data sync Service APIs](#data-sync-service-apis)

 [Booking Service APIs](#booking-service-apis)

 [BatchJob Service APIs](#batchjob-service-apis)

 [Notification Service APIs](#notification-service-apis)

 [Transliteration Service APIs](#transliteration-service-apis)

<!--te-->

**Note**: id,version and requestTime, responseTime in request and response bodies are optional fields and not consumed by pre registration application unless defined. Though we need to pass these as part of the request, it should not be tested.
***

#Auth Service APIs
This service details used by Pre-Registration portal to authenticate user by sending otp to the user, validating with userid and otp.

* [POST /login/sendOtp](#post-login-sendotp)
* [POST /login/validateOtp](#post-login-validateotp)
* [POST /logout/invalidateToken](#post-logout-invalidatetoken)

###POST /login/sendOtp
This request will send the OTP to the requested user in the preferred channel(sms/email)

#### Resource URL
https://mosip.io/pre-registration/auth/v1.0/login/sendOtp

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.pre-registration.auth.sendotp
version |Yes|version of the application|1.0
requestTime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.userid |Yes|user id of the applicant(mobile number/email address)|8907654778
request.langcode|Yes|The preferred language code |fra

#### Request:
```JSON
{
	"id": "mosip.pre-registration.auth.sendotp",
	"version": "1.0",
	"requestTime": "2019-03-15T07:24:47.605Z",
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
	"id": "mosip.pre-registration.auth.sendotp",
	"version": "1.0",
	"responseTime": "2019-03-15T07:24:50.246Z",
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
	"id": "mosip.pre-registration.auth.sendotp",
	"version": "1.0",
	"responseTime": "2019-03-15T08:09:42.327Z",
	"response": null,
	"errors": [
		{
		 "errorCode": "PRG_AUTH_001",
		 "message": "OTP failed to send through a specified channel"
		}
	]	
}
```

###POST /login/validateOtp
This request will validate the otp with respect to userid and provide the authorize token in the browser cookies.

#### Resource URL
https://mosip.io/pre-registration/auth/v1.0/login/validateOtp

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.pre-registration.auth.useridotp
version |Yes|version of the application|1.0
requestTime |Yes|Time of the request|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.userid |Yes|user id of the applicant (mobile number/email address)|8907654778
request.otp|Yes| received OTP  |345674

#### Request:
```JSON
{
	"id": "mosip.pre-registration.auth.useridotp",
	"version": "1.0",
	"requestTime": "2019-03-15T08:28:04.783Z",
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
	"id": "mosip.pre-registration.auth.useridotp",
	"version": "1.0",
	"responseTime": "2019-03-15T08:08:13.246Z",
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
    "id": "mosip.pre-registration.auth.useridotp",
    "version": "1.0",
    "responseTime": "2019-03-27T06:22:19.673Z",
    "response": null,
    "errors": [
        {
            "errorCode": "KER-OTV-005",
            "message": "Validation can't be performed against this key. Generate OTP first."
        }
    ]
}
```

###POST /logout/invalidateToken
This request will invalidate the authorization token when force logout is done.

#### Resource URL
https://mosip.io/pre-registration/auth/v1.0/logout/invalidateToken

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
    "id": "mosip.pre-registration.auth.useridotp",
    "version": "1.0",
    "responseTime": "2019-03-27T06:22:19.673Z",
    "response": {
         "message": "Token has been invalidated successfully"
    },
    "errors": null
}
```

# 2.7.2 Demographic Service APIs
This service details used by Pre-Registration portal to maintain the demographic form by providing his/her basic demographic details.

### Host
##### Integration - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | True |
| DELETE | True |

#### 2.7.2.1 POST Operation
#### Path -  `/applications`
#### Summary
Create new pre-registration with demographic details to generate pre-registration id and associate with demographic details.

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

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
###### Description: Failed to create a pre-registration. 
```JSON
{
  "id": "mosip.pre-registration.demographic.create",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
        {
		"errorCode": "PRG_PAM_APP_001",
		"message": "UNABLE_TO_CREATE_THE_PRE_REGISTRATION"
		}
	]
}
```
###### Other Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_CORE_REQ_004|INVALID_REQUEST_BODY|Invalid or empty Request Body.
PRG_PAM_APP_001|UNABLE_TO_CREATE_THE_PRE_REGISTRATION|Failed to create a pre-registration.

#### 2.7.2.2 PUT Operation
#### Path -  `/applications/<preRegistrationId>`
#### Summary
Update pre-registration's demographic details by providing pre-registration id in the path parameter and updated demographic details in request body.

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

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

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
      "langCode": "eng",
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
		"message": "UNABLE_TO_UPDATE_THE_PRE_REGISTRATION"
		}
	]
}
```
###### Other Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_CORE_REQ_004|INVALID_REQUEST_BODY|Invalid or empty Request Body.
PRG_PAM_APP_006|UNABLE_TO_FETCH_THE_PRE_REGISTRATION|unable to fetch details based on pre-registration-id.
PRG_PAM_APP_008|UNABLE_TO_UPDATE_THE_PRE_REGISTRATION| unable to update pre-registration demographic detials.

#### 2.7.2.3 GET Operation
#### Path -  `/applications/<preRegistrationId>`
#### Summary
Retrieve Pre-Registration demographic data by pre-Registration id provided in request path parameter.

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|64269837502851

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
###### Description: unable to fetch the details by pre-registration id.
```JSON
{
  "id": "mosip.pre-registration.demographic.fetch.details",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response":null,
  "errors": [
	{
	"errorCode": "PRG_PAM_APP_006",
	"message": "UNABLE_TO_FETCH_THE_PRE_REGISTRATION"
	}
   ]
}
```
#### 2.7.2.4 DELETE Operation
#### Path -  `/applications/<preRegistrationId>`
#### Summary 
Discard the entire pre-registration details based pre-registration id provided in request path parameter.

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|pre-registration id of the application|64269837502851

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
  "id": "mosip.pre-registration.demographic.delete",
  "version":"1.0",
  "responsetime": "2019-02-11T07:15:18.565Z",
  "response": [
    {
      "preRegistrationId": "64269837502851",
      "deletedBy": "9876453738",
      "deletedDateTime": "2019-02-11T07:15:18.549Z"
    }
  ],
  "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid pre-registration id
```JSON
{
  "id": "mosip.pre-registration.demographic.delete",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
		{
		"errorCode": "PRG_PAM_APP_006",
		"message": "UNABLE_TO_FETCH_THE_PRE_REGISTRATION"
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
		"message": "FAILED_TO_DELETE_THE_PRE_REGISTRATION_RECORD"
		}
	]
}
```

#### 2.7.2.5 GET Operation
#### Path -  `/applications/status/<preRegistrationId>`
#### Summary
Retrieve pre-registration application status by providing the pre-registration id in request path parameter.

#### Request Path Parameter
Name | Required | Description | Comment
-----|----------|-------------|--------
preRegistrationId |Yes|Id of the application|62076019780925

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
###### Description: Invalid or empty pre-registration id.
```JSON
{
  "id": "mosip.pre-registration.demographic.fetch.status",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
	{
		"errorCode": "PRG_PAM_APP_006",
		"message": "UNABLE_TO_FETCH_THE_PRE_REGISTRATION"
	}
   ]
}
```

#### 2.7.2.6 GET Operation
#### Path -  `/applications/<user_id>`
#### Summary
Retrieve All Pre-Registration id, Full name in both language, Status Code and Appointment details and Postal Code by user id.

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
user_id |Yes|User Id of the application|sanober@gmail.com

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
  "response":[
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
   ],
   "errors": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: No pre-registration data available for user id.
```JSON
{
  "id": "mosip.pre-registration.demographic.fetch.basic",
  "version":"1.0",
  "responsetime": "2019-02-11T13:46:00.534Z",
  "response": null,
  "errors": [
	{
	 "errorCode": "PRG_PAM_APP_005",
	 "message": "NO_RECORD_FOUND_FOR_USER_ID"
	}
   ]
}
```

# 2.7.3 Document Service APIs
This service enables Pre-Registration portal to request for uploading the document for a particular pre-registration.

### Host
##### QA - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

***
#### [Swagger API spec 0.8.0 version link](https://github.com/mosip/mosip/tree/0.8.0/docs/design/pre-registration/service/Document-Service-API-Spec.yaml)
***

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | False |
| DELETE | True |

#### 2.7.3.1 POST Operation
#### Path -  `/documents`
#### Summary
Upload document for a pre-registration Id.

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.document.upload
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.pre_registration_id |Yes|Pre-registration id of the application|49158360813920
request.doc_cat_code |Yes|Document category code|POI
request.doc_typ_code |Yes|Document type code|address
request.lang_code |Yes|Language code of the application|ENG

```JSON
{
		"id": "mosip.pre-registration.document.upload",
		"version" : "1.0",
		"requesttime" : "2019-03-13T07:22:57.086Z",
		"request" :
		{
			"pre_registartion_id" : "36732486130976",
			"doc_cat_code" : "POA",
			"doc_typ_code" : "address",
			"lang_code" : "ENG"
		 }
}
```

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document uploaded successfully
```JSON
{
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T16:41:06.659Z",
  "response": [
    {
      "preRegsitrationId": "49158360813920",
      "documnetId": "2c979c01680905860168091c21970001",
      "documentName": "passport.PDF",
      "documentCat": "POI",
      "documentType": "identity",
      "resMsg": "DOCUMENT_UPLOAD_SUCCESSFUL"
    }
  ],
  "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{ 
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
		{
		"errorCode": "PRG_PAM_DOC_007",
		"message": "DOCUMENT_EXCEEDING_PERMITTED_SIZE"
		}
    ]
}
```

###### Other Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_CORE_REQ_004|INVALID_REQUEST_BODY|If the Request Body is empty.
PRG_PAM_DOC_004|DOCUMENT_INVALID_FORMAT|Invalid document format.
PRG_PAM_APP_005|UNABLE_TO_FETCH_THE_PRE_REGISTRATION|When preregistration data is not found for the preregistration id in the DB.
PRG_PAM_DOC_014|MANDATORY_FIELD_NOT_FOUND |If the document & preregistration id, status code, document category code or preregistration data is empty are failed to store in the db.
PRG_PAM_DOC_010|DOCUMENT_FAILED_IN_VIRUS_SCAN| Document virus scan failed. 
PRG_PAM_DOC_020|DEMOGRAPHIC_GET_RECORD_FAILED| Retrieval of preregistration data failed.


#### 2.7.3.2 POST Operation
#### Path -  `/documents/copy`
#### Summary
This service enables Pre-Registration portal to request for copy the document from one pre-registration id to another.


#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
catCode|Yes|Document category code|POA
destinationPreId |Yes|Destination Pre-registration id of the application|67531403498547
sourcePrId |Yes|Source Pre-registration id of the application|97285429827016

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document successfully copied
```JSON
{
  "id": "mosip.pre-registration.document.copy",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response": [
    {
      "sourcePreRegId": "97285429827016",
      "sourceDocumnetId": "4028abea68334b510168334e62060001",
      "destPreRegId": "67531403498547",
      "destDocumnetId": "2c9180836833aa3101685b88e12f0016"
    }
  ],
  "errors":null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Document not found for the source pre-registration Id
```JSON
{
  "id": "mosip.pre-registration.document.upload",
  "version" : "1.0",
  "responsetime": "2019-01-16T17:31:04.021Z",
  "response":null,
  "errors":[
		{
        "errorCode": "PRG_PAM_DOC_005",
        "message": "DOCUMENT_IS_MISSING"
        }
	]
}
```

###### Other Failure Details:
Code|Message|Description
-----|----------|-------------
PRG_PAM_DOC_018|INVALID_REQUEST_PARAMETER|Source preregistration id or Destination preregistration id is empty or invalid.
PRG_PAM_DOC_009|DOCUMENT_FAILED_TO_UPLOAD|HDFS exception.
PRG_PAM_DOC_011|DOCUMENT_FAILED_TO_COPY|if the copied document & document details are failed to store in the db.


#### 2.7.3.3 GET Operation
#### Path -  `/documents`
#### Summary
This service enables Pre-Registration portal request to retrieve all document associated with particular pre-registration.

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
pre_registration_id |Yes|Pre-registration id of the application|97285429827016

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Documents retrieved successfully
```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-01-17T11:31:44.994Z",
  "response": [
    {
      "pre_registration_id": "97285429827016",
      "doc_name": "morethan1mb.PDF",
      "doc_id": "4028abea68334b510168334e62060001",
      "doc_cat_code": "POA",
      "doc_typ_code": "address",
      "doc_file_format": "pdf",
      "multipartFile": "{ByteCode}"
    },
    {
      "prereg_id": "97285429827016",
      "doc_name": "Doc.pdf",
      "doc_id": "2c979ec9683c5aaf01683c7807110000",
      "doc_cat_code": "POB",
      "doc_typ_code": "address",
      "doc_file_format": "pdf",
      "multipartFile": "{ByteCode}"
    },
    {
      "prereg_id": "97285429827016",
      "doc_name": "Address.pdf",
      "doc_id": "2c979ec9683c5aaf01683c7892bc0001",
      "doc_cat_code": "POI",
      "doc_typ_code": "address",
      "doc_file_format": "",
      "multipartFile": "{ByteCode}"
    }
  ]
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty pre-registration Id
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_018",
    "message": "INVALID_REQUEST_PARAMETER"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If the document is not found in the db for the preregistration id
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description:  ceph exception
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_FAILED_TO_FETCH"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```

#### 2.7.3.4 DELETE Operation
#### Path -  `/documents`
#### Summary
This service enables Pre-Registration portal, request to delete the document for a particular document id.

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
documentId |Yes|document id of the application|2c9180836833aa31016837aac4c40012

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Document successfully deleted
```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-01-17T11:46:49.220Z",
  "response": [
    {
      "documnet_Id": "2c9180836833aa31016837aac4c40012",
      "resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If the document is not found in the db for the preregistration id
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: ceph exception
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_006",
    "message": "DOCUMENT_FAILED_TO_DELETE"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```
#### 2.7.3.5 DELETE Operation
#### Path -  `/documents/byPreRegId`
#### Summary
This service enables Pre-Registration portal, request to delete all the document for a particular pre-registration id.

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
pre_registration_id |Yes|pre-registration id of the application|37802950913289

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Documents successfully deleted
```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-01-17T11:52:22.165Z",
  "response": [
    {
      "documnet_Id": "2c9180836833aa31016833b242c50000",
      "resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
    },
	{
      "documnet_Id": "2c9180836833aa31016833b242c22120",
      "resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty pre-registration Id
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_018",
    "message": "INVALID_REQUEST_PARAMETER"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: if the document & document details are failed to delete from the db
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_005",
    "message": "DOCUMENT_IS_MISSING"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: ceph exception
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_DOC_006",
    "message": "DOCUMENT_FAILED_TO_DELETE"
  },
  "id": "string",
  "responsetime": "2019-01-16T15:15:05.467Z",
  "response": null
}
```

# 2.7.4 Data sync Service APIs
This service enables Pre-Registration to a registration client , request to retrieve all pre-registration ids based on registration client id, appointment date and an user type.

### Host
##### Integration - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

***
#### [Swagger API spec 0.8.0 version link](https://github.com/mosip/mosip/tree/0.8.0/docs/design/pre-registration/service/Datasync-Service-API-Spec.yaml)
***

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | False |
| DELETE | False |

#### 2.7.4.1 POST Operation
#### Path -  `/datasync`
#### Summary
Retrieve all the pre-registration Ids by date range and registration center Id.

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.datasync
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.registration-client-id |Yes|Registration center Id of the application|12
request.from-date |Yes|From date of the application|2019-01-01 00:00:00
request.to-date |Yes|To date of the application|2019-01-31 00:00:00
request.user-id |Yes|user Id of the application|Officer

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request:
```JSON
{
  "id": "mosip.pre-registration.datasync",
  "version": "1.0",
  "requesttime": "2019-02-11T06:57:29.969Z",
  "request": {
    "registration-client-id":"10005",
    "from-date":"2018-02-11 00:00:00",
    "to-date":"2019-02-12 00:00:00",
    "user-id":"Officer"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: All Pre-Registration Ids fetched successfully
```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T07:07:24.757Z",
  "response": {
    "transactionId": "aee82061-2dcb-11e9-b69e-b1fffe7cd4d7",
    "countOfPreRegIds": "12",
    "preRegistrationIds": {
      "69032701821381": "2019-02-11T07:07:24.500Z",
      "42839738507687": "2019-02-11T07:07:24.612Z",
      "45219759079506": "2019-02-11T07:07:24.662Z",
      "40685960418214": "2019-02-11T07:07:24.711Z",
      "62750730690468": "2019-02-11T07:07:24.270Z",
      "52948359801624": "2019-02-11T07:07:24.559Z",
      "54680925863583": "2019-02-11T07:07:24.752Z",
      "20328697253154": "2019-02-11T07:07:24.320Z",
      "28304826952645": "2019-02-11T07:07:24.437Z",
      "38419640168598": "2019-02-11T07:07:24.383Z",
      "94625367217037": "2019-02-11T07:07:24.203Z",
      "62457394860916": "2019-02-11T07:07:24.144Z"
    }
  }
}

```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:50:25.969Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:39:35.058Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:39:35.058Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_004",
    "message": "INVALID_REQUEST_BODY"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:39:35.058Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Empty registration center Id
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_009",
    "message": "INVALID_REGISTRATION_CENTER_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:41:35.396Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty from-date or to-date
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_010",
    "message": "INVALID_REQUESTED_DATE"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:42:16.393Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Empty user id
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_003",
    "message": "INVALID_USER_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If appointment is not booked under the registration center Id for the preregistration id
```JSON
{
  "err": {
    "errorCode": "PRG_BOOK_RCI_013",
    "message": "BOOKING_DATA_NOT_FOUND"
  },
  "id": "string",
  "version":"1.0",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If retrieval of booking data fails
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_013",
    "message": "FAILED_TO_GET_PRE_REG_ID_BY_REG_CLIENT_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: If retrieval of preregistration data fails 
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_007",
    "message": "DEMOGRAPHIC_GET_RECORD_FAILED"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If no preregistration data created within the from date & to date
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_APP_005",
    "message": "RECORD_NOT_FOUND_FOR_DATE_RANGE"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:27:36.387Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If retrieval of preregistration data fails 
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_007",
    "message": "DEMOGRAPHIC_GET_RECORD_FAILED"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: File operation failed 
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_014",
    "message": "FILE_IO_EXCEPTION"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: When demographic JSON file & documents are not zipped
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_005",
    "message": "FAILED_TO_CREATE_A_ZIP_FILE"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:45:35.030Z",
  "response": null
}
```

#### 2.7.4.2 GET Operation
#### Path -  `/datasync`
#### Summary
This service enables Pre-Registration to a registration client , request to retrieve particular pre-registration data based on a pre-registration id.

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
pre_registration_id |Yes|Pre Registration id|94625367217037

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes
#### Request:
```JSON
94625367217037
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Data Sync records fetched
```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T07:54:24.043Z",
  "response": {
    "pre-registration-id": "94625367217037",
    "registration-client-id": "10005",
    "appointment-date": "2019-02-13",
    "from-time-slot": "09:00",
    "to-time-slot": "09:15",
    "zip-filename": "94625367217037",
    "zip-bytes": "{ByteCode}"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If data does not exists for the preregistration id
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_APP_005",
    "message": "UNABLE_TO_FETCH_THE_PRE_REGISTRATION"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:58:27.909Z",
  "response": null
}
```
#### 2.7.4.3 POST Operation
#### Path -  `/datasync/store`
#### Summary
This service enables Pre-Registration to a registration processor , request to retrieve all processed pre-registration ids and store in pre-registration database and update the status code in main table.

#### Request Body Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.datasync
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.createdBy |Yes|Created user of the application|5766477466
request.createdDateTime |Yes|Created date & time of the application|2019-01-16T06:15:25.721Z
request.langCode |Yes|Language of the application|AR
request.preRegistrationIds |Yes|List of Preregistration Ids|42973267563920
request.updateBy |Yes|Updated user of the application|5766477466
request.updateDateTime |Yes|Updated date & time of the application|2019-01-16T06:15:25.721Z

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes
#### Request:
```JSON
{
  "id": "mosip.pre-registration.datasync",
  "version": "1.0",
  "requesttime": "2019-02-11T07:05:08.850Z",
  "request": {
    "createdBy": "987654321",
    "createdDateTime": "2019-02-04T08:06:54.230Z",
    "langCode": "12L",
    "preRegistrationIds": [
      "94625367217037",
      "43526512857302"
    ],
    "updateBy": "987654321",
    "updateDateTime": "2019-02-11T08:06:54.230Z"
  }
}
```
#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Consumed Pre-Registrations saved
```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T07:05:08.850Z",
  "response": {
    "transactionId": "26fde349-0e56-11e9-99e1-f7683fbbce99",
    "countOfPreRegIds": "1",
    "preRegistrationIds": "1"
  }
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:11:42.742Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:12:48.242Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:12:48.242Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_004",
    "message": "INVALID_REQUEST_BODY"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:12:48.242Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: If there are no pre-registration ids passed in request body
```JSON
{
  "err": {
    "errorCode": "PRG_DATA_SYNC_011",
    "message": "INVALID_REQUESTED_PRE_REG_ID_LIST"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:16:17.412Z",
  "response": null
}
```
# 2.7.5 Booking Service APIs
This service details used by Pre-Registration portal to book an appointment by providing his/her basic appointment details.

### Host
##### Integration - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

***
#### [Swagger API spec 0.8.0 version link](https://github.com/mosip/mosip/tree/0.8.0/docs/design/pre-registration/service/Booking-Service-API-Spec.yaml)
***

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | True |
| POST | True |
| PUT | True |
| DELETE | False |

#### 2.7.5.1 GET Operation
#### Path -  `/appointment`
#### Summary
Retrieve Pre-Registration appointment details by pre-Registration id.

#### Request Query Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
pre_registration_id |Yes|Id of the application|37802950913289

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment details successfully retrieved

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T13:24:18.868Z",
  "response": {
    "registration_center_id": "1",
    "appointment_date": "2019-02-13",
    "time_slot_from": "16:10",
    "time_slot_to": "16:23"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Unable to fetch the pre-Registration demographic data
```JSON
{
  "err": {
    "errorCode": "PRG_BOOK_RCI_013",
    "message": "BOOKING_DATA_NOT_FOUND"
  },
  "id": "string",
  "responsetime": "2019-02-11T08:45:42.797Z",
  "response": null
}
```
#### 2.7.5.2 GET Operation
#### Path -  `/appointment/availability`
#### Summary
Retrieve Pre-Registration appointment slots available for booking.

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
registration_center_id |Yes|Registration Center Id|1004

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Availability details fetched successfully

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T13:33:07.495Z",
  "response": {
    "regCenterId": "1004",
    "centerDetails": [
      {
        "date": "2019-02-13",
        "timeSlots": [
          {
            "fromTime": "15:44:00",
            "toTime": "15:57:00",
            "availability": 4
          },
          {
            "fromTime": "16:10:00",
            "toTime": "16:23:00",
            "availability": 3
          }
        ],
        "holiday": false
      },
      {
        "date": "2019-02-14",
        "timeSlots": [
          {
            "fromTime": "15:57:00",
            "toTime": "16:10:00",
            "availability": 4
          }
        ],
        "holiday": true
      }
    ]
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Unable to fetch available slots.
```JSON

{
  "err": {
    "errorCode": "PRG_BOOK_RCI_015",
    "message": "PRG_BOOK_RCI_015 --> NO_TIME_SLOTS_ASSIGNED_TO_THAT_REG_CENTER"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:33:43.114Z",
  "response": null
}
```
#### 2.7.5.3 POST Operation
#### Path -  `/appointment`
#### Summary
This service enables by Pre-Registration to book an registration center, request to book and re-book an appointment with a selected registration center and time slot. After successful booking update the status code Booked in main table.

#### Request Body Parameters for book
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationId|Yes|pre Registration Id|37802950913289
request.newBookingDetails.registration_center_id |Yes|Registration center Id of the application|1
request.newBookingDetails.appointment_date |Yes|Date of the appointment|2019-01-19
request.newBookingDetails.time_slot_from |Yes|Time Slot From|12:15:00
request.newBookingDetails.time_slot_from |Yes|Time Slot To|12:28:00
request.oldBookingDetail|No

#### Request Body Parameters for rebook
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationId|Yes|pre Registration Id|37802950913289
request.oldBookingDetails.registration_center_id |Yes|Registration center Id of the application|1
request.oldBookingDetails.appointment_date |Yes|Date of the appointment|2019-01-19
request.oldBookingDetails.time_slot_from |Yes|Time Slot From|12:15:00
request.oldBookingDetails.time_slot_from |Yes|Time Slot To|12:28:00
request.newBookingDetails.registration_center_id |Yes|Registration center Id of the application|1
request.newBookingDetails.appointment_date |Yes|Date of the appointment|2019-01-20
request.newBookingDetails.time_slot_from |Yes|Time Slot From|12:28:00
request.newBookingDetails.time_slot_from |Yes|Time Slot To|12:41:00

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request for book:
```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "version": "1.0",
  "requesttime": "2019-01-09T15:31:32.957Z",
  "request": [
  {
  "preRegistrationId": "20910892067562",
      "newBookingDetails": {
        "registration_center_id": "1",
        "appointment_date": "2019-02-13",
        "time_slot_from": "15:31:00",
        "time_slot_to": "15:44:00"
      }
    }
  ]
}
```
#### Request for rebook:
```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "version": "1.0",
  "requesttime": "2019-01-09T15:31:32.957Z",
  "request": [
    {
      "preRegistrationId": "20910892067562",
        "oldBookingDetails": {
        "registration_center_id": "1",
        "appointment_date": "2019-01-19",
        "time_slot_from": "15:31:00",
        "time_slot_to": "15:44:00"
      },
      "newBookingDetails": {
        "registration_center_id": "1",
        "appointment_date": "2019-02-13",
        "time_slot_from": "15:44:00",
        "time_slot_to": "15:57:00"
      }
    }
  ]
}
```


#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment booked successfully

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T13:21:21.617Z",
  "response": [
    {
      "preRegistrationId": "25316846873293",
      "bookingStatus": "Booked",
      "bookingMessage": "APPOINTMENT_SUCCESSFULLY_BOOKED"
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid Pre Registration Id.
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_APP_005",
    "message": "INVALID_PRE_REGISTRATION_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:34:34.085Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Availability not found for selected time.
```JSON
{
  "err": {
    "errorCode": "PRG_BOOK_RCI_002",
    "message": "AVAILABILITY_NOT_FOUND_FOR_THE_SELECTED_TIME"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:16.091Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_002",
    "message":  "INVALID_REQUEST_VERSION"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```
#### 2.7.5.4 PUT Operation
#### Path -  `/appointment`
#### Summary
This service enables by Pre-Registration to cancel an appointment booking, request to cancel an booked appointment with a selected registration center and time slot. After successful canceling an booking update the status code Canceled in appointment table.

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.preRegistrationId|Yes|pre Registration Id|37802950913289
request.registration_center_id |Yes|Registration center Id of the application|1
request.appointment_date |Yes|Date of the appointment|2019-01-19
request.time_slot_from |Yes|Time Slot From|12:15:00
request..time_slot_from |Yes|Time Slot To|12:28:00


#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request:
```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "version": "1.0",
  "requesttime": "2019-01-06T15:56:35.398Z",
  "request": {
    "pre_registration_id": "20910892067562",
     "registration_center_id": "1",
        "appointment_date": "2019-02-13",
        "time_slot_from": "15:31:00",
        "time_slot_to": "15:44:00"
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment canceled successfully

```JSON
{
  "err": null,
  "status": true,
  "responsetime": "2019-02-11T13:16:59.352Z",
  "response": {
    "transactionId": "4ffecd8e-2dff-11e9-841f-99921eec72ea",
    "message": "APPOINTMENT_SUCCESSFULLY_CANCELED"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid Pre Registration Id for registration center.
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_APP_005",
    "message": "INVALID_PRE_REGISTRATION_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:37:28.680Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Version
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "err": {
    "errorCode":"PRG_CORE_REQ_004",
    "message":"INVALID_REQUEST_BODY"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:35:49.602Z",
  "response": null
}
```
#### 2.7.5.5 POST Operation
#### Path -  `/appointment/preIdsByRegId`
#### Summary
Retrieve Pre-Registration appointment details by pre-Registration id and registration center id for the use of Data sync service.

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.booking.book
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.registration_center_id|Yes|Registration Center Id|1
request.preRegistrationId|Yes|pre Registration Id|37802950913289,..

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request:

```JSON
{
  "id": "mosip.pre-registration.booking.book",
  "version": "1.0",
  "requesttime": "2019-01-06T15:56:35.398Z",
  "request": {
    "registartion_center_id": "12",
    "pre_registration_ids": [
      "97285429827016"
    ]
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Retrieved all pre-registration ids successfully.

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T13:41:01.029Z",
  "response": [
    {
      "registartion_center_id": "1",
      "pre_registration_ids": [
        "20910892067562"
      ]
    }
  ]
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Unable to fetch.
```JSON
{
  "err": {
    "errorCode": "PRG_BOOK_RCI_013",
    "message": "BOOKING_DATA_NOT_FOUND"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:41:43.543Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Id
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_001",
    "message": "INVALID_REQUEST_ID"
  },
  "id": "string",
  "responsetime": "2019-02-11T12:53:14.075Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty request version
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_002",
    "message": "INVALID_REQUEST_VERSION"
  },
  "id": "string",
  "responsetime": "2019-02-11T12:53:14.075Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Date & Time
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_003",
    "message": "INVALID_REQUEST_DATETIME"
  },
  "id": "string",
  "responsetime": "2019-02-11T12:53:14.075Z",
  "response": null
}
```

##### Failure Response:
###### Status code: '200'
###### Description: Invalid or empty Request Body
```JSON
{
  "err": {
    "errorCode": "PRG_CORE_REQ_004",
    "message": "INVALID_REQUEST_BODY"
  },
  "id": "string",
  "responsetime": "2019-02-11T12:53:14.075Z",
  "response": null
}
```
#### 2.7.5.6 PUT Operation
#### Path -  `/appointment/availability/sync`
#### Summary
Synchronize booking slots availability table with master data.

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Appointment details successfully retrieved

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-01-06T15:56:35.398Z",
  "response": {
    "message":"Master Data Sync is successful"
   }
}
```

# 2.7.6 BatchJob Service APIs
This service is used by Pre-Registration portal to update an exipred pre registration id  and consumed pre registration id.

### Host
##### Integration - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

***
#### [Swagger API spec 0.8.0 version link](https://github.com/mosip/mosip/tree/0.8.0/docs/design/pre-registration/service/BatchJob-Service-API-Spec.yaml)
***

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | False |
| POST | False |
| PUT | True |
| DELETE | False |

#### 2.7.6.1 PUT Operation
#### Path -  `/expiredStatus`
#### Summary
Update status of pre-Registration id to expired in database if booking date is less then current date.

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Status updated successfully

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-01-17T13:28:44.595Z",
  "response": "Status to expired updated successfully"
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No pre registration id found to update
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_BAT_001",
    "message": "PRG_PAM_BAT_001 --> NO_PRE_REGISTRATION_ID_FOUND_TO_UPDATE_EXPIRED_STATUS"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:09:08.063Z",
  "response": null
}
```
#### 2.7.6.2 PUT Operation
#### Path -  `/consumedStatus`
#### Summary
Update status of pre-Registration id to consumed in database based on details given by registration client.

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Status updated successfully

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-01-17T13:28:44.595Z",
  "response": "Status to consumed updated successfully"
}
```
##### Failure Response:
###### Status code: '200'
###### Description: No pre registration id found to update
```JSON
{
  "err": {
    "errorCode": "PRG_PAM_BAT_001",
    "message": "PRG_PAM_BAT_001 --> NO_PRE_REGISTRATION_ID_FOUND_TO_UPDATE_CONSUMED_STATUS"
  },
  "id": "string",
  "responsetime": "2019-02-11T07:09:08.063Z",
  "response": null
}
```
# 2.7.7 Notification Service APIs
This service details used by Pre-Registration portal to trigger notification and get QRCode.

### Host
##### Integration - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -

***
#### [Swagger API spec 0.8.0 version link](https://github.com/mosip/mosip/tree/0.8.0/docs/design/pre-registration/service/Notification-Service-API-Spec.yaml)
***

#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| POST | True |

#### 2.7.7.1 POST Operation
#### Path -  `/notification`
#### Summary
Notify the user via Email and SMS.

#### Request Part Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
name |Yes|user name of the application|Sanober Noor
preId|Yes|Pre Registration of the application|37802950913289
appointmentDate| Booking appointment date|2019-01-18
appointmentTime| Booking appointment time| 12:02
mobNum| user Mobile number on which he will get sms nitification|9480456789
emailID| user email Id |sanober@gmail.com
multipart file| pdf file of acknowledgment page|37802950913289.pdf
LangCode| language code whatever user choose while login|eng

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request:
```JSON
{
			"name": "sanober noor",
			"preId": "37802950913289",
			"appointmentDate": "2019-01-22",
			"appointmentTime": "22:57",
			"mobNum": "9748107386",
			"emailID": "sanober.noor2@mindtree.com"
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Email and sms request  successfully submitted retrieved

```JSON
{
  "err": null,
  "id": "string",
  "responsetime": "2019-02-11T12:51:00.787Z",
  "response": {
    "name": "sanober noor",
    "preId": "1234567890",
    "appointmentDate": "2019-01-22",
    "appointmentTime": "22:57",
    "mobNum": "9748107386",
    "emailID": "sanober.noor2@mindtree.com"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Mobile nubmer or Email Id not given
```JSON
{
  "err": {
    "errorCode": "PRG_ACK_001",
    "message": "MOBILE_NUMBER_OR_EMAIL_ADDRESS_NOT_FILLED"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:00:10.584Z",
  "response": null
}
```
##### Failure Response:
###### Status code: '200'
###### Description: INCORRECT MANDATORY FIELDS
```JSON
{
  "err": {
    "errorCode": "PRG_ACK_002",
    "message": "PRG_ACK_002 --> INCORRECT_MANDATORY_FIELDS"
  },
  "id": "string",
  "responsetime": "2019-02-11T13:07:33.215Z",
  "response": null
}
```
#### 2.7.7.2 POST Operation
#### Path -  `/generateQRCode`
#### Summary
To generate QR Code of acknowledgement

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request:
```JSON
{
	"name": "sanober noor",
	"preId": "37802950913289",
	"appointmentDate": "2019-01-22",
	"appointmentTime": "22:57",
	"mobNum": "9748107386",
	"emailID": "sanober.noor2@mindtree.com"
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: QR CODE generated  successfully 

```JSON
{
	"err": null,
	"id": "string",
	"responsetime": "2019-02-11T13:19:54.099Z",
	"response": {
	"qrcode":{ByteCode}
	}
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Failed to generate QR code
```JSON
{
    "errorCode": "PRG_ACK_006",
    "message": "QRCODE_FAILED_TO_GENERATE"
}
```

# 2.7.8 Transliteration Service APIs
This service is used by Pre-Registration portal to transliterate given value from one language to another language. In this API transliteration is using IDB ICU4J library , so accuracy will be less.

### Host
##### Integration - `http://qa.mosip.io`
##### Development - `http://dev.mosip.io`
##### Production -
#### HTTP Operation Allowed
| Method | Allowed |
| ------------ | ------------ |
| GET | False |
| POST | True |
| PUT | False |
| DELETE | False |

#### 2.7.8.1 POST Operation
#### Path -  `/transliterate`
#### Summary
Transliterate from_Field_value to to_field_value based on given valid from_lang_code to to_lang_code.

#### Parameters
Name | Required | Description | Example
-----|----------|-------------|--------
id |Yes|Id of the application|mosip.pre-registration.transliteration.transliterate
version |Yes|version of the application|1.0
requesttime |Yes|Request time of the application|2019-01-16T05:23:08.019Z
request |Yes|Request for the application|
request.from_field_lang|Yes|From language code|eng
request.from_field_name |Yes|From filed name|Name1
request.from_field_value |Yes|From field value |Kishan
request.to_field_lang |Yes|To language code|ara
request.to_field_name |Yes|From filed name|Name2
#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes
#### Request:

```JSON
{
  "id": "mosip.pre-registration.transliteration.transliterate",
  "requesttime": "2018-10-17T07:22:57.086Z",
  "version": "1.0",
  "request": 
  {
    "from_field_lang": "eng",
    "from_field_name": "Name1",
    "from_field_value": "Kishan",
    "to_field_lang": "ara",
    "to_field_name": "Name2",
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
  "err": null,
  "id": "string",
  "responsetime": "2019-03-12T06:48:26.671Z",
  "response": {
    "from_field_name": "Name1",
    "from_field_value": "Kishan",
    "from_field_lang": "eng",
    "to_field_name": "Name2",
    "to_field_value": "كِسهَن",
    "to_field_lang": "ara"
  }
}
```
##### Failure Response:
###### Status code: '200'
###### Description: Invalid field
```JSON
{
  "err": {
    "message": "INCORRECT_MANDATORY_FIELDS",
    "errorcode": "PRG_TRL_APP_002"
  },
  "id": "string",
  "responsetime": "2019-03-12T06:48:47.891Z",
  "response": null
}
```