# 1. Key Manager
## 1.1 Public key-get service

This service will provides the public key for the specific application. 

### Resource URL
### `GET /publickey`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description |  Example
-----|----------|-------------|--------
applicationId |Yes|Id of the application| REGISTRATION,IDA
referenceId|No|Id of the Machine/TSP|
timeStamp |Yes|Date-time  in UTC ISO-8601| 2007-12-03T10:15:30Z

### Example Request
/keymanager/v1.0/publickey/REGISTRATION?timeStamp=2018-12-09T06%3A39%3A03.683Z

### Example Response
```JSON

{
  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
  "issuedAt": "2018-01-01T10:00:00",
  "expiryAt": "2018-12-10T06:12:51.994"
}

```

## 1.2 Decrypt Symmetric key

This service will decrypt the encrypted symmetric key 

### Resource URL
### `POST /keymanager/v1.0/symmetrickey`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description |  Example
-----|----------|-------------|--------
applicationId |Yes|Id of the application| REGISTRATION,IDA
referenceId|No|Id of the Machine/TSP|
timeStamp |Yes|Date-time  in UTC ISO-8601| 2007-12-03T10:15:30Z

### Example Request
/keymanager/v1.0/publickey/REGISTRATION?timeStamp=2018-12-09T06%3A39%3A03.683Z

### Example Response
```JSON

{
  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
  "issuedAt": "2018-01-01T10:00:00",
  "expiryAt": "2018-12-10T06:12:51.994"
}

```


# 2 Crypto Manager
## 2.1 Encryption Post Service

This service will encrypt provided plain string data with session symmetric key and encrypt symmetric key with application specific public key. This will respond combined encrypted data and symmetric key having a key splitter.  

### Resource URL
### `POST /cryptomanager/v1.0/encrypt`


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


### Example Request

```
{
  "applicationId": "REGISTRATION",
  "data": "string",
  "referenceId": "REF01",
  "timeStamp": "2018-11-10T06:12:52.994Z"
}
```

### Example Response
```
{
  "data": "wk4RM2su2lBXuhx3_EtBijXTDp0Y20fJA6tmoONPjr6YBLqwu_YRWiSa10o-bQWesb-IobxPg-KsZq-Gc0L6Rq6besw-rMavg5a5nPU7b3pAug0N6Ek4B7S8v_tc5cu7LBRdBv1mRSS2onxXbT2R4qeEwl_11KtxPs_ek6g4vV6oEQRem2fPhop_21DaoWVEZFovHAAJDqSFj3R38A-fxvHHpVSa9BRTe-DeTKj_xZsNYXQixZR3jMdijtm8Q7lIT3E1x8LYp-hG3RhR_xC7trAOTqilzLjLfirE3Wjfor5bhLiG9eZyTb52ihKsDV1l2oBAhn9Aao_fYl3UD5QekSNLRVlfU1BMSVRURVIjeKen-3j5KhnE-93Qfe_pBfMBIKEkTJJ7pR-4cO7l-X0"
}
```



## 2.2 Decryption Post Service

This service will dencrypt encryted data along with symmetric key having splitter. 

### Resource URL
### `POST /cryptomanager/v1.0/decrypt`


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


### Example Request

```
{
{
  "applicationId": "REGISTRATION",
  "data": "Fj3R38A-fxvHHpVSa9BRTe-DeTKj_xZsNYXQixZR3jMdijtm8Q7lIT3E1x8_xC7trAOTqilzLjLfirE3Wjfor5b",
  "referenceId": "REF01",
  "timeStamp": "2018-12-10T06:12:52.994Z"
}
}
```

### Example Response
```
{
  "data": "string"
}
```


# 3 Sync data
## 3.1 Sync Master data-get service

This service will provides the list of all master data. This service is used mainly by the Enrolment client module. In case, other modules calls this service, the machineid will be empty. The machineid will be used to get the location and based on the location, the holiday list will be retrieved. If the requestdate is not passed, all the master data will be returned. If the requestdate is passed, all the data will be returned for which the created or updated date is greater than equal request date. 

### Resource URL
### `GET /masterdata`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineId|Yes|Id of the machine| | 
lastUpdated|No|Date in UTC ISO format| | 

### Example Request

/syncdata/v1.0/masterdata/7888

