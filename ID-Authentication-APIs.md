This wiki page details the REST services exposed by ID Authentication.

## 1. Auth Request
This service details Auth Request to be used by TSPs to authenticate an Individual. Below are various authentication types supported by this service - 
1. OTP based - TOTP
2. Pin based - Static Pin
3. Demo based - PersonalIdentity, Address, FullAddress
4. Bio based - Fingerprint, IRIS and Face

### Resource URL
### `POST identity/auth/v1.0/<MISP-LK>`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.identity.auth
ver | Y | API version | | 1.0
reqTime| Y |Time when Request was captured| | 2018-10-17T07:22:57.086+05:30
txnID | Y | Transaction ID of API | | 1234567890
idvId | Y | Individual's UIN or VID | | 486493840596
idvIdType | Y | Individual's ID Type | D | V
tspID|Y|TSP ID| |TSP0000005
authType| Y | Individual Authentication Types supported| | 
authType: personalIdentity| Y | Demographic Authentication - Personal Identity | false| false
authType: address| Y | Demographic Authentication - Address Line | false| false
authType: bio| Y | Bio-metric Authentication Type | false|false
authType: otp| Y | OTP Authentication Type | false|false
authType: pin| Y | Pin Authentication Type |false |false
key: sessionKey| Y | TSP Session Key, encrypted using TSP Public Key | | 
key: publicKeyCert| Y | TSP Public Key Certificate used to Digitally Sign the request | | 
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: identity: name|N| name attribute of Individual's Identity| | 
request: identity: addressLine1|N| addressLine1 attribute of Individual's Identity| |  
request: identity: fullAddress|N| fullAddress attribute of Individual's Identity| | 
request: identity: leftIndex|N| Left Index of Individual's Fingerprint| |
request: identity: leftEye|N| Left Eye of Individual's IRIS| |

### Sample Request Header
##### MOSIP-AuthX = `<Partner Digital Signature re-issued by MOSIP>`

### Sample Request Body
```JSON
{
  //API Metadata
  "id": "mosip.identity.auth",
  "version": "1.0",
  //Request Metadata 
  "partnerID": "AP000001",
  "policy": "<auth-policy-id>",
  "transactionID": "1234567890",
  "requestTime": "2019-02-15T10:01:57.086+05:30",
  "requestedAuth": {
    "otp": true,
    "demo": false,
    "bio": false,
    "pin": false
  },
  "bioMetadata": [
    {
      "bioType": "FMR",
      "deviceId": "",
      "deviceProviderID": ""
    },
    {
      "bioType": "IIR",
      "deviceId": "",
      "deviceProviderID": ""
    }
  ],
  "sessionKey": "<encrypted and encoded session key>",
  //Identity Request
  "request": {//This element should be encrypted and encoded using session key
    "identity": {
      "UIN": "4074317832",
      "VID": "9830872690593682",
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
      "fullAddress": [
        {
          "language": "ar",
          "value": "عنوان العينة سطر 2, عنوان العينة سطر 1"
        },
        {
          "language": "fr",
          "value": "exemple d'adresse ligne 1, exemple d'adresse ligne 2"
        }
      ],
      "biometrics": [
        {
          "type": "FINGER",
          "subType": "UNKNOWN",
          "value": "<base64 encoded value>"
        },
        {
          "type": "FINGER",
          "subType": "RIGTHT_POINTER",
          "value": "<base64 encoded value>"
        },
        {
          "type": "IRIS",
          "subType": "RIGHT",
          "value": "<base64 encoded value>"
        }
      ]
    },
    "additionalFactors": {
      "totp": "123456",
      "staticPin": "987654"
    }
  }
}
```

### Sample Response Header     
##### MOSIP-AuthX = `<MOSIP Digital Signature>`

### Sample Response Body
#### Success Scenario :
Status Code : 200 (OK)

