This page details the Services and their respective APIs of xxx module.

* [Auth Service](#Auth-Service)
* [Demographic Service]

# Auth Service (Public)
This service details used by Pre-Registration portal to authenticate user by sending otp to the user , validating with userid and otp.

* [POST /sendotp](#post-sendotp)
* [POST /useridotp](#post-uderidotp)
* [POST /invalidatetoken](#post-invalidatetoken)

# POST /sendotp
This request will send the OTP to the requested user
## Resource URL
https://mosip.io/v1/prereg-login/sendotp

## Resource Details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

## Parameters
Name | Required | Description | Comment
-----|----------|-------------|--------
id |Yes|id |mosip.pre-registration.auth.sendotp
version |Yes|version of the application|1.0
requesttime |Yes|Time of the request|2019-01-16T05:23:08.019Z
userid |Yes|user id of the applicant|8907654778
langcode|Yes|The preferred language code |eng

#### Request:
```JSON
{
	"id": "mosip.pre-registration.auth.sendotp",
	"version": "1.0",
	"requesttime": "2019-03-15T07:24:47.605Z",
	"request": {
		"langCode": "eng",
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
	"id": "mosip.pre-registration.auth.sendotp",
	"version": "1.0",
	"responsetime": "2019-03-15T07:24:50.246Z",
	"response": {
		"message": "Sms Request Sent"
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
	"responsetime": "2019-03-15T08:09:42.327Z",
	"response": null,
	"errors": [
		{
		 "errorCode": "PRG_AUTH_001",
		 "message": "SEND_OTP_FAILED"
		}
	]	
}
```