### Example Response
```JSON
{
   "holidays":[
      {
         "holidayID":"string",
         "holidayDate":"string",
         "holidayName":"string",
         "holidayDay":"string",
         "holidayMonth":"string",
         "holidayYear":"string",
         "languagecode":"string"
      }
   ],
   "blacklistedwords":[
      {
         "id":"string",
         "value":"asdf",
         "languagecode":"string"
      },
      {
         "id":"string",
         "value":"asdf",
         "languagecode":"string"
      },
      {
         "id":"string",
         "value":"asdf",
         "languagecode":"string"
      }
   ],
   "machinetypes":[
      {
         "machinetypecode":"string",
         "machinename":"string",
         "description":"string",
         "languagecode":"boolean",
         "isactive":"string"
      },
      {
         "machinetypecode":"string",
         "machinename":"string",
         "description":"string",
         "languagecode":"boolean",
         "isactive":"string"
      }
   ],
   "successfully_updated_documenttypes":[
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      },
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      },
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      },
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      }
   ],
   "packetonholdreasons":[
      {
         "packetonholdreasonid":"string",
         "packetonholdreasondesc":"string",
         "languagecode":"string"
      },
      {
         "packetonholdreasonid":"string",
         "packetonholdreasondesc":"string",
         "languagecode":"string"
      }
   ],
   "packetrejectionreasons":[
      {
         "packetrejectionreasonid":"string",
         "packetrejectionreasondesc":"string",
         "languagecode":"string",
         "locationcode":"string"
      },
      {
         "packetrejectionreasonid":"string",
         "packetrejectionreasondesc":"string",
         "languagecode":"string",
         "locationcode":"string"
      }
   ],
   "reason_category":[
      {
         "code":"string",
         "name":"string",
         "desc":"string",
         "lang_code":"string",
         "reason_lists":[
            {
               "code":"string",
               "name":"string",
               "desc":"string",
               "lang_code":"string"
            },
            {
               "code":"string",
               "name":"string",
               "desc":"string",
               "lang_code":"string"
            }
         ]
      }
   ],
   "locations":[
      {
         "locationHierarchylevel":"number",
         "locationHierarchyName":"string",
         "isActive":true
      },
      {
         "locationHierarchylevel":"number",
         "locationHierarchyName":"string",
         "isActive":true
      }
   ],
   "biometricattributes":[
      {
         "biometricattribute":[
            {
               "biometricatributeid":"string"
            },
            {
               "biometricattribute":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "biometricattribute":[
            {
               "biometricatributeid":"string"
            },
            {
               "biometricattribute":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "registrationcenters":[
      {
         "registrationcentername":"",
         "centertypecode":"",
         "addressline1":"",
         "addressline2":"",
         "addressline3 ":"",
         "longitude ":"",
         "latitude":"",
         "contactphone":"",
         "numberofkiosks":"",
         "workinghours":"",
         "perkioskprocesstime":"",
         "officestarttime":"",
         "officeendtime":"",
         "holidaylocationcode":"",
         "isactive":"",
         "centertype":"",
         "address":"",
         "contactnumber":"",
         "pincode":"",
         "locationcode":""
      },
      {
         "registrationcentername":"",
         "centertypecode":"",
         "addressline1":"",
         "addressline2":"",
         "addressline3 ":"",
         "longitude ":"",
         "latitude":"",
         "contactphone":"",
         "numberofkiosks":"",
         "workinghours":"",
         "perkioskprocesstime":"",
         "officestarttime":"",
         "officeendtime":"",
         "holidaylocationcode":"",
         "isactive":"",
         "centertype":"",
         "address":"",
         "contactnumber":"",
         "pincode":"",
         "locationcode":""
      }
   ],
   "applicationtypes":[
      {
         "applicationtype":[
            {
               "applicationtypeid":"string"
            },
            {
               "applicationtypetype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "applicationtype":[
            {
               "applicationtypeid":"string"
            },
            {
               "applicationtypetype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "idtypes":[
      {
         "code":"string",
         "descr":"string",
         "languagecode":"string"
      },
      {
         "code":"string",
         "descr":"string",
         "languagecode":"string"
      }
   ],
   "biometrictypes":[
      {
         "biometrictype":[
            {
               "biometrictypeid":"string"
            },
            {
               "biometrictype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "biometrictype":[
            {
               "biometrictypeid":"string"
            },
            {
               "biometrictype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "titles":[
      {
         "title":[
            {
               "titleid":"string"
            },
            {
               "titletype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "title":[
            {
               "titleid":"string"
            },
            {
               "titletype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "genders":[
      {
         "gender":[
            {
               "genderid":"string"
            },
            {
               "gendertype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "gender":[
            {
               "genderid":"string"
            },
            {
               "gendertype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "languages":[
      {
         "language":[
            {
               "languagecode":"string"
            },
            {
               "languagename":"string"
            }
         ]
      },
      {
         "language":[
            {
               "languagecode":"string"
            },
            {
               "languagename":"string"
            }
         ]
      }
   ],
   "devices":[
      {
         "devicetype":"string",
         "devicemodel":"string",
         "languagecode":"string"
      },
      {
         "devicetype":"string",
         "devicemodel":"string",
         "languagecode":"string"
      }
   ],
   "machines":[
      {
         "machineid":"string",
         "machinename":"string",
         "macid":"string",
         "serialnumber":"string",
         "isactive":"boolean",
         "languagecode":"string"
      },
      {
         "machineid":"string",
         "machinename":"string",
         "macid":"string",
         "serialnumber":"string",
         "isactive":"boolean",
         "languagecode":"string"
      }
   ],
   "documentformats":[
      {
         "id":"id",
         "format":"pdf",
         "languagecode":"string"
      },
      {
         "id":"id",
         "format":"png",
         "languagecode":"string"
      },
      {
         "id":"id",
         "format":"jpeg",
         "languagecode":"string"
      },
      {
         "id":"id",
         "format":"gif",
         "languagecode":"string"
      }
   ],
   "documentcategories":[
      {
         "id":"id",
         "value":"POA",
         "languagecode":"string"
      },
      {
         "id":"id",
         "value":"POI",
         "languagecode":"string"
      },
      {
         "id":"id",
         "value":"POR",
         "languagecode":"string"
      },
      {
         "id":"id",
         "value":"POB",
         "languagecode":"string"
      }
   ]
}
```