```JSON
{
  //API Metadata
  "id": "mosip.identity.auth",
  "version": "1.0",
  //Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Auth Response
  "status": "Y",
  "staticToken": "<static_token>",
  "errors": []
}
```

#### Failed Response:
Status Code : 200 (OK)

```JSON
{
  //API Metadata
  "id": "mosip.identity.auth",
  "version": "1.0",
  //Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  //Auth Response
  "status": "Y",
  "staticToken": "<static_token>",
  "errors": [
    {
      "code": "IDA-MLC-002",
      "message": "Invalid UIN"
    }
  ]
}
```

## 2. KYC Auth Request
This service details KYC Auth Request to be used by TSPs to authenticate an Individual, and retrieve Individual's KYC details as response. Below are various authentication types supported by KYC Auth - 
1. OTP based - TOTP
2. Pin based - Static Pin
3. Bio based - Fingerprint, IRIS and Face

### Resource URL
### `POST identity/kyc/v1.0/<MISP-LK>`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.identity.kyc
ver | Y | API Version | | version of API
consentReq|Y|Individual's consent|false|true
ekycAuthType|Y|Auth type for requested KYC Auth| | O
authRequest: id | Y | API Id | | mosip.identity.auth
authRequest: ver | Y | API version | | 1.0
authRequest: reqTime| Y |Time when Request was captured| | 2018-10-17T07:22:57.086+05:30
authRequest: txnID | Y | Transaction ID of API | | 1234567890
authRequest: idvId | Y | Individual's UIN or VID | | 486493840596
authRequest: idvIdType | Y | Individual's ID Type | D | V
authRequest: spID|Y|TSP ID| |TSP0000005
authRequest: authType| Y | Individual Authentication Types supported| | 
authRequest: authType: personalIdentity| Y | Demographic Authentication - Personal Identity | false| false
authRequest: authType: address| Y | Demographic Authentication - Address Line | false| false
authRequest: authType: bio| Y | Bio-metric Authentication Type | false|false
authRequest: authType: otp| Y | OTP Authentication Type | false|false
authRequest: authType: pin| Y | Pin Authentication Type |false |false
authRequest: key: sessionKey| Y | TSP Session Key, encrypted using TSP Public Key | | 
authRequest: key: publicKeyCert| Y | TSP Public Key Certificate used to Digitally Sign the request | | 
authRequest: request| Y | Auth request attributes to be used for authenticating Individual | | 
authRequest: request: identity: name|N| name attribute of Individual's Identity| | 
authRequest: request: identity: addressLine1|N| addressLine1 attribute of Individual's Identity| |  
authRequest: request: identity: fullAddress|N| fullAddress attribute of Individual's Identity| | 
authRequest: request: identity: leftIndex|N| Left Index of Individual's Fingerprint| |
authRequest: request: identity: leftEye|N| Left Eye of Individual's IRIS| |

### Sample Request Header
##### MOSIP-AuthX = `<Partner Digital Signature re-issued by MOSIP>`

### Sample Request
```JSON
{
  // API Metadata
  "id": "mosip.identity.kyc",
  "version": "1.0",
  // Request Metadata
  "partnerID": "KP000001",
  "policyID": "<kyc-policy-id>",
  "transactionID": "1234567890",
  "requestTime": "2019-02-15T10:01:57.086+05:30",
  "requestedAuth": {
      "otp": true,
      "demo": false,
      "bio": true,
      "pin": true
  },
  "bioMetadata": [
    {
      "bioType": "FMR",
      "deviceId": "",
      "deviceProviderID": ""
    },
    {
      "bioType": "IIR",
      "deviceId": "",
      "deviceProviderID": ""
    }
  ],
  "kycMetadata" : {
	"consentRequired": true,
	"secondaryLangCode": "<sec-lang-code>"
  },
  "sessionKey": "<encrypted and encoded session key>",
  //Identity Request 
  "request": {// This element should be encrypted and encoded using session key
    "identity": {
      "UIN": "4074317832",
      "VID": "9830872690593682",
      "biometrics": [
        {
          "type": "FINGER",
          "subType": "UNKNOWN",
          "value": "<base64 encoded value>"
        },
        {
          "type": "FINGER",
          "subType": "RIGTHT_POINTER",
          "value": "<base64 encoded value>"
        },
        {
          "type": "IRIS",
          "subType": "RIGHT",
          "value": "<base64 encoded value>"
        }
      ]
    },
    "additionalFactors": {
      "totp": "123456",
      "staticPin": "987654"
    }
  }
}
```

