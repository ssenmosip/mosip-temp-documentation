This wiki page details the REST services exposed by ID Authentication.

## 1. Authentication
This service details authentication (yes/no auth) that can be used by Partners to authenticate an Individual. Below are various authentication types supported by this service - 
1. OTP based - TOTP (Time based OTP)
2. Pin based - Static Pin
3. Demo based - Name, DOB, Age, Gender, Address, FullAddress
4. Bio based - Fingerprint, IRIS and Face

Users of Authentication service - 
1. `MISP (MOSIP Infrastructure Service Provider)` - MISP's role is limited to infrastructure provisioning and acting as a gate keeper for all authentication requests sent to this service
2. `Partners` - Auth Partners register themselves with MOSIP, under a MISP. Authentication requests are captured by Auth Partners and sent to MOSIP, via MISP.

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
MISP-LK| Y | MISP License Key | | 
id | Y | API Id | | mosip.identity.auth
version | Y | API version | | 1.0
partnerId | Y | Auth Partner ID | |
policyId | Y | Policy ID of Auth Partner | |
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
requestedAuth| Y | Authentication Types requested| | 
requestedAuth: otp| Y | OTP Authentication Type | false| false
requestedAuth: demo| Y | Demographic Authentication Type | false| false
requestedAuth: bio| Y | Biometric Authentication Type | false|false
requestedAuth: pin| Y | Static Pin Authentication Type |false |false
bioMetadata| N | Biometric metadata when Bio Auth is requested | | 
bioMetadata: bioType| Y | Biometric Type requested | |FMR or IIR or FID 
bioMetadata: deviceId| Y | Biometric Device ID | | 
bioMetadata: deviceProviderID| Y | Biometric Device Provider ID | | 
sessionKey| Y | Session Key encrypted using MOSIP Public Key | | 
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: identity: UIN| N | UIN of an Individual| | 
request: identity: VID| N | VIDof an Individual| | 
request: identity: name| N | name attribute of Individual's Identity| | 
request: identity: addressLine1|N| addressLine1 attribute of Individual's Identity| |  
request: identity: fullAddress|N| fullAddress attribute of Individual's Identity| | 
request: identity: biometrics|N| Biometrics of an Individual| |
request: additionalFactors|N| Additional Factors of Auth requested| |
request: additionalFactors: totp|N| OTP used for requested OTP Auth| |
request: additionalFactors: staticPin|N| Static Pin used for requested Pin Auth| |

### Sample Request Header
##### MOSIP-AuthX = `<Partner Digital Signature re-issued by MOSIP>`