## 3.2 Global config details-get service

This service will return back the global configuration data of the MOSIP platform. 

### Resource URL
### `GET /globalconfigs`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
-NA-

### Example Response
```JSON
{
		"archivalPolicy":"arc_policy_2",
		"otpTimeOutInMinutes":2,
		"numberOfWrongAttemptsForOtp":5,
		"accountFreezeTimeoutInHours":10, 
		"uinLength":24,
		"vidLength":32,
		"pridLength":32,
		"tokenIdLength":23,
		"tspIdLength":24,
		"registrationCenterId":"KDUE83CJ3",
		"machineId":"MCBD3UI3",
		"mobilenumberlength":10,
		"restrictedNumbers":"8732,321,65",
		"languagesSupported":"eng,ara,fra"
}
```

## 3.3 Registration Center Config details-get service

This service will return back the global configuration data of the MOSIP platform. 

### Resource URL
### `GET /registrationcenterconfig/{registrationcenterid}`


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
-NA-

### Example Response
```JSON
{
		"loginMode":"bootable dongle",
		"fingerprintQualityThreshold":120,
		"fingerprintRetryAttempts":234,
		"irisQualityThreshold":25,
		"irisRetryAttempts":10,
		"faceQualityThreshold":25,
		"faceRetry":12,
		"supervisorVerificationRequiredForExceptions":true,
		"operatorRegSubmissionMode":"fingerprint",
		"supervisorAuthMode":"IRIS",
		"emailNotificationTemplateOtp":"Hello $user, the OTP is $otp",
		"smsNotificationTemplateOtp":"OTP for your request is $otp",
		"emailNotificationTemplateNewReg":"Hello $user, the OTP is $otp",
		"smsNotificationTemplateNewReg":"OTP for your request is $otp",
		"emailNotificationTemplateRegCorrection":"Hello $user, the OTP is $otp",
		"smsNotificationTemplateRegCorrection":"OTP for your request is $otp",
		"emailNotificationTemplateUpdateUIN":"Hello $user, the OTP is $otp",
		"smsNotificationTemplateUpdateUIN":"OTP for your request is $otp",
		"emailNotificationTemplateLostUIN":"Hello $user, the OTP is $otp",
		"smsNotificationTemplateLostUIN":"OTP for your request is $otp",
		"passwordExpiryDurationInDays":3,
		"keyValidityPeriodRegPack":3,
		"keyValidityPeriodPreRegPack":3,
		"retentionPeriodAudit":3,
		"automaticSyncFreqServerToClient":25,
		"blockRegistrationIfNotSynced":10,
		"maxDurationRegPermittedWithoutMasterdataSyncInDays":10,
		"maxDurationWithoutMasterdataSyncInDays":7,
		"modeOfNotifyingIndividual":"mobile",
		"noOfFingerprintAuthToOnboardUser":10,
		"noOfIrisAuthToOnboardUser":10,
		"multifactorauthentication":true,
		"gpsDistanceRadiusInMeters":3,
		"officerAuthType":"password",
		"supervisorAuthType":"password",
		"defaultDOB":"1-Jan",
		"maxDocSizeInMB":150
}
```


# 4 UIN
## 4.1 UIN-get service

This service will return unused UIN from UIN pool 