### Sample Response Header     
##### MOSIP-AuthX = `<MOSIP Digital Signature>`

### Sample Response Body
#### Success Scenario :
Status Code : 200 (OK)

```JSON
{
  // API Metadata
  "id": "mosip.identity.kyc",
  "version": "1.0",
  // Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  // Auth Response
  "status": "Y",
  "staticToken": "<static_token>",
  "errors": [],
  "response": {// encoded encrypted KYC info using Partner's public key
    "ttl": "time_to_live_for_KYC_Info",
    "identity": {
      "name": [
        {
          "language": "ar",
          "value": "ابراهيم"
        },
        {
          "language": "fr",
          "value": "Ibrahim"
        }
      ],
      "dateOfBirth": [
        {
          "language": "ar",
          "value": "16/04/1955"
        }
      ],
      "age": [
        {
          "language": "ar",
          "value": "30"
        }
      ],
      "gender": [
        {
          "language": "ar",
          "value": "الذكر"
        }
      ],
      "phoneNumber": [
        {
          "language": "ar",
          "value": "+212-5398-12345"
        }
      ],
      "emailId": [
        {
          "language": "ar",
          "value": "sample@samplamail.com"
        }
      ],
      "addressLine1": [
        {
          "language": "ar",
          "value": "عنوان العينة سطر 1"
        },
        {
          "language": "fr",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "addressLine2": [
        {
          "language": "ar",
          "value": "عنوان العينة سطر 2"
        },
        {
          "language": "fr",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "addressLine3": [
        {
          "language": "ar",
          "value": "عنوان العينة سطر 3"
        },
        {
          "language": "fr",
          "value": "exemple d'adresse ligne 3"
        }
      ],
      "location1": [
        {
          "language": "ar",
          "value": "طنجة - تطوان - الحسيمة"
        },
        {
          "language": "fr",
          "value": "Tanger-Tétouan-Al Hoceima"
        }
      ],
      "pinCode": [
        {
          "language": "ar",
          "value": "85000"
        },
        {
          "language": "fr",
          "value": "85000"
        }
      ],
      "photo": [
        {
          "value": "encoded_face_image_byte_array"
        }
      ]
    }
  }
}
```

#### Failed Response:
Status Code : 200 (OK)

```JSON
{
  // API Metadata
  "id": "mosip.identity.kyc",
  "version": "1.0",
  // Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  // Auth Response
  "status": "Y",
  "staticToken": "<static_token>",
  "errors": [
      {
        "code": "IDA-MLC-002",
        "message": "Invalid UIN"
      }
    ]
}
```

## 3. OTP Request
This service enables TSP to request for an OTP for an Individual. The OTP will be send via message or email to the Individual. This OTP should then be used to authenticate an Individual using Auth service.

### Resource URL - `POST identity/otp/v1.0/<MISP-LK>`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id| |mosip.identity.otp
ver|Y|API Version| |1.0
tspID|Y|TSP ID| |tsp1234567
idvId|Y|TSP ID| |tsp1234567
idvIdType|Y|TSP ID| |tsp1234567
reqTime|Y|Time when Request was captured| |2018-10-17T07:22:57.086+05:30
txnID|Y|Request Transaction ID| |abc123abc

### Sample Request Header
##### MOSIP-AuthX = `<Partner Digital Signature re-issued by MOSIP>`

