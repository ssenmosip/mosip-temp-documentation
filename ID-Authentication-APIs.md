This wiki page details the REST services exposed by ID Authentication.

## 1. Auth Request
This service details Auth Request to be used by TSPs to authenticate an Individual. Below are various authentication types supported by this service - 
1. OTP based
2. Pin based - Static Pin
3. Demo based - PersonalIdentity, Address, FullAddress
4. Bio based - Fingerprint, IRIS and Face

### Resource URL
### `POST identity/auth`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.identity.auth
ver|Y |API version| | 1.0
idvId|Y|Individual's UIN/VID| |1234567890 
idvIdType|Y|Individual's ID Type| D| D
authType|Y|Individual Authentication Types supported| | pi
authType: personalIdentity| Y | Personal Identity Authentication Type| false| true
authType: address| Y | Address Authentication Type |false| false  
authType: fullAddress| Y  | Full Address Authentication Type | false| false
authType: bio| Y | Bio-metric Authentication Type | false|false
authType: otp| Y | OTP Authentication Type | false|false
authType: pin| Y | Pin Authentication Type |false |false
muaCode|Y|TSP User Agency code| |tspLevel1ID 
reqTime|Y|Time when Request was captured| | 2018-10-04T05:57:20.929+0000
txnID|Y|Request Transaction ID| | txn12345
reqHmac|Y|SHA of request element| | 
matchInfo|N|Match Info for pi and fad authentication types| | 
matchInfo: authType|N|Authentication type| | fad
matchInfo: matchingStrategy|N|Matching Strategy | E | P
matchInfo: matchingThreshold|N|Matching Threshold| 60 | 80   
pinInfo|N|Pin Info for pin and otp authentication types| | 
pinInfo: type|N|Static Pin or Dynamic Pin - otp| | 
pinInfo: value|N|Value of static pin or otp | | 
request| Y | ID request to be authenticated | | 
request: identity: name|N| name attribute of ID Object| | 
request: identity: dateOfBirth|N| dob attribute of ID Object| | 
request: identity: gender|N| gender attribute of ID Object| | 
request: identity: addressLine1|N| addressLine1 attribute of ID Object| |  
request: identity: fullAddress|N| fullAddress attribute of ID Object| | 
request: identity: leftEye|N| leftEye attribute of ID Object| |
request: identity: rightThumb|N| rightThumb attribute of ID Object| |

### Sample Request
```JSON
{
//API Metadata
  "id": "mosip.identity.auth",
  "version": "1.0",
//Request Metadata
  "tspID": "tsp54321",
  "licenseKey": "<licenseKey>",
  "transactionID": "txn1234567",
  "requestTime": "2018-10-17T07:22:57.086+05:30",
  "requestedAuth": {
    "demo": true,
    "pin": true,
    "bio": false,
    "otp": true
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
// auth request
  "request": {
// This element will be encrypted and encoded
   "identity": {
      "UIN": "6789 5645 3456",
      "VID": "6789 5645 3456",
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
      "fullAddress": [
        {
          "language": "ar",
          "value": "فاس-الدار البيضاء"
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
      "spin": "987654"
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
  "err": []
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

## 2. eKYC Service

### Sample Request
```JSON
{
	"id": "mosip.identity.kyc",
	"ver": "1.0",
	"consentReq": true,
	"ePrintReq": true,
        "secLangReq" : true,
        "eKycAuthType" : "",
	"authRequest": {// no PPI, only encoding required
		"idvId": "1234567890",
		"idvIdType": "V",
		"authType": {
			"demo": true,
			"pin": false,
			"bio": false
		},
		"txnID": "txn12345",
                "tspID" : "tsp54321",
		"reqTime": "2018-10-17T07:22:57.086+05:30",
		"demoInfo": [
			{
				"authType": "fullAddress",
				"language": "fr",
				"matchingStrategy": "P",
				"matchingThreshold": 60
			}
		],
		"pinInfo": 
                [                        
                       {
			        "value": "123456",
			        "type": "otp"
		        }
                 ],
		"request": {//encoded and encrypted using mua public key
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
				"fullAddress": [
					{
						"language": "ar",
						"value": "فاس-الدار البيضاء"
					},
					{
						"language": "fr",
						"value": "Casablanca"
					}
				]
			}
		}
	}
}
```

### Sample Response
#### Success Response :

Status Code : 200(OK)
```JSON
{
	"status": true,//status of auth + kyc
	"err": [],
	"txnID": "txn12345",
	"resTime": "2018-10-17T13:40:19.590+0000",
	"ttl" : "time_to_live_for_KYC_Info",
	"response": { // encoded encrypted using KUA's public key
		"auth": { //No PII to encrypt this separately, only encoding
			"status": true,
			"err": [],
			"txnID": "txn12345",
			"resTime": "2018-10-17T13:40:19.590+0000",
			"info": {
				"idvIdType": "V",
				"reqTime": "2018-10-17T07:22:57.086+0000",
				"ver": "1.0",
				"demoInfo": [
					{
						"authType": "fullAddress",
						"language": "fr",
						"mathingStrategy": "P",
						"matchingThreshold": 60
					}
				],
				"usageData": "0xaf100000af100000"
			}
		},
		"kyc": { // encodes KYC details
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
				"location": [
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
}
```

#### Fail Response:

Status Code : 500(Error)

```JSON
{
	"status" : false,
	"err": [
           {
              "code": "IDA-MLC-002",
              "message": "Invalid UIN"
           }
        ],
	"txnID": "txn12345",
	"resTime": "2018-10-17T13:45:19.590Z",
}
```

## 3. OTP Request
This service enables TSP to request for an OTP for an Individual. The OTP will be send via message or email to the Individual. This OTP should then be used to authenticate an Individual using Auth service.

### Resource URL - `POST identity/otp`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id| |mosip.identity.otp
version|Y|API version| | 1.0
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
  "version": "1.0",
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

