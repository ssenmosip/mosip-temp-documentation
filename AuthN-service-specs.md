# 1. Authentication - Username and password

This service will authenticate an user by username and password combination.

### Resource URL
### `POST /authenticate/unpwd`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
userName|Yes|User name of the user| -NA- | -NA-
password|Yes|Password of the user| -NA- | -NA-

### Example Request
```JSON
{
  "userName": "string",
  "password": "string"
}

```
### Example Response
```JSON
{
  "userName": "m1030380",
  "mobilenumber": "0987654321",
  "email": "asdfa@asdf.com",
  "roles": "DIVISION_ADMIN,SUPERVISOR,OPERATOR",
}

```




# 2. Authentication - Only OTP

This service will authenticate an user only by the OTP method. 

### Resource URL
### `POST /authenticate/otp`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
email|Yes|Email to which the OTP has to be sent| -NA- | -NA-
langCode|Yes|Language in which the OTP message will be sent. This is a ISO 639-2 format| -NA- | ara
mobilenumber|Yes|Phone number to which the OTP has to be sent| -NA- | -NA- 
otpChannel|Yes|Channel of the OTP. It should be either of email or mobilenumber| mobilenumber | email

### Example Request
```JSON
{
  "email": "string",
  "langCode": "string",
  "mobilenumber": "number",
  "otpChannel": "string"
}
```
### Example Response
```JSON
{
  "userName": "m1030380",
  "mobilenumber": "0987654321",
  "email": "asdfa@asdf.com",
  "roles": "DIVISION_ADMIN,SUPERVISOR,OPERATOR",
}
```




# 3. Verify OTP

The above service will send the OTP to the user. This service validates the OTP which is sent by the user. 

### Resource URL
### `POST /authenticate/verify_otp`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
otp|Yes|OTP which is sent to the user for authentication| -NA- | 645728
key|Yes|The id of the channel to which the OTP has been sent| -NA- | 9288987374 or soandso@mail.com

### Example Request
```JSON
{
  "otp": "string",
  "key": "string"
}
```
### Example Response
```JSON
{
  "userName": "m1030380",
  "mobilenumber": "0987654321",
  "email": "asdfa@asdf.com",
  "roles": "DIVISION_ADMIN,SUPERVISOR,OPERATOR",
}
```




# 4. Authentication - Username, password and OTP

This service will authenticate an user by username and password combination along with OTP. Once the username and password is supplied, the authenticity of the credentials are checked first. And then the OTP will be sent to the registered mobile number and email ID. AuthToken will not be generated at this point. Once the OTP is verified, the AuthToken is generated and returned. 

### Resource URL
### `POST /authenticate/unpwdotp`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
userName|Yes|Username of the user| -NA- | -NA-
password|Yes|Password of the user| -NA- | -NA-
email|Yes|Email to which the OTP has to be sent| -NA- | -NA-
langCode|Yes|Language in which the OTP message will be sent. This is a ISO 639-2 format| | 
mobilenumber|Yes|Phone number to which the OTP has to be sent| -NA- | -NA- 
otpChannel|Yes|Channel of the OTP. It should be either of email or mobilenumber| mobilenumber | email

### Example Request
```JSON
{
  "userName": "m1030380",
  "mobilenumber": "0987654321",
  "email": "asdfa@asdf.com",
  "roles": "DIVISION_ADMIN,SUPERVISOR,OPERATOR",
}
```
### Example Response
```JSON
{
	"message":"OTP has been sent successfully"
}
```



# 5. Validate Token service

This service will validate the token. 

### Resource URL
### `GET /validate_token`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
AuthToken|Yes|AuthToken passed in the request header| -NA- | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiJiMDhmODZhZi0zNWRhLTQ4ZjItOGZhYi1jZWYzOTA0NjYwYmQifQ.-xN_h82PHVTCMA9vdoHrcZxH-x5mb11y1537t3rGzcM
 

### Example Request
```Request Header
AuthToken
```
### Example Response
```JSON
{
  "userName": "m1030380",
  "mobilenumber": "0987654321",
  "email": "asdfa@asdf.com",
  "roles": "DIVISION_ADMIN,SUPERVISOR,OPERATOR",
}
```




# 6. Logout

This service will logout the user. 

### Resource URL
### `GET /logout`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
AuthToken|Yes|AuthToken passed in the request header| | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiJiMDhmODZhZi0zNWRhLTQ4ZjItOGZhYi1jZWYzOTA0NjYwYmQifQ.-xN_h82PHVTCMA9vdoHrcZxH-x5mb11y1537t3rGzcM
 

### Example Request
```Request Header
AuthToken
```
### Example Response
```JSON
{
	"message":"User had been logged out successfully"
}
```
