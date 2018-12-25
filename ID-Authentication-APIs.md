This wiki page details the REST services exposed by ID Authentication.

## 1. Auth Request
This service details Auth Request to be used by TSPs to authenticate an Individual. Below are various authentication types supported by this service - 
1. OTP based - TOTP
2. Pin based - Static Pin
3. Demo based - PersonalIdentity, Address, FullAddress
4. Bio based - Fingerprint, IRIS and Face

### Resource URL
### `POST identity/auth/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.identity.auth
tspID|Y|TSP ID| |tsp5432111
licenseKey|Y|TSP's License Key| | 
transactionID|Y|Request Transaction ID| | pi
requestTime| Y |Time when Request was captured| | 2018-10-17T07:22:57.086+05:30
requestedAuth| Y | Individual Authentication Types supported| | 
requestedAuth: demo| Y | demographic Authentication Type | false| false
requestedAuth: bio| Y | Bio-metric Authentication Type | false|false
requestedAuth: otp| Y | OTP Authentication Type | false|false
requestedAuth: pin| Y | Pin Authentication Type |false |false
bioMetadata|N|Additional information on Biometric Auth| |
bioMetadata: bioType|Y|Type of Biometric Auth requested| | FTD
bioMetadata: deviceInfo|Y|Device Information used for Biometric Auth requested| |
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: identity: UIN|N| UIN attribute of Individual's Identity| | 
request: identity: VID|N| VIDattribute of Individual's Identity| | 
request: identity: name|N| name attribute of Individual's Identity| | 
request: identity: addressLine1|N| addressLine1 attribute of Individual's Identity| |  
request: identity: fullAddress|N| fullAddress attribute of Individual's Identity| | 
request: identity: biometricData|N| biometric attributes of Individual's Identity| |
request: otherFactors: totp|N| TOTP to used for authenticating Individual| | 
request: otherFactors: spin|N| Static PIN to used for authenticating Individual| |

### Sample Request
```JSON
{
//API Metadata
  "id": "mosip.identity.auth",
//Request Metadata
  "tspID": "tsp54321",
  "licenseKey": "<licenseKey>",
  "transactionID": "txn1234567",
  "requestTime": "2018-10-17T07:22:57.086+05:30",
  "requestedAuth": {
    "demo": true,
    "pin": true,
    "bio": false,
    "otp": false,
    "kyc": true,
  },
  "bioMetadata": [
    {
      "bioType": "FTD",
      "deviceInfo": {
        "deviceId": "",
        "make": "",
        "model": ""
      }
    },
    {
      "bioType": "IID",
      "deviceInfo": {
        "deviceId": "",
        "make": "",
        "model": ""
      }
    }
  ],
  "kycMetadata": {
 	"consentRequired": true,
	"ePrintRequired": true,
	"secLangRequired" : true
  }
// auth request
  "request": {
// This element will be encrypted and encoded
   "identity": {
      "UIN": "6789 5645 3456",
      "VID": "6789 5645 3456",
      "name": [
        {
          "language": "ar",
          "value": "Ø§Ø¨Ø±Ø§Ù‡ÙŠÙ…"
        },
        {
          "language": "fr",
          "value": "Ibrahim"
        }
      ],
      "addressLine1": [
        {
          "language": "ar",
          "value": "Ø¹Ù†ÙˆØ§Ù† Ø§Ù„Ø¹ÙŠÙ†Ø© Ø³Ø·Ø± 1"
        },
        {
          "language": "fr",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "fullAddress": [
        {
          "language": "ar",
          "value": "Ù�Ø§Ø³-Ø§Ù„Ø¯Ø§Ø± Ø§Ù„Ø¨ÙŠØ¶Ø§Ø¡"
        },
        {
          "language": "fr",
          "value": "Casablanca"
        }
      ],
      "biometricData": [
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
    "otherFactors": {
      //better name for this
      "totp": "123456",
      "spin": "987654",
      "challengeResponse": "12341234",
      "rsaKey": "<rsa-pub-key>"
    }
  }
}
```
### Sample Response
#### Success Response :

Status Code : 200(OK)

```JSON
{
  //APIMetadata
  "id": "mosip.identity.auth",
  "version": "1.0",
  //ResponseMetadata
  "transactionID": "txn12345",
  "staticToken": "<static_token>",
  "requestTime": "2018-10-17T07:22:57.086+05:30",
  "responseTime": "2018-10-17T07:23:19.590+05:30",
  //Response
  "status": "Y",
  "err": [],
  "response": {// encoded encrypted using KUA's public key
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
    },
    "ePrint": "encoded printable pdf format of MOSIP card"
  }
}
```

#### Fail Response:

Status Code : 500(Error)

```JSON
{
  //APIMetadata
  "id": "mosip.identity.auth",
  "version": "1.0",
  //ResponseMetadata
  "transactionID": "txn12345",
  "staticToken": "<static_token>",
  "requestTime": "2018-10-17T07:22:57.086+05:30",
  "responseTime": "2018-10-17T07:23:19.590+05:30",
  //Response
  "status": "N",
  "err": [
    {
      "code": "IDA-MLC-002",
      "message": "Invalid UIN"
    }
  ]
}
```

## 2. OTP Request
This service enables TSP to request for an OTP for an Individual. The OTP will be send via message or email to the Individual. This OTP should then be used to authenticate an Individual using Auth service.

### Resource URL - `POST identity/otp/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id| |mosip.identity.otp
tspID|Y|TSP ID| |tsp1234567
licenseKey|Y|Licence Key of TSP|| 
transactionID|Y|Request Transaction ID| |abc123abc
requestTime|Y|Time when Request was captured| |2018-10-17T07:22:57.086+05:30
request: identity : UIN|Y|Individual's UIN| | 678956453456
request: identity : VID|Y|Individual's VID| | 678956453456
request: channel: email|N|Communication channel to send OTP|false| true


### Sample Request
```JSON
{
  "id": "mosip.identity.otp",
  "tspID": "tsp54321",
  "licenseKey": "<licenseKey>",
  "transactionID": "txn12345",
  "requestTime": "2018-10-17T07:22:57.086+05:30",
  "request": {
    "identity": {
      "UIN": "678956453456",
      "VID": "678956453456"
    },
    "channel": {
      "email": true,
      "mobile": false
    }
  }
}

```
### Sample Response
#### Success Response:
Status Code : 200 (OK)
```JSON
{
  "id": "mosip.identity.otp",
  "version": "1.0",
  "transactionID": "txn12345",
  "responseTime": "2018-10-17T07:23:19.590+05:30",
  "err": [
    
  ],
  "response": {
    "maskedMobile": "XXXXXXX123",
    "maskedEmail": "abXXXXXXXXXcd@xyz.com"
  }
}
```

#### Failed Response :   
Status Code : 500 (Error)
```JSON
{
  "id": "mosip.identity.otp",
  "version": "1.0",
  "transactionID": "txn12345",
  "responseTime": "2018-10-17T07:23:19.590+05:30",
  "err": [
    {
      "code": "IDA-OTA-006",
      "message": "OTP is Invalid"
    }
  ]
}
```

