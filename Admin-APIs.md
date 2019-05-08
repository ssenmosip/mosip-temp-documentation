* [Login](#login)

# Login

* [GET /authfactors](#get-authfactors)
* [POST /useridPwd](#post-useridPwd)


### GET /authfactors

This service will give back the authentication factors for the login of the user. It will accept the username and find the user's groups. Based on the groups, the auth factors are decided and send back. 

#### Resource URL
<div>https://mosip.io/v1/admin/authfactors</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Part Parameters
Name | Required | Description |  Example
-----|----------|-------------|--------
userid |Yes|User id of the user| UDAE423
timeStamp |Yes|Date-time  in UTC ISO-8601| 2007-12-03T10:15:30Z

#### Request
<div>https://mosip.io/v1/keymanager/publickey/REGISTRATION?userid=UDAE423&timeStamp=2018-12-09T06%3A39%3A03.683Z </div>

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: List of auth factors are returned
```JSON

{
  "id": "mosip.io.authfactors",
  "version": "1.0",
  "metadata": {},
  "responsetime": "2007-12-03T10:15:30Z",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
			["PASSWORD", "OTP", "FINGERPRINT_TYPE-1"]
	    }
	
}
```

##### Error Response:
###### Status code: '200'
###### Description: If the user is not found. 
```JSON

{
  "id": "mosip.io.authfactors",
  "version": "1.0",
  "metadata": {},
  "responsetime": "2007-12-03T10:15:30Z",
  "errors": [
    {
      "errorCode": "ADMN-AUTH-001",
      "message": "The userid is not found in the system"
    }
  ]
}
```


### POST /useridPwd

This service will authenticate the username and password. This service will call the login service in the Auth API and will return the token back to the caller. 

#### Resource URL
<div>https://mosip.io/v1/admin/useridPwd</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | The response will be sent in the Response Header and also a JSON message will be returned. 
Requires Authentication | no

#### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
username|Yes|This is the username of the user. | -NA- | M392380
password|Yes|This is the channel in which the OTP will be sent. It should be one of the {"EMAIL", "MOBILENUMBER"}| -NA- | MOBILENUMBER
appid|Yes|This is the application ID of the caller of this service.| -NA- | ADMIN

#### Example Request
```JSON
{
	"id": "mosip.admin.authentication.useridPwd",
	"version":"1.0",	
	"requesttime":"2007-12-03T10:15:30Z",
	"request": {
		"username": "M392380",
		"password": "fdkj943lkj32k32ew$8Kf",
		"appid": "REGISTRATIONCLIENT"
	}
}
```
#### Example Response

Success Response 

```
Response Cookie:

Set-Cookie →Authorization=Mosip-TokeneyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbmRpdmlkdWFsIiwibW9iaWxlIjoiOTY2MzE3NTkyOCIsIm1haWwiOiJpbmRpdmlkdWFsQGdtYWlsLmNvbSIsInJvbGUiOiJwZXJzb24iLCJpYXQiOjE1NTEzNDU1NjUsImV4cCI6MTU1MTM1MTU2NX0.pCyibViXo31enOgRD60BnKjEpEA-78yzbWnZGChxCIZ5lTpYnhgm-0dtoT3neFebTJ8eAI7-o8jDWMCMqq6uSw; Max-Age=6000000; Expires=Wed, 08-May-2019 19:59:43 GMT; Path=/; Secure; HttpOnly


JSON:
{
	"id": "mosip.admin.authentication.useridPwd",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
                "status": "success",
		"message":"Username and password combination had been validated successfully"
	}
}

```


Error Responses

1. Invalid credentials: If the passed credentials is not correct. 
```JSON

{
	"id": "mosip.authentication.useridPwd",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"errors":[
			{
				"errorCode": "AUTH_ERR_INVALIDCREDENTIALS",
				"message": "The passed in credentials is not correct"
		  }	
		]
}

```

2. Invalid application ID: If the passed in application is not correct. 
```JSON

{
	"id": "mosip.authentication.useridPwd",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"errors":[
			{
				"errorCode": "AUTH_ERR_INVALIDAPPID",
				"message": "The passed in application ID is not correct"
		  }	
		]
}

```
