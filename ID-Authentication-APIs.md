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
kycMetadata: consentRequired| Y |Consent of Individual to retrieve KYC details| |
kycMetadata: ePrintRequired| N |Printable format of KYC details required in response| |
kycMetadata: secLangRequired| N |KYC Details required in secondary language in response| |
sessionKey| Y | TSP Session Key, encrypted using TSP Public Key | | 
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
  "id": "mosip.identity.auth",
  "ver": "1.0",
  "reqTime": "2019-01-23T10:01:57.086+05:30",
  "txnID": "1234567890",
  "muaCode": "1234567890",
  "idvId": "486493840596",
  "idvIdType": "D",
  "tspID": "TSP0000005",
  "authType": {
    "address": false,
    "bio": false,
    "otp": false,
    "personalIdentity": true,
    "pin": false
  },
  "key": {
    "publicKeyCert": "<Base 64 encoded TSP public key>",
    "sessionKey": "<encrypted and encoded session key>"
  },
  // This element should be encrypted and encoded by Session Key
  "request": {
    "identity": {
      "fullName": [
        {
          "language": "ara",
          "value": "ابراهيم بن علي"
        }
      ]
    }
  }
}
```

### Sample Response
#### Success Scenario :
Status Code : 200 (OK)

```JSON
{
  "ver": "1.0",
  "resTime": "2019-01-23T15:38:26.597+05:30",
  "status": "Y",
  "txnID": "1234567890",
  "info": {
    "idType": "D",
    "reqTime": "2019-01-23T10:01:57.086+05:30",
    "matchInfos": [
      {
        "authType": "personalIdentity",
        "language": "ara",
        "matchingStrategy": "E",
        "matchingThreshold": 100
      }
    ],
    "bioInfos": [],
    "usageData": "0x2000000020000000"
  },
  "err": [],
}
```

#### Failed Response:
Status Code : 200 (OK)

```JSON
{
  "ver": "1.0",
  "resTime": "2019-01-23T15:38:26.597+05:30",
  "status": "N",
  "txnID": "1234567890",
  "err": [
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
### `POST identity/kyc/v1.0`

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
kycMetadata: consentRequired| Y |Consent of Individual to retrieve KYC details| |
kycMetadata: ePrintRequired| N |Printable format of KYC details required in response| |
kycMetadata: secLangRequired| N |KYC Details required in secondary language in response| |
sessionKey| Y | TSP Session Key, encrypted using TSP Public Key | | 
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
  "id": "mosip.identity.kyc",
  "ver": "1.0",
  "consentReq": true,
  "ekycAuthType": "I",
  // This element should be Base 64 encoded"
  authRequest": {
    "id": "mosip.identity.auth",
    "ver": "1.0",
    "reqTime": "2019-01-18T11:00:32.149+05:30",
    "txnID": "1234567890",
    "idvId": "647082439732",
    "idvIdType": "D",
    "muaCode": "1234567890",
    "tspID": "string",
    "authType": {
      "address": false,
      "bio": true,
      "otp": false,
      "personalIdentity": false,
      "pin": false
    },
    "bioInfo": [
      {
        "bioType": "irisImg",
        "deviceInfo": {
          "deviceId": "123143",
          "make": "cogent",
          "model": "steel"
        }
      }
    ],
    "key": {
    	"publicKeyCert": "<Base 64 encoded TSP public key>",
    	"sessionKey": "<encrypted and encoded session key>"
  	},
  	// This element should be encrypted and encoded by Session Key
    "request": {
      "identity": {
        "leftEye": [
          {
            "value": "<Base 64 encoded IRIS ISO Image>"
          }
        ]
      }
    }
  }
}
```

### Sample Response
#### Success Scenario :
Status Code : 200 (OK)

```JSON
{
  "kyc": {
    "identity": {
      "fullName": [
        {
          "language": "fre",
          "value": "Ibrahim Bin Ali"
        }
      ],
      "gender": [
        {
          "language": "fre",
          "value": "mâle"
        }
      ],
      "dateOfBirth": [
        {
          "value": "1955/04/15"
        }
      ],
      "addressLine1": [
        {
          "language": "fre",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "addressLine2": [
        {
          "language": "fre",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "addressLine3": [
        {
          "language": "fre",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "city": [
        {
          "language": "fre",
          "value": "Casablanca"
        }
      ],
      "region": [
        {
          "language": "fre",
          "value": "Tanger-Tétouan-Al Hoceima"
        }
      ],
      "province": [
        {
          "language": "fre",
          "value": "Fès-Meknès"
        }
      ],
      "postalCode": [
        {
          "value": "570004"
        }
      ],
      "email": [
        {
          "value": "abc@xyz.com"
        }
      ],
      "phone": [
        {
          "language": null,
          "value": "9876543210"
        }
      ]
    },
    "idvId": "XXXXXXXX9732"
  },
  "auth": {
    "ver": 1.0,
	"resTime": "2019-01-23T13:38:45.222Z",
	"txnID": "1234567890",
	"status": "Y",
    "err": [
      
    ],
    "info": {
      "idType": "D",
      "reqTime": "2019-01-23T11:00:32.149+05:30",
      "matchInfos": [
        
      ],
      "bioInfos": [
        {
          "bioType": "irisImg",
          "deviceInfo": {
            "deviceId": "123143",
            "make": "cogent",
            "model": "steel"
          }
        }
      ],
      "usageData": "0x0000001000000010"
    }
  }
}
```

#### Failed Response:
Status Code : 200 (OK)

```JSON
{
  "auth": {
    "ver": 1.0,
    "resTime": "2019-01-23T13:38:45.222Z",
    "txnID": "1234567890",
    "status": "N",
    "err": [
      {
        "code": "IDA-MLC-002",
        "message": "Invalid UIN"
      }
    ]
  }
}
```

## 3. OTP Request
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
 	// API Metadata
	"id": "mosip.identity.otp",
	//Request Metadata
	"tspID": "tsp54321",
	"idvId": "426789089018",
	"idvIdType": "D",
	"muaCode": "1234567890",
	"reqTime": "2019-01-24T14:33:19.931+05:30",
	"txnID": "txn12345",
	"ver": "1.0"
}

```
### Sample Response
#### Success Scenario:
Status Code : 200 (OK)

```JSON
{
  // API Metadata
  "id": "mosip.identity.otp",
  "version": "1.0",
  // Response Metadata
  "transactionID": "txn12345",
  "responseTime": "2018-10-17T07:23:19.590+05:30",
  // OTP Response
  "err": [],
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
  "responseTime": "2018-10-17T07:23:19.590+05:30",
  // OTP Response
  "err": [
    {
      "code": "IDA-OTA-006",
      "message": "OTP is Invalid"
    }
  ]
}
```

## 3. Static Pin Storage
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
   "err": []
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
   "err": [
	   {
	      "code": "IDA-SPA-003",
	      "message": "Could not store static pin of the Individual"
	    }
   ]
}
```
