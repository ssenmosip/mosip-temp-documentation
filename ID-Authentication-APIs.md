
This section details about the REST services in ID Authentication module.
* [Authentication Service](#authentication-service-public) - This service can be used by Partners to authenticate an Individual using OTP, Demographic or Biometric-based authentication.
* [eKYC Service](#ekyc-service-public) - This service can be used by Partners to retrieve KYC details of an Individual, after authenticating them using OTP or Biometric-based authentication.
* [OTP Request Service](#otp-request-service-public) - This service can be used by Partners to send OTP on behalf of Individual, which can then be used for OTP-based authentication.
* [Internal Authentication Service](#authentication-service-internal) - This service can be used by MOSIP modules to authenticate Individual using Biometric-based authentication.

## Authentication Service (Public)
This service details authentication (yes/no auth) that can be used by Partners to authenticate an Individual. Below are various authentication types supported by this service - 
1. OTP based - OTP (Time based OTP)
2. Demographic based - Name, DOB, Age, Gender, Address, FullAddress
3. Biometric based - Fingerprint, IRIS and Face

#### Users of Authentication service -
1. `MISP (MOSIP Infrastructure Service Provider)` - MISP's role is limited to infrastructure provisioning and acting as a gate keeper for all authentication requests sent to this service. The MISP is also responsible for the policy creation on the MOSIP servers so their partners will follow the set policy.
2. `Partners` - Auth-Partners register themselves with MOSIP, under a MISP. Authentication requests are captured by Auth-Partners and sent to MOSIP, via MISP.

* [POST /idauthentication/v1/identity/auth/](#post-idauthenticationv1identityauth) 

### POST /idauthentication/v1/identity/auth/
This request will authenticate an Individual, based on provided authentication type(s).

#### Resource URL
<div>https://mosip.io/idauthentication/v1/identity/auth/:Auth-Partner-ID/:MISP-LicenseKey</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.identity.auth
version | Y | API version | | v1
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
requestedAuth| Y | Authentication Types requested| | 
requestedAuth: otp| Y | OTP Authentication Type | false| false
requestedAuth: demo| Y | Demographic Authentication Type | false| false
requestedAuth: bio| Y | Biometric Authentication Type | false|false
individualId| Y | VID of Individual | | 9830872690593682 
individualIdType| Y | Allowed Type of Individual ID - VID, UIN | VID |
consentObtained| Y | If consent of Individual is obtained | true
keyIndex| Y | Thumbprint of public key certificate used for encryption of sessionKey | 
requestSessionKey| Y | Session Key encrypted using MOSIP Public Key | | 
requestHMAC| Y | sha256 of request block before encryption and hash is encrypted using requestSessionKey | |
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: otp| N | OTP | | 
request: timestamp| N | Timestamp when request block was captured| | 
request: demographics|N| Demographic data of an Individual| |
request: biometrics|N| Biometric data of an Individual| |

Mandatory fields for different types of authentications- 
1. **OTP Auth** - request: **otp** attribute is mandatory 
2. **Demographic Auth** - request: **demographics**  attribute is mandatory
2. **Biometric Auth** - request: **biometrics** attribute is mandatory

#### Request Body
```JSON
{
  "id": "mosip.identity.auth",
  "version": "v1",
  "requestTime": "2019-02-15T10:01:57.086+05:30",
  "transactionID": "1234567890",
  "requestedAuth": {
    "otp": true,
    "demo": false,
    "bio": false
  },
  "consentObtained": true,
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "keyIndex": "<thumbprint of the public key certficate used for enryption of sessionKey. This is necessary for key rotaion>",
  "requestSessionKey": "<encrypted with MOSIP public key and encoded session key>",
  "requestHMAC": "<sha256 of the request block before encryption and the hash is encrypted using the requestSessionKey>",
  "request": {
    "timestamp": "2019-02-15T10:01:56.086+05:30 - ISO format timestamp",
    "otp": "123456",
    "demographics": {
      "name": [
        {
          "language": "ara",
          "value": "ابراهيم بن علي"
        },
        {
          "language": "fra",
          "value": "Ibrahim Ibn Ali"
        }
      ],
      "gender": [
        {
          "language": "ara",
          "value": "الذكر"
        },
        {
          "language": "fra",
          "value": "mâle"
        }
      ],
      "age": "25",
      "dob": "25/11/1990",
      "fullAddress": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 1, عنوان العينة سطر 2"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 1, exemple d'adresse ligne 2"
        }
      ]
    },
    "biometrics": [
      {
        "data": {
          "mosipProcess": "",
          "environment": "",
          "version": "",
          "deviceCode": "",
          "deviceProviderID": "",
          "deviceServiceID": "",
          "deviceServiceVersion": "",
          "bioType": "FMR",
          "bioSubType": "UNKNOWN",
          "bioValue": "<encrypted with session key and base64 encoded biometric data>",
          "transactionID": "1234567890",
          "timestamp": "2019-02-15T10:01:57.086+05:30",
          "requestedScore": "<floating point number to represent the minimum required score for the capture>",
          "qualityScore": "<floating point number representing the score for the current capture>"
        },
        "hash": "sha256(sha256 hash of the previous data block + sha256 of the current data block before encryption)",
        "sessionKey": "<encrypted with MOSIP public key and encoded session key biometric>",
        "signature": "base64 signature of the data and metaData block"
      },
      {
        "data": {
          "mosipProcess": "",
          "environment": "",
          "version": "",
          "deviceCode": "",
          "deviceProviderID": "",
          "deviceServiceID": "",
          "deviceServiceVersion": "",
          "bioType": "IIR",
          "bioSubType": "RIGHT",
          "bioValue": "<encrypted with session key and base64 encoded biometric data>",
          "transactionID": "1234567890",
          "timestamp": "2019-02-15T10:01:57.086+05:30"
        },
        "hash": "sha256(sha256 hash of the previous data block + sha256 of the current data block before encryption)",
        "sessionKey": "<encrypted with MOSIP public key and encoded session key biometric>",
        "signature": "base64 signature of the data and metaData block"
      }
    ]
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)
###### Description : Successfully authenticated an Individual    

```JSON
{
  //API Metadata
  "id": "mosip.identity.auth",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "txn12345",
  //Auth Response
  "response": {
    "authStatus": true,
    "staticToken": "<static_token>"
  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    
###### Description : Authentication of an Individual failed

```JSON
{
  //API Metadata
  "id": "mosip.identity.auth",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "txn12345",
  //Auth Response
  "response": {
    "authStatus": false,
    "staticToken": null
  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN",
      "actionMessage": "Please retry with the correct UIN"
    }
  ]
}
```

## eKYC Service (Public)
This service details authentication (eKYC auth) that can be used by Partners to authenticate an Individual and send Individual's KYC details as response. Below are various authentication types supported by eKYC Authentication - 
1. OTP Authentication - OTP
2. Biometric Authentication - Fingerprint, IRIS and Face

* [POST /idauthentication/v1/identity/kyc/](#post-idauthenticationv1identitykyc) 

### POST /idauthentication/v1/identity/kyc/
This request will provide KYC details of Individual, once an Individual is successfully authenticated.

#### Resource URL
<div>https://mosip.io/idauthentication/v1/identity/kyc/:eKYC-Partner-ID/:MISP-LicenseKey</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
version | Y | API version |  | v1
partnerId | Y | eKYC Partner ID | |
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
requestedAuth| Y | Authentication Types requested| | 
requestedAuth: otp| Y | OTP Authentication Type | false| false
requestedAuth: demo| N | Demographic Authentication Type | false| false
requestedAuth: bio| Y | Biometric Authentication Type | false|false
individualId| Y | VID of Individual | | 9830872690593682 
individualIdType| Y | Allowed Type of Individual ID - VID, UIN | VID |
consentObtained| Y | If consent of Individual is obtained | true
secondaryLangCode| Y | Secondary Language Code | |
keyIndex| Y | Thumbprint of public key certificate used for encryption of sessionKey | 
requestSessionKey| Y | Session Key encrypted using MOSIP Public Key | | 
requestHMAC| Y | sha256 of request block before encryption and hash is encrypted using requestSessionKey | |
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: otp| N | OTP | | 
request: timestamp| N | Timestamp when request block was captured| | 
request: biometrics|N| Biometrics of an Individual| |
request: transactionID|N| Transaction ID provided by Device Service| |


#### Request Body
```JSON
{
  "id": "mosip.identity.kyc",
  "version": "v1",
  "requestTime": "2019-02-15T10:01:57.086+05:30",
  "transactionID": "1234567890",
  "requestedAuth": {
    "otp": true,
    "demo": false,
    "bio": true
  },
  "consentObtained": true,
  "secondaryLangCode": "<sec-lang-code>",
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "keyIndex": "<thumbprint of the public key certficate used for enryption of sessionKey. This is necessary for key rotaion>",
  "requestSessionKey": "<encrypted with MOSIP public key and encoded session key>",
  "requestHMAC": "<sha256 of the request block before encryption and the hash is encrypted using the requestSessionKey>",
  "request": {
    "timestamp": "2019-02-15T10:01:56.086+05:30 - ISO format timestamp",
    "otp": "123456",
    "biometrics": [
      {
        "data": {
          "mosipProcess": "",
          "environment": "",
          "version": "",
          "deviceCode": "",
          "deviceProviderID": "",
          "deviceServiceID": "",
          "deviceServiceVersion": "",
          "bioType": "FMR",
          "bioSubType": "UNKNOWN",
          "bioValue": "<encrypted with session key and base64 encoded biometric data>",
          "transactionID": "1234567890",
          "timestamp": "2019-02-15T10:01:57.086+05:30",
          "requestedScore": "<floating point number to represent the minimum required score for the capture>",
          "qualityScore": "<floating point number representing the score for the current capture>"
        },
        "hash": "sha256(sha256 hash of the previous data block + sha256 of the current data block before encryption)",
        "sessionKey": "<encrypted with MOSIP public key and encoded session key biometric>",
        "signature": "base64 signature of the data and metaData block"
      }
    ]
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)
###### Description : Successful KYC Authentication of an Individual    

```JSON
{
  //API Metadata
  "id": "mosip.identity.kyc",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "txn12345",
  //Auth Response
  "response": {
    "kycStatus": true,
    "staticToken": "<static_token>",
    "identity": {// encoded encrypted KYC info using Partner's public key
      "name": [
        {
          "language": "ara",
          "value": "ابراهيم"
        },
        {
          "language": "fra",
          "value": "Ibrahim"
        }
      ],
      "dob": "25/11/1990",
      "gender": [
        {
          "language": "ara",
          "value": "الذكر"
        }
      ],
      "phoneNumber": "+212-5398-12345",
      "emailId": "sample@samplamail.com",
      "addressLine1": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 1"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "addressLine2": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 2"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "addressLine3": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 3"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 3"
        }
      ]
    }
  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)
###### Description : KYC Authentication of an Individual failed    

```JSON
{
  //API Metadata
  "id": "mosip.identity.kyc",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "txn12345",
  //Auth Response
  "response": {// encoded encrypted KYC info using Partner's public key
    "kycStatus": false,
    "identity": null
  },
  "errors": [
      {
        "errorCode": "IDA-MLC-002",
        "errorMessage": "Invalid UIN",
        "actionMessage": "Please retry with the correct UIN"
      }
    ]
}
```

## OTP Request Service (Public)
This service enables Partners to request for an OTP for an Individual. The OTP will be send via message or email as requested to the Individual. This OTP can then be used to authenticate an Individual using Authentication or eKYC service.

* [POST /idauthentication/v1/identity/kyc/](#post-idauthenticationv1otp) 

### POST /idauthentication/v1/otp/
This request will send an OTP to the Individual.

#### Resource URL 
<div>https://mosip.io/idauthentication/v1/otp/:Partner-ID/:MISP-LicenseKey</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | mosip.identity.otp | 
version | Y | API version |  | v1 
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
individualId| Y | VID | | 9830872690593682
individualIdType| Y | Allowed Type of Individual ID - VID, UIN | VID
otpChannel| Y | Allowed OTP Channels - EMAIL, PHONE| | true


#### Request Body
```JSON
{
  "id": "mosip.identity.otp",
  "version": "v1",
  "requestTime": "2019-02-15T07:22:57.086+05:30",
  "transactionID": "txn12345",
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "otpChannel": [
    "EMAIL",
    "PHONE"
  ]
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)
###### Description : OTP for Authentication or KYC Service was successfully sent to the Individual        

```JSON
{
  //API Metadata
  "id": "mosip.identity.otp",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "txn12345",
  //OTP Response
  "response": {
    "maskedMobile": "XXXXXXX123",
    "maskedEmail": "abXXXXXXXXXcd@xyz.com"
  },
  "errors": null
}
```

##### Failed Response:   
###### Status Code : 200 (OK)
###### Description : Failed to send OTP to the Individual   

```JSON
{
  //API Metadata
  "id": "mosip.identity.otp",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "txn12345",
  //OTP Response
  "response": null,
  "errors": [
    {
      "errorCode": "IDA-MLC-003",
      "errorMessage": "Invalid VID",
      "actionMessage": "Please retry with correct VID"
    }
  ]
}
```

## Authentication Service (Internal)
This service details authentication (yes/no auth) that can be used by MOSIP modules to authenticate an Individual using UserID/VID/UIN. Below are various authentication types supported by this service - Biometric based - Fingerprint, IRIS and Face

* [POST /idauthentication/v1/identity/auth/internal](#post-idauthenticationv1identityauthinternal) 

### POST /idauthentication/v1/identity/auth/internal
This request will authenticate an Operator/Supervisor using Biometric authentication.

#### Users of Internal Authentication service -
1. `Registration Client` - Registration Client can authenticate biometrics of Operator or Supervisor while onboarding them.
2. `Registration Processor` - Registration Processor can authenticate biometrics of Operator or Supervisor while processing registration packets.

#### Resource URL
<div>https://mosip.io/idauthentication/v1/identity/auth/internal</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.identity.auth.internal
version | Y | API version | | v1
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
requestedAuth| Y | Authentication Types requested| | 
requestedAuth: otp| Y | OTP Authentication Type | false| false
requestedAuth: demo| Y | Demographic Authentication Type | false| false
requestedAuth: bio| Y | Biometric Authentication Type | false|false
individualId| Y | UserID of Operator/Supervisor | | 9830872690593682 
individualIdType| Y | Allowed Type of Individual ID - USERID, VID, UIN | USERID |
consentObtained| Y | If consent of Individual is obtained | true
keyIndex| Y | Thumbprint of public key certificate used for encryption of sessionKey | 
requestSessionKey| Y | Session Key encrypted using MOSIP Public Key | | 
requestHMAC| Y | sha256 of request block before encryption and hash is encrypted using requestSessionKey | |
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: timestamp| N | Timestamp when request block was captured| | 
request: biometrics|N| Biometric data of an Individual| |


#### Request Body
```JSON
{
  "id": "mosip.identity.auth.internal",
  "version": "v1",
  "requestTime": "2019-02-15T10:01:57.086+05:30",
  "transactionID": "1234567890",
  "requestedAuth": {
    "bio": true,
    "demo": false
  },
  "consentObtained": true,
  "individualId": "9830872690593682",
  "individualIdType": "USERID",
  "keyIndex": "<thumbprint of the public key certificate used for encryption of sessionKey. This is necessary for key rotaion>",
  "requestSessionKey": "<encrypted with MOSIP public key and encoded session key>",
  "requestHMAC": "<sha256 of the request block before encryption and the hash is encrypted using the requestSessionKey>",
  "request": {
    "timestamp": "2019-02-15T10:01:56.086+05:30 - ISO format timestamp",
    "biometrics": [
      {
        "data": {
          "bioType": "FMR",
          "bioSubType": "UNKNOWN",
          "bioValue": "<base64 encoded biometric data>"
        }
      },
      {
        "data": {
          "bioType": "IIR",
          "bioSubType": "RIGHT",
          "bioValue": "<base64 encoded biometric data>"
        }
      }
    ]
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)
###### Description : Successfully authenticated an Individual    

```JSON
{
  //API Metadata
  "id": "mosip.identity.auth.internal",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "1234567890",
  //Auth Response
  "response": {
    "authStatus": true
  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    
###### Description : Authentication of an Individual failed

```JSON
{
  //API Metadata
  "id": "mosip.identity.auth.internal",
  "version": "v1",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Response Metadata
  "transactionID": "1234567890",
  //Auth Response
  "response": {
    "authStatus": false
  },
  "errors": [
    {
      "errorCode": "IDA-MLC-009",
      "errorMessage": "Invalid UserId",
      "actionMessage": "Please retry with the correct UserId"
    }
  ]
}
```