### Sample Request
```JSON
{
  // API Metadata
  "id": "mosip.identity.otp",
  "version": "1.0",
  // Request Metadata
  "partnerID": "AP000001",
  "policy": "<auth-policy-id>",
  "transactionID": "txn12345",
  "requestTime": "2019-02-15T07:22:57.086+05:30",
  // OTP Request
  "request": {
    "identity": {
      "UIN": "4074317832",
      "VID": "9830872690593682"
    },
    "channel": {
      "email": true,
      "mobile": false
    }
  }
}
```

### Sample Response Header     
##### MOSIP-AuthX = `<MOSIP Digital Signature>`

### Sample Response Body
#### Success Scenario:
Status Code : 200 (OK)

```JSON
{
  // API Metadata
  "id": "mosip.identity.otp",
  "version": "1.0",
  // Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  // OTP Response
  "errors": [],
  "response": {
    "maskedMobile": "XXXXXXX123",
    "maskedEmail": "abXXXXXXXXXcd@xyz.com"
  }
}
```

#### Failed Scenario :   
Status Code : 200 (OK)

```JSON
{
  // API Metadata
  "id": "mosip.identity.otp",
  "version": "1.0",
  // Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2019-02-15T07:23:19.590+05:30",
  // OTP Response
  "err": [
    {
      "errorCode": "IDA-OTA-006",
      "errorMessage": "OTP is invalid"
    }
  ]
}
```

## 4. Static Pin Storage
This is an internal service to be used by Resident Services to store Static Pin generated by an Individual. This Static Pin should then be used to authenticate an Individual using Auth service.

### Resource URL - `POST identity/static-pin/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id| |mosip.identity.otp
version|Y|TSP ID| |tsp1234567
requestTime|Y|Time when Request was captured| |2018-10-17T07:22:57.086+05:30
request: identity : UIN|Y|Individual's UIN| | 678956453456
request: identity : VID|Y|Individual's VID| | 678956453456
request: staticPin|Y|Static Pin to be stored||123456


### Sample Request
```JSON
{
  "id": "mosip.identity.static-pin",
  "version": "1.0",
  "requestTime": "2019-01-21T07:22:57.086+05:30",
  "request": {
	"identity": {
	  "UIN": "678956453456",
	  "VID": "678956453456"
	},
	"staticPin" : "123456"
  }
}
```

### Sample Response

#### Success Scenario:
Status Code : 200 (OK)

```JSON
{
  "id": "mosip.identity.static-pin",
  "version": "1.0",
  "responseTime": "2019-01-21T07:22:58.086+05:30",
  "status": "Y",
  "errors": []
}
```

#### Failed Scenario :   
Status Code : 200 (OK)

```JSON
{
  "id": "mosip.identity.static-pin",
  "version": "1.0",
  "responseTime": "2019-01-21T07:22:58.086+05:30",
  "status": "Y",
  "errors": [
	   {
	      "code": "IDA-SPA-003",
	      "message": "Could not store static pin of the Individual"
	    }
   ]
}
```

## 5. VID Generator
This is an internal service to be used by Resident Services to generate VID requested by an Individual. This VID should then act as a proxy ID for an Individual (active for limited duration). This VID could be used to authenticate an Individual (as a replacement for UIN) using Auth service.

### Resource URL - `POST identity/vid/v1.0/{uin}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Sample Response

#### Success Scenario:
Status Code : 200 (OK)

```JSON
{
  "id": "mosip.identity.vid",
  "version": "1.0",
  "responseTime": "2019-01-21T07:22:58.086+05:30",
  "vid": "678956453456",
  "errors": []
}
```

#### Failed Scenario :   
Status Code : 200 (OK)

```JSON
{
  "id": "mosip.identity.vid",
  "version": "1.0",
  "responseTime": "2019-01-21T07:22:58.086+05:30",
  "errors": [
	   {
	      "code": "IDA-MLC-002",
	      "message": "Invalid UIN"
	    }
   ]
}
```