### Sample Request Body
```JSON
{
	// API Metadata
	"id": "mosip.identity.auth",
	"version": "1.0",
	// Request Metadata
	"requestTime": "2019-02-15T10:01:57.086+05:30",
	"transactionID": "1234567890",
	"requestedAuth": {
		"otp": true,
		"demo": false,
		"bio": false
	},
	"consentObtained": true,// Consent Obtained for performing Auth
	"individualId": "9830872690593682",
	"individualIdType": "VID",	
	"sessionKey": "<encrypted (RSA OAEP) with MOSIP public key and encoded session key>",
	"keyIndex": "<thumbprint of the public key certficate used for enryption of sessionKey. This is necessary for key rotaion>",
	//Identity Request
	"request": {// This element should be encrypted and encoded using session key AES GCM
		"timestamp": "2019-02-15T10:01:56.086+05:30 - ISO format timestamp",
		"factors": {
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
				"gender" : [ 
					{
						"language" : "ara",
						"value" : "الذكر"
					}, 
					{
						"language" : "fra",
						"value" : "mâle"
					} 
				],
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
					"transactionID": "1234567890",
					"requestedBioType": {// Data sent by Partner Application
						"FMR" : true,
						"FIR" : false,
						"IIR" : false,
						"FID" : false
					},
					"metaData": {// Data sent by RD Service
							"deviceCode": "",// This is digital ID of device given by MOSIP device service
							"deviceProviderID": "",
							"deviceServiceID": "",// RD Service ID
							"deviceServiceVersion":""// RD Service Version
					},
					"values": [//Data sent by RD Service
						{
							"type": "FMR",
							"subType": "UNKNOWN",
							"value": "<base64 encoded value>",
							"timestamp": "2019-02-15T10:01:57.086+05:30",
							"signature": "base64 signature of the block"
						},
						{
							"type": "FMR",
							"subType": "RIGTHT_POINTER",
							"value": "<base64 encoded value>",
							"timestamp": "2019-02-15T10:01:57.086+05:30",
							"signature": "base64 signature of the block"
						}
					]
				},
				{
					"transactionID": "1234567890",
					"requestedBioType": {
						"FMR" : false,
						"FIR" : false,
						"IIR" : true,
						"FID" : false
					},
					"metaData": {
							"deviceCode": "",// This is digital ID of device given by MOSIP device service
							"deviceProviderID": "",
							"deviceServiceID": "",// RD Service ID
							"deviceServiceVersion":""// RD Service Version
					},
					"values": [
						{
							"type": "IIR",
							"subType": "RIGHT",
							"value": "<base64 encoded value>",
							"timestamp": "2019-02-15T10:01:57.086+05:30",
							"signature": "base64 signature of the block"
						}
					]
				}
			]
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

## 2. eKYC
This service details authentication (eKYC auth) that can be used by Partners to authenticate an Individual and send Individual's KYC details as response. Below are various authentication types supported by eKYC Auth - 
1. OTP Auth - Time-based OTP (OTP)
2. Bio Auth - Fingerprint, IRIS and Face

### Resource URL
### `POST identity/kyc/1.0/<eKYC-Partner-ID>/<MISP-LK>`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
MISP-LK| Y | MISP License Key | | 
id | Y | API Id | mosip.identity.kyc | 
version | Y | API version | 1.0 | 
partnerId | Y | eKYC Partner ID | |
policyId | Y | Policy ID of eKYC Partner | |
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
requestedAuth| Y | Authentication Types requested| | 
requestedAuth: otp| Y | OTP Authentication Type | false| false
requestedAuth: demo| N | Demographic Authentication Type | false| false
requestedAuth: bio| Y | Biometric Authentication Type | false|false
requestedAuth: pin| Y | Static Pin Authentication Type |false |false
bioMetadata| N | Biometric metadata when Bio Auth is requested | | 
bioMetadata: bioType| Y | Biometric Type requested | |FMR or IIR or FID 
bioMetadata: deviceId| Y | Biometric Device ID | | 
bioMetadata: deviceProviderID| Y | Biometric Device Provider ID | | 
kycMetadata| Y | KYC metadata requested | | 
kycMetadata: consentRequired| Y | Individual's consent for eKYC Auth | | 
kycMetadata: secondaryLangCode| N | Secondary Language code to send eKYC response | | 
sessionKey| Y | Session Key encrypted using MOSIP Public Key | | 
request| Y | Auth request attributes to be used for authenticating Individual | | 
request: identity: UIN| N | UIN of an Individual| | 
request: identity: VID| N | VIDof an Individual| | 
request: identity: biometrics|N| Biometrics of an Individual| |
request: additionalFactors|N| Additional Factors of Auth requested| |
request: additionalFactors: totp|N| OTP used for requested OTP Auth| |
request: additionalFactors: staticPin|N| Static Pin used for requested Pin Auth| |

### Sample Request Header
##### MOSIP-AuthX = `<Partner Digital Signature re-issued by MOSIP>`

### Sample Request
```JSON
{
	// API Metadata
	"id": "mosip.identity.auth",
	"version": "1.0",
	// Request Metadata
	"requestTime": "2019-02-15T10:01:57.086+05:30",
	"transactionID": "1234567890",
	"requestedAuth": {
		"otp": true,
		"demo": false,
		"bio": false
	},
	"consentObtained": true,
	"secondaryLangCode" : "<sec-lang-code>",
	"individualId": "9830872690593682",
	"individualIdType": "VID",	
	"sessionKey": "<encrypted (RSA OAEP) with MOSIP public key and encoded session key>",
	"keyIndex": "<thumbprint of the public key certficate used for enryption of sessionKey. This is necessary for key rotaion>",
	//Identity Request
	"request": {// This element should be encrypted and encoded using session key AES GCM
		"timestamp": "2019-02-15T10:01:56.086+05:30 - ISO format timestamp",
		"factors": {
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
				"gender" : [ 
					{
						"language" : "ara",
						"value" : "الذكر"
					}, 
					{
						"language" : "fra",
						"value" : "mâle"
					} 
				],
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
					"transactionID": "1234567890",
					"requestedBioType": {// Data sent by Partner Application
						"FMR" : true,
						"FIR" : false,
						"IIR" : false,
						"FID" : false
					},
					"metaData": {// Metadata sent by RD Service
							"deviceCode": "",// This is digital ID of device given by MOSIP device service
							"deviceProviderID": "",
							"deviceServiceID": "",// RD Service ID
							"deviceServiceVersion":""// RD Service Version
					},
					"values": [//Biometrics Data sent by RD Service
						{
							"type": "FMR",
							"subType": "UNKNOWN",
							"value": "<base64 encoded value>",
							"timestamp": "2019-02-15T10:01:57.086+05:30",
							"signature": "base64 signature of the block"
						},
						{
							"type": "FMR",
							"subType": "RIGTHT_POINTER",
							"value": "<base64 encoded value>",
							"timestamp": "2019-02-15T10:01:57.086+05:30",
							"signature": "base64 signature of the block"
						}
					]
				},
				{
					"transactionID": "1234567890",
					"requestedBioType": {
						"FMR" : false,
						"FIR" : false,
						"IIR" : true,
						"FID" : false
					},
					"metaData": {
							"deviceCode": "",// This is digital ID of device given by MOSIP device service
							"deviceProviderID": "",
							"deviceServiceID": "",// RD Service ID
							"deviceServiceVersion":""// RD Service Version
					},
					"values": [
						{
							"type": "IIR",
							"subType": "RIGHT",
							"value": "<base64 encoded value>",
							"timestamp": "2019-02-15T10:01:57.086+05:30",
							"signature": "base64 signature of the block"
						}
					]
				}
			]
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
      "dob": "1955/04/06",
      "age": 30,
      "gender": [
        {
          "language": "ar",
          "value": "الذكر"
        }
      ],
      "phoneNumber": "+212-5398-12345",
      "emailId": "sample@samplamail.com",
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
      "postalCode": "85000",
      "photo": "encoded_face_image_byte_array"
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
This service enables Partners to request for an OTP for an Individual. The OTP will be send via message or email as requested to the Individual. This OTP can then be used to authenticate an Individual using Authentication or eKYC service.

### Resource URL - `POST identity/otp/v1.0/<MISP-LK>`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
MISP-LK| Y | MISP License Key | | 
id | Y | API Id | mosip.identity.otp | 
version | Y | API version | 1.0 | 
partnerId | Y | Auth or eKYC Partner ID | |
policyId | Y | Policy ID of Auth or eKYC Partner | |
transactionID| Y | Transaction ID of request | | 1234567890
requestTime| Y |Time when Request was captured| | 2019-02-15T10:01:57.086+05:30
request| Y | Attributes to be used for requesting for an OTP | | 
request: identity: UIN| N | UIN of an Individual| | 
request: identity: VID| N | VID of an Individual| | 
request: channel: email| N | Request OTP to be sent to Individual's email| | true
request: channel: phone| N | Request OTP to be sent to Individual's phone| | true

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
  "policyID": "<auth-policy-id>",
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
      "phone": false
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
This is an internal service to be used by Resident Services to store Static Pin generated by an Individual. This Static Pin should then be used to authenticate an Individual using Authentication service.

### Resource URL - `POST identity/static-pin/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id| |mosip.identity.static-pin
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