### Resource URL
### `GET /uingenerator/v1.0/uin`
 

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
-NA-

### Example Response
```
{
  "uin": "734168915279"
}
```


# 5 SMS Notification
## 5.1 SMS Notification Post Service

This service will send request to SMS gateway. 

### Resource URL
### `POST /sms/send`


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request

/smsnotifier/v1.0/sms/send

```
{
  "message": "Your Booking Request accepted. B-Ref BI56793",
  "number": "89900074454"
}

```

### Example Response
```
{
  "message": "Sms Request Sent",
  "status": "success"
}
```



# 6 Email Notification
## 6.1 Email Notification Post Service

This service will send request to Email/SMTP Service. 

### Resource URL
### `POST /email/send`


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


### Example Request

/emailnotifier/v1.0/email/send

```
-H "Content-Type: multipart/form-data" 
-F "attachments={}" 
-F "mailCc=user1@gmail.com" 
-F "mailContent=OTP for Auth" 
-F "mailSubject=OTP" 
-F "mailTo=admin1@gmail.com"
```

### Example Response
```
{
  "message": "Email Request sent",
  "status": "success"
}
```



# 7 OTP Manager
## 7.1 OTP Generator
This component facilitates generation of OTP for various purposes. EG: Login in Pre-registration

The OTP Generator component will receive a request to generate OTP, validate if the OTP generation request is from an authorized source, call OTP generator API with the input parameters (Key), receive the OTP from the OTP generator API which is generated based on the OTP generation policy and respond to the source with the OTP.

The OTP Generator can also reject a request from a blocked/frozen account and assign a validity to each OTP that is generated, based on the defined policy

### Resource URL
### `POST /generate`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
key |Yes|Key| | 9820173642



### Example Request

/otpmanager/v1.0/otp/generate

```
{
   "key": "9820173642"
}
```
### Example Response
```JSON
{
  "otp": "849004",
  "status": "GENERATION_SUCCESSFUL"
}
```

## 7.2 OTP Validator
This component facilitates basic validation of an OTP. 

This includes: Receiving a request for OTP validation with required input parameters (Key), Validating the pattern of OTP generated based on defined policy, validating if the OTP is active/inactive and responding to the source with a response (Valid/Invalid)

This component also facilitates deletion of every successfully validated OTP when consumed and freezing an account for exceeding the number of retries/wrong input of OTP. 

### Resource URL
### `GET /validate`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
key |Yes|Key| | 9820173642
otp|Yes|OTP| | 123456

### Example Request

/otpmanager/v1.0/validate?key=9820173642&otp=123456

### Example Response
```
{
  "status": "success",
  "message": "VALIDATION SUCCESSFUL"
}
```





# 8. Audit Manager
Audits are events/transactions which need to be captured and stored to facilitate auditing. This data could further be used for reporting by the business.

This includes auditing various event types like System events (Periodic scans), Business events/transactions (Change in demo data), Security Events etc.

The Audit Manager component will receive a request to audit and store data, validate the request is from an authorized source, securely store the requested data and respond back with an acknowledgement of storage (Success/Failure). This component will also ensure non-auditable data is not stored.

It will also ensure audit data stored is archived based on the defined archival policy.

### Resource URL
### `POST /audits`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
eventId|Yes|ID of the event| | 
eventName|Yes|Name of the event| | Periodic Scan
eventType|Yes|Type of the event| | System Event
actionTimeStamp|Yes|Timestamp of the event| | 2018-10-04T05:57:20.929Z
hostName|Yes|Hostname| | Hostname
hostIp|Yes|IP of the host| | 2018-10-04T05:57:20.929Z
applicationId|Yes|ID of the Application| | 1
applicationName|Yes|Name of the event| | Registration
sessionUserId|Yes|Session User Id| | 
sessionUserName|Yes|Session User name| | 
id|Yes|ID| | 15426388761562
idType|Yes|ID Type| | Unique Id
createdBy|Yes|Actor of the event| | 
moduleName|No|Name of the module| | Schedulor
moduleId|No|ID of the module| | SCHE93
description|No|Description of the event| |Example description 

### Example Request
```JSON
{
  "eventId": "string",
  "eventName": "string",
  "eventType": "string",
  "actionTimeStamp": "2018-10-04T05:57:20.929Z",
  "hostName": "string",
  "hostIp": "string",
  "applicationId": "string",
  "applicationName": "string",
  "sessionUserId": "string",
  "sessionUserName": "string",
  "id": "string",
  "idType": "string",
  "createdBy": "string",
  "moduleName": "string",
  "moduleId": "string",
  "description": "string"
}
```
### Example Response
```JSON
{
  "status": true
}
```