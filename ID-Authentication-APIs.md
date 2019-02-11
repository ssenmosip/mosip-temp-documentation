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

### Sample Request
```JSON
{
  "id": "mosip.identity.auth",
  "ver": "1.0",
  "reqTime": "2019-01-23T10:01:57.086+05:30",
  "txnID": "1234567890",
  "idvId": "486493840596",
  "idvIdType": "D",
  "tspID": "TSP0000005",
  "authType": {
  	 "personalIdentity": true,
    "address": false,
    "bio": false,
    "otp": false,
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
ver|Y|API Version| |1.0
tspID|Y|TSP ID| |tsp1234567
idvId|Y|TSP ID| |tsp1234567
idvIdType|Y|TSP ID| |tsp1234567
reqTime|Y|Time when Request was captured| |2018-10-17T07:22:57.086+05:30
txnID|Y|Request Transaction ID| |abc123abc

### Sample Request
```JSON
{
 	// API Metadata
	"id": "mosip.identity.otp",
	"ver": "1.0",
	//Request Metadata
	"tspID": "tsp54321",
	"idvId": "426789089018",
	"idvIdType": "D",
	"reqTime": "2019-01-24T14:33:19.931+05:30",
	"txnID": "txn12345"
}

```
### Sample Response
#### Success Scenario:
Status Code : 200 (OK)

```JSON
{
  "txnID": "txn67890",
  "resTime": "2019-01-25T12:10:07.899+05:30",
  "ver": "1.0",
  "status": "Y",
  "err": [],
  "info": {
    "idType": "D",
    "reqTime": "2019-01-24T17:19:17.078+05:30",
    "usageData": "<usage and matched data on bits>"
  }
}
```

#### Failed Scenario :   
Status Code : 200 (OK)

```JSON
{
  "ver": "1.0",
  "txnID": "txn67890",
  "resTime": "2019-01-25T12:11:11.416+05:30",
  "status": "N",
  "err": [
    {
      "errorCode": "IDA-OTA-006",
      "errorMessage": "OTP is invalid"
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

## 3. VID Generator
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
  "err": []
}
```

#### Failed Scenario :   
Status Code : 200 (OK)

```JSON
{
  "id": "mosip.identity.vid",
  "version": "1.0",
  "responseTime": "2019-01-21T07:22:58.086+05:30",
  "err": [
	   {
	      "code": "IDA-MLC-002",
	      "message": "Invalid UIN"
	    }
   ]
}
```