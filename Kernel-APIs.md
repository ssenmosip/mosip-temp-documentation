* [Key Manager](#key-manager)

* [Crypto Manager Service](#crypto-manager)

* [Data Sync Service](#sync-data)

* [UIN Service](#uin)

* [SMS Notification Service](#sms-notification)

* [Email Notification Service](#email-notification)

* [Audit Service](#audit-manager)

* [License Key Service](#license-key-manager)

* [Applicant Types Service](#applicant-type)

* [Individual Types Service](#individual-types)

*﻿﻿ [Digital Signatures](#digital-signatures)

* ﻿﻿[Static Token generator](#static-token-generator)
 




# Key Manager

* [GET /publickey](#get-publickey)
* [POST /decrypt](#post-decrypt)


##  Public key-get service

This service will provide the public key for the specific application. 

### Resource URL
### GET /publickey

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
v1/keymanager/publickey/REGISTRATION?timeStamp=2018-12-09T06%3A39%3A03.683Z

### Example Response
```JSON

{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
		  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
		  "issuedAt": "2018-01-01T10:00:00",
		  "expiryAt": "2018-12-10T06:12:51.994"
	    }
	
}
```

##  Decrypt Symmetric key

This service will decrypt the encrypted symmetric key 

### Resource URL
### POST /decrypt

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

v1/keymanager/decrypt

```
{	
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
	"request": {
		  "applicationId": "REGISTRATION",
		  "encryptedSymmetricKey": "encryptedSymmetricKey",
		  "referenceId": "REF01",
		  "timeStamp": "2018-12-10T06:12:52.994Z"
	}
}
```



### Example Response
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
 "response": {
	    "symmetricKey": "decryptedSymmetricKey"
	}
}

```


# Crypto Manager

* [POST v1/cryptomanager/encrypt](#post-v1cryptomanagerencrypt)
* [POST v1/cryptomanager/decrypt](#decryption-post-service)

##  Encryption Post Service

This service will encrypt provided plain string data with session symmetric key and encrypt symmetric key with application specific public key. This will respond combined encrypted data and symmetric key having a key splitter.  

### Resource URL
### POST v1/cryptomanager/encrypt


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


### Example Request

```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
	"request": {
		"applicationId": "REGISTRATION",
		"data": "string",
		"referenceId": "REF01",
		"timeStamp": "2018-11-10T06:12:52.994Z"
	}	  
}
```

### Example Response
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
 "response": {
		"data": "wk4RM2su2lBXuhx3_EtBijXTDp0Y20fJA6tmoONPjr6YBLqwu_YRWiSa10o-bQWesb-IobxPg-KsZq-Gc0L6Rq6besw-rMavg5a5nPU7b3pAug0N6Ek4B7S8v_tc5cu7LBRdBv1mRSS2onxXbT2R4qeEwl_11KtxPs_ek6g4vV6oEQRem2fPhop_21DaoWVEZFovHAAJDqSFj3R38A-fxvHHpVSa9BRTe-DeTKj_xZsNYXQixZR3jMdijtm8Q7lIT3E1x8LYp-hG3RhR_xC7trAOTqilzLjLfirE3Wjfor5bhLiG9eZyTb52ihKsDV1l2oBAhn9Aao_fYl3UD5QekSNLRVlfU1BMSVRURVIjeKen-3j5KhnE-93Qfe_pBfMBIKEkTJJ7pR-4cO7l-X0"
	}
}	
```



## Decryption Post Service

This service will dencrypt encryted data along with symmetric key having splitter. 

### Resource URL
### POST v1/cryptomanager/decrypt


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


### Example Request

```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
	"request": {
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
 "response": {
 		"data": "string"
             }
}	
```


# Sync data

* [GET /masterdata](#get-masterdata)

* [GET /masterdata](#get-masterdata-1)

* [GET /configs](#get-configs)

* [GET /roles](#get-roles)

* [GET /userdetails/{regid}](#get-userdetailsregid)

* [GET /publickey](#get-publickey-1)

## Sync Master data-get service

This service will provides the list of all master data. This service is used mainly by the Enrolment client module. 

### Resource URL
### GET /masterdata

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
macaddress|No|MAC address of the machine| | 
serialnumber|No|serial number of the machine| | 
lastUpdated|No|Date in UTC ISO format| | 

### Example Request

v1/syncdata/masterdata?macaddress=e1:01:2b:c2:1d:b0&serialnumber=NM5328114630

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
     {
      "errorCode": "string",
      "message": "string"
     }
     ],
  "response": {
		"lastSyncTime": "2019-03-04T12:34:15.477Z",
		 "registrationCenter": [
    {
      "id": "10007",
      "name": "Center Sidi Taibi",
      "centerTypeCode": "REG",
      "addressLine1": "Rabat Road",
      "addressLine2": "Sidi Taibi",
      "addressLine3": "Morroco",
      "latitude": "34.192861",
      "longitude": "-6.683662",
      "locationCode": "14025",
      "holidayLocationCode": "KTA",
      "contactPhone": "811552880",
      "numberOfStations": null,
      "workingHours": "8:00:00",
      "numberOfKiosks": 1,
      "perKioskProcessTime": "00:15:00",
      "centerStartTime": "09:00:00",
      "centerEndTime": "17:00:00",
      "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
      "contactPerson": "Monty Carlo",
      "lunchStartTime": "13:00:00",
      "lunchEndTime": "14:00:00",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterTypes": [
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "REG",
      "name": "Ordinaire",
      "descr": "Centre dinscription régulière"
    }
  ],
  "machineDetails": [
    {
      "id": "10007",
      "name": "Machine 7",
      "serialNum": "LK8186452621",
      "macAddress": "6d:a6:30:56:66:9f",
      "ipAddress": "192.168.0.227",
      "machineSpecId": "1001",
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "machineSpecification": [
    {
      "id": "1001",
      "name": "ستر  ",
      "brand": "دلّ  ",
      "model": "3568",
      "machineTypeCode": "DKS",
      "minDriverversion": "1.454",
      "description": "لأخذ التسجيلات",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    }
  ],
  "machineType": [
    {
      "code": "DKS",
      "name": "الحاسوب",
      "description": "أجهزة الكمبيوتر المكتبية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    }
  ],
  "devices": [
    {
      "id": "3000027",
      "name": "Finger Print Scanner 7",
      "serialNum": "CX8481464983",
      "deviceSpecId": "165",
      "macAddress": "d4:98:44:dd:aa:f1",
      "ipAddress": null,
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "deviceTypes": [
    {
      "code": "FRS",
      "name": "Finger Print Scanner",
      "description": "For scanning fingerprints",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "deviceSpecifications": [
    {
      "id": "165",
      "name": "Fingerprint Scanner",
      "brand": "Safran Morpho",
      "model": "1300 E2",
      "deviceTypeCode": "FRS",
      "minDriverversion": "1.12",
      "description": "To scan fingerprint",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "holidays": [
    {
      "holidayId": "2000049",
      "holidayDate": "2019-01-01",
      "holidayDay": "2",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "Jour de l’an",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    }
  ],
  "documentCategories": [
    {
      "code": "POA",
      "name": "Proof of Address",
      "description": "Address Proof",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "documentTypes": [
    {
      "code": "CIN",
      "name": "CNIE card",
      "description": "Moroccan National Electronic ID Card",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "validDocumentMapping": [
    {
      "docTypeCode": "CIN",
      "docCategoryCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "templates": [
    {
      "id": "1101",
      "name": "Template for authorization content",
      "description": "Template for authorization content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name\nYour Authentication of UIN $uin using $authType on $date at $time Hrs $status at a device deployed by MOSIP Services",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "auth-email-content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "templatesTypes": [
    {
      "code": "auth-email-content",
      "description": "Template for authorization content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "templateFileFormat": [
    {
      "code": "txt",
      "description": "Text File",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "reasonCategory": [
    {
      "code": "MNA",
      "name": "Manual Adjudication",
      "description": "Rejection during Manual Adjudication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "reasonList": [
    {
      "code": "APM",
      "name": "Age-Photo Mismatch",
      "description": "Mismatch between the Age and Photo",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "blackListedWords": [
    {
      "word": "shit",
      "description": "Blacklisted Word",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "locationHierarchy": [
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MOR",
      "name": "الْـمَغْرِبُ",
      "hierarchyLevel": 0,
      "hierarchyName": "بلد",
      "parentLocCode": null,
      "createdBy": null,
      "updatedBy": null
    }
  ],
  "biometricattributes": [
    {
      "code": "LTM",
      "name": "Left Thumb",
      "description": "Print of Left Thumb",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "biometricTypes": [
    {
      "code": "FNR",
      "name": "Fingerprint",
      "description": "Finger prints of the applicant",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "applications": [
    {
      "code": "app01",
      "name": "application 1",
      "description": "app description",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "applicantValidDocuments": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "001",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    }
  ],
  "individualTypes": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "FR",
      "name": "Foreigner"
    }
  ],
  "appDetails": [
    {
      "id": "10001",
      "name": "Pre-Registration",
      "descr": "Web portal for pre-registrations",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    }
  ],
  "appRolePriorities": [
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "SUPERADMIN",
      "priority": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    }
  ],
  "screenAuthorizations": [
    {
      "screenId": "approveRegistrationRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "processList": [
    {
      "id": "login_auth",
      "name": "Login authentication",
      "descr": "Login authentication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachines": [
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterDevices": [
    {
      "regCenterId": "10007",
      "deviceId": "3000027",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachineDevices": [
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000027",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterUserMachines": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "cntrId": "10007",
      "machineId": "10007",
      "usrId": "110007"
    }
  ],
  "registrationCenterUsers": [
    {
      "regCenterId": "10007",
      "userId": "110007",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachineHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "effectivetimes": "2019-02-27T10:50:57.626598"
    }
  ],
  "registrationCenterDeviceHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "deviceId": "3000027",
      "effectivetimes": "2019-02-27T10:50:57.589Z"
    }
  ],
  "registrationCenterMachineDeviceHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000027",
      "effectivetimes": "2019-02-27T10:50:57.607964"
    }
  ],
  "registrationCenterUserMachineMappingHistory": [
    {
      "cntrId": "10007",
      "machineId": "10007",
      "usrId": "110007",
      "effectivetimes": "2019-02-27T10:50:57.660Z"
    }
  ],
  "registrationCenterUserHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCntrId": "10007",
      "userId": "110007",
      "effectDateTimes": "2019-02-27T10:50:57.644336"
    }
  ]
}
}
```

##  Sync Master data-get service

This service will provides the list of all master data. This service is used mainly by the Enrollment client module. 

### Resource URL
### GET /masterdata

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
regcenterId|Yes|Registration center id| |
macaddress|No|MAC address of the machine| | 
serialnumber|No|serial number of the machine| | 
lastUpdated|No|Date in UTC ISO format| | 

### Example Request

v1/syncdata/masterdata/10001?macaddress=e1:01:2b:c2:1d:b0&serialnumber=NM5328114630

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response": {
		"lastSyncTime": "2019-03-04T12:34:15.477Z",
		 "registrationCenter": [
    {
      "id": "10007",
      "name": "Center Sidi Taibi",
      "centerTypeCode": "REG",
      "addressLine1": "Rabat Road",
      "addressLine2": "Sidi Taibi",
      "addressLine3": "Morroco",
      "latitude": "34.192861",
      "longitude": "-6.683662",
      "locationCode": "14025",
      "holidayLocationCode": "KTA",
      "contactPhone": "811552880",
      "numberOfStations": null,
      "workingHours": "8:00:00",
      "numberOfKiosks": 1,
      "perKioskProcessTime": "00:15:00",
      "centerStartTime": "09:00:00",
      "centerEndTime": "17:00:00",
      "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
      "contactPerson": "Monty Carlo",
      "lunchStartTime": "13:00:00",
      "lunchEndTime": "14:00:00",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterTypes": [
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "REG",
      "name": "Ordinaire",
      "descr": "Centre dinscription régulière"
    }
  ],
  "machineDetails": [
    {
      "id": "10007",
      "name": "Machine 7",
      "serialNum": "LK8186452621",
      "macAddress": "6d:a6:30:56:66:9f",
      "ipAddress": "192.168.0.227",
      "machineSpecId": "1001",
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "machineSpecification": [
    {
      "id": "1001",
      "name": "ستر  ",
      "brand": "دلّ  ",
      "model": "3568",
      "machineTypeCode": "DKS",
      "minDriverversion": "1.454",
      "description": "لأخذ التسجيلات",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    }
  ],
  "machineType": [
    {
      "code": "DKS",
      "name": "الحاسوب",
      "description": "أجهزة الكمبيوتر المكتبية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    }
  ],
  "devices": [
    {
      "id": "3000027",
      "name": "Finger Print Scanner 7",
      "serialNum": "CX8481464983",
      "deviceSpecId": "165",
      "macAddress": "d4:98:44:dd:aa:f1",
      "ipAddress": null,
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "deviceTypes": [
    {
      "code": "FRS",
      "name": "Finger Print Scanner",
      "description": "For scanning fingerprints",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "deviceSpecifications": [
    {
      "id": "165",
      "name": "Fingerprint Scanner",
      "brand": "Safran Morpho",
      "model": "1300 E2",
      "deviceTypeCode": "FRS",
      "minDriverversion": "1.12",
      "description": "To scan fingerprint",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "holidays": [
    {
      "holidayId": "2000049",
      "holidayDate": "2019-01-01",
      "holidayDay": "2",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "Jour de l’an",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    }
  ],
  "documentCategories": [
    {
      "code": "POA",
      "name": "Proof of Address",
      "description": "Address Proof",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "documentTypes": [
    {
      "code": "CIN",
      "name": "CNIE card",
      "description": "Moroccan National Electronic ID Card",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "validDocumentMapping": [
    {
      "docTypeCode": "CIN",
      "docCategoryCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "templates": [
    {
      "id": "1101",
      "name": "Template for authorization content",
      "description": "Template for authorization content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name\nYour Authentication of UIN $uin using $authType on $date at $time Hrs $status at a device deployed by MOSIP Services",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "auth-email-content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "templatesTypes": [
    {
      "code": "auth-email-content",
      "description": "Template for authorization content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "templateFileFormat": [
    {
      "code": "txt",
      "description": "Text File",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "reasonCategory": [
    {
      "code": "MNA",
      "name": "Manual Adjudication",
      "description": "Rejection during Manual Adjudication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "reasonList": [
    {
      "code": "APM",
      "name": "Age-Photo Mismatch",
      "description": "Mismatch between the Age and Photo",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "blackListedWords": [
    {
      "word": "shit",
      "description": "Blacklisted Word",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "locationHierarchy": [
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MOR",
      "name": "الْـمَغْرِبُ",
      "hierarchyLevel": 0,
      "hierarchyName": "بلد",
      "parentLocCode": null,
      "createdBy": null,
      "updatedBy": null
    }
  ],
  "biometricattributes": [
    {
      "code": "LTM",
      "name": "Left Thumb",
      "description": "Print of Left Thumb",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "biometricTypes": [
    {
      "code": "FNR",
      "name": "Fingerprint",
      "description": "Finger prints of the applicant",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "applications": [
    {
      "code": "app01",
      "name": "application 1",
      "description": "app description",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "applicantValidDocuments": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "001",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    }
  ],
  "individualTypes": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "FR",
      "name": "Foreigner"
    }
  ],
  "appDetails": [
    {
      "id": "10001",
      "name": "Pre-Registration",
      "descr": "Web portal for pre-registrations",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    }
  ],
  "appRolePriorities": [
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "SUPERADMIN",
      "priority": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    }
  ],
  "screenAuthorizations": [
    {
      "screenId": "approveRegistrationRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "processList": [
    {
      "id": "login_auth",
      "name": "Login authentication",
      "descr": "Login authentication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachines": [
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterDevices": [
    {
      "regCenterId": "10007",
      "deviceId": "3000027",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachineDevices": [
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000027",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterUserMachines": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "cntrId": "10007",
      "machineId": "10007",
      "usrId": "110007"
    }
  ],
  "registrationCenterUsers": [
    {
      "regCenterId": "10007",
      "userId": "110007",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachineHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "effectivetimes": "2019-02-27T10:50:57.626598"
    }
  ],
  "registrationCenterDeviceHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "deviceId": "3000027",
      "effectivetimes": "2019-02-27T10:50:57.589Z"
    }
  ],
  "registrationCenterMachineDeviceHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000027",
      "effectivetimes": "2019-02-27T10:50:57.607964"
    }
  ],
  "registrationCenterUserMachineMappingHistory": [
    {
      "cntrId": "10007",
      "machineId": "10007",
      "usrId": "110007",
      "effectivetimes": "2019-02-27T10:50:57.660Z"
    }
  ],
  "registrationCenterUserHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCntrId": "10007",
      "userId": "110007",
      "effectDateTimes": "2019-02-27T10:50:57.644336"
    }
  ]
}
}
```

## Config details-get service

This service will return back the global and registration configuration data of the MOSIP platform. 

### Resource URL
### GET /configs

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

v1/syncdata/configs

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
	"response": {
	  "registrationConfiguration": {
		"keyValidityPeriodPreRegPack": "3",
		"smsNotificationTemplateRegCorrection": "OTP for your request is $otp",
		"defaultDOB": "1-Jan",
		"smsNotificationTemplateOtp": "OTP for your request is $otp",
		"supervisorVerificationRequiredForExceptions": "true",
		"keyValidityPeriodRegPack": "3",
		"irisRetryAttempts": "10",
		"fingerprintQualityThreshold": "120",
		"multifactorauthentication": "true",
		"smsNotificationTemplateUpdateUIN": "OTP for your request is $otp",
		"supervisorAuthType": "password",
		"maxDurationRegPermittedWithoutMasterdataSyncInDays": "10",
		"modeOfNotifyingIndividual": "mobile",
		"emailNotificationTemplateUpdateUIN": "Hello $user the OTP is $otp",
		"maxDocSizeInMB": "150",
		"emailNotificationTemplateOtp": "Hello $user the OTP is $otp",
		"emailNotificationTemplateRegCorrection": "Hello $user the OTP is $otp",
		"faceRetry": "12",
		"noOfFingerprintAuthToOnboardUser": "10",
		"smsNotificationTemplateLostUIN": "OTP for your request is $otp",
		"supervisorAuthMode": "IRIS",
		"operatorRegSubmissionMode": "fingerprint",
		"officerAuthType": "password",
		"faceQualityThreshold": "25",
		"gpsDistanceRadiusInMeters": "3",
		"automaticSyncFreqServerToClient": "25",
		"maxDurationWithoutMasterdataSyncInDays": "7",
		"loginMode": "bootable dongle",
		"irisQualityThreshold": "25",
		"retentionPeriodAudit": "3",
		"fingerprintRetryAttempts": "234",
		"emailNotificationTemplateNewReg": "Hello $user the OTP is $otp",
		"passwordExpiryDurationInDays": "3",
		"emailNotificationTemplateLostUIN": "Hello $user the OTP is $otp",
		"blockRegistrationIfNotSynced": "10",
		"noOfIrisAuthToOnboardUser": "10",
		"smsNotificationTemplateNewReg": "OTP for your request is $otp"
	  },
	  "globalConfiguration": {
		"mosip.kernel.email.max-length": "50",
		"mosip.kernel.email.domain.ext-max-lenght": "7",
		"mosip.kernel.rid.sequence-length": "5",
		"mosip.kernel.uin.uin-generation-cron": "0 * * * * *",
		"mosip.kernel.email.special-char": "!#$%&'*+-/=?^_`{|}~.",
		"mosip.kernel.prid.sequence-limit": "3",
		"mosip.kernel.email.domain.ext-min-lenght": "2",
		"mosip.kernel.machineid.length": "4",
		"mosip.supported-languages": "eng,ara,fra",
		"auth.header.name": "Authorization",
		"mosip.kernel.phone.min-length": "9",
		"mosip.kernel.virus-scanner.host": "104.211.209.102",
		"mosip.kernel.email.min-length": "7",
		"mosip.kernel.uin.length.conjugative-even-digits-limit": "3",
		"mosip.kernel.rid.machineid-length": "5",
		"mosip.kernel.prid.repeating-block-limit": "3",
		"mosip.kernel.vid.length.repeating-block-limit": "2",
		"mosip.kernel.rid.length": "29",
		"mosip.kernel.uin.restricted-numbers": "786,666",
		"mosip.kernel.keygenerator.asymmetric-algorithm-name": "RSA ",
		"mosip.kernel.email.domain.special-char": "-",
		"mosip.kernel.vid.length.repeating-limit": "2",
		"mosip.kernel.uin.length.reverse-digits-limit": "5",
		"mosip.kernel.vid.not-start-with": "0,1",
		"mosip.kernel.registrationcenterid.length": "4",
		"mosip.kernel.phone.special-char": "+ -",
		"mosip.kernel.uin.uins-to-generate": "200000",
		"mosip.kernel.vid.length": "16",
		"mosip.kernel.uin.length.repeating-block-limit": "2",
		"mosip.kernel.uin.length.sequence-limit": "3",
		"mosip.kernel.keygenerator.symmetric-algorithm-length": "256",
		"mosip.kernel.keygenerator.symmetric-algorithm-name": "AES",
		"mosip.kernel.crypto.symmetric-algorithm-name": "AES",
		"mosip.kernel.virus-scanner.port": "3310",
		"mosip.kernel.rid.centerid-length": "5",
		"mosip.kernel.uin.length.digits-limit": "5",
		"mosip.kernel.rid.timestamp-length": "14",
		"mosip.kernel.vid.length.sequence-limit": "3",
		"mosip.kernel.keygenerator.asymmetric-algorithm-length": "2048",
		"mosip.kernel.uin.min-unused-threshold": "100000",
		"auth.role.prefix": "ROLE_",
		"auth.server.validate.url": "https://integ.mosip.io/authmanager/validate_token",
		"mosip.kernel.prid.length": "14",
		"mosip.kernel.syncdata.registration-center-config-file": 
                "registration-${spring.profiles.active}.properties",
		"mosip.kernel.crypto.asymmetric-algorithm-name": "RSA",
		"mosip.kernel.uin.length": "12",
		"mosip.kernel.phone.max-length": "15",
		"mosip.kernel.prid.repeating-limit": "2",
	        "mosip.kernel.tokenid.length": "36",
		"mosip.kernel.tspid.length": "4",
		"mosip.kernel.syncdata.global-config-file": "application-${spring.profiles.active}.properties",
		"mosip.kernel.prid.not-start-with": "0,1",
		"mosip.kernel.tokenid.sequence-limit": "3",
		"mosip.kernel.uin.length.repeating-limit": "2",
		"mosip.kernel.data-key-splitter": "#KEY_SPLITTER#"
	  }
	}
}
```

## Get All Roles 

This service will return back the all roles of the applications. 

### Resource URL
### GET /roles


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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	   "roles": [
		  {
		  "roleId": "REGISTRATION_ADMIN",
		  "roleName": "REGISTRATION_ADMIN",
		  "roleDescription": "Registration administrator"
		},
		{
		  "roleId": "TSP",
		  "roleName": "TSP",
		  "roleDescription": "Trusted Service Provider"
		}
	  ]
	}
}		
```

## Get list of users and role-mapping 

This service will return back the list of users and its role-mapping based on the registration-center-id. 

### Resource URL
### GET /userdetails/{regid}


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
/userdetails/10001

### Example Response
```JSON

{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	   "userDetails": [
		 {
		  "userName": "110001",
		  "mail": "user@mosip.com",
		  "mobile": "987654321",
		  "langCode": null,
		  "userPassword": "e1NIQTI1Nn05SmN0UmJRb01OR0FOZzhxSzE2U0hsOW5xaGl0Q2VsTjBjME1CQi90RXlrPQ==",
		  "name": "user",
		  "roles": [
			"REGISTRATION_ADMIN"
		  ]
		}
	  ]
	}
}	
```
## Public key-get service

This service will provide the public key for the specific application fetched from key manager. 

### Resource URL
### GET /publickey

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
v1/syncdata/publickey/REGISTRATION?timeStamp=2018-12-09T06%3A39%3A03.683Z

### Example Response
```JSON

{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
		  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
		  "issuedAt": "2018-01-01T10:00:00",
		  "expiryAt": "2018-12-10T06:12:51.994"
	    }
}	
```


# UIN
## UIN-get service

* [GET /uin](#uin-get-service)

* [PUT /uin](#put-uin)

This service will return unused UIN from UIN pool 

### Resource URL
### `GET /uin`
 

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

v1/uingenerator/uin

### Example Response
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	  "uin": "734168915279"
	    }
}
```


## UIN- Status Update service

This service will update the issued UN status to Assigned or Unassigned(Unused).  

### Resource URL
### `PUT /uin`
 

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

PUT v1/uingenerator/uin
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request" : {
                 "uin":"5193698130",
                 "status":"ASSIGNED"
              }
}
```


### Example Response
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response": {
                 "uin":"5193698130",
                  "status":"ASSIGNED"
              }
}
```

# SMS Notification

* [POST /sms/send](#post-smssend)

## SMS Notification Post Service

This service will send request to SMS gateway. 

### Resource URL
### `POST /sms/send`


### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
message |Yes|Message in the SMS| | This is the sample SMS message
number |Yes|Mobile number to which the SMS have to be sent| | 743764398

### Example Request

v1/smsnotifier/sms/send

```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
   "request": {
		"message": "Your Booking Request accepted. B-Ref BI56793",
		"number": "89900074454"
	}
}

```

### Example Response
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response": {
	  "message": "Sms Request Sent",
	  "status": "success"
	}
}	
```

# Email Notification

* [POST /email/send](#post-emailsend)
## Email Notification Post Service

This service will send request to Email/SMTP Service. 

### Resource URL
### `POST /email/send`


### Resource details

Resource Details | Description
------------ | -------------
Request format | Form Data
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
mailTo |Yes|Mail ID of the recepient| |```mosip@mindtree.com```
mailCc |No|Mail ID of the recepient| |```mosip@mindtree.com```
mailSubject |Yes|Mail ID of the recepient| | Sample mail subject
mailContent |No|Mail ID of the recepient| | Sample mail content
attachments |No|Mail ID of the recepient| | multipart/formdata


### Example Request

v1/emailnotifier/email/send

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	  "message": "Email Request sent",
	  "status": "success"
	}
}	
```




# Audit Manager
Audits are events/transactions which need to be captured and stored to facilitate auditing. This data could further be used for reporting by the business.

This includes auditing various event types like System events (Periodic scans), Business events/transactions (Change in demo data), Security Events etc.

The Audit Manager component will receive a request to audit and store data, validate the request is from an authorized source, securely store the requested data and respond back with an acknowledgement of storage (Success/Failure). This component will also ensure non-auditable data is not stored.

It will also ensure audit data stored is archived based on the defined archival policy.

* [POST /audits](#post-audits)

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
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
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	  "status": true
	   }
}
```



# License Key Manager
TSPs call the IDA to authenticate the Individuals. There can be various service calls such as Demographic, biometric based authentications. Each service calls have the permission associated. When a service call comes to the IDA, a request is sent to the Kernel module to retrieve the permissions for the License Key.

This service facilitates generation of license key, mapping the license key to several permissions, and fetch permissions mapped to a license key.

## License Key Generation

This component generates a license key for a specified TSP ID.

* [POST /license/generate](#post-licensegenerate)

* [POST /license/permission](#post-licensepermission)

* [GET /license/permission](#get-licensepermission)

* [PUT /license/status](#put-licensestatus)


### Resource URL
### `POST /license/generate`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
licenseExpiryTime|Yes|The time at which the license will expire| |2019-03-07T10:00:00.000Z 
tspId|Yes|The TSP ID against which the license key generated will be mapped| |9837

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
		"licenseExpiryTime": "2019-03-07T10:00:00.000Z",
		"tspId": "9837"
	     }
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	  "licenseKey": "gR7Mw7tA7S7qifkf"
	}
}
```
## Mapping Permissions

This component maps various permissions provided to a specified license key.

### `POST /license/permission`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
licenseKey|Yes|The license key to which the permissions will be mapped| |gR7Mw7tA7S7qifkf 
tspId|Yes|The TSP ID against which the license key is mapped| |9837
permissions|Yes|The list of permissions that will be mapped to the TSP-licensekey mentioned.| |OTP Trigger

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
   "request": {
		"licenseKey": "gR7Mw7tA7S7qifkf",
		"permissions": [
			"OTP Trigger","OTP Authentication"
		],
		"tspId": "9837"
	}
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	  "status": "Mapped License with the permissions"
	    }
}
```

## Fetching Permissions 

This component fetches various permission mapped to a license key.

### `GET /license/permission`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
licenseKey|Yes|The license key for which the permissions need to be fetched| |gR7Mw7tA7S7qifkf 
tspId|Yes|The TSP ID against which the license key is mapped| |9837

### Example Request
```
license/permission?licenseKey=gR7Mw7tA7S7qifkf&tspId=9837
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
	     "permissions": [
		          "OTP Trigger",
		          "OTP Authentication"
	                   ]
	    }
}
```


## Change license key status

This service moves the status of the license key to SUSPENDED status.

### `PUT /license/status`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
licenseKey|Yes|The license key for which the permissions need to be fetched| |gR7Mw7tA7S7qifkf 
status|Yes|The status of the license key. It is an enumeration {ACTIVE, SUSPENDED, BLOCKED}| |ACTIVE

### Example Request
```
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
		"licensekey":"gR7Mw7tA7S7qifkf",
		"status":"ACTIVE"
	     }
}
```
### Example Response
Sample Success Response:

```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response" : {
		"message":"The status had been changed successfully. "
	     }
}	
```


Sample Error Response:

```JSON
{
  "id": "string",
  "version": "string",
  "responsetime": "2019-04-04T05:03:18.287Z",
  "metadata": null,
  "response": null,
  "errors": [
    {
      "errorCode": "PRG_PAM_APP_001",
     "message": "License key not found"
    }
  ]
}


# 11. Applicant type

These set of services does various operations regarding the applicant type.

## 11.1 Get applicant type

This service finds the Applicant type for the combination of Individual type code,Gender code ,DOB ,Biometric available and Language code. If there is a combination entry exists for these combinations, the corresponding Applicant Type code is returned. 

### Resource URL
### `POST /applicanttype/getApplicantType`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
individualTypeCode|Yes|The code of the individual type| -NA- |INDTYP_002
genderCode|Yes|The code of the Gender. | -NA- |ML
dateofbirth|Yes|Date of birth in UTC standard ISO8601 format| -NA- |2008-10-04T05:00:00.000Z
biometricAvailable|No|Is the biometric details available| -NA- |true
languagecode|Yes|Language code in ISO 639-2 standard| -NA- |eng

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
		"attributes": [{
				"attribute": "IndividualType",
				"value": "Foreigner"
			},
			{
				"attribute": "genderCode",
				"value": "ML"
			},
			{
				"attribute": "dateofbirth",
				"value": "2008-10-04T05:00:00.000Z"
			},
			{
				"attribute": "biometricAvailable",
				"value": true
			},
			{
				"attribute": "languagecode",
				"value": "eng"
			}
		]

	}
}
```

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response" : {
		"applicationtypecode": "APP-C-94"
	}
}
```


## 11.2 Get document category and types

This service returns the document category and the document types associated with a particular applicant type. 

### Resource URL
### `GET /applicanttype/getDocCatAndTyp?applicationtypecode=APP-C-94&languages=eng&language=fra'

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicantTypeCode|Yes|The code of the applicant type| -NA- |APP-C-94
languagecode|Yes|Language code in ISO 639-2 standard| -NA- |eng,ara

### Example Request
```JSON
-NA-
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response" : {
		"documentcategories": [
			{
				"id": "DOC_CAT_001", 
				"value": "POA", 
				"languagecode":"string",
				"documenttypes": [
					{
						"code": "code", 
						"name": "name", 
						"descr":"descr", 
						"lang_code":"lang_code", 
						"is_active":"is_active
					}
				]			
			}
		]
	}
}
```



## 11.3 Get document categories

This service returns the document categories for a particular applicant type. 

### Resource URL
### `GET /applicanttype/getDocCategories?applicationtypecode="APP-C-94"`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicantTypeCode|Yes|The code of the applicant type| -NA- |APP-C-94


### Example Request
NA
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response" : {
		"documentcategories": [
			{
				"id": "DOC_CAT_001", 
				"value": "POA", 
				"languagecode":"string",
			}
		]
	}
}
```



## 11.4 Is applicant type combination exists

This service checks whether the combination exists for a particular Applicanttype code, Document. 

### Resource URL
### `GET /applicanttype/isApplicantTypeExists/{applicationtypecode}/{docCategoryCode}/{docTypeCode}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicantTypeCode|Yes|The code of the applicant type| -NA- |APP-C-94
docCategoryCode|Yes|The code of the document category| -NA- |DOC_CAT_2
docTypeCode|Yes|The code of the document type| -NA- |DOC_TYP_E

### Example Request
```JSON
-NA-
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response" : {
		"isExists":true
	}
}
```


# 12. Individual types

These set of services does various operations regarding the Individual types.

## 12.1 Get all individual types

This service returns all the individual types. 

### Resource URL
### `GET /individualtype/getAllIndividualTypes`

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
```JSON
-NA-
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response": {
		"individualtypes": [{
			"code": "IND-C-94",
			"name": "Foreign Child",
			"lang_code": "eng",
			"is_active": true
		}]
	}
}
```


## 12.2 Get all individual types

These set of services does various operations regarding the Individual types.

### Resource URL
### `GET /individualtype/getIndividualTypes/{individualTypeCode}/{languagecode}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
individualTypeCode|Yes|The code of the individual type| -NA- |IND-C-94
languagecode|Yes|Language code in ISO 639-2 standard| -NA- |eng

### Example Request
```JSON
-NA-
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
"response" : {
		"individualtype": {
			"code": "IND-C-94",
			"name": "Foreign Child",
			"lang_code": "eng",
			"is_active": true
		}
	}
}
```


# 13. Digital signatures

#### Background

Digital signatures are needed in various places of the MOSIP system. Few example can be, in the Registration client, the operator like to digitally sign the packet. Or, every request from the server can be digitally once again signed by the server. 

#### Solution



**The key solution considerations are**

- Following are the steps to digitally sign the services in the system, 

1. Create a hash for the web service response using cryptomanager APIs. 

2. Encrypt the hash using the existing "/cryptomanager/v1.0/encrypt" service can be used. In the "referenceId", the value as "HASH" can be passed.

3. Once the has is encrypted, the encrypted hash is sent as part of the header. 

4. The client is supposed to have the latest public key which is active on that date. 

5. Signature have to be enforced in the all the API's which the server hosts. 

- Create a common utility java project which creates the signature. 

- Use this common utility project, attach the signature in all the response. 



**Module diagram**



![Module Diagram](_images/kernel-cryptography-digitalsignature.jpeg)



## Implementation


**kernel-cryptography-digitalsignature** [README](../../../kernel/kernel-cryptography-digitalsignature/README.md)


# 14. Static Token generator

## 14.1 Get static token

This service returns a static token for the requested UIN and Partner ID. It will return the same Static Token for every call made with the same UIN and Partner ID. 

### Resource URL
### `GET tokenidgenerator/{uin}/{partnercode}`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
UIN|Yes|UIN of the individual.| -NA- |2345346532564566
partnercode|Yes|ID of the partner.| -NA- |9373

### Example Request
```JSON
-NA-
```
### Example Response

#### Success response
```JSON
{
	"id": "mosip.kernel.tokenid.generate",
	"version": "1.0",
	"metadata": {},
	"responsetime": "2019-04-04T05:03:18.287Z",
	"response": {
                  "tokenID": "268177021248100621690339355202974361"
                     },
        "errors": []
}
```


#### Failure response
```JSON
{
	"id": "mosip.kernel.tokenid.generate",
	"version": "1.0",
	"metadata": {},
	"responsetime": "2019-04-04T05:03:18.287Z",
	"response": null,
        "errors": [
            {
             "errorCode": "KER-TIG-010",
             "message": "UIN and partner code cannot be empty"
            }
     ]
}
```