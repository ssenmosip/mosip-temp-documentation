This section details out all Resident Service REST APIs

* [OTP Request API](#post-residentv1reqotp)

* [UIN Generation Status Check API](#post-residentv1ridcheck-status)

* [e-UIN API](#post-residentv1reqeuin)

* [Re-print UIN API](#post-residentv1reqprint-uin)

* [Retrieve Lost UIN API](#post-residentv1requin)

* [Retrieve Lost RID API](#post-residentv1reqrid)

* [UIN Update API](#post-residentv1requpdate-uin)

* [UIN Update Status Check API](#post-residentv1urnchecks-tatus)

* [VID Generate API](#post-/residentv1vid)

* [VID Revoke API](#patch-residentv1vid{vid})

* [Lock Authentication Type API](#post-residentv1reqauth-lock)

* [UnLock Authentication Type API](#post-residentv1reqauth-unlock)

* [Authentication History API](#post-residentv1reqauth-history)


## POST /resident/v1/req/otp
This service enables Individual to request for an OTP. The OTP will be send via registered message/email to the Individual. This OTP can then be used to authenticate in other resident services.

#### Resource URL 
<div>https://mosip.io/resident/v1/req/otp</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | mosip.resident.otp | 
version | Y | API version |  | v1 
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:03.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualId| N | VID | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - VID, UIN, demo | VID 
request: demographics|N| Demographic data of an Individual| |


Mandatory fields for different types of authentications- 
* If individualIdType is  VID or UIN then individualId is Mandatory
* If individualIdType is demo then  demographics is Mandatory


#### Request Body -1
```JSON
{
  "id": "mosip.resident.otp",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:03.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "demographics": null
  }
}
```

#### Request Body -2
```JSON
{
  "id": "mosip.resident.otp",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:03.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": null,
  "individualIdType": "demo",
  "demographics": {
      "name": [
        {
          "language": "fra",
          "value": "Ibrahim Ibn Ali"
        }
      ],
      "gender": [
        {
          "language": "fra",
          "value": "mâle"
        }
      ],
      "postalCode": {
          "type": "10004"
        },
      "phone": {
          "type": "998989989809"
        },
      "email": {
          "type": "abcdefgh@xyz.com"
        }
    }
  }
}
```


#### Responses:
##### Success Response:
###### Status Code : 200 (OK)
###### Description : OTP for Authentication was successfully sent to the Individual        

```JSON
{
  "id": "mosip.resident.otp",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "response": {
    "maskedMobile": "XXXXXXX123",
    "maskedEmail": "abXXXXXXXXXcd@xyz.com"
  },
  "errors": null
}
```

##### Failed Response:   
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.otp",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "response": null,
  "errors": [
    {
      "errorCode": "RES-REP-089",
      "errorMessage": "Invalid VID"
    }
  ]
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-045 | Error occurred while fetching Templates | Fetch Issue
KER-MSD-145 | Exception during inserting data into db | Insertion Issue
KER-MSD-046 | Template not found. | Data Not Found
KER-MSD-095 | Error occurred while updating Template | Update Issue
KER-MSD-096 | Error occurred while deleting Template | Delete Issue



## POST /resident/v1/rid/check-status
This service will respond with service request (UIN Generation/Updataion,Reprint etc) status to registerd phone/email.

#### Resource URL
<div>https://mosip.io/resident/v1/rid/check-status</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.uinstatus
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| N | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualId| Y | RID | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - RID | RID 

#### Request Body
```JSON
{
  "id": "mosip.resident.uinstatus",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "RID"
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.uinstatus",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.uinstatus",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```



## POST /resident/v1/req/euin
This request will authenticate an Individual based on provided OTP and UIN PDF will be sent to registered Email.

#### Resource URL
<div>https://mosip.io/resident/v1/req/euin</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.euin
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualId| Y | VID | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - VID, UIN | VID 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.euin",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "otp": "123456"
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.euin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.euin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```



## POST /resident/v1/req/print-uin
This request will authenticate an Individual based on provided OTP and post a request for UIN re-print to Postal Service.

#### Resource URL
<div>https://mosip.io/resident/v1/req/print-uin</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.reprintuin
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualId| Y | VID | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - VID, UIN | VID 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.reprintuin",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "otp": "123456"
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.reprintuin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.reprintuin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```



## POST /resident/v1/req/uin
This request will authenticate an Individual based on provided OTP and UIN PDF will be sent to registered Email.


#### Resource URL
<div>https://mosip.io/resident/v1/req/uin</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.lostuin
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualIdType| Y | Allowed Type of Individual ID - demo | demo 
request: otp| Y | OTP | | 
request: demographics|N| Demographic data of an Individual| |


#### Request Body
```JSON
{
  "id": "mosip.resident.lostuin",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualIdType": "demo",
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
      "postalCode": {
          "type": "10004"
        },
      "phone": {
          "type": "998989989809"
        },
      "email": {
          "type": "abcdefgh@xyz.com"
        }
    }
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)

```JSON
{
  "id": "mosip.resident.lostuin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.lostuin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```



## POST /resident/v1/req/rid
This request will authenticate an Individual based on provided OTP and RID will be sent to registered Phone/Email.


#### Resource URL
<div>https://mosip.io/resident/v1/req/rid</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.lostrid
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualIdType| Y | Allowed Type of Individual ID - demo | demo 
request: otp| Y | OTP | | 
request: demographics|N| Demographic data of an Individual| |


#### Request Body
```JSON
{
  "id": "mosip.resident.lostrid",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualIdType": "demo",
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
      "postalCode": {
          "type": "10004"
        },
      "phone": {
          "type": "998989989809"
        },
      "email": {
          "type": "abcdefgh@xyz.com"
        }
    }
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)

```JSON
{
  "id": "mosip.resident.lostrid",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.lostrid",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```



## POST /resident/v1/req/update-uin
This request will authenticate an Individual based on provided OTP and RID will be sent to registered Phone/Email after successfully placing update request to Registration Processor.


#### Resource URL
<div>https://mosip.io/resident/v1/req/update-uin</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.uin
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualId| Y | UIN | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - VID, UIN | UIN 
request: otp| Y | OTP | | 
request: demographics|Y| Demographic data of an Individual| |


#### Request Body
```JSON
{
  "id": "mosip.resident.uin",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "UIN",
  "otp": "123456",
  "demographics": {
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
        "value": "عنوان العينة سطر 2"
      },
      {
        "language": "fra",
        "value": "exemple d'adresse ligne 2"
      }
    ],
    "region": [
      {
        "language": "fra",
        "value": "RSK"
      }
    ],
    "province": [
      {
        "language": "fra",
        "value": "Kénitra"
      }
    ],
    "city": [
      {
        "language": "fra",
        "value": "Kénitra"
      }
    ],
    "postalCode": "10111"
    }
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)

```JSON
{
  "id": "mosip.resident.uin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.uin",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```




## POST /resident/v1/vid
This request will authenticate an Individual based on provided OTP and will generate VID for the respective UIN.

#### Resource URL
<div>https://mosip.io/resident/v1/vid</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.vid
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: vidType	| Y |	VID Type	- PERPETUAL or  TEMPORARY | 
request: individualId| Y | UIN | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - UIN | UIN 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.vid",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "UIN",
  "otp": "123456",
  "vidType": "PERPETUAL" 
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.vid",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.vid",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```


## PATCH /resident/v1/vid/{vid}
This request will authenticate an Individual based on provided OTP and will revoke respective VID.

#### Resource URL
<div>https://mosip.io/resident/v1/vid/9830872690593682</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.vidstatus
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: vidStatus	| Y| 	Status of VID	-	REVOKED |
request: individualId| Y | VID | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - VID | VID 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.vidstatus",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "VID",
  "otp": "123456",
  "vidStatus": 'REVOKED'
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.vidstatus",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.vidstatus",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```



## POST /resident/v1/req/auth-lock
This request will authenticate an Individual based on provided OTP and will lock provided authentication types.

#### Resource URL
<div>https://mosip.io/resident/v1/req/auth-lock</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.authlock
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: authType	| Y| 	Allowed Type	-	demo,bio,bio-FMR,bio-IIR,bio-FID |
request: individualId| Y | UIN | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - UIN,VID | UIN 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.authlock",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "UIN",
  "otp": "123456",
  "authType": ["bio-FMR","bio-FID"]
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.authlock",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.authlock",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```

## POST /resident/v1/req/auth-unlock
This request will authenticate an Individual based on provided OTP and will unlock provided locked authentication types.

#### Resource URL
<div>https://mosip.io/resident/v1/req/auth-unlock</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.authunlock
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: authType	| Y| 	Allowed Type	-demo,bio,bio-FMR,bio-IIR,bio-FID  |
request: individualId| Y | UIN | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - UIN,VID | UIN 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.authunlock",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "UIN",
  "otp": "123456",
  "authType": ["bio-FMR"]
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.authunlock",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.authunlock",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```


## POST /resident/v1/req/auth-history
This request will authenticate an Individual based on provided OTP and auth history will be sent to registred Phone/Email.

#### Resource URL
<div>https://mosip.io/resident/v1/req/auth-history</div>

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | API Id | | mosip.resident.authhistory
version | Y | API version | | v1
requestTime| Y |Time when Request was captured| | 2018-12-09T06:39:04.683Z
request: transactionID| Y | Transaction ID of request | | dabed834-974f-11e9-bc42-526af7764f64
request: individualId| Y | UIN | | 9830872690593682
request: individualIdType| Y | Allowed Type of Individual ID - UIN,VID | UIN 
request: otp| Y | OTP | | 


#### Request Body
```JSON
{
  "id": "mosip.resident.authhistory",
  "version": "v1",
  "requestTime": "2018-12-09T06:39:04.683Z",
  "request": {
  "transactionID": "dabed834-974f-11e9-bc42-526af7764f64",
  "individualId": "9830872690593682",
  "individualIdType": "UIN",
  "otp": "123456"
  }
}
```

#### Responses:
##### Success Response:
###### Status Code : 200 (OK)   

```JSON
{
  "id": "mosip.resident.authhistory",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": null
}
```

##### Failed Response:
###### Status Code : 200 (OK)    

```JSON
{
  "id": "mosip.resident.authhistory",
  "version": "v1",
  "responseTime": "2018-12-09T06:39:04.683Z",
  "response": {

  },
  "errors": [
    {
      "errorCode": "IDA-MLC-002",
      "errorMessage": "Invalid UIN"
    }
  ]
}
```