# MOSIP API List
This page and its sub-pages will have the API specifications of various features of MOSIP

## 1. Kernel
### 1.1. Public key
#### 1.1.1 Public key-get service

This service will provides the public key of the Enrolment client. 

##### Resource URL
##### `GET /publickey`

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description |  Example
-----|----------|-------------|--------
applicationId |Yes|Id of the application| REGISTRATION,IDA
referenceId|Yes|Id of the Machine/TSP|
timeStamp |Yes|Date-time without time-zone in ISO-8601| 2007-12-03T10:15:30

##### Example Request
/publickey/REGISTRATION?referenceId=1001&timeStamp=2018-11-29T12%3A00

##### Example Response
```JSON
{
  "publicKey": "Base64 encoded public Key",
  "keyExpiryTime": "Key Expiry Time in ISO-8601",
  "keyGenerationTime": "Key Generation Time in ISO-8601"
}
```
### 1.2 Sync Master
#### 1.2.1 Sync Master data-get service

This service will provides the list of all master data. This service is used mainly by the Enrolment client module. In case, other modules calls this service, the machineid will be empty. The machineid will be used to get the location and based on the location, the holiday list will be retrieved. If the requestdate is not passed, all the master data will be returned. If the requestdate is passed, all the data will be returned for which the created or updated date is greater than equal request date. 

##### Resource URL
##### `GET /syncmasterdata`

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineid|No|Id of the machine| | 
requestdate|No|Date in ISO format| | 

##### Example Request
-NA-

##### Example Response
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
### 1.3 Global config
#### 1.3.1 Global config details-get service

This service will return back the global configuration data of the MOSIP platform. 

##### Resource URL
##### `GET /globalconfigs`

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

##### Example Request
-NA-

##### Example Response
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
		"restrictedNumbers":[
			"8732","321","65"
		]
}
```
### 1.4 Enrolment Client config
#### 1.4.1 Enrolment client Config details-get service

This service will return back the global configuration data of the MOSIP platform. 

##### Resource URL
##### `GET /enrolmentclientconfigs`

This service will return back the configuration data Enrolment Client module of the MOSIP platform. 

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

##### Example Request
-NA-

##### Example Response
```JSON
{
		"loginMode":"bootable dongle",
		"languages":{
			"primary":"arabic",
			"secondary":"french"
		},
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
		"automatedSyncFrequency": {
			"masterDataServerToClient":3,
			"clientConfigServerToClient":3,
			"regIdsClientToServer":3,
			"regPacketStatusServerToClient":3,
			"loginCredentialsSync":3,
			"policySyncServerToClient":3,
			"clientStateServerToClient":3,
			"userRoleRightsServerToClient":3,
		},
		"automaticSyncFreqServerToClient":25,
		"blockRegistrationIfNotSynced":10,
		"maxDurationRegPermittedWithoutMasterdataSyncInDays":10,
		"maxDurationWithoutMasterdataSyncInDays":7,
		"modeOfNotifyingIndividual":"mobile",
		"noOfFingerprintAuthToOnboardUser":10,
		"noOfIrisAuthToOnboardUser":10,
		"PROCESS_WORKFLOW_CONFIG":"TODO",
		"gpsDistanceRadiusInMeters":3,
		"officerAuthType":"password",
		"supervisorAuthType":"password",
		"defaultDOB":"1-Jan",
		"maxDocSizeInMB":150
}
```

### 1.5 Machine Types

#### 1.5.1 Machine Types Master-get service

This service will provides the list of all machine types in all languages. 


##### Resource URL
##### `GET /machinetypes`

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

##### Example Request
```JSON
-NA-
```

##### Example Response
```JSON
{
	"code":"KJDS9",
	"name":"Laptop",
	"descr":"This is the Level-2 high performance laptop",
	"lang_code":"eng",
	"is_active":true
}
```

### 1.5 Machine Specifications

#### 1.5.1 Machine Specifications Master-get service

This service will provides the list of all Machine Specifications in all languages. 


##### Resource URL
##### `GET /machinespecifications`

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

##### Example Request
```JSON
-NA-
```

##### Example Response
```JSON
{
	"id":"KJDS9",
	"name":"Laptop",
	"brand":"Hewlett Packard",
	"model":"L34-324",
	"mtyp_code":"GEW8",
	"min_driver_ver":"1.4",
	"descr":"This is a medium configuration",
	"lang_code":"eng",
	"is_active":true
}
```


#### 1.5.2 Machine Specifications Master-get based on language service

This service will provides the list of all Machine Specifications in a specific language. 


##### Resource URL
##### `GET /machinespecifications/{lang_code}`

##### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

##### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
lang_code|Yes|Language code of the machine type| | 

##### Example Request
```JSON
-NA-
```

##### Example Response
```JSON
{
	"id":"KJDS9",
	"name":"Laptop",
	"brand":"Hewlett Packard",
	"model":"L34-324",
	"mtyp_code":"GEW8",
	"min_driver_ver":"1.4",
	"descr":"This is a medium configuration",
	"lang_code":"eng",
	"is_active":true
}
```


## 2. Authentication
AM: Put auth list here
* Auth API 1
* Auth API 2

## 3. Pre-Registration
* [Service APIs](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs)

## 4. Registration-Processor
* [Registration-Processor APIs](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs) 

## 5. Registration
* [Registration APIs](https://github.com/mosip/mosip/wiki/Registration-APIs) 

# ABIS APIs

https://github.com/mosip/mosip/wiki/ABIS-APIs
