[1. Key Manager Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#1-key-manager)

[2. Crypto Manager Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#2-crypto-manager)

[3. Data Sync Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#3-sync-data)

[4. UIN Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#4-uin)

[5. SMS Notification Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#5-sms-notification)

[6. Email Notification Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#6-email-notification)

[7. OTP Manager Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#7-otp-manager)

[8. Audit Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#8-audit-manager)

[9. License Key Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#9-license-key-manager)

[10. OTP Notification Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#10-otp-notification)

[11. Applicant Types Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#11-applicant-type)

[12. Individual Types Service](https://github.com/mosip/mosip/wiki/Kernel-APIs#12-individual-types)

[13. UIN acknowledgement service](https://github.com/mosip/mosip/wiki/Kernel-APIs#13-uin-acknowledgement-service)


# 1. Key Manager
## 1.1 Public key-get service

This service will provide the public key for the specific application. 

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
	"id": "mosip.keymanager.publickey",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
		  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
		  "issuedAt": "2018-01-01T10:00:00",
		  "expiryAt": "2018-12-10T06:12:51.994"
		}
	}
}
```

## 1.2 Decrypt Symmetric key

This service will decrypt the encrypted symmetric key 

### Resource URL
### `POST /decrypt`

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

/keymanager/v1.0/decrypt

```
{
	"id": "mosip.keymanager.decrypt",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		  "applicationId": "REGISTRATION",
		  "encryptedSymmetricKey": "encryptedSymmetricKey",
		  "referenceId": "REF01",
		  "timeStamp": "2018-12-10T06:12:52.994Z"
	}
}
```



### Example Response
```JSON

{
	"id": "mosip.keymanager.decrypt",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
		"symmetricKey": "decryptedSymmetricKey"
	}
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
	"id": "mosip.cryptomanager.encrypt",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
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
	"id": "mosip.keymanager.encrypt",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
		"data": "wk4RM2su2lBXuhx3_EtBijXTDp0Y20fJA6tmoONPjr6YBLqwu_YRWiSa10o-bQWesb-IobxPg-KsZq-Gc0L6Rq6besw-rMavg5a5nPU7b3pAug0N6Ek4B7S8v_tc5cu7LBRdBv1mRSS2onxXbT2R4qeEwl_11KtxPs_ek6g4vV6oEQRem2fPhop_21DaoWVEZFovHAAJDqSFj3R38A-fxvHHpVSa9BRTe-DeTKj_xZsNYXQixZR3jMdijtm8Q7lIT3E1x8LYp-hG3RhR_xC7trAOTqilzLjLfirE3Wjfor5bhLiG9eZyTb52ihKsDV1l2oBAhn9Aao_fYl3UD5QekSNLRVlfU1BMSVRURVIjeKen-3j5KhnE-93Qfe_pBfMBIKEkTJJ7pR-4cO7l-X0"
	}
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
	"id": "mosip.cryptomanager.decrypt",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
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
	"id": "mosip.cryptomanager.decrypt",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
		"data": "string"
	}
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

/syncdata/v1.0/masterdata/10001

### Example Response
```JSON
{
	"id": "mosip.sync.getmasterdata",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
		"lastSyncTime": "2019-03-04T12:34:15.477Z",
		"registrationCenter": [{
			"id": "10001",
			"name": "المركز أ بن منصور",
			"centerTypeCode": "REG",
			"addressLine1": "P4238",
			"addressLine2": "بن منصور",
			"addressLine3": " المغرب",
			"latitude": "35.52117",
			"longitude": "-6.453276",
			"locationCode": "14022",
			"holidayLocationCode": "KTA",
			"contactPhone": "944945765",
			"numberOfStations": null,
			"workingHours": "8:00:00",
			"numberOfKiosks": 1,
			"perKioskProcessTime": "00:15:00",
			"centerStartTime": "09:00:00",
			"centerEndTime": "17:00:00",
			"timeZone": "(GTM+01:00) توقيت وسط أوروبا",
			"contactPerson": "جهن د ",
			"lunchStartTime": "13:00:00",
			"lunchEndTime": "14:00:00",
			"isDeleted": null,
			"langCode": "ara",
			"isActive": true
		}],
		"registrationCenterTypes": [{
			"isDeleted": null,
			"langCode": "fra",
			"isActive": true,
			"code": "REG",
			"name": "Ordinaire",
			"descr": "Centre dinscription régulière"
		}],
		"machineDetails": [{
			"id": "10001",
			"name": "Machine 1",
			"serialNum": "NM5328114630",
			"macAddress": "e1:01:2b:c2:1d:b0",
			"ipAddress": "192.168.0.150",
			"machineSpecId": "1001",
			"validityDateTime": null,
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"machineSpecification": [{
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
		}],
		"machineType": [{
			"code": "DKS",
			"name": "الحاسوب",
			"description": "أجهزة الكمبيوتر المكتبية",
			"isDeleted": null,
			"langCode": "ara",
			"isActive": true
		}],
		"devices": [{
			"id": "3000021",
			"name": "Finger Print Scanner 1",
			"serialNum": "SZ5912878988",
			"deviceSpecId": "165",
			"macAddress": "85:bb:97:4b:14:05",
			"ipAddress": null,
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"deviceTypes": [{
			"code": "CMR",
			"name": "Camera",
			"description": "For capturing photo",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"deviceSpecifications": [{
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
		}],
		"holidays": [{
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
		}],
		"documentCategories": [{
			"code": "POA",
			"name": "Proof of Address",
			"description": "Address Proof",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"documentTypes": [{
			"code": "CIN",
			"name": "CNIE card",
			"description": "Moroccan National Electronic ID Card",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"validDocumentMapping": [{
			"docTypeCode": "CIN",
			"docCategoryCode": "POI",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"templates": [{
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
		}],
		"templatesTypes": [{
			"code": "auth-email-content",
			"description": "Template for authorization content",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"templateFileFormat": [{
			"code": "txt",
			"description": "Text File",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"reasonCategory": [{
			"code": "MNA",
			"name": "Manual Adjudication",
			"description": "Rejection during Manual Adjudication",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"reasonList": [{
			"code": "APM",
			"name": "Age-Photo Mismatch",
			"description": "Mismatch between the Age and Photo",
			"rsnCatCode": "CLR",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"blackListedWords": [{
			"word": "shit",
			"description": "Blacklisted Word",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"locationHierarchy": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"code": "MOR",
			"name": "Morroco",
			"hierarchyLevel": 0,
			"hierarchyName": "Country",
			"parentLocCode": null,
			"createdBy": null,
			"updatedBy": null
		}],
		"biometricattributes": [{
				"code": "LTM",
				"name": "Left Thumb",
				"description": "Print of Left Thumb",
				"biometricTypeCode": "FNR",
				"isDeleted": null,
				"langCode": "eng",
				"isActive": true
			},
			{
				"code": "PTT",
				"name": "صور",
				"description": "طباعة الصور",
				"biometricTypeCode": "PHT",
				"isDeleted": null,
				"langCode": "ara",
				"isActive": true
			}
		],
		"biometricTypes": [{
			"code": "FNR",
			"name": "Fingerprint",
			"description": "Finger prints of the applicant",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"applications": [{
			"code": "1111",
			"name": "Pre_Reg",
			"description": "string",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"idTypes": [{
			"code": "UIN",
			"name": "Unique Identification Number",
			"descr": "National ID given to the applicant",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"titles": [{
			"code": "MIR",
			"titleName": "Mr",
			"titleDescription": "Male Title",
			"langCode": "eng",
			"isDeleted": null,
			"isActive": true
		}],
		"genders": [{
			"code": "MLE",
			"genderName": "Male",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"languages": [{
			"code": "eng",
			"name": "English",
			"family": "Indo-European",
			"nativeName": "English",
			"isDeleted": null,
			"isActive": true
		}],
		"applicantValidDocuments": [{
			"appTypeCode": "001",
			"docTypeCode": "CIN",
			"docCatCode": "POI",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"individualTypes": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"code": "FR",
			"name": "Foreigner"
		}],
		"registrationCenterMachines": [{
			"regCenterId": "10001",
			"machineId": "10001",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"registrationCenterDevices": [{
			"regCenterId": "10001",
			"deviceId": "3000021",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"registrationCenterMachineDevices": [{
			"regCenterId": "10001",
			"machineId": "10001",
			"deviceId": "3000021",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"registrationCenterUserMachines": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"cntrId": "10001",
			"machineId": "10001",
			"usrId": "110001"
		}],
		"registrationCenterUsers": [{
			"regCenterId": "10001",
			"userId": "110001",
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true
		}],
		"registrationCenterMachineHistory": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"regCenterId": "10001",
			"machineId": "10001",
			"effectivetimes": "2019-02-28T10:24:38.460784"
		}],
		"registrationCenterDeviceHistory": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"regCenterId": "10001",
			"deviceId": "3000021",
			"effectivetimes": "2019-02-28T10:24:38.420Z"
		}],
		"registrationCenterMachineDeviceHistory": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"regCenterId": "10001",
			"machineId": "10001",
			"deviceId": "3000021",
			"effectiveDateTime": null
		}],
		"registrationCenterUserMachineMappingHistory": [{
			"cntrId": "10001",
			"machineId": "10001",
			"usrId": "110001",
			"effectivetimes": "2019-02-28T10:24:38.496Z"
		}],
		"registrationCenterUserHistory": [{
			"isDeleted": null,
			"langCode": "eng",
			"isActive": true,
			"regCntrId": "10001",
			"userId": "110001",
			"effectDateTimes": "2019-02-28T10:24:38.478467"
		}]
	}
}
```


## 3.2 Sync Master data-get service

### `GET /masterdata`

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

/syncdata/v1.0/masterdata?macaddress=6d:a6:30:56:66:9f&serialnumber=LK8186452621

### Example Response
```JSON
{
	"id": "mosip.sync.getmasterdata",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
  "lastSyncTime": "2019-03-20T04:53:51.487Z",
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
    },
    {
      "id": "10007",
      "name": "centre Sidi Taibi",
      "centerTypeCode": "REG",
      "addressLine1": "Route de Rabat",
      "addressLine2": "Sidi Taibi",
      "addressLine3": "Maroc",
      "latitude": "34.192861",
      "longitude": "-6.683662",
      "locationCode": "14025",
      "holidayLocationCode": "KTA",
      "contactPhone": "753640112",
      "numberOfStations": null,
      "workingHours": "8:00:00",
      "numberOfKiosks": 1,
      "perKioskProcessTime": "00:15:00",
      "centerStartTime": "09:00:00",
      "centerEndTime": "17:00:00",
      "timeZone": "GTM + 01h00) HEURE EUROPEENNE CENTRALE",
      "contactPerson": "Monty Carlo",
      "lunchStartTime": "13:00:00",
      "lunchEndTime": "14:00:00",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "10007",
      "name": "مركز  سيدي الطيبي ",
      "centerTypeCode": "REG",
      "addressLine1": "الرباط طريق",
      "addressLine2": "سيدي الطيبي",
      "addressLine3": " المغرب",
      "latitude": "34.192861",
      "longitude": "-6.683662",
      "locationCode": "14025",
      "holidayLocationCode": "KTA",
      "contactPhone": "680758944",
      "numberOfStations": null,
      "workingHours": "8:00:00",
      "numberOfKiosks": 1,
      "perKioskProcessTime": "00:15:00",
      "centerStartTime": "09:00:00",
      "centerEndTime": "17:00:00",
      "timeZone": "(GTM+01:00) توقيت وسط أوروبا",
      "contactPerson": "منتي َرل  ",
      "lunchStartTime": "13:00:00",
      "lunchEndTime": "14:00:00",
      "isDeleted": null,
      "langCode": "ara",
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
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "REG",
      "name": "Regular",
      "descr": "Regular Registration Center"
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "REG",
      "name": "منتظم",
      "descr": "مركز التسجيل العادي"
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
    },
    {
      "id": "1001",
      "name": "Vostro",
      "brand": "Dell",
      "model": "3568",
      "machineTypeCode": "DKS",
      "minDriverversion": "1.454",
      "description": "To take enrollments",
      "isDeleted": null,
      "langCode": "eng",
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
    },
    {
      "code": "DKS",
      "name": "Dekstop",
      "description": "Desktop Computer",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "DKS",
      "name": "Ordinateur",
      "description": "Ordinateurs de bureau",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "id": "3000047",
      "name": "IRIS Scanner 7",
      "serialNum": "UV7414544701",
      "deviceSpecId": "327",
      "macAddress": "bb:dc:5f:96:f3:27",
      "ipAddress": null,
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000067",
      "name": "Web Camera 7",
      "serialNum": "T808S5482593162",
      "deviceSpecId": "736",
      "macAddress": "ed:e0:cf:f5:84:20",
      "ipAddress": null,
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000087",
      "name": "Document Scanner 7",
      "serialNum": "FA289M3966558",
      "deviceSpecId": "801",
      "macAddress": "11:12:fc:9b:04:32",
      "ipAddress": null,
      "validityDateTime": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000107",
      "name": "Printer 7",
      "serialNum": "AA786R5772199",
      "deviceSpecId": "920",
      "macAddress": "04:fb:9c:f4:20:16",
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
    },
    {
      "code": "FRS",
      "name": "ماسح بصمة الأصبع",
      "description": "لمسح بصمات الأصابع",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "FRS",
      "name": "Scanner dempreintes digitales",
      "description": "Scannez les empreintes digitales",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "IRS",
      "name": "Iris Scanner",
      "description": "For scanning Iris",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "IRS",
      "name": "ايريس الماسح الضوئي",
      "description": "لمسح القزحية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "IRS",
      "name": "Scanner dIris",
      "description": "Pour scanner liris",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "CMR",
      "name": "Camera",
      "description": "For capturing photo",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "CMR",
      "name": "الة تصوير",
      "description": "لالتقاط الصور",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "CMR",
      "name": "Caméra",
      "description": "Pour capturer une photo",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "SCN",
      "name": "Document Scanner",
      "description": "For scanning documents",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "SCN",
      "name": "وثيقة الماسح الضوئي",
      "description": "لمسح المستندات ضوئيًا",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "SCN",
      "name": "Scanner de documents",
      "description": "Pour numériser des documents",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "PRT",
      "name": "Printer",
      "description": "For printing Documents",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "PRT",
      "name": "طابعة",
      "description": "لطباعة الوثائق",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "PRT",
      "name": "Imprimante",
      "description": "Pour imprimer des documents",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "id": "165",
      "name": "فِنرِّنت سCَنّر ",
      "brand": "سافران مورفو",
      "model": "1301 E2",
      "deviceTypeCode": "FRS",
      "minDriverversion": "1.12",
      "description": "لمسح بصمة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "327",
      "name": "High Speed Dual Iris Scanner",
      "brand": "Cogent ",
      "model": "3M ",
      "deviceTypeCode": "IRS",
      "minDriverversion": "2.34",
      "description": "To scan iris",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "327",
      "name": "هِغ سد دَُل ِرِس سCَنّر",
      "brand": "نّت",
      "model": "3M ",
      "deviceTypeCode": "IRS",
      "minDriverversion": "2.34",
      "description": "لمسح قزحية العين",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "736",
      "name": "Webcam ",
      "brand": "Logitech ",
      "model": "C270 ",
      "deviceTypeCode": "CMR",
      "minDriverversion": "2.086",
      "description": "To capture photo",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "736",
      "name": "وبَم   ",
      "brand": "لِته   ",
      "model": "C270 ",
      "deviceTypeCode": "CMR",
      "minDriverversion": "2.086",
      "description": "لالتقاط صورة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "801",
      "name": "imageFORMULA ",
      "brand": "Canon ",
      "model": "DR-C130",
      "deviceTypeCode": "SCN",
      "minDriverversion": "1.02",
      "description": "To scan documents",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "801",
      "name": "مَفرمُلَ   ",
      "brand": "َنّ",
      "model": "DR-C131",
      "deviceTypeCode": "SCN",
      "minDriverversion": "1.02",
      "description": "لمسح المستندات ضوئيًا",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "920",
      "name": "Single Function Inkjet ",
      "brand": "Canon ",
      "model": "TS207 ",
      "deviceTypeCode": "PRT",
      "minDriverversion": "1.123",
      "description": "To print documents",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "920",
      "name": "سِنل فُنتٍ ِنكجت",
      "brand": "َنّ",
      "model": "TS207 ",
      "deviceTypeCode": "PRT",
      "minDriverversion": "1.123",
      "description": "لطباعة الوثائق",
      "isDeleted": null,
      "langCode": "ara",
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
    },
    {
      "holidayId": "2000001",
      "holidayDate": "2019-01-01",
      "holidayDay": "2",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "New Year's Day",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000025",
      "holidayDate": "2019-01-01",
      "holidayDay": "2",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "الميلادية رأس السنة",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000050",
      "holidayDate": "2019-01-11",
      "holidayDay": "5",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "Anniversaire du manifeste de l’indépendance",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000002",
      "holidayDate": "2019-01-11",
      "holidayDay": "5",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "Anniversary of the Independence Manifesto",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000026",
      "holidayDate": "2019-01-11",
      "holidayDay": "5",
      "holidayMonth": "1",
      "holidayYear": "2019",
      "holidayName": "الذكرى السنوية لإعلان الاستقلال",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000051",
      "holidayDate": "2019-05-01",
      "holidayDay": "3",
      "holidayMonth": "5",
      "holidayYear": "2019",
      "holidayName": "Fête du travail / May Day",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000003",
      "holidayDate": "2019-05-01",
      "holidayDay": "3",
      "holidayMonth": "5",
      "holidayYear": "2019",
      "holidayName": "Labour Day/May Day",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000027",
      "holidayDate": "2019-05-01",
      "holidayDay": "3",
      "holidayMonth": "5",
      "holidayYear": "2019",
      "holidayName": "عيد العمال/مايو يوم",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000004",
      "holidayDate": "2019-06-05",
      "holidayDay": "3",
      "holidayMonth": "6",
      "holidayYear": "2019",
      "holidayName": "Eid al-Fitr",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000052",
      "holidayDate": "2019-06-05",
      "holidayDay": "3",
      "holidayMonth": "6",
      "holidayYear": "2019",
      "holidayName": "Eid al-Fitr",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000028",
      "holidayDate": "2019-06-05",
      "holidayDay": "3",
      "holidayMonth": "6",
      "holidayYear": "2019",
      "holidayName": "عيد الفطر المبارك",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000005",
      "holidayDate": "2019-07-30",
      "holidayDay": "2",
      "holidayMonth": "7",
      "holidayYear": "2019",
      "holidayName": "Feast of the Throne",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000053",
      "holidayDate": "2019-07-30",
      "holidayDay": "2",
      "holidayMonth": "7",
      "holidayYear": "2019",
      "holidayName": "Fête du trône",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000029",
      "holidayDate": "2019-07-30",
      "holidayDay": "2",
      "holidayMonth": "7",
      "holidayYear": "2019",
      "holidayName": "عيد العرش",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000054",
      "holidayDate": "2019-08-12",
      "holidayDay": "1",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Aïd al-Adha",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000006",
      "holidayDate": "2019-08-12",
      "holidayDay": "1",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Eid al-Adha",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000030",
      "holidayDate": "2019-08-12",
      "holidayDay": "1",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "عيد الأضحى",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000055",
      "holidayDate": "2019-08-14",
      "holidayDay": "3",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Anniversaire de la récupération de Oued Ed-Dahab",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000007",
      "holidayDate": "2019-08-14",
      "holidayDay": "3",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Anniversary of the Recovery Oued Ed-Dahab",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000031",
      "holidayDate": "2019-08-14",
      "holidayDay": "3",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "الذكرى السنوية لاستعادة واد اد-دهب",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000056",
      "holidayDate": "2019-08-20",
      "holidayDay": "2",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Anniversaire de la révolution du roi et le peuple",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000008",
      "holidayDate": "2019-08-20",
      "holidayDay": "2",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Anniversary of the Revolution of the King and the People",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000032",
      "holidayDate": "2019-08-20",
      "holidayDay": "2",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "الذكرى السنوية لثورة الملك والشعب",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000057",
      "holidayDate": "2019-08-21",
      "holidayDay": "3",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Journée de la jeunesse",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000009",
      "holidayDate": "2019-08-21",
      "holidayDay": "3",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "Youth Day",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000033",
      "holidayDate": "2019-08-21",
      "holidayDay": "3",
      "holidayMonth": "8",
      "holidayYear": "2019",
      "holidayName": "يوم الشباب",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000058",
      "holidayDate": "2019-09-01",
      "holidayDay": "7",
      "holidayMonth": "9",
      "holidayYear": "2019",
      "holidayName": "Hégire nouvel an",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000010",
      "holidayDate": "2019-09-01",
      "holidayDay": "7",
      "holidayMonth": "9",
      "holidayYear": "2019",
      "holidayName": "Hijra New Year",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000034",
      "holidayDate": "2019-09-01",
      "holidayDay": "7",
      "holidayMonth": "9",
      "holidayYear": "2019",
      "holidayName": "العام الهجري الجديد",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000059",
      "holidayDate": "2019-11-06",
      "holidayDay": "3",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "Anniversaire de la marche verte",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000011",
      "holidayDate": "2019-11-06",
      "holidayDay": "3",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "Anniversary of the Green March",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000035",
      "holidayDate": "2019-11-06",
      "holidayDay": "3",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "الذكرى للمسيرة الخضراء",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000060",
      "holidayDate": "2019-11-10",
      "holidayDay": "7",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "Anniversaire de Mohammed",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000012",
      "holidayDate": "2019-11-10",
      "holidayDay": "7",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "The Prophet Muhammad's Birthday",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000036",
      "holidayDate": "2019-11-10",
      "holidayDay": "7",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "عيد ميلاد النبي محمد",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "holidayId": "2000061",
      "holidayDate": "2019-11-18",
      "holidayDay": "1",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "Fête de l’indépendance",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "holidayId": "2000013",
      "holidayDate": "2019-11-18",
      "holidayDay": "1",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "Independence Day",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "holidayId": "2000037",
      "holidayDate": "2019-11-18",
      "holidayDay": "1",
      "holidayMonth": "11",
      "holidayYear": "2019",
      "holidayName": "يوم الاستقلال",
      "locationCode": "KTA",
      "isDeleted": null,
      "langCode": "ara",
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
    },
    {
      "code": "POA",
      "name": "إثبات العنوان",
      "description": "عنوان الدليل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "POA",
      "name": "Un justificatif de domicile",
      "description": "Preuve dadresse",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "POI",
      "name": "Proof of Identity",
      "description": "Identity Proof",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "POI",
      "name": "إثبات هوية",
      "description": "إثبات الهوية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "POI",
      "name": "Preuve didentité",
      "description": "Preuve didentité",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "POR",
      "name": "Proof of Relationship",
      "description": "Proof Relationship of the person",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "POR",
      "name": "إثبات العلاقة",
      "description": "إثبات علاقة الشخص",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "POR",
      "name": "Preuve de relation",
      "description": "Preuve de relation de la personne",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "POB",
      "name": "Proof of Birth",
      "description": "Proof date of birth of the person",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "POB",
      "name": "إثبات الميلاد",
      "description": "تاريخ إثبات ميلاد الشخص",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "POB",
      "name": "Preuve de naissance",
      "description": "Preuve de la date de naissance de la personne",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "POE",
      "name": "Proof of Biometric Exception",
      "description": "Proof of Biometric Exception",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "POE",
      "name": "دليل استثناء البيومترية",
      "description": "دليل استثناء البيومترية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "POE",
      "name": "Preuve dexception biométrique",
      "description": "Preuve dexception biométrique",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "code": "CIN",
      "name": "نَتِنَل ِد",
      "description": "بطاقة الهوية الوطنية المغربية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "CIN",
      "name": "carte didentité",
      "description": "Carte didentité électronique nationale marocaine",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RNC",
      "name": "Rental contract",
      "description": "Rental Agreement of address",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RNC",
      "name": "عقد ايجار",
      "description": "اتفاق تأجير العنوان",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RNC",
      "name": "Contrat de location",
      "description": "Contrat de location dadresse",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "COR",
      "name": "Certificate of residence",
      "description": "Proof of Resident",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "COR",
      "name": "شهادة الاقامة",
      "description": "اثبات محل الاقامة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "COR",
      "name": "Certificat de résidence",
      "description": "Preuve de résidence",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "CRN",
      "name": "Certificate of Relationship",
      "description": "Proof relationship of a person",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "CRN",
      "name": "شهادة العلاقة",
      "description": "علاقة إثبات للشخص",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "CRN",
      "name": "Certificat de relation",
      "description": "Preuve de relation dune personne",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "COB",
      "name": "Certificate of Birth",
      "description": "Proof birth and age of a person",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "COB",
      "name": "شهادة الميلاد",
      "description": "إثبات الولادة وعمر الشخص",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "COB",
      "name": "Certificat de naissance",
      "description": "Preuve de naissance et âge dune personne",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "COE",
      "name": "Certification of Exception",
      "description": "Certificate of Exception",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "COE",
      "name": "شهادة استثناء",
      "description": "شهادة استثناء",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "COE",
      "name": "Certification dexception",
      "description": "Certification dexception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "PSP",
      "name": "جواز سفر",
      "description": "إثبات الهوية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "PSP",
      "name": "Passport",
      "description": "Proof of Idendity",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "PSP",
      "name": "Passeport",
      "description": "Preuve didentité",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "docTypeCode": "COB",
      "docCategoryCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "docTypeCode": "COR",
      "docCategoryCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "docTypeCode": "RNC",
      "docCategoryCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "docTypeCode": "CRN",
      "docCategoryCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "docTypeCode": "PSP",
      "docCategoryCode": "POI",
      "isDeleted": true,
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
    },
    {
      "id": "1102",
      "name": "Template for authorization subject",
      "description": "Template for authorization subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin Authentication $status",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "auth-email-subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1103",
      "name": "Template for authorization SMS",
      "description": "Template for authorization SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Your Authentication of UIN $uin using $authType on $date at $time Hrs $status at a device deployed by MOSIP Services.",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "auth-sms",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1104",
      "name": "Template for Email Content",
      "description": "Template for Email Content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name\nOTP for UIN  $uin is $otp and is valid for $validTime minutes. (Generated on $date at $time Hrs)",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "otp-email-content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1105",
      "name": "Template for Email Subject",
      "description": "Template for Email Subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin: OTP Request",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "otp-email-subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1106",
      "name": "Template for OTP in SMS ",
      "description": "Template for OTP in SMS ",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP for UIN  $uin is $otp and is valid for $validTime minutes. (Generated on $date at $time Hrs)",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "otp-sms",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1101",
      "name": "قالب لمحتوى التخويل",
      "description": "قالب لمحتوى التخويل",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP لـ UIN $uin هو $otp وهو صالح لمدة $validTime دقيقة. (التي تم إنشاؤها على $date في $time ساعات)",
      "moduleId": "10004",
      "moduleName": "مصادقة الهوية",
      "templateTypeCode": "auth-email-content",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1102",
      "name": "قالب لموضوع التخويل",
      "description": "قالب لموضوع التخويل",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin: Authentication $status",
      "moduleId": "10004",
      "moduleName": "مصادقة الهوية",
      "templateTypeCode": "auth-email-subject",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1103",
      "name": "قالب لرسالة التفويض",
      "description": "قالب لرسالة التفويض",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "لديك مصادقة UIN $uin باستخدام authType$ على date$ في time Hs $status$ في جهاز تم نشره بواسطة \"خدمات MOSIP\".",
      "moduleId": "10004",
      "moduleName": "مصادقة الهوية",
      "templateTypeCode": "auth-sms",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1104",
      "name": "قالب لمحتوى البريد الإلكتروني",
      "description": "قالب لمحتوى البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name\nOTP لـ UIN $uin هو $otp وهو صالح لمدة $validTime دقيقة. (التي تم إنشاؤها على $date في $time ساعات)",
      "moduleId": "10004",
      "moduleName": "مصادقة الهوية",
      "templateTypeCode": "otp-email-content",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1105",
      "name": "قالب لموضوع البريد الإلكتروني",
      "description": "قالب لموضوع البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin: OTP Request",
      "moduleId": "10004",
      "moduleName": "مصادقة الهوية",
      "templateTypeCode": "otp-email-subject",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1106",
      "name": "قالب كلمة المرور لمرة واحدة في الرسالة",
      "description": "قالب كلمة المرور لمرة واحدة في الرسالة",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP لـ UIN $uin هو $otp وهو صالح لمدة $validTime دقيقة. (التي تم إنشاؤها على $date في $time ساعات)",
      "moduleId": "10004",
      "moduleName": "مصادقة الهوية",
      "templateTypeCode": "otp-sms",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1101",
      "name": "Modèle de contenu dautorisation",
      "description": "Modèle de contenu dautorisation",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nVotre authentification UIN $uin utilisant $authType le $date à $time Hrs $status sur un périphérique déployé par \"MOSIP Services\"",
      "moduleId": "10004",
      "moduleName": "Authentification ID",
      "templateTypeCode": "auth-email-content",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1102",
      "name": "Modèle pour sujet dautorisation",
      "description": "Modèle pour sujet dautorisation",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin: $status dauthentification",
      "moduleId": "10004",
      "moduleName": "Authentification ID",
      "templateTypeCode": "auth-email-subject",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1103",
      "name": "Modèle de SMS dautorisation",
      "description": "Modèle de SMS dautorisation",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Votre authentification UIN $uin utilisant $authType le $date à $time Hrs $status sur un périphérique déployé par \"MOSIP Services\".",
      "moduleId": "10004",
      "moduleName": "Authentification ID",
      "templateTypeCode": "auth-sms",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1104",
      "name": "Modèle de contenu de courrier électronique",
      "description": "Modèle de contenu de courrier électronique",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nOTP pour UIN $uin est $otp et est valide pour $validTime minutes. (Généré le $date à $time Hrs)",
      "moduleId": "10004",
      "moduleName": "Authentification ID",
      "templateTypeCode": "otp-email-content",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1105",
      "name": "Modèle pour sujet demail",
      "description": "Modèle pour sujet demail",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin: Requête OTP",
      "moduleId": "10004",
      "moduleName": "Authentification ID",
      "templateTypeCode": "otp-email-subject",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1106",
      "name": "Modèle pour OTP dans SMS",
      "description": "Modèle pour OTP dans SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP pour UIN $uin est $otp et est valide pour $validTime minutes. (Généré le $date à $time Hrs)",
      "moduleId": "10004",
      "moduleName": "Authentification ID",
      "templateTypeCode": "otp-sms",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1107",
      "name": "Template for duplicate UIN Email",
      "description": "Template for duplicate UIN Email",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour Request for Registration $RID has failed because an UIN has been found against your details. Please visit your nearest Registration Office.\nAnd Visit https://mosip.io/grievances\n\nThanks and Regards,\nMOSIP Team",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_DUP_UIN_EMAIL",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1108",
      "name": "Template for duplicate UIN SMS",
      "description": "Template for duplicate UIN SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour Request for Registration $RID has failed because an UIN has been found against your details. Please visit your nearest Registration Office.\nAnd Visit https://mosip.io/grievances",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_DUP_UIN_SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1109",
      "name": "Template for Technical Issue Email",
      "description": "Template for Technical Issue Email",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour Request for Registration $RID has failed because of an Technical issue please visit your nearest Registration Office.\nAnd Visit https://mosip.io/grievances\n\nThanks and Regards,\nMOSIP Team",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_TEC_ISSUE_EMAIL",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1110",
      "name": "Template for Technical Issue SMS",
      "description": "Template for Technical Issue SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour Request for Registration $RID has failed because of an Technical issue please visit your nearest Registration Office.\nAnd Visit https://mosip.io/grievances",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_TEC_ISSUE_SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1111",
      "name": "Template for UIN generation Email",
      "description": "Template for UIN generation Email",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour UIN for the Registration $RID has been successfully generated and will reach soon at your Postal Address.\n\nThanks and Regards,\nMOSIP Team",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_GEN_EMAIL",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1112",
      "name": "Template for UIN generation SMS",
      "description": "Template for UIN generation SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour UIN for the Registration $RID has been successfully generated and will reach soon at your Postal Address.",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_GEN_SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1113",
      "name": "Template for update details Email",
      "description": "Template for update details Email",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour UIN details have been updated corresponding to the Registration Number $RID and a Physical Copy of your UIN will reach you soon at your Postal Address.\n\nThanks and Regards,\nMOSIP Team",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_UPD_EMAIL",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1114",
      "name": "Template for update Details SMS",
      "description": "Template for update Details SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Hi $name,\nYour UIN details have been updated corresponding to the Registration Number $RID and a Physical Copy of your UIN will reach you soon at your Postal Address.",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_UPD_SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1107",
      "name": "قالب لبريد إلكتروني مكرر الهوية",
      "description": "قالب لبريد إلكتروني مكرر الهوية",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nالخاص بك لأنه تم العثور على UIN مقابل بياناتك. يرجى زيارة أقرب مكتب تسجيل $RID فشل طلب التسجيل\nوزيارة https://mosip.io/grievances\n\nشكرا مع تحياتي،\nفريق MOSIP",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_DUP_UIN_EMAIL",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1108",
      "name": "قالب لرسالة الهوية المكررة",
      "description": "قالب لرسالة الهوية المكررة",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name،\nفشل طلب التسجيل $RID الخاص بك لأنه تم العثور على UIN مقابل بياناتك. يرجى زيارة أقرب مكتب تسجيل.\nوزيارة https://mosip.io/grievances",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_DUP_UIN_SMS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1109",
      "name": "نموذج للبريد الإلكتروني لمشكلة فنية",
      "description": "نموذج للبريد الإلكتروني لمشكلة فنية",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nشل طلب التسجيل $RID بسبب مشكلة فنية ، يرجى زيارة أقرب مكتب تسجيل.\nوزيارة https://mosip.io/grievances\n\nشكرا مع تحياتي،\nفريق MOSIP",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_TEC_ISSUE_EMAIL",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1110",
      "name": "قالب لرسالة المشكلة الفنية",
      "description": "قالب لرسالة المشكلة الفنية",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name،\nفشل طلب التسجيل $RID بسبب مشكلة فنية ، يرجى زيارة أقرب مكتب تسجيل.\nوزيارة https://mosip.io/grievances",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_TEC_ISSUE_SMS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1111",
      "name": "قالب لتوليد الهوية البريد الإلكتروني",
      "description": "قالب لتوليد الهوية البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name،\nتم إنشاء UIN الخاص بك للتسجيل $RID بنجاح وستصل قريبًا إلى العنوان البريدي الخاص بك.\n\nشكرا مع تحياتي،\nفريق MOSIP",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_UIN_GEN_EMAIL",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1112",
      "name": "قالب لرسالة توليد الهوية",
      "description": "قالب لرسالة توليد الهوية",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nتم إنشاء UIN الخاص بك للتسجيل $RID بنجاح وستصل قريبًا إلى العنوان البريدي الخاص بك.",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_UIN_GEN_SMS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1113",
      "name": "قالب للحصول على تفاصيل التحديث",
      "description": "قالب للحصول على تفاصيل التحديث",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nتم تحديث تفاصيل UIN الخاصة بك المقابلة لرقم التسجيل $RID وستصل إليك نسخة فعلية من UIN الخاصة بك على العنوان البريدي الخاص بك.\n\nشكرا مع تحياتي،\nفريق MOSIP",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_UIN_UPD_EMAIL",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1114",
      "name": "قالب لتحديث تفاصيل الرسالة",
      "description": "قالب لتحديث تفاصيل الرسالة",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nتم تحديث تفاصيل UIN الخاصة بك المقابلة لرقم التسجيل $RID وستصل إليك نسخة فعلية من UIN الخاصة بك على العنوان البريدي الخاص بك.",
      "moduleId": "10003",
      "moduleName": "معالج التسجيل",
      "templateTypeCode": "RPR_UIN_UPD_SMS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1107",
      "name": "Modèle de courrier didentité en double",
      "description": "Modèle de courrier didentité en double",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nVotre demande d'enregistrement $RID a échoué car un UIN a été trouvé contre vos coordonnées. Veuillez visiter votre bureau d'inscription le plus proche.\nEt visitez https://mosip.io/grievances\n\nMerci et salutations,\nÉquipe MOSIP",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_DUP_UIN_EMAIL",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1108",
      "name": "Modèle de message didentité en double",
      "description": "Modèle de message didentité en double",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nVotre demande d'enregistrement $RID a échoué car un UIN a été trouvé contre vos coordonnées. Veuillez visiter votre bureau d'inscription le plus proche.\nEt visitez https://mosip.io/grievances",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_DUP_UIN_SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1109",
      "name": "Modèle pour courrier électronique de problème technique",
      "description": "Modèle pour courrier électronique de problème technique",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nVotre demande d'enregistrement $RID a échoué à cause d'un problème technique, veuillez vous rendre au bureau d'inscription le plus proche.\nEt visitez https://mosip.io/grievances\n\nMerci et salutations,\nÉquipe MOSIP",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_TEC_ISSUE_EMAIL",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1110",
      "name": "Modèle de message de problème technique",
      "description": "Modèle de message de problème technique",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nVotre demande d'enregistrement $RID a échoué à cause d'un problème technique, veuillez vous rendre au bureau d'inscription le plus proche.\nEt visitez https://mosip.io/grievances",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_TEC_ISSUE_SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1111",
      "name": "Modèle de courrier électronique de génération didentité",
      "description": "Modèle de courrier électronique de génération didentité",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nVotre UIN pour l'enregistrement $RID a été généré avec succès et vous parviendra sous peu à votre adresse postale.\n\nMerci et salutations,\nÉquipe MOSIP",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_UIN_GEN_EMAIL",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1112",
      "name": "Modèle de message de génération didentité",
      "description": "Modèle de message de génération didentité",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nVotre UIN pour l'enregistrement $RID a été généré avec succès et vous parviendra sous peu à votre adresse postale.",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_UIN_GEN_SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1113",
      "name": "Modèle pour les détails de la mise à jour Email",
      "description": "Modèle pour les détails de la mise à jour Email",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nLes détails de votre UIN correspondant au numéro d’enregistrement $RID ont été mis à jour et une copie physique de votre UIN vous parviendra sous peu à votre adresse postale.\n\nMerci et salutations,\nÉquipe MOSIP",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_UIN_UPD_EMAIL",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1114",
      "name": "Modèle pour la mise à jour Détails Message",
      "description": "Modèle pour la mise à jour Détails Message",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Bonjour $name,\nLes détails de votre UIN correspondant au numéro d’enregistrement $RID ont été mis à jour et une copie physique de votre UIN vous parviendra sous peu à votre adresse postale.",
      "moduleId": "10003",
      "moduleName": "Processeur dinscription",
      "templateTypeCode": "RPR_UIN_UPD_SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1115",
      "name": "Template for new registration Email Content",
      "description": "Template for new registration Email Content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name, \nThank you for registering with the digital identity platform. Your registration id is $RegistrationID. If there are any corrections to be made in your details, please contact the Registration centre within the next 4 days.",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "NewReg-email-content-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1116",
      "name": "Template for new registration Email Subject",
      "description": "Template for new registration Email Subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Registration confirmation",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "NewReg-email-subject-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1117",
      "name": "Template for new registration SMS",
      "description": "Template for new registration SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name,\nThank you for registering with the digital identity platform. Your registration id is $RegistrationID. If there are any corrections to be made in your details, please contact the Registration centre within the next 4 days. ",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "NewReg-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1118",
      "name": "Template for OTP generation Email Content",
      "description": "Template for OTP generation Email Content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name, \nOTP for username $username is $otp and is valid for $validTime minutes (Generated on $date at $time hrs).",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "OTP-email-content-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1119",
      "name": "Template for OTP generation Email Subject",
      "description": "Template for OTP generation Email Subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "One time password from digital identify platfor",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "OTP-email-subject-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1120",
      "name": "Template for OTP SMS",
      "description": "Template for OTP SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name, \nOTP for username $username is $otp and is valid for $validTime minutes (Generated on $date at $time hrs).",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "OTP-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1121",
      "name": "Template for update registration Email Content",
      "description": "Template for update registration Email Content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name, \nThank you for updating your details with the digital identity platform. Your registration id is $RegistrationID. If there are any corrections to be made in your details, please contact the Registration centre within the next 4 days.",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "Update-email-content-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1122",
      "name": "Template for update registration Email Subject",
      "description": "Template for update registration Email Subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Registration update confirmation",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "Update-email-subject-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1123",
      "name": "Template for update registration SMS",
      "description": "Template for update registration SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name, \nThank you for updating your details with the digital identity platform. Your registration id is $RegistrationID. If there are any corrections to be made in your details, please contact the Registration centre within the next 4 days.",
      "moduleId": "10002",
      "moduleName": "Registration Client",
      "templateTypeCode": "Update-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1115",
      "name": "قالب للتسجيل الجديد محتوى البريد الإلكتروني",
      "description": "قالب للتسجيل الجديد محتوى البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nنشكرك على التسجيل في منصة الهوية الرقمية. رقم التسجيل الخاص بك هو $RegistrationID. إذا كان هناك أي تصحيحات يتم إدخالها في تفاصيلك ، يرجى الاتصال بمركز التسجيل في غضون 4 أيام مقبلة.",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "NewReg-email-content-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1116",
      "name": "قالب للتسجيل الجديد البريد الإلكتروني الموضوع",
      "description": "قالب للتسجيل الجديد البريد الإلكتروني الموضوع",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "تأكيد التسجيل",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "NewReg-email-subject-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1117",
      "name": "قالب لرسالة التسجيل الجديدة",
      "description": "قالب لرسالة التسجيل الجديدة",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nنشكرك على التسجيل في منصة الهوية الرقمية. رقم التسجيل الخاص بك هو $RegistrationID. إذا كان هناك أي تصحيحات يتم إدخالها في تفاصيلك ، يرجى الاتصال بمركز التسجيل في غضون 4 أيام مقبلة.",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "NewReg-sms-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1118",
      "name": "قالب لتوليد OTP محتوى البريد الإلكتروني",
      "description": "قالب لتوليد OTP محتوى البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nOTP لاسم المستخدم $username هو $otp وصالحة لدقائق $validTime (منشأ على $date في $time hrs).",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "OTP-email-content-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1119",
      "name": "قالب لتوليد OTP البريد الإلكتروني الموضوع",
      "description": "قالب لتوليد OTP البريد الإلكتروني الموضوع",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "كلمة مرور مرة واحدة من منصة تحديد الرقمية",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "OTP-email-subject-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1120",
      "name": "قالب لرسالة OTP",
      "description": "قالب لرسالة OTP",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nOTP لاسم المستخدم $username هو $otp وصالحة لدقائق $validTime (منشأ على $date في $time hrs).",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "OTP-sms-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1121",
      "name": "قالب لتحديث تسجيل محتوى البريد الإلكتروني",
      "description": "قالب لتحديث تسجيل محتوى البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nشكرا لتحديث التفاصيل الخاصة بك مع منصة الهوية الرقمية. رقم التسجيل الخاص بك هو $RegistrationID. إذا كان هناك أي تصحيحات يتم إدخالها في تفاصيلك ، يرجى الاتصال بمركز التسجيل في غضون 4 أيام مقبلة",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "Update-email-content-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1122",
      "name": "قالب لتسجيل التحديث البريد الإلكتروني الموضوع",
      "description": "قالب لتسجيل التحديث البريد الإلكتروني الموضوع",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "تأكيد تحديث التسجيل",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "Update-email-subject-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1123",
      "name": "قالب لرسالة تسجيل التحديث",
      "description": "قالب لرسالة تسجيل التحديث",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ،\nشكرا لتحديث التفاصيل الخاصة بك مع منصة الهوية الرقمية. رقم التسجيل الخاص بك هو $ RegistrationID. إذا كان هناك أي تصحيحات يتم إدخالها في تفاصيلك ، يرجى الاتصال بمركز التسجيل في غضون 4 أيام مقبلة.",
      "moduleId": "10002",
      "moduleName": "عميل التسجيل",
      "templateTypeCode": "Update-sms-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1115",
      "name": "Modèle pour nouvelle inscription Email Content",
      "description": "Modèle pour nouvelle inscription Email Content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nMerci de vous être inscrit sur la plateforme d'identité numérique. Votre identifiant d'enregistrement est $RegistrationID. Si des corrections doivent être apportées à vos données, veuillez contacter le centre d’inscription dans les 4 prochains jours.",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "NewReg-email-content-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1116",
      "name": "Modèle pour nouvelle inscription Objet de le-mail",
      "description": "Modèle pour nouvelle inscription Objet de le-mail",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Confirmation d'enregistrement",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "NewReg-email-subject-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1117",
      "name": "Modèle de nouvelle inscription SMS",
      "description": "Modèle de nouvelle inscription SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nMerci de vous être inscrit sur la plateforme d'identité numérique. Votre identifiant d'enregistrement est $RegistrationID. Si des corrections doivent être apportées à vos données, veuillez contacter le centre d’inscription dans les 4 prochains jours.",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "NewReg-sms-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1118",
      "name": "Modèle de contenu de courrier électronique de génération dOTP",
      "description": "Modèle de contenu de courrier électronique de génération dOTP",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nOTP pour le nom d'utilisateur $username est $otp et est valide pour $validTime minutes (Généré le $date à $heure hrs).",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "OTP-email-content-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1119",
      "name": "Modèle pour le sujet de-mail de génération dOTP",
      "description": "Modèle pour le sujet de-mail de génération dOTP",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Mot de passe unique de la plateforme d'identification numérique",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "OTP-email-subject-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1120",
      "name": "Modèle pour SMS OTP",
      "description": "Modèle pour SMS OTP",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nOTP pour le nom d'utilisateur $username est $otp et est valide pour $validTime minutes (Généré le $date à $heure hrs).",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "OTP-sms-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1121",
      "name": "Modèle pour lenregistrement de la mise à jour",
      "description": "Modèle pour lenregistrement de la mise à jour",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name,\nMerci de mettre à jour vos coordonnées avec la plateforme d’identité numérique. Votre identifiant d'enregistrement est $RegistrationID. Si des corrections doivent être apportées à vos données, veuillez contacter le centre d’inscription dans les 4 prochains jours.",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "Update-email-content-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1122",
      "name": "Modèle denregistrement de mise à jour Objet de le-mail",
      "description": "Modèle denregistrement de mise à jour Objet de le-mail",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Confirmation de la mise à jour de l'inscription",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "Update-email-subject-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1123",
      "name": "Modèle pour SMS denregistrement de mise à jour",
      "description": "Modèle pour SMS denregistrement de mise à jour",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Merci de mettre à jour vos coordonnées avec la plateforme d’identité numérique. Votre identifiant d'enregistrement est $RegistrationID. Si des corrections doivent être apportées à vos données, veuillez contacter le centre d’inscription dans les 4 prochains jours.",
      "moduleId": "10002",
      "moduleName": "Client dinscription",
      "templateTypeCode": "Update-sms-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1124",
      "name": "Template for Email Acknowledgement",
      "description": "Template for Email Acknowledgement",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name,\nYour Pre-Registration for UIN is Completed Successfully\non $Date at $Time. Your ID is #$PRID.\nAppointment is scheduled for $Appointmentdate at $Appointmenttime.\nyou will also receive the details on your registered Mobile Number",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "Email-Acknowledgement",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1126",
      "name": "Template for OTP Email Content",
      "description": "Template for OTP Email Content",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Dear $name,\nTP for Pre-Registration  $PRID is $otp and is valid for $validTime minutes. (Generated on $date at $time Hrs)",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "otp-email-content-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1127",
      "name": "Template for OTP Email Subject",
      "description": "Template for OTP Email Subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Pre-Registration $PRID: OTP Request",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "otp-email-subject-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1128",
      "name": "Template for OTP SMS",
      "description": "Template for OTP SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP for Pre-Registration  $PRID is $otp and is valid for $validTime minutes. (Generated on $date at $time Hrs)",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "otp-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1129",
      "name": "Template for SMS Acknowledgement",
      "description": "Template for SMS Acknowledgement",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Your Pre-Registration for UIN is Completed Successfully\non $Date at $Time. Your ID is #$PRID.\nAppointment is scheduled for $Appointmentdate at $Appointmenttime.\nyou will also receive the details on your registered email address",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "SMS-Acknowledgement",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1124",
      "name": "قالب لتأكيد البريد الإلكتروني",
      "description": "قالب لتأكيد البريد الإلكتروني",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ، \nتم الانتهاء من التسجيل المسبق ل uin بنجاح علي $Date في $Time. رقم التعريف الخاص بك هو # $PRID. ومن المقرر تعيين $Appointmentdate في $Appointmenttime. ",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "Email-Acknowledgement",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1126",
      "name": "قالب لمحتوى البريد الإلكتروني OTP",
      "description": "قالب لمحتوى البريد الإلكتروني OTP",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$name ، \nOTP لـ Pre-Registration $PRID هو $otp وهو صالح لمدة $validTime دقيقة. (التي تم إنشاؤها على $date في $time ساعات)",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "otp-email-content-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1127",
      "name": "قالب لموضوع البريد الإلكتروني OTP",
      "description": "قالب لموضوع البريد الإلكتروني OTP",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Pre-Registration $PRID: OTP Request",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "otp-email-subject-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1128",
      "name": "قالب ل OTP SMS",
      "description": "قالب ل OTP SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP لـ Pre-Registration $PRID هو $otp وهو صالح لمدة $validTime دقيقة. (التي تم إنشاؤها على $date في $time ساعات)",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "otp-sms-template",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1129",
      "name": "قالب للإشعار SMS",
      "description": "قالب للإشعار SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "\nتم الانتهاء من التسجيل المسبق ل uin بنجاح\nعلي $Date في $Time. رقم التعريف الخاص بك هو # $PRID.\nومن المقرر تعيين $Appointmentdate في $Appointmenttime.\nسوف تتلقي أيضا التفاصيل علي عنوان البريد الكتروني المسجل الخاص بك",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "SMS-Acknowledgement",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1124",
      "name": "Template for email confirmation",
      "description": "Template for email confirmation",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name, \nvotre pré-inscription à l'UIN est terminée avec succès sur $Date à $Time. Votre ID est # $PRID.\nLe rendez-vous est prévu pour $Appointmentdate à $Appointmenttime.\nvous recevrez également les détails sur votre numéro de mobile enregistré",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "Email-Acknowledgement",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1126",
      "name": "OTP Email Content Template",
      "description": "OTP Email Content Template",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Cher $name, \nOTP pour Pre-Registration $PRID est $otp et est valide pour $validTime minutes. (Généré le $date à $time Hrs)",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "otp-email-content-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1127",
      "name": "Template for OTP email subject",
      "description": "Template for OTP email subject",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Pre-Registration $PRID: Requête OTP",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "otp-email-subject-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1128",
      "name": "Template for OTP SMS",
      "description": "Template for OTP SMS",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "OTP pour Pre-Registration $PRID est $otp et est valide pour $validTime minutes. (Généré le $date à $time Hrs)",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "otp-sms-template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1129",
      "name": "Template for SMS Acknowledgment",
      "description": "Template for SMS Acknowledgment",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Votre pré-inscription pour UIN est terminée avec succès sur $Date à $Time. \nVotre ID est # $PRID.\nLe rendez-vous est prévu pour $Appointmentdate à $Appointmenttime.\nvous recevrez également les détails sur votre adresse email enregistrée",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "SMS-Acknowledgement",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1130",
      "name": "Template for email subject of Acknowledgement",
      "description": "Template for email subject of Acknowledgement",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Pre-Registration $PRID: Acknowledgement ",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "Acknowledgement-email-subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1130",
      "name": "Modèle pour le sujet d'email d'accusé de réception",
      "description": "Modèle pour le sujet d'email d'accusé de réception",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Pré-inscription $PRID: accusé de réception ",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "Acknowledgement-email-subject",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1130",
      "name": "قالب للتسليم البريد الكتروني الموضوع",
      "description": "قالب للتسليم البريد الكتروني الموضوع",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "$PRID التسجيل المسبق: شكر",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "Acknowledgement-email-subject",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "00890",
      "name": "Template for authorization subject test1",
      "description": "Template for authorization subject test1",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "UIN $uin Authentication $status",
      "moduleId": "10004",
      "moduleName": "ID Authentication",
      "templateTypeCode": "auth-email-subject",
      "isDeleted": true,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1125",
      "name": "قالب للشاشة شكر وتقدير",
      "description": "قالب للشاشة شكر وتقدير",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "1.\tالمبدا التوجيهي 1\n2.\tالمبدا التوجيهي 2\n3.\tالمبدا التوجيهي 3\n4.\tالمبدا التوجيهي 4\n5.\tالمبدا التوجيهي 5\n6.\tالمبدا التوجيهي 6\n7.\tالمبدا التوجيهي 7\n8.\tالمبدا التوجيهي 8\n9.\tالمبدا التوجيهي 9\n10.\tالمبدا التوجيهي 10",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "Onscreen-Acknowledgement",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1125",
      "name": "Template for Onscreen Acknowledgment",
      "description": "Template for Onscreen Acknowledgment",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "1.\tGuideline 1\n2.\tGuideline 2\n3.\tGuideline 3\n4.\tGuideline 4\n5.\tGuideline 5\n6.\tGuideline 6\n7.\tGuideline 7\n8.\tGuideline 8\n9.\tGuideline 9\n10.\tGuideline 10",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "Onscreen-Acknowledgement",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1125",
      "name": "On-screen recognition template",
      "description": "On-screen recognition template",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "1.\tLigne directrice 1\n2.\tLigne directrice 2\n3.\tLigne directrice 3\n4.\tLigne directrice 4\n5.\tLigne directrice 5\n6.\tLigne directrice 6\n7.\tLigne directrice 7\n8.\tLigne directrice 8\n9.\tLigne directrice 9\n10.\tLigne directrice 10",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "Onscreen-Acknowledgement",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1201",
      "name": "Modèle SMS de reconnaissance",
      "description": "Modèle de confirmation dinscription",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "cher ${ResidentName},\nMerci de vous être inscrit à la plateforme d’identité numérique. Votre identifiant d’inscription est\"${RID}\". Les détails démographiques sont les suivants:\n1.Rendez-vous amoureux:${Date}\n2.Nom complet:${FullName}\n3.Date de naissance:${DOB}\n4.Le sexe:${Gender}\n5.Ligne d’adresse 1:${AddressLine1}\n6.Ligne d’adresse 2:${AddressLine2}\n7.Ligne d’adresse 3:${AddressLine3}\n8.Région:${Region}\n9.Ville:${City}\n10.état ou province:${Province}\n11.code postal:${PostalCode}\n12.Mobile:${Mobile}\n13.Email:${Email}\n\nSi des corrections doivent être apportées aux informations ci-dessus, veuillez contacter le centre d’inscription dans les 4 prochains jours.",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-sms-notification",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1201",
      "name": "قالب SMS شكر",
      "description": "نموذج شكر التسجيل",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "العزيز ${ResidentName},\nنشكرك على التسجيل في منصة Digital Identity. معرف التسجيل الخاص بك هو \"${RID}\". التفاصيل الديموغرافية هي على النحو التالي:\n1.تاريخ:${Date}\n2.الاسم الكامل:${FullName}\n3.تاريخ الولادة:${DOB}\n4.جنس:${Gender}\n5.خط عنوان 1:${AddressLine1}\n6.خط عنوان 2:${AddressLine2}\n7.خط عنوان 3:${AddressLine3}\n8.منطقة:${Region}\n9.مدينة:${City}\n10.الولاية أو المقاطعة:${Province}\n11.الرمز البريدي:${PostalCode}\n12.التليفون المحمول:${Mobile}\n13.البريد الإلكتروني:${Email}\n\nإذا كان هناك أي تصحيحات يجب إدخالها على التفاصيل المذكورة أعلاه ، يرجى الاتصال بمركز التسجيل في غضون 4 أيام مقبلة.",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-sms-notification",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1201",
      "name": "Acknowledgement SMS Template",
      "description": "Registration Acknowledgement Template",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "Dear ${ResidentName},\nThank you for registering with Digital Identity platform . Your registration id is \"${RID}\". The demographic details are as follows:\n1.Date:${Date}\n2.Full Name:${FullName}\n3.Date of Birth:${DOB}\n4.Gender:${Gender}\n5.Address Line 1:${AddressLine1}\n6.Address Line 2:${AddressLine2}\n7.Address Line 3:${AddressLine3}\n8.Region:${Region}\n9.City:${City}\n10.State or Province:${Province}\n11.Postal Code:${PostalCode}\n12.Mobile:${Mobile}\n13.Email:${Email}\n\nIf there are any corrections to be made to the above details, kindly contact the Registration centre within the next 4 days.",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-sms-notification",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1202",
      "name": "Modèle de courrier électronique daccusé de réception",
      "description": "Modèle de confirmation d inscription",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "cher ${ResidentName},\nMerci de vous être inscrit à la plateforme d’identité numérique. Votre identifiant d’inscription est\"${RID}\". Les détails démographiques sont les suivants:\n1.Rendez-vous amoureux:${Date}\n2.Nom complet:${FullName}\n3.Date de naissance:${DOB}\n4.Le sexe:${Gender}\n5.Ligne d’adresse 1:${AddressLine1}\n6.Ligne d’adresse 2:${AddressLine2}\n7.Ligne d’adresse 3:${AddressLine3}\n8.Région:${Region}\n9.Ville:${City}\n10.état ou province:${Province}\n11.code postal:${PostalCode}\n12.Mobile:${Mobile}\n13.Email:${Email}\n\nSi des corrections doivent être apportées aux informations ci-dessus, veuillez contacter le centre d’inscription dans les 4 prochains jours.",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-email-notification",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1202",
      "name": "Acknowledgement Email Template",
      "description": "Registration Acknowledgement Template",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "Dear ${ResidentName},\nThank you for registering with Digital Identity platform . Your registration id is \"${RID}\". The demographic details are as follows:\n1.Date:${Date}\n2.Full Name:${FullName}\n3.Date of Birth:${DOB}\n4.Gender:${Gender}\n5.Address Line 1:${AddressLine1}\n6.Address Line 2:${AddressLine2}\n7.Address Line 3:${AddressLine3}\n8.Region:${Region}\n9.City:${City}\n10.State or Province:${Province}\n11.Postal Code:${PostalCode}\n12.Mobile:${Mobile}\n13.Email:${Email}\n\nIf there are any corrections to be made to the above details, kindly contact the Registration centre within the next 4 days.",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-email-notification",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1202",
      "name": "نموذج البريد الإلكتروني شكرًا",
      "description": "نموذج شكر التسجيل",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "العزيز ${ResidentName},\nنشكرك على التسجيل في منصة Digital Identity. معرف التسجيل الخاص بك هو \"${RID}\". التفاصيل الديموغرافية هي على النحو التالي:\n1.تاريخ:${Date}\n2.الاسم الكامل:${FullName}\n3.تاريخ الولادة:${DOB}\n4.جنس:${Gender}\n5.خط عنوان 1:${AddressLine1}\n6.خط عنوان 2:${AddressLine2}\n7.خط عنوان 3:${AddressLine3}\n8.منطقة:${Region}\n9.مدينة:${City}\n10.الولاية أو المقاطعة:${Province}\n11.الرمز البريدي:${PostalCode}\n12.التليفون المحمول:${Mobile}\n13.البريد الإلكتروني:${Email}\n\nإذا كان هناك أي تصحيحات يجب إدخالها على التفاصيل المذكورة أعلاه ، يرجى الاتصال بمركز التسجيل في غضون 4 أيام مقبلة.",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-email-notification",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "preregistration",
      "name": "otp service",
      "description": "OTP Send Service",
      "fileFormatCode": "txt",
      "model": "string",
      "fileText": "Please find the OTP $otp",
      "moduleId": "10001",
      "moduleName": "login",
      "templateTypeCode": "otp-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "ida",
      "name": "otp service",
      "description": "OTP Send Service",
      "fileFormatCode": "txt",
      "model": "string",
      "fileText": "Please find the OTP $otp",
      "moduleId": "10001",
      "moduleName": "login",
      "templateTypeCode": "otp-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "registrationprocessor",
      "name": "otp service",
      "description": "OTP Send Service",
      "fileFormatCode": "txt",
      "model": "string",
      "fileText": "Please find the OTP $otp",
      "moduleId": "10001",
      "moduleName": "login",
      "templateTypeCode": "otp-sms-template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1205",
      "name": "enregistrement\n Modèle de reconnaissance - partie 3",
      "description": "Accusé de réception généré après lenregistrement - Partie 3",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<tr ${AckReceipt}><td><div class=\"biometrics\"><h5 class=\"leftLittle\">${leftLittle}</h5><h5 class=\"leftRing\">${leftRing}</h5><h5 class=\"leftMiddle\">${leftMiddle}</h5><h5 class=\"leftIndex\">${leftIndex}</h5><img src=\"${LeftPalmImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"rightIndex\">${rightIndex}</h5><h5 class=\"rightMiddle\">${rightMiddle}</h5><h5 class=\"rightRing\">${rightRing}</h5><h5 class=\"rightLittle\">${rightLittle}</h5><img src=\"${RightPalmImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"leftThumb\">${leftThumb}</h5><h5 class=\"rightThumb\">${rightThumb}</h5><img src=\"${ThumbsImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td ${leftSlapCaptured}><img src=\"${CapturedLeftSlap}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightSlapCaptured}><img src=\"${CapturedRightSlap}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${thumbsCaptured}><img src=\"${CapturedThumbs}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr><tr ${AckReceipt}><td><p ${MissingLeftFingers} class=\"headings\">${LeftSlapExceptionPrim} / ${LeftSlapExceptionSec}</p></td><td><p ${MissingRightFingers} class=\"headings\">${RightSlapExceptionPrim} / ${RightSlapExceptionSec}</p></td><td><p ${MissingThumbs} class=\"headings\">${ThumbsExceptionPrim} / ${ThumbsExceptionSec}</p></td></tr><tr ${Preview}><td ${leftSlapCaptured}><p ${MissingLeftFingers} class=\"headings\">${LeftSlapExceptionPrim} / ${LeftSlapExceptionSec}</p></td><td ${rightSlapCaptured}><p ${MissingRightFingers} class=\"headings\">${RightSlapExceptionPrim} / ${RightSlapExceptionSec}</p></td><td ${thumbsCaptured}><p ${MissingThumbs} class=\"headings\">${ThumbsExceptionPrim} / ${ThumbsExceptionSec}</p></td></tr></table><hr/><table class=\"dataTable\"><tr><td ${ROImage}><img src=\"${ROImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td><p class=\"headings\">${RONamePrimLabel} / ${RONameSecLabel}</p><br/>${ROName}<br/>${RONameSec}</td><td><p class=\"headings\">${RegCenterPrimLabel} / ${RegCenterSecLabel}</p><br/>${RegCenter}<br/>${RegCenterSec}</td></tr></table><hr/><br/></div><div ${FaceCaptureEnabled} ${AckReceipt} class=\"photo\"><p class=\"applicantPhotoLabel\">${PhotoPrim} / ${PhotoSec}</p><img class=\"applicantPhoto\" src=\"${ApplicantImageSource}\" border=\"0\" width=\"100\" height=\"100\"/></div><div ${FaceCaptureEnabled} ${Preview} class=\"previewPhoto\"><p class=\"applicantPhotoLabel\">${PhotoPrim} / ${PhotoSec}</p><img class=\"applicantPhoto\" src=\"${ApplicantImageSource}\" border=\"0\" width=\"100\" height=\"100\"/></div><div ${AckReceipt}><p>${ImportantGuidelines}</p><ul><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim Ad minim veniam, quis nostrud exercitation. Ullamco laboris nisi ut aliquip exea commodo consequat. Duis aute irure dolor in Reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.Cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id.</span></li><br/><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et.</span></li><br/><li><span>Dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex.</span></li><br/><li><span>Commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat.Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim Ad minim veniam, quis nostrud exercitation. Ullamco laboris nisi ut aliquip exea commodo consequat. Duis aute irure dolor in Reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.Cupidatat non proident, sunt in culpa qui offici.</span></li><br/><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et.</span></li></ul></div></div></body></html>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part3",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1204",
      "name": "enregistrement\n Modèle de reconnaissance - partie 2",
      "description": "Accusé de réception généré après lenregistrement - Partie 2",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<td><p class=\"headings\">${ParentUINPrimLabel} / ${ParentUINSecLabel}</p><br/>${ParentUIN}</td></tr></table><br/><p ${DocumentsEnabled} class=\"head\"><b>${DocumentsPrimLabel}</b></p><div ${DocumentsEnabled} ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyDocuments\">${Modify}</button></div><hr ${DocumentsEnabled}/><table ${DocumentsEnabled}><tr><td><p class=\"headings\">${DocumentsPrimLabel} / ${DocumentsSecLabel}</p><br/>${Documents}<br/>${DocumentsSec}</td></tr></table><br/><p ${BiometricsEnabled} class=\"head\"><b>${BiometricsPrimLabel}</b></p><div ${BiometricsEnabled} ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyBiometrics\">${Modify}</button></div><hr ${BiometricsEnabled}/><table ${BiometricsEnabled}><tr><td><p class=\"headings\">${BiometricsPrimLabel} / ${BiometricsSecLabel}</p><br/>${Biometrics}<br/>${BiometricsSec}</td></tr></table><table ${IrisDisabled}><tr><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td></tr><tr><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td></tr></table><table ${IrisEnabled} ${WithException} class=\"biometricsTable\"><tr ${AckReceipt}><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td><td><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${Preview}><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td><td ${leftEyeCaptured}><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td ${rightEyeCaptured}><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${AckReceipt}><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td><div class=\"biometrics\"><h5 class=\"iris\">${LeftEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"iris\">${RightEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td ${leftEyeCaptured}><img src=\"${CapturedLeftEye}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightEyeCaptured}><img src=\"${CapturedRightEye}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr></table><table ${IrisEnabled} class=\"tableWithoutException\" ${WithoutException}><tr ${AckReceipt}><td><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${Preview}><td ${leftEyeCaptured}><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td ${rightEyeCaptured}><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${AckReceipt}><td><div class=\"biometrics\"><h5 class=\"irisWithoutException\">${LeftEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"irisWithoutException\">${RightEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td ${leftEyeCaptured}><img src=\"${CapturedLeftEye}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightEyeCaptured}><img src=\"${CapturedRightEye}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr></table><table ${FingerprintsCaptured} class=\"biometricsTable\"><tr ${AckReceipt}><td><p class=\"headings\">${LeftPalmPrimLabel} / ${LeftPalmSecLabel}</p></td><td><p class=\"headings\">${RightPalmPrimLabel} / ${RightPalmSecLabel}</p></td><td><p class=\"headings\">${ThumbsPrimLabel} / ${ThumbsSecLabel}</p></td></tr><tr ${Preview}><td ${leftSlapCaptured}><p class=\"headings\">${LeftPalmPrimLabel} / ${LeftPalmSecLabel}</p></td><td ${rightSlapCaptured}><p class=\"headings\">${RightPalmPrimLabel} / ${RightPalmSecLabel}</p></td><td ${thumbsCaptured}><p class=\"headings\">${ThumbsPrimLabel} / ${ThumbsSecLabel}</p></td></tr>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part2",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1203",
      "name": "enregistrement\n Modèle de remerciement - Partie 1",
      "description": "Accusé de réception généré après lenregistrement - Partie 1",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<html><head><style>body{font-family:\"Roboto\";}table, .head{font-size:13px;}.previewPhoto{float:right;position:absolute;top:220px;}.photo{float:right;position:absolute;top:370px;}.applicantPhoto{position:absolute;top:-35px;left:670px;}.applicantPhotoLabel{color:#808080;font-size:10px;position:absolute;white-space:nowrap;top:-70px;left:690px;}.form{display:inline-block;}.section{align:center;padding:30px;width:800px;margin:auto;}.headings{color:#808080;font-size:10px;}td,p{display:inline;}.dataTable{word-wrap:break-word;table-layout:fixed;width:70%;}.headerTable{width:80%;}.uinHeaderTable{width:100%;}h5{display:inline;position:absolute;}.iris{top:-15px;left:158px;}.irisWithoutException{top:-15px;left:120px;}.tableWithoutException{width:50%;text-align:center;table-layout:fixed;margin:0 auto;}.biometricsTable{width:100%;text-align:center;table-layout:fixed;}.biometrics{position:relative;}.leftLittle{top:15px;left:98px;}.leftRing{top:3px;left:111px;}.leftMiddle{top:-7px;left:127px;}.leftIndex{top:3px;left:140px;}.rightIndex{top:3px;left:113px;}.rightMiddle{top:-7px;left:127px;}.rightRing{top:3px;left:140px;}.rightLittle{top:15px;left:154px;}.leftThumb{top:-4px;left:113px;}.rightThumb{top:-4px;left:138px;}li span{color:black;font-size:12px;}li{color:lightgrey}button{float:right;font-size:12px;border:none;background-color:transparent;outline:none;}button:active{background-color:black;color:white;}.modify{float:right;}</style></head><body><div class=\"section\"><div class=\"form\"><table ${AckReceipt} class=\"${headerTable}\"><tr><td><img src=\"${QRCodeSource}\" border=\"0\" width=\"210\" height=\"210\"/></td><td><p class=\"headings\">${RIDPrimLabel} / ${RIDSecLabel}</p><br/>${RID}</td><td ${UINUpdate}><p class=\"headings\">${UINPrimLabel} / ${UINSecLabel}</p><br/>${UIN}</td><td><p class=\"headings\">${DatePrimLabel} / ${DateSecLabel}</p><br/>${Date}</td></tr></table><table ${Preview} class=\"headerTable\"><tr><td><p class=\"headings\">${PreRegIDPrimLabel} / ${PreRegIDSecLabel}</p><br/>${PreRegID}</td><td><p class=\"headings\">${DatePrimLabel} / ${DateSecLabel}</p><br/>${Date}</td></tr></table><br/><hr/><p class=\"head\"><b>${DemographicInfo}</b></p><div ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyDemographicInfo\">${Modify}</button></div><hr/><table class=\"dataTable\"><tr><td><p class=\"headings\">${FullNamePrimLabel} / ${FullNameSecLabel}</p><br/>${FullName}<br/>${FullNameSec}</td><td><p class=\"headings\">${GenderPrimLabel} / ${GenderSecLabel}</p><br/>${Gender}<br/>${GenderSec}</td></tr><tr><td><p class=\"headings\">${DOBPrimLabel} / ${DOBSecLabel}</p><br/>${DOB}</td><td><p class=\"headings\">${AgePrimLabel} / ${AgeSecLabel}</p><br/>${Age} ${YearsPrim} / ${YearsSec}</td></tr><tr><td><p class=\"headings\">${ForiegnerPrimLabel} / ${ForiegnerSecLabel}</p><br/>${ResidenceStatus}<br/>${ResidenceStatusSec}</td><td><p class=\"headings\">${AddressLine1PrimLabel} / ${AddressLine1SecLabel}</p><br/>${AddressLine1}<br/>${AddressLine1Sec}</td></tr><tr><td><p class=\"headings\">${AddressLine2PrimLabel} / ${AddressLine2SecLabel}</p><br/>${AddressLine2}<br/>${AddressLine2Sec}</td><td><p class=\"headings\">${RegionPrimLabel} / ${RegionSecLabel}</p><br/>${Region}<br/>${RegionSec}</td></tr><tr><td><p class=\"headings\">${ProvincePrimLabel} / ${ProvinceSecLabel}</p><br/>${Province}<br/>${ProvinceSec}</td><td><p class=\"headings\">${LocalAuthorityPrimLabel} / ${LocalAuthoritySecLabel}</p><br/>${LocalAuthority}<br/>${LocalAuthoritySec}</td></tr><tr><td><p class=\"headings\">${MobilePrimLabel} / ${MobileSecLabel}</p><br/>${Mobile}</td><td><p class=\"headings\">${PostalCodePrimLabel} / ${PostalCodeSecLabel}</p><br/>${PostalCode}</td></tr><tr><td><p class=\"headings\">${EmailPrimLabel} / ${EmailSecLabel}</p><br/>${Email}</td><td><p class=\"headings\">${CNIEPrimLabel} / ${CNIESecLabel}</p><br/>${CNIE}</td></tr><tr ${WithParent}><td><p class=\"headings\">${ParentNamePrimLabel} / ${ParentNameSecLabel}</p><br/>${ParentName}<br/>${ParentNameSec}</td>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part1",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "1205",
      "name": "قالب الاعتراف بالتسجيل - الجزء 3",
      "description": "إقرار تم إنشاؤه بعد التسجيل - الجزء 3",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<tr ${AckReceipt}><td><div class=\"biometrics\"><h5 class=\"leftLittle\">${leftLittle}</h5><h5 class=\"leftRing\">${leftRing}</h5><h5 class=\"leftMiddle\">${leftMiddle}</h5><h5 class=\"leftIndex\">${leftIndex}</h5><img src=\"${LeftPalmImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"rightIndex\">${rightIndex}</h5><h5 class=\"rightMiddle\">${rightMiddle}</h5><h5 class=\"rightRing\">${rightRing}</h5><h5 class=\"rightLittle\">${rightLittle}</h5><img src=\"${RightPalmImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"leftThumb\">${leftThumb}</h5><h5 class=\"rightThumb\">${rightThumb}</h5><img src=\"${ThumbsImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td ${leftSlapCaptured}><img src=\"${CapturedLeftSlap}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightSlapCaptured}><img src=\"${CapturedRightSlap}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${thumbsCaptured}><img src=\"${CapturedThumbs}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr><tr ${AckReceipt}><td><p ${MissingLeftFingers} class=\"headings\">${LeftSlapExceptionPrim} / ${LeftSlapExceptionSec}</p></td><td><p ${MissingRightFingers} class=\"headings\">${RightSlapExceptionPrim} / ${RightSlapExceptionSec}</p></td><td><p ${MissingThumbs} class=\"headings\">${ThumbsExceptionPrim} / ${ThumbsExceptionSec}</p></td></tr><tr ${Preview}><td ${leftSlapCaptured}><p ${MissingLeftFingers} class=\"headings\">${LeftSlapExceptionPrim} / ${LeftSlapExceptionSec}</p></td><td ${rightSlapCaptured}><p ${MissingRightFingers} class=\"headings\">${RightSlapExceptionPrim} / ${RightSlapExceptionSec}</p></td><td ${thumbsCaptured}><p ${MissingThumbs} class=\"headings\">${ThumbsExceptionPrim} / ${ThumbsExceptionSec}</p></td></tr></table><hr/><table class=\"dataTable\"><tr><td ${ROImage}><img src=\"${ROImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td><p class=\"headings\">${RONamePrimLabel} / ${RONameSecLabel}</p><br/>${ROName}<br/>${RONameSec}</td><td><p class=\"headings\">${RegCenterPrimLabel} / ${RegCenterSecLabel}</p><br/>${RegCenter}<br/>${RegCenterSec}</td></tr></table><hr/><br/></div><div ${FaceCaptureEnabled} ${AckReceipt} class=\"photo\"><p class=\"applicantPhotoLabel\">${PhotoPrim} / ${PhotoSec}</p><img class=\"applicantPhoto\" src=\"${ApplicantImageSource}\" border=\"0\" width=\"100\" height=\"100\"/></div><div ${FaceCaptureEnabled} ${Preview} class=\"previewPhoto\"><p class=\"applicantPhotoLabel\">${PhotoPrim} / ${PhotoSec}</p><img class=\"applicantPhoto\" src=\"${ApplicantImageSource}\" border=\"0\" width=\"100\" height=\"100\"/></div><div ${AckReceipt}><p>${ImportantGuidelines}</p><ul><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim Ad minim veniam, quis nostrud exercitation. Ullamco laboris nisi ut aliquip exea commodo consequat. Duis aute irure dolor in Reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.Cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id.</span></li><br/><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et.</span></li><br/><li><span>Dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex.</span></li><br/><li><span>Commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat.Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim Ad minim veniam, quis nostrud exercitation. Ullamco laboris nisi ut aliquip exea commodo consequat. Duis aute irure dolor in Reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.Cupidatat non proident, sunt in culpa qui offici.</span></li><br/><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et.</span></li></ul></div></div></body></html>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part3",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1204",
      "name": "الب الاعتراف بالتسجيل - الجزء 2",
      "description": "الإقرار المتولد بعد التسجيل - الجزء 2",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<td><p class=\"headings\">${ParentUINPrimLabel} / ${ParentUINSecLabel}</p><br/>${ParentUIN}</td></tr></table><br/><p ${DocumentsEnabled} class=\"head\"><b>${DocumentsPrimLabel}</b></p><div ${DocumentsEnabled} ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyDocuments\">${Modify}</button></div><hr ${DocumentsEnabled}/><table ${DocumentsEnabled}><tr><td><p class=\"headings\">${DocumentsPrimLabel} / ${DocumentsSecLabel}</p><br/>${Documents}<br/>${DocumentsSec}</td></tr></table><br/><p ${BiometricsEnabled} class=\"head\"><b>${BiometricsPrimLabel}</b></p><div ${BiometricsEnabled} ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyBiometrics\">${Modify}</button></div><hr ${BiometricsEnabled}/><table ${BiometricsEnabled}><tr><td><p class=\"headings\">${BiometricsPrimLabel} / ${BiometricsSecLabel}</p><br/>${Biometrics}<br/>${BiometricsSec}</td></tr></table><table ${IrisDisabled}><tr><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td></tr><tr><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td></tr></table><table ${IrisEnabled} ${WithException} class=\"biometricsTable\"><tr ${AckReceipt}><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td><td><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${Preview}><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td><td ${leftEyeCaptured}><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td ${rightEyeCaptured}><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${AckReceipt}><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td><div class=\"biometrics\"><h5 class=\"iris\">${LeftEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"iris\">${RightEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td ${leftEyeCaptured}><img src=\"${CapturedLeftEye}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightEyeCaptured}><img src=\"${CapturedRightEye}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr></table><table ${IrisEnabled} class=\"tableWithoutException\" ${WithoutException}><tr ${AckReceipt}><td><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${Preview}><td ${leftEyeCaptured}><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td ${rightEyeCaptured}><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${AckReceipt}><td><div class=\"biometrics\"><h5 class=\"irisWithoutException\">${LeftEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"irisWithoutException\">${RightEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td ${leftEyeCaptured}><img src=\"${CapturedLeftEye}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightEyeCaptured}><img src=\"${CapturedRightEye}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr></table><table ${FingerprintsCaptured} class=\"biometricsTable\"><tr ${AckReceipt}><td><p class=\"headings\">${LeftPalmPrimLabel} / ${LeftPalmSecLabel}</p></td><td><p class=\"headings\">${RightPalmPrimLabel} / ${RightPalmSecLabel}</p></td><td><p class=\"headings\">${ThumbsPrimLabel} / ${ThumbsSecLabel}</p></td></tr><tr ${Preview}><td ${leftSlapCaptured}><p class=\"headings\">${LeftPalmPrimLabel} / ${LeftPalmSecLabel}</p></td><td ${rightSlapCaptured}><p class=\"headings\">${RightPalmPrimLabel} / ${RightPalmSecLabel}</p></td><td ${thumbsCaptured}><p class=\"headings\">${ThumbsPrimLabel} / ${ThumbsSecLabel}</p></td></tr>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part2",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1203",
      "name": "قالب الاعتراف بالتسجيل - الجزء 1",
      "description": "إقرار تم إنشاؤه بعد التسجيل - الجزء 1",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<html><head><style>body{font-family:\"Roboto\";}table, .head{font-size:13px;}.previewPhoto{float:right;position:absolute;top:220px;}.photo{float:right;position:absolute;top:370px;}.applicantPhoto{position:absolute;top:-35px;left:670px;}.applicantPhotoLabel{color:#808080;font-size:10px;position:absolute;white-space:nowrap;top:-70px;left:690px;}.form{display:inline-block;}.section{align:center;padding:30px;width:800px;margin:auto;}.headings{color:#808080;font-size:10px;}td,p{display:inline;}.dataTable{word-wrap:break-word;table-layout:fixed;width:70%;}.headerTable{width:80%;}.uinHeaderTable{width:100%;}h5{display:inline;position:absolute;}.iris{top:-15px;left:158px;}.irisWithoutException{top:-15px;left:120px;}.tableWithoutException{width:50%;text-align:center;table-layout:fixed;margin:0 auto;}.biometricsTable{width:100%;text-align:center;table-layout:fixed;}.biometrics{position:relative;}.leftLittle{top:15px;left:98px;}.leftRing{top:3px;left:111px;}.leftMiddle{top:-7px;left:127px;}.leftIndex{top:3px;left:140px;}.rightIndex{top:3px;left:113px;}.rightMiddle{top:-7px;left:127px;}.rightRing{top:3px;left:140px;}.rightLittle{top:15px;left:154px;}.leftThumb{top:-4px;left:113px;}.rightThumb{top:-4px;left:138px;}li span{color:black;font-size:12px;}li{color:lightgrey}button{float:right;font-size:12px;border:none;background-color:transparent;outline:none;}button:active{background-color:black;color:white;}.modify{float:right;}</style></head><body><div class=\"section\"><div class=\"form\"><table ${AckReceipt} class=\"${headerTable}\"><tr><td><img src=\"${QRCodeSource}\" border=\"0\" width=\"210\" height=\"210\"/></td><td><p class=\"headings\">${RIDPrimLabel} / ${RIDSecLabel}</p><br/>${RID}</td><td ${UINUpdate}><p class=\"headings\">${UINPrimLabel} / ${UINSecLabel}</p><br/>${UIN}</td><td><p class=\"headings\">${DatePrimLabel} / ${DateSecLabel}</p><br/>${Date}</td></tr></table><table ${Preview} class=\"headerTable\"><tr><td><p class=\"headings\">${PreRegIDPrimLabel} / ${PreRegIDSecLabel}</p><br/>${PreRegID}</td><td><p class=\"headings\">${DatePrimLabel} / ${DateSecLabel}</p><br/>${Date}</td></tr></table><br/><hr/><p class=\"head\"><b>${DemographicInfo}</b></p><div ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyDemographicInfo\">${Modify}</button></div><hr/><table class=\"dataTable\"><tr><td><p class=\"headings\">${FullNamePrimLabel} / ${FullNameSecLabel}</p><br/>${FullName}<br/>${FullNameSec}</td><td><p class=\"headings\">${GenderPrimLabel} / ${GenderSecLabel}</p><br/>${Gender}<br/>${GenderSec}</td></tr><tr><td><p class=\"headings\">${DOBPrimLabel} / ${DOBSecLabel}</p><br/>${DOB}</td><td><p class=\"headings\">${AgePrimLabel} / ${AgeSecLabel}</p><br/>${Age} ${YearsPrim} / ${YearsSec}</td></tr><tr><td><p class=\"headings\">${ForiegnerPrimLabel} / ${ForiegnerSecLabel}</p><br/>${ResidenceStatus}<br/>${ResidenceStatusSec}</td><td><p class=\"headings\">${AddressLine1PrimLabel} / ${AddressLine1SecLabel}</p><br/>${AddressLine1}<br/>${AddressLine1Sec}</td></tr><tr><td><p class=\"headings\">${AddressLine2PrimLabel} / ${AddressLine2SecLabel}</p><br/>${AddressLine2}<br/>${AddressLine2Sec}</td><td><p class=\"headings\">${RegionPrimLabel} / ${RegionSecLabel}</p><br/>${Region}<br/>${RegionSec}</td></tr><tr><td><p class=\"headings\">${ProvincePrimLabel} / ${ProvinceSecLabel}</p><br/>${Province}<br/>${ProvinceSec}</td><td><p class=\"headings\">${LocalAuthorityPrimLabel} / ${LocalAuthoritySecLabel}</p><br/>${LocalAuthority}<br/>${LocalAuthoritySec}</td></tr><tr><td><p class=\"headings\">${MobilePrimLabel} / ${MobileSecLabel}</p><br/>${Mobile}</td><td><p class=\"headings\">${PostalCodePrimLabel} / ${PostalCodeSecLabel}</p><br/>${PostalCode}</td></tr><tr><td><p class=\"headings\">${EmailPrimLabel} / ${EmailSecLabel}</p><br/>${Email}</td><td><p class=\"headings\">${CNIEPrimLabel} / ${CNIESecLabel}</p><br/>${CNIE}</td></tr><tr ${WithParent}><td><p class=\"headings\">${ParentNamePrimLabel} / ${ParentNameSecLabel}</p><br/>${ParentName}<br/>${ParentNameSec}</td>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part1",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1203",
      "name": "Registration Acknowledgement Template - Part 1",
      "description": "Acknowledgement generated after registration - Part 1",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<html><head><style>body{font-family:\"Roboto\";}table, .head{font-size:13px;}.previewPhoto{float:right;position:absolute;top:220px;}.photo{float:right;position:absolute;top:370px;}.applicantPhoto{position:absolute;top:-35px;left:670px;}.applicantPhotoLabel{color:#808080;font-size:10px;position:absolute;white-space:nowrap;top:-70px;left:690px;}.form{display:inline-block;}.section{align:center;padding:30px;width:800px;margin:auto;}.headings{color:#808080;font-size:10px;}td,p{display:inline;}.dataTable{word-wrap:break-word;table-layout:fixed;width:70%;}.headerTable{width:80%;}.uinHeaderTable{width:100%;}h5{display:inline;position:absolute;}.iris{top:-15px;left:158px;}.irisWithoutException{top:-15px;left:120px;}.tableWithoutException{width:50%;text-align:center;table-layout:fixed;margin:0 auto;}.biometricsTable{width:100%;text-align:center;table-layout:fixed;}.biometrics{position:relative;}.leftLittle{top:15px;left:98px;}.leftRing{top:3px;left:111px;}.leftMiddle{top:-7px;left:127px;}.leftIndex{top:3px;left:140px;}.rightIndex{top:3px;left:113px;}.rightMiddle{top:-7px;left:127px;}.rightRing{top:3px;left:140px;}.rightLittle{top:15px;left:154px;}.leftThumb{top:-4px;left:113px;}.rightThumb{top:-4px;left:138px;}li span{color:black;font-size:12px;}li{color:lightgrey}button{float:right;font-size:12px;border:none;background-color:transparent;outline:none;}button:active{background-color:black;color:white;}.modify{float:right;}</style></head><body><div class=\"section\"><div class=\"form\"><table ${AckReceipt} class=\"${headerTable}\"><tr><td><img src=\"${QRCodeSource}\" border=\"0\" width=\"210\" height=\"210\"/></td><td><p class=\"headings\">${RIDPrimLabel} / ${RIDSecLabel}</p><br/>${RID}</td><td ${UINUpdate}><p class=\"headings\">${UINPrimLabel} / ${UINSecLabel}</p><br/>${UIN}</td><td><p class=\"headings\">${DatePrimLabel} / ${DateSecLabel}</p><br/>${Date}</td></tr></table><table ${Preview} class=\"headerTable\"><tr><td><p class=\"headings\">${PreRegIDPrimLabel} / ${PreRegIDSecLabel}</p><br/>${PreRegID}</td><td><p class=\"headings\">${DatePrimLabel} / ${DateSecLabel}</p><br/>${Date}</td></tr></table><br/><hr/><p class=\"head\"><b>${DemographicInfo}</b></p><div ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyDemographicInfo\">${Modify}</button></div><hr/><table class=\"dataTable\"><tr><td><p class=\"headings\">${FullNamePrimLabel} / ${FullNameSecLabel}</p><br/>${FullName}<br/>${FullNameSec}</td><td><p class=\"headings\">${GenderPrimLabel} / ${GenderSecLabel}</p><br/>${Gender}<br/>${GenderSec}</td></tr><tr><td><p class=\"headings\">${DOBPrimLabel} / ${DOBSecLabel}</p><br/>${DOB}</td><td><p class=\"headings\">${AgePrimLabel} / ${AgeSecLabel}</p><br/>${Age} ${YearsPrim} / ${YearsSec}</td></tr><tr><td><p class=\"headings\">${ForiegnerPrimLabel} / ${ForiegnerSecLabel}</p><br/>${ResidenceStatus}<br/>${ResidenceStatusSec}</td><td><p class=\"headings\">${AddressLine1PrimLabel} / ${AddressLine1SecLabel}</p><br/>${AddressLine1}<br/>${AddressLine1Sec}</td></tr><tr><td><p class=\"headings\">${AddressLine2PrimLabel} / ${AddressLine2SecLabel}</p><br/>${AddressLine2}<br/>${AddressLine2Sec}</td><td><p class=\"headings\">${RegionPrimLabel} / ${RegionSecLabel}</p><br/>${Region}<br/>${RegionSec}</td></tr><tr><td><p class=\"headings\">${ProvincePrimLabel} / ${ProvinceSecLabel}</p><br/>${Province}<br/>${ProvinceSec}</td><td><p class=\"headings\">${LocalAuthorityPrimLabel} / ${LocalAuthoritySecLabel}</p><br/>${LocalAuthority}<br/>${LocalAuthoritySec}</td></tr><tr><td><p class=\"headings\">${MobilePrimLabel} / ${MobileSecLabel}</p><br/>${Mobile}</td><td><p class=\"headings\">${PostalCodePrimLabel} / ${PostalCodeSecLabel}</p><br/>${PostalCode}</td></tr><tr><td><p class=\"headings\">${EmailPrimLabel} / ${EmailSecLabel}</p><br/>${Email}</td><td><p class=\"headings\">${CNIEPrimLabel} / ${CNIESecLabel}</p><br/>${CNIE}</td></tr><tr ${WithParent}><td><p class=\"headings\">${ParentNamePrimLabel} / ${ParentNameSecLabel}</p><br/>${ParentName}<br/>${ParentNameSec}</td>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part1",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1204",
      "name": "Registration Acknowledgement Template - Part 2",
      "description": "Acknowledgement generated after registration - Part 2",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<td><p class=\"headings\">${ParentUINPrimLabel} / ${ParentUINSecLabel}</p><br/>${ParentUIN}</td></tr></table><br/><p ${DocumentsEnabled} class=\"head\"><b>${DocumentsPrimLabel}</b></p><div ${DocumentsEnabled} ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyDocuments\">${Modify}</button></div><hr ${DocumentsEnabled}/><table ${DocumentsEnabled}><tr><td><p class=\"headings\">${DocumentsPrimLabel} / ${DocumentsSecLabel}</p><br/>${Documents}<br/>${DocumentsSec}</td></tr></table><br/><p ${BiometricsEnabled} class=\"head\"><b>${BiometricsPrimLabel}</b></p><div ${BiometricsEnabled} ${Preview} class=\"modify\"><img src=\"${ModifyImageSource}\" border=\"0\" width=\"15\" height=\"15\"/><button id=\"modifyBiometrics\">${Modify}</button></div><hr ${BiometricsEnabled}/><table ${BiometricsEnabled}><tr><td><p class=\"headings\">${BiometricsPrimLabel} / ${BiometricsSecLabel}</p><br/>${Biometrics}<br/>${BiometricsSec}</td></tr></table><table ${IrisDisabled}><tr><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td></tr><tr><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td></tr></table><table ${IrisEnabled} ${WithException} class=\"biometricsTable\"><tr ${AckReceipt}><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td><td><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${Preview}><td><p class=\"headings\">${ExceptionPhotoPrimLabel} / ${ExceptionPhotoSecLabel}</p></td><td ${leftEyeCaptured}><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td ${rightEyeCaptured}><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${AckReceipt}><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td><div class=\"biometrics\"><h5 class=\"iris\">${LeftEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"iris\">${RightEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td><img src=\"${ExceptionImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td ${leftEyeCaptured}><img src=\"${CapturedLeftEye}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightEyeCaptured}><img src=\"${CapturedRightEye}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr></table><table ${IrisEnabled} class=\"tableWithoutException\" ${WithoutException}><tr ${AckReceipt}><td><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${Preview}><td ${leftEyeCaptured}><p class=\"headings\">${LeftEyePrimLabel} / ${LeftEyeSecLabel}</p></td><td ${rightEyeCaptured}><p class=\"headings\">${RightEyePrimLabel} / ${RightEyeSecLabel}</p></td></tr><tr ${AckReceipt}><td><div class=\"biometrics\"><h5 class=\"irisWithoutException\">${LeftEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"irisWithoutException\">${RightEye}</h5><img src=\"${EyeImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td ${leftEyeCaptured}><img src=\"${CapturedLeftEye}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightEyeCaptured}><img src=\"${CapturedRightEye}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr></table><table ${FingerprintsCaptured} class=\"biometricsTable\"><tr ${AckReceipt}><td><p class=\"headings\">${LeftPalmPrimLabel} / ${LeftPalmSecLabel}</p></td><td><p class=\"headings\">${RightPalmPrimLabel} / ${RightPalmSecLabel}</p></td><td><p class=\"headings\">${ThumbsPrimLabel} / ${ThumbsSecLabel}</p></td></tr><tr ${Preview}><td ${leftSlapCaptured}><p class=\"headings\">${LeftPalmPrimLabel} / ${LeftPalmSecLabel}</p></td><td ${rightSlapCaptured}><p class=\"headings\">${RightPalmPrimLabel} / ${RightPalmSecLabel}</p></td><td ${thumbsCaptured}><p class=\"headings\">${ThumbsPrimLabel} / ${ThumbsSecLabel}</p></td></tr>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part2",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1205",
      "name": "Registration Acknowledgement Template - Part 3",
      "description": "Acknowledgement generated after registration - Part 3",
      "fileFormatCode": "txt",
      "model": "velocity",
      "fileText": "<tr ${AckReceipt}><td><div class=\"biometrics\"><h5 class=\"leftLittle\">${leftLittle}</h5><h5 class=\"leftRing\">${leftRing}</h5><h5 class=\"leftMiddle\">${leftMiddle}</h5><h5 class=\"leftIndex\">${leftIndex}</h5><img src=\"${LeftPalmImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"rightIndex\">${rightIndex}</h5><h5 class=\"rightMiddle\">${rightMiddle}</h5><h5 class=\"rightRing\">${rightRing}</h5><h5 class=\"rightLittle\">${rightLittle}</h5><img src=\"${RightPalmImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td><td><div class=\"biometrics\"><h5 class=\"leftThumb\">${leftThumb}</h5><h5 class=\"rightThumb\">${rightThumb}</h5><img src=\"${ThumbsImageSource}\" border=\"0\" width=\"85\" height=\"80\"/></div></td></tr><tr ${Preview}><td ${leftSlapCaptured}><img src=\"${CapturedLeftSlap}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${rightSlapCaptured}><img src=\"${CapturedRightSlap}\" border=\"0\" width=\"85\" height=\"80\"/></td><td ${thumbsCaptured}><img src=\"${CapturedThumbs}\" border=\"0\" width=\"85\" height=\"80\"/></td></tr><tr ${AckReceipt}><td><p ${MissingLeftFingers} class=\"headings\">${LeftSlapExceptionPrim} / ${LeftSlapExceptionSec}</p></td><td><p ${MissingRightFingers} class=\"headings\">${RightSlapExceptionPrim} / ${RightSlapExceptionSec}</p></td><td><p ${MissingThumbs} class=\"headings\">${ThumbsExceptionPrim} / ${ThumbsExceptionSec}</p></td></tr><tr ${Preview}><td ${leftSlapCaptured}><p ${MissingLeftFingers} class=\"headings\">${LeftSlapExceptionPrim} / ${LeftSlapExceptionSec}</p></td><td ${rightSlapCaptured}><p ${MissingRightFingers} class=\"headings\">${RightSlapExceptionPrim} / ${RightSlapExceptionSec}</p></td><td ${thumbsCaptured}><p ${MissingThumbs} class=\"headings\">${ThumbsExceptionPrim} / ${ThumbsExceptionSec}</p></td></tr></table><hr/><table class=\"dataTable\"><tr><td ${ROImage}><img src=\"${ROImageSource}\" border=\"0\" width=\"80\" height=\"80\"/></td><td><p class=\"headings\">${RONamePrimLabel} / ${RONameSecLabel}</p><br/>${ROName}<br/>${RONameSec}</td><td><p class=\"headings\">${RegCenterPrimLabel} / ${RegCenterSecLabel}</p><br/>${RegCenter}<br/>${RegCenterSec}</td></tr></table><hr/><br/></div><div ${FaceCaptureEnabled} ${AckReceipt} class=\"photo\"><p class=\"applicantPhotoLabel\">${PhotoPrim} / ${PhotoSec}</p><img class=\"applicantPhoto\" src=\"${ApplicantImageSource}\" border=\"0\" width=\"100\" height=\"100\"/></div><div ${FaceCaptureEnabled} ${Preview} class=\"previewPhoto\"><p class=\"applicantPhotoLabel\">${PhotoPrim} / ${PhotoSec}</p><img class=\"applicantPhoto\" src=\"${ApplicantImageSource}\" border=\"0\" width=\"100\" height=\"100\"/></div><div ${AckReceipt}><p>${ImportantGuidelines}</p><ul><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim Ad minim veniam, quis nostrud exercitation. Ullamco laboris nisi ut aliquip exea commodo consequat. Duis aute irure dolor in Reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.Cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id.</span></li><br/><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et.</span></li><br/><li><span>Dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex.</span></li><br/><li><span>Commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat.Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim Ad minim veniam, quis nostrud exercitation. Ullamco laboris nisi ut aliquip exea commodo consequat. Duis aute irure dolor in Reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.Cupidatat non proident, sunt in culpa qui offici.</span></li><br/><li><span>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et.</span></li></ul></div></div></body></html>",
      "moduleId": "10005",
      "moduleName": "registration",
      "templateTypeCode": "reg-ack-template-part3",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "registrationclient",
      "name": "otp service",
      "description": "OTP Send Service",
      "fileFormatCode": "txt",
      "model": "string",
      "fileText": "Please find the OTP $otp",
      "moduleId": "10001",
      "moduleName": "login",
      "templateTypeCode": "otp-sms-template",
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
    },
    {
      "code": "auth-email-subject",
      "description": "Template for authorization subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "auth-sms",
      "description": "Template for authorization SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "otp-email-content",
      "description": "Template for Email Content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "otp-email-subject",
      "description": "Template for Email Subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "otp-sms",
      "description": "Template for OTP in SMS ",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "auth-email-content",
      "description": "قالب لمحتوى التخويل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "auth-email-subject",
      "description": "قالب لموضوع التخويل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "auth-sms",
      "description": "قالب لرسالة التفويض",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "otp-email-content",
      "description": "قالب لمحتوى البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "otp-email-subject",
      "description": "قالب لموضوع البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "otp-sms",
      "description": "قالب كلمة المرور لمرة واحدة في الرسالة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "auth-email-content",
      "description": "Modèle de contenu dautorisation",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "auth-email-subject",
      "description": "Modèle pour sujet dautorisation",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "auth-sms",
      "description": "Modèle de SMS dautorisation",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "otp-email-content",
      "description": "Modèle de contenu de courrier électronique",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "otp-email-subject",
      "description": "Modèle pour sujet demail",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "otp-sms",
      "description": "Modèle pour OTP dans SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_DUP_UIN_EMAIL",
      "description": "Template for duplicate UIN Email",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_DUP_UIN_SMS",
      "description": "Template for duplicate UIN SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_TEC_ISSUE_EMAIL",
      "description": "Template for Technical Issue Email",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_TEC_ISSUE_SMS",
      "description": "Template for Technical Issue SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_UIN_GEN_EMAIL",
      "description": "Template for UIN generation Email",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_UIN_GEN_SMS",
      "description": "Template for UIN generation SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_UIN_UPD_EMAIL",
      "description": "Template for update details Email",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_UIN_UPD_SMS",
      "description": "Template for update Details SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_DUP_UIN_EMAIL",
      "description": "قالب لبريد إلكتروني مكرر الهوية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_DUP_UIN_SMS",
      "description": "قالب لرسالة الهوية المكررة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_TEC_ISSUE_EMAIL",
      "description": "نموذج للبريد الإلكتروني لمشكلة فنية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_TEC_ISSUE_SMS",
      "description": "قالب لرسالة المشكلة الفنية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_UIN_GEN_EMAIL",
      "description": "قالب لتوليد الهوية البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_UIN_GEN_SMS",
      "description": "قالب لرسالة توليد الهوية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_UIN_UPD_EMAIL",
      "description": "قالب للحصول على تفاصيل التحديث",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_UIN_UPD_SMS",
      "description": "قالب لتحديث تفاصيل الرسالة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_DUP_UIN_EMAIL",
      "description": "Modèle de courrier didentité en double",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_DUP_UIN_SMS",
      "description": "Modèle de message didentité en double",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_TEC_ISSUE_EMAIL",
      "description": "Modèle pour courrier électronique de problème technique",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_TEC_ISSUE_SMS",
      "description": "Modèle de message de problème technique",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_UIN_GEN_EMAIL",
      "description": "Modèle de courrier électronique de génération didentité",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_UIN_GEN_SMS",
      "description": "Modèle de message de génération didentité",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_UIN_UPD_EMAIL",
      "description": "Modèle pour les détails de la mise à jour Email",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_UIN_UPD_SMS",
      "description": "Modèle pour la mise à jour Détails Message",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "NewReg-email-content-template",
      "description": "Template for new registration Email Content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "NewReg-email-subject-template",
      "description": "Template for new registration Email Subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "NewReg-sms-template",
      "description": "Template for new registration SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "OTP-email-content-template",
      "description": "Template for OTP generation Email Content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "OTP-email-subject-template",
      "description": "Template for OTP generation Email Subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "OTP-sms-template",
      "description": "Template for OTP SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Update-email-content-template",
      "description": "Template for update registration Email Content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Update-email-subject-template",
      "description": "Template for update registration Email Subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Update-sms-template",
      "description": "Template for update registration SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "NewReg-email-content-template",
      "description": "قالب للتسجيل الجديد محتوى البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "NewReg-email-subject-template",
      "description": "قالب للتسجيل الجديد البريد الإلكتروني الموضوع",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "NewReg-sms-template",
      "description": "قالب لرسالة التسجيل الجديدة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "OTP-email-content-template",
      "description": "قالب لتوليد OTP محتوى البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "OTP-email-subject-template",
      "description": "قالب لتوليد OTP البريد الإلكتروني الموضوع",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "OTP-sms-template",
      "description": "قالب لرسالة OTP",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Update-email-content-template",
      "description": "قالب لتحديث تسجيل محتوى البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Update-email-subject-template",
      "description": "قالب لتسجيل التحديث البريد الإلكتروني الموضوع",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Update-sms-template",
      "description": "قالب لرسالة تسجيل التحديث",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "NewReg-email-content-template",
      "description": "Modèle pour nouvelle inscription Email Content",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "NewReg-email-subject-template",
      "description": "Modèle pour nouvelle inscription Objet de le-mail",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "NewReg-sms-template",
      "description": "Modèle de nouvelle inscription SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "OTP-email-content-template",
      "description": "Modèle de contenu de courrier électronique de génération dOTP",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "OTP-email-subject-template",
      "description": "Modèle pour le sujet de-mail de génération dOTP",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "OTP-sms-template",
      "description": "Modèle pour SMS OTP",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Update-email-content-template",
      "description": "Modèle pour lenregistrement de la mise à jour",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Update-email-subject-template",
      "description": "Modèle denregistrement de mise à jour Objet de le-mail",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Update-sms-template",
      "description": "Modèle pour SMS denregistrement de mise à jour",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Email-Acknowledgement",
      "description": "Template for Email Acknowledgement",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Onscreen-Acknowledgement",
      "description": "Template for Onscreen Acknowledgment",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "otp-email-content-template",
      "description": "Template for OTP Email Content",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "otp-email-subject-template",
      "description": "Template for OTP Email Subject",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "otp-sms-template",
      "description": "Template for OTP SMS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "SMS-Acknowledgement",
      "description": "Template for SMS Acknowledgement",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Email-Acknowledgement",
      "description": "قالب لتأكيد البريد الإلكتروني",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Onscreen-Acknowledgement",
      "description": "قالب للشاشة شكر وتقدير",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "otp-email-content-template",
      "description": "قالب لمحتوى البريد الإلكتروني OTP",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "otp-email-subject-template",
      "description": "قالب لموضوع البريد الإلكتروني OTP",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "otp-sms-template",
      "description": "قالب ل OTP SMS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "SMS-Acknowledgement",
      "description": "قالب للإشعار SMS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Email-Acknowledgement",
      "description": "Template for email confirmation",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Onscreen-Acknowledgement",
      "description": "On-screen recognition template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "otp-email-content-template",
      "description": "OTP Email Content Template",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "otp-email-subject-template",
      "description": "Template for OTP email subject",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "otp-sms-template",
      "description": "Template for OTP SMS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "SMS-Acknowledgement",
      "description": "Template for SMS Acknowledgment",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Acknowledgement-email-subject",
      "description": "Template for email subject of Acknowledgement",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Acknowledgement-email-subject",
      "description": "قالب للتسليم البريد الكتروني الموضوع",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Acknowledgement-email-subject",
      "description": "Modèle pour le sujet d'email d'accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-sms-notification",
      "description": "Registration Acknowledgement Template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-sms-notification",
      "description": "نموذج شكر التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "reg-sms-notification",
      "description": "accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-email-notification",
      "description": "Registration Acknowledgement Template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-email-notification",
      "description": "نموذج شكر التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "reg-email-notification",
      "description": "accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-acknowledgement-template",
      "description": "Registration Acknowledgement Template",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-acknowledgement-template",
      "description": "نموذج شكر التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "reg-acknowledgement-template",
      "description": "accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-ack\n-template-part1",
      "description": "Registration Acknowledgement Template - Part 1",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-ack\n-template-part2",
      "description": "Registration Acknowledgement Template - Part 2",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-ack\n-template-part3",
      "description": "Registration Acknowledgement Template - Part 3",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part1",
      "description": "نموذج شكر التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part2",
      "description": "نموذج شكر التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part3",
      "description": "نموذج شكر التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part1",
      "description": "accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part2",
      "description": "accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part3",
      "description": "accusé de réception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part1",
      "description": "Registration Acknowledgement Template - Part 1",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part2",
      "description": "Registration Acknowledgement Template - Part 2",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "reg-ack-template-part3",
      "description": "Registration Acknowledgement Template - Part 3",
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
    },
    {
      "code": "xml",
      "description": "XML File",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "json",
      "description": "Json File",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "txt",
      "description": "ملف نصي",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "xml",
      "description": "ملف XML",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "json",
      "description": "ملف Json",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "txt",
      "description": "Fichier texte",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "xml",
      "description": "Fichier XML",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "json",
      "description": "Fichier Json",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "html",
      "description": "html File",
      "isDeleted": false,
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
    },
    {
      "code": "CLR",
      "name": "Client Rejection",
      "description": "Rejection in Registration Client",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "MNA",
      "name": "الفصل اليدوي",
      "description": "رفض خلال الفصل اليدوي",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "CLR",
      "name": "رفض العميل",
      "description": "رفض تسجيل العميل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "MNA",
      "name": "Manuel arbitrage",
      "description": "Renvoi en cours de sélection manuelle",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "CLR",
      "name": "Rejet de client",
      "description": "Rejet en enregistrement Client",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "code": "GPM",
      "name": "Gender-Photo Mismatch",
      "description": "Gender-Photo Mismatch between Gender and Photo ",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "IAD",
      "name": "Invalid Address",
      "description": "Invalid Address found",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "DPG",
      "name": "Duplicate Registration",
      "description": "Duplicate Registration found",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "OTH",
      "name": "Others",
      "description": "Others",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "ADM",
      "name": "All the Details are matching",
      "description": "All the Details are matching",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "ADD",
      "name": "All the Demographic Details are Matching",
      "description": "All the Demographic Details are Matching",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "OPM",
      "name": "Only the Photograph is Matching",
      "description": "Only the Photograph is Matching",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "SDM",
      "name": "Some of the Demographic Details are Matching",
      "description": "Some of the Demographic Details are Matching",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "APM",
      "name": "عدم تطابق العمر-صور",
      "description": "حدث عدم تطابق بين العمر وصور",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "GPM",
      "name": "عدم تطابق نوع الجنس-صور",
      "description": "عدم تطابق نوع الجنس-صور بين الجنسين وصور ",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "IAD",
      "name": "عنوان غير صالح",
      "description": "يتم العثور على عنوان غير صالح",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "DPG",
      "name": "تسجيل مكرر",
      "description": "تكرار التسجيل العثور على",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "OTH",
      "name": "الآخرين",
      "description": "الآخرين",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "ADM",
      "name": "يتم مطابقة جميع التفاصيل",
      "description": "يتم مطابقة جميع التفاصيل",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "ADD",
      "name": "جميع تفاصيل ديموغرافية هي مطابقة",
      "description": "جميع تفاصيل ديموغرافية هي مطابقة",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "OPM",
      "name": "إلا الصورة هي مطابقة",
      "description": "إلا الصورة هي مطابقة",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "SDM",
      "name": "بعض التفاصيل الديمغرافية هي مطابقة",
      "description": "بعض التفاصيل الديمغرافية هي مطابقة",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "APM",
      "name": "Décalage de lâge-Photo",
      "description": "Discordance entre lâge et la Photo",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "GPM",
      "name": "Incompatibilité de sexe-Photo",
      "description": "Sexe-Photo discordance entre le sexe et la Photo ",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "IAD",
      "name": "Adresse non valide",
      "description": "Adresse non valide trouvée",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "DPG",
      "name": "Enregistrement en double",
      "description": "Double enregistrement trouvé",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "OTH",
      "name": "Dautres",
      "description": "Dautres",
      "rsnCatCode": "CLR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "ADM",
      "name": "Tous les détails sont adaptent",
      "description": "Tous les détails sont adaptent",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "ADD",
      "name": "Tous les détails démographiques sont Matching",
      "description": "Tous les détails démographiques sont Matching",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "OPM",
      "name": "La photographie est le rapprochement",
      "description": "La photographie est le rapprochement",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "SDM",
      "name": "Certains détails démographiques sont Matching",
      "description": "Certains détails démographiques sont Matching",
      "rsnCatCode": "MNA",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "word": "damn",
      "description": "Blacklisted Word",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "word": "nigga",
      "description": "Blacklisted Word",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "word": "dammit",
      "description": "Blacklisted Word",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "word": "الخراء",
      "description": "كلمة القائمة السوداء",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "word": "لعنة",
      "description": "كلمة القائمة السوداء",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "word": "نيغا",
      "description": "كلمة القائمة السوداء",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "word": "اللعنة",
      "description": "كلمة القائمة السوداء",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "word": "Merde",
      "description": "Mot sur la liste noire",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "word": "Damn",
      "description": "Mot sur la liste noire",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "word": "nigga",
      "description": "Mot sur la liste noire",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "word": "bon sang",
      "description": "Mot sur la liste noire",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "word": "fuk",
      "description": "fuk word",
      "isDeleted": true,
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
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "MOR",
      "name": "Maroc",
      "hierarchyLevel": 0,
      "hierarchyName": "Pays",
      "parentLocCode": null,
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "RSK",
      "name": "Rabat Sale Kenitra",
      "hierarchyLevel": 1,
      "hierarchyName": "Region",
      "parentLocCode": "MOR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "RSK",
      "name": "جهة الرباط سلا القنيطرة",
      "hierarchyLevel": 1,
      "hierarchyName": "منطقة",
      "parentLocCode": "MOR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "RSK",
      "name": "Rabat-Salé-Kénitra",
      "hierarchyLevel": 1,
      "hierarchyName": "Région",
      "parentLocCode": "MOR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "KTA",
      "name": "Kenitra",
      "hierarchyLevel": 2,
      "hierarchyName": "Province",
      "parentLocCode": "RSK",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "KTA",
      "name": "القنيطرة",
      "hierarchyLevel": 2,
      "hierarchyName": "المحافظة",
      "parentLocCode": "RSK",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "KTA",
      "name": "Kénitra",
      "hierarchyLevel": 2,
      "hierarchyName": "Province",
      "parentLocCode": "RSK",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "BNMR",
      "name": "Ben Mansour",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "BNMR",
      "name": "بن منصور",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "BNMR",
      "name": "Ben Mansour",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14022",
      "name": "14022",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "BNMR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14022",
      "name": "14022",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "BNMR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14022",
      "name": "14022",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "BNMR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "MNAS",
      "name": "Mnasra",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MNAS",
      "name": "منَسرَ ",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "MNAS",
      "name": "Mnasra",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14053",
      "name": "14053",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "MNAS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14053",
      "name": "14053",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "MNAS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14053",
      "name": "14053",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "MNAS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "MOGR",
      "name": "Mograne",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MOGR",
      "name": "مڭرن",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "MOGR",
      "name": "Mograne",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14023",
      "name": "14023",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "MOGR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14023",
      "name": "14023",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "MOGR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14023",
      "name": "14023",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "MOGR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "ASSM",
      "name": "Assam",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "ASSM",
      "name": "العصام",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "ASSM",
      "name": "Assam",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14000",
      "name": "14000",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "ASSM",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14000",
      "name": "14000",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "ASSM",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14000",
      "name": "14000",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "ASSM",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "MEHD",
      "name": "Mehdia",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MEHD",
      "name": "مهدية",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "MEHD",
      "name": "Mehdia",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14110",
      "name": "14110",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "MEHD",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14110",
      "name": "14110",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "MEHD",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14110",
      "name": "14110",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "MEHD",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "OLOJ",
      "name": "Ouled Oujih",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "OLOJ",
      "name": "اولاد اوجيه",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "OLOJ",
      "name": "Ouled Oujih",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14080",
      "name": "14080",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "OLOJ",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14080",
      "name": "14080",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "OLOJ",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14080",
      "name": "14080",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "OLOJ",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "SDTB",
      "name": "Sidi Taibi",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "SDTB",
      "name": "سيدي الطيبي",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "SDTB",
      "name": "Sidi Taibi",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14025",
      "name": "14025",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "SDTB",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14025",
      "name": "14025",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "SDTB",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14025",
      "name": "14025",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "SDTB",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "SATZ",
      "name": "Sidi Allal Tazi",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "SATZ",
      "name": "علال التازي",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "SATZ",
      "name": "Sidi Allal Tazi",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "KTA",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "14050",
      "name": "14050",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "SATZ",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "14050",
      "name": "14050",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "SATZ",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "14050",
      "name": "14050",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "SATZ",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "RBT",
      "name": "Rabat",
      "hierarchyLevel": 2,
      "hierarchyName": "Province",
      "parentLocCode": "RSK",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "RBT",
      "name": "الرباط",
      "hierarchyLevel": 2,
      "hierarchyName": "المحافظة",
      "parentLocCode": "RSK",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "RBT",
      "name": "Rabat",
      "hierarchyLevel": 2,
      "hierarchyName": "Province",
      "parentLocCode": "RSK",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "AGDL",
      "name": "Agdal",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "AGDL",
      "name": "أكدال",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "AGDL",
      "name": "Agdal",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10106",
      "name": "10106",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "AGDL",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10106",
      "name": "10106",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "AGDL",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10106",
      "name": "10106",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "AGDL",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "QRHS",
      "name": "Quartier Hassan",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "QRHS",
      "name": "حي حسان",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "QRHS",
      "name": "Quartier Hassan",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10000",
      "name": "10000",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "QRHS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "SOUS",
      "name": "Souissi",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "SOUS",
      "name": "السويسي",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10000",
      "name": "10000",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "QRHS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10000",
      "name": "10000",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "QRHS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "MOR",
      "name": "Morroco",
      "hierarchyLevel": 0,
      "hierarchyName": "Country",
      "parentLocCode": null,
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "SOUS",
      "name": "Souissi",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10105",
      "name": "10105",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "SOUS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10105",
      "name": "10105",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "SOUS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10105",
      "name": "10105",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "SOUS",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "MADI",
      "name": "Madinat Al Irfane",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MADI",
      "name": "مدينة العرفان",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "MADI",
      "name": "Madinat Al Irfane",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10112",
      "name": "10112",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "MADI",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10112",
      "name": "10112",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "MADI",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10112",
      "name": "10112",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "MADI",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "HARD",
      "name": "Hay Riad",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "HARD",
      "name": "حي الرياض",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "HARD",
      "name": "Hay Riad",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10104",
      "name": "10104",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "HARD",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10104",
      "name": "10104",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "HARD",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10104",
      "name": "10104",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "HARD",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "MDDR",
      "name": "Medina de Rabat",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "MDDR",
      "name": "مدينة",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "MDDR",
      "name": "Médina de Rabat",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10036",
      "name": "10036",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "MDDR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10036",
      "name": "10036",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "MDDR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10036",
      "name": "10036",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "MDDR",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "ELYF",
      "name": "EL YOUSSOUFIA",
      "hierarchyLevel": 3,
      "hierarchyName": "Local Administrative Authority",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "ELYF",
      "name": "اليوسفية",
      "hierarchyLevel": 3,
      "hierarchyName": "الهيئة الإدارية المحلية",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "ELYF",
      "name": "EL YOUSSOUFIA",
      "hierarchyLevel": 3,
      "hierarchyName": "Autorité administrative locale",
      "parentLocCode": "RBT",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "10190",
      "name": "10190",
      "hierarchyLevel": 4,
      "hierarchyName": "Postal Code",
      "parentLocCode": "ELYF",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "10190",
      "name": "10190",
      "hierarchyLevel": 4,
      "hierarchyName": "الرمز البريدي",
      "parentLocCode": "ELYF",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "10190",
      "name": "10190",
      "hierarchyLevel": 4,
      "hierarchyName": "code postal",
      "parentLocCode": "ELYF",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "bng",
      "name": "bng-south",
      "hierarchyLevel": 2,
      "hierarchyName": "city",
      "parentLocCode": "karnataka",
      "createdBy": null,
      "updatedBy": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "bng",
      "name": "bng-south",
      "hierarchyLevel": 2,
      "hierarchyName": "city",
      "parentLocCode": "karnataka",
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
    },
    {
      "code": "RTM",
      "name": "Right Thumb",
      "description": "Print of Right Thumb",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RIF",
      "name": "Right Index Finger",
      "description": "Print of Right Index Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "LMF",
      "name": "Left Middle Finger",
      "description": "Print of Left Middle Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RMF",
      "name": "Right Middle Finger",
      "description": "Print of Right Middle Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "LRF",
      "name": "Left Ring Finger",
      "description": "Print of Left Ring Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RRF",
      "name": "Right Ring Finger",
      "description": "Print of Right Ring Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "LLF",
      "name": "Left Little Finger",
      "description": "Print of Left Little Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RLF",
      "name": "Right Little Finger",
      "description": "Print of Right Little Finger",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "LIR",
      "name": "Left Iris",
      "description": "Print of Left Iris",
      "biometricTypeCode": "IRS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RIR",
      "name": "Right Iris",
      "description": "Print of Right Iris",
      "biometricTypeCode": "IRS",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "PTT",
      "name": "Photo",
      "description": "Print of Photo",
      "biometricTypeCode": "PHT",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "LTM",
      "name": "الإبهام الأيمن",
      "description": "طباعة إبهام الأيمن",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RTM",
      "name": "الإبهام الأيمن",
      "description": "طباعة إبهام الأيمن",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "LIF",
      "name": "السبابة اليسرى",
      "description": "طباعة سبابة اليسرى",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RIF",
      "name": "السبابة اليمنى",
      "description": "طباعة سبابة اليمنى",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "LMF",
      "name": "الإصبع الأوسط الأيسر",
      "description": "طباعة للاصبع الأوسط الأيسر",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RMF",
      "name": "الإصبع الأوسط الأيمن",
      "description": "طباعة للاصبع الأوسط الأيمن",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "LRF",
      "name": "البنصر الأيسر",
      "description": "الطباعة من اليسار خاتم الإصبع",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RRF",
      "name": "بنصر الحق",
      "description": "طباعة بنصر الحق",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "LLF",
      "name": "خنصر اليسرى",
      "description": "طباعة خنصر اليسرى",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RLF",
      "name": "خنصر اليمنى",
      "description": "طباعة خنصر اليمنى",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "LIR",
      "name": "قزحية العين اليسرى",
      "description": "طباعة من قزحية العين اليسرى",
      "biometricTypeCode": "IRS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RIR",
      "name": "قزحية العين اليمنى",
      "description": "طباعة قزحية الحق",
      "biometricTypeCode": "IRS",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "PTT",
      "name": "صور",
      "description": "طباعة الصور",
      "biometricTypeCode": "PHT",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "LTM",
      "name": "Pouce gauche",
      "description": "Impression du pouce gauche",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RTM",
      "name": "Pouce droit",
      "description": "Impression de votre pouce droit",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "LIF",
      "name": "Index gauche",
      "description": "Impression de lindex gauche",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RIF",
      "name": "Index droit",
      "description": "Impression de lindex droit",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "LMF",
      "name": "Doigt du milieu gauche",
      "description": "Impression du doigt du milieu gauche",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RMF",
      "name": "Doigt du milieu droit",
      "description": "Impression du doigt du milieu droit",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "LRF",
      "name": "Annulaire gauche",
      "description": "Impression de lannulaire gauche",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RRF",
      "name": "Annulaire droit",
      "description": "Impression de lannulaire droit",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "LLF",
      "name": "Auriculaire gauche",
      "description": "Impression de lauriculaire gauche",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RLF",
      "name": "Bon petit doigt",
      "description": "Impression dauriculaire droite",
      "biometricTypeCode": "FNR",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "LIR",
      "name": "Iris gauche",
      "description": "Impression de lIris gauche",
      "biometricTypeCode": "IRS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RIR",
      "name": "Droit dIris",
      "description": "Impression dIris droite",
      "biometricTypeCode": "IRS",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "PTT",
      "name": "Photo",
      "description": "Impression de Photo",
      "biometricTypeCode": "PHT",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "LIF",
      "name": "string",
      "description": "string",
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
    },
    {
      "code": "IRS",
      "name": "Iris",
      "description": "Iris of the applicant",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "PHT",
      "name": "Photo",
      "description": "Photo of the face of the applicant",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "FNR",
      "name": "بصمة الإصبع",
      "description": "بصمات الأصابع لمقدم الطلب",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "IRS",
      "name": "قزحية العين",
      "description": "آيريس لمقدم الطلب",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "PHT",
      "name": "صور",
      "description": "صورة لوجه مقدم الطلب",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "FNR",
      "name": "Empreintes digitales",
      "description": "Empreintes digitales du demandeur",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "IRS",
      "name": "Iris",
      "description": "Iris du demandeur",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "PHT",
      "name": "Photo",
      "description": "Photo du visage du demandeur",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "abc",
      "name": "string",
      "description": "string",
      "isDeleted": null,
      "langCode": "ara",
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
    },
    {
      "code": "0099999",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100000",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100001",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100002",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100003",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100004",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100005",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100006",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100007",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100008",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100009",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100010",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100012",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100011",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100013",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100014",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100015",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100016",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100017",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100018",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100019",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100020",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100021",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100022",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100023",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100024",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100026",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100025",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100027",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100028",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100029",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100030",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100031",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100032",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100033",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100037",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100035",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100036",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100038",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100040",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100041",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100039",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100042",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100043",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100044",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100034",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100045",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100046",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100047",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100048",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100049",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100050",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100051",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100052",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100053",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100054",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100055",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100056",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100057",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100058",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100059",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100060",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100061",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100062",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100063",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100064",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100065",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100066",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100067",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0100068",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0000999",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001000",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001001",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001002",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001003",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001004",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001005",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001006",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001007",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001008",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001009",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001010",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001011",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001012",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001013",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001014",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001015",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001016",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001017",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001018",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001019",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001020",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001021",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001022",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001023",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001024",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001025",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001026",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001027",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001028",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001030",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001029",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001031",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001032",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001033",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001034",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001035",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001036",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001037",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001038",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001039",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001040",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001041",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001042",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001043",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001044",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001045",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001046",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001047",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001048",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001049",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001050",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001051",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001052",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001053",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001054",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001055",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001056",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001057",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001058",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001059",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001060",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001061",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001062",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001064",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001063",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001065",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001066",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001067",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001068",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001069",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001070",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001071",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001072",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001073",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001074",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001075",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001076",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001077",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001078",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001079",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001080",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001081",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001082",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001083",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001084",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001085",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001086",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001087",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001088",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001089",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001090",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001091",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001092",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001093",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001094",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001095",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001096",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001097",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001098",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001099",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001100",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001118",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001102",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001119",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001106",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001111",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001114",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001105",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001101",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001113",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001116",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001108",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001110",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001117",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001115",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001104",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001109",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001103",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001129",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001138",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001130",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001139",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001166",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001141",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001128",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001132",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001142",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001160",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001136",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001134",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001121",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001140",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001152",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001164",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001162",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001125",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001157",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001135",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001137",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001169",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001124",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001182",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001150",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001181",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001196",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001200",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001193",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001197",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001202",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001190",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001198",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001194",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001204",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001189",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001206",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001171",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001201",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001172",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001167",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001175",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001161",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001210",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001163",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001203",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001212",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001217",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001173",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001220",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001219",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001229",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001213",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001209",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001168",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001144",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001227",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001228",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001191",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001153",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001188",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001147",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001199",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001174",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001225",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001176",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001192",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001240",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001233",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001214",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001231",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001250",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001237",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001232",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001234",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001239",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001241",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001195",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001211",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001247",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001207",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001236",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001258",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001235",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001224",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001243",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001252",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001275",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001259",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001272",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001262",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001246",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001244",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001245",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001263",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001276",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001274",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001226",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001221",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001216",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001260",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001254",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001292",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001297",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001280",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001296",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001281",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001278",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001269",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001270",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001286",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001264",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001273",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001253",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001222",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001223",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001186",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001299",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001300",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001303",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001261",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001279",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001230",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001126",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001123",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001282",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001127",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001285",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001289",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001256",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001242",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001284",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001257",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001288",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001205",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001294",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001310",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001255",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001177",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001215",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001180",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001323",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001321",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001325",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001277",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001309",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001156",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001265",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001306",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001312",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001301",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001155",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001179",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001308",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001320",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001271",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001251",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001328",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001249",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001266",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001332",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001248",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001267",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001338",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001348",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001350",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001322",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001347",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001340",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001333",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001353",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001317",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001351",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001339",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001342",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001287",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001335",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001304",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001343",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001337",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001344",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001354",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001331",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001345",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001336",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001341",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001361",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001352",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001133",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001356",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001298",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001208",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001365",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001131",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001290",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001369",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001367",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001364",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001120",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001307",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001363",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001158",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001187",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001218",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001362",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001349",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001370",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001387",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001389",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001386",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001371",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001383",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001385",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001377",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001384",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001318",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001374",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001368",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001311",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001178",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001372",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001291",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001315",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001376",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001346",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001238",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001314",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001355",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001295",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001143",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001122",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001360",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001293",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001357",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001366",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001112",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001379",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001149",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001185",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001373",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001324",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001326",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001378",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001396",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001394",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001148",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001411",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001390",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001397",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001151",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001170",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001413",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001416",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001401",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001392",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001443",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001442",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001417",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001410",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001381",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001415",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001159",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001388",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001412",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001425",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001421",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001334",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001305",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001313",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001283",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001327",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001330",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001380",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001447",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001445",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001433",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001434",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001426",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001404",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001405",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001406",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001408",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001450",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001449",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001438",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001439",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001398",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001435",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001183",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001448",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001414",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001455",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001444",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001457",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001465",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001454",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001464",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001399",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001456",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001476",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001446",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001409",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001452",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001451",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001154",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001268",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001329",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001427",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001458",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001462",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001463",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001483",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001485",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001486",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001493",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001461",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001484",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001491",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001488",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001494",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001492",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001487",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001479",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001489",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001478",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001496",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001514",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001505",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001490",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001502",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001510",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001441",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001460",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001477",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001440",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001495",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001509",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001424",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001501",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001453",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001459",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001107",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001316",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001146",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001358",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001515",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001375",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001184",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001391",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001302",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001359",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001499",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001526",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001528",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001527",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001407",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001521",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001508",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001504",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001529",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001497",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001525",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001523",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001507",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001431",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001500",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001393",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001534",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001550",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001402",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001470",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001524",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001530",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001422",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001395",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001517",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001543",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001469",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001400",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001518",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001432",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001535",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001498",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001436",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001428",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001565",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001562",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001506",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001423",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001420",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001566",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001429",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001467",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001473",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001542",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001468",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001538",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001437",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001382",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001520",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001564",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001567",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001466",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001475",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001519",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001575",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001511",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001419",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001319",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001533",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001592",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001561",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001556",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001571",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001558",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001569",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001568",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001570",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001522",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001532",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001531",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001516",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001555",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001591",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001588",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001546",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001482",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001557",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001586",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001541",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001582",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001512",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001513",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001594",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001503",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001549",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001596",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001577",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001403",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001430",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001573",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001418",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001480",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001547",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001544",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001579",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001536",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001559",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001548",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001595",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001481",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001625",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001623",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001545",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001474",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001624",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001626",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001560",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001578",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001537",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001576",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001540",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001580",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001585",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001605",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001645",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001638",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001603",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001629",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001593",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001604",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001574",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001553",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001600",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001616",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001554",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001620",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001614",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001589",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001601",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001612",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001637",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001635",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001643",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001627",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001552",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001660",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001587",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001639",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001667",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001471",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001661",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001666",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001664",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001642",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001602",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001663",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001644",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001590",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001662",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001646",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001665",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001633",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001630",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001636",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001674",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001632",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001597",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001606",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001685",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001539",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001610",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001680",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001679",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001622",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001682",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001687",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001628",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001697",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001688",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001691",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001700",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001681",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001551",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001684",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001631",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001617",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001701",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001634",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001619",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001618",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001584",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001613",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001705",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001615",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001699",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001713",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001649",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001703",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001715",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001607",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001711",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001727",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001728",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001725",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001726",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001710",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001716",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001730",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001677",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001689",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001702",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001693",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001683",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001698",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001686",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001714",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001692",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001676",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001694",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001704",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001695",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001621",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001572",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001563",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001707",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001583",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001598",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001581",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001670",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001690",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001599",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001659",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001472",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001675",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001678",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001673",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001736",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001737",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001740",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001741",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001738",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001734",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001731",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001733",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001611",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001706",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001739",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001750",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001729",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001744",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001748",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001753",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001718",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001720",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001609",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001732",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001754",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001735",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001650",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001672",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001776",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001766",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001742",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001696",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001723",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001709",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001768",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001763",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001764",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001772",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001793",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001784",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001792",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001779",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001791",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001743",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001751",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001778",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001765",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001782",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001767",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001771",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001773",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001774",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001799",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001800",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001788",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001797",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001801",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001786",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001790",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001657",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001783",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001795",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001769",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001798",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001608",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001655",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001780",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001640",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001762",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001785",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001656",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001787",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001755",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001708",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001796",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001641",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001712",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001794",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001722",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001647",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001817",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001658",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001721",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001807",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001804",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001789",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001812",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001805",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001816",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001668",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001652",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001834",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001814",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001819",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001653",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001818",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001830",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001815",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001824",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001820",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001724",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001648",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001813",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001821",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001717",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001669",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001829",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001671",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001828",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001761",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001770",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001808",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001719",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001752",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001775",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001806",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001849",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001810",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001848",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001850",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001802",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001826",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001809",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001827",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001803",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001811",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001851",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001861",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001756",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001825",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001859",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001823",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001654",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001758",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001871",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001855",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001895",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001651",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001873",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001840",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001870",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001842",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001847",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001872",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001878",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001912",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001843",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001864",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001749",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001747",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001911",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001760",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001746",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001852",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001836",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001839",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001757",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001877",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001845",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001833",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001844",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001759",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001745",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001908",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001915",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001919",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001869",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001868",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001835",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001867",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001777",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001879",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001874",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001923",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001846",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001832",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001838",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001882",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001841",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001924",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001822",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001921",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001932",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001914",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001900",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001916",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001922",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001920",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001781",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001831",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001893",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001939",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001862",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001853",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001860",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001857",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001909",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001837",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001876",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001858",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001940",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001913",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001866",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001865",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001926",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001856",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001854",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001889",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001901",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001943",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001903",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001885",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001930",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001881",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001944",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001952",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001965",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001966",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001887",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001897",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001947",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001863",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001950",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001875",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001907",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001910",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001941",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001933",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001938",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001891",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001942",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001918",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001892",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001945",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001880",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001974",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001980",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001961",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001979",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001890",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001948",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001964",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001963",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001896",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001985",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001993",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001986",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001978",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001946",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001975",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001949",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001929",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001928",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001936",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001984",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001935",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001990",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001955",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001934",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001925",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001970",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001976",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001973",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001888",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001951",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001972",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001981",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001956",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001995",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001983",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001886",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001905",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001962",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001894",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001902",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001898",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001917",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001959",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001883",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001998",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001982",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001957",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002010",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001884",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002015",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001971",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002013",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002014",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001996",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002000",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002016",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001953",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002024",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002041",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002035",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002025",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002028",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002039",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002030",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001931",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001937",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002022",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002053",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002021",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001906",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002020",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002033",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002006",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001992",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002038",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002042",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002037",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002050",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001958",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002032",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002003",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001994",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001967",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001991",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002019",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001927",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002066",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001977",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002008",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002018",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002052",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002040",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001997",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001987",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001954",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002046",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001904",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002034",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002017",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001960",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002044",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001968",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002043",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002048",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002051",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002027",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002005",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002036",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002029",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002045",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001989",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002047",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002072",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002070",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002075",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002073",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002071",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001969",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002007",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002004",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002002",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002009",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002097",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002102",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002161",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002189",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002154",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002219",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002135",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002244",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002250",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002302",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002322",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002359",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002248",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002374",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002393",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002279",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002465",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002459",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002340",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002481",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002505",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002550",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002609",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002580",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002594",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002433",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002608",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002671",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002681",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002661",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002744",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002665",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002804",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002786",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002815",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002820",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002868",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002873",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002649",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002933",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002956",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002964",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002978",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002953",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002963",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003021",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003004",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003051",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003107",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003169",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003148",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003151",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003199",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003139",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003091",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003234",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003288",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003152",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003281",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003294",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003371",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003344",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003361",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003453",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003448",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003462",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003489",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003525",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003531",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003560",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003567",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003434",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003595",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003633",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003597",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003709",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003671",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003746",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003537",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003593",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003660",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003774",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003816",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003827",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003888",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003878",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003884",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002023",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002120",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002062",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002160",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002078",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002194",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002206",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002266",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002088",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002303",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002110",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002297",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002331",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002334",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002377",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002386",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002337",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002425",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002458",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002477",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002470",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002508",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002553",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002520",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002604",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002620",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002629",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002510",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002621",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002696",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002679",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002767",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002714",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002796",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002749",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002818",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002821",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002614",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002896",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002706",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002911",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002766",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002876",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002960",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003012",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002913",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003007",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003010",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003030",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003110",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003161",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003114",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003133",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003201",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003112",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003236",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003225",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003276",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003309",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003314",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003086",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003352",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003377",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003389",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003406",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003450",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003505",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003474",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003521",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003454",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003551",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003327",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003429",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003613",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003637",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003607",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003703",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003704",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003697",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003773",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003743",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003689",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003850",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003817",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003812",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003874",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003803",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003921",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002031",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002076",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002095",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002165",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002172",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002001",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002090",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002173",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002215",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002239",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002319",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002305",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002290",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002327",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002298",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002380",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002431",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002434",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002457",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002501",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002495",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002552",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002539",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002611",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002593",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002572",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002625",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002636",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002601",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002703",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002754",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002769",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002738",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002790",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002780",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002784",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002830",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002831",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002899",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002898",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002840",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002968",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002977",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002967",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002992",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002998",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003065",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002995",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003089",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003067",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003157",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003177",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003150",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003191",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003212",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003062",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003235",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003269",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003310",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003304",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003251",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003353",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003384",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003369",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003442",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003438",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003490",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003398",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003523",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003539",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003575",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003349",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003449",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003631",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003585",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003645",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003684",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003694",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003659",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003669",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003748",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003761",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003821",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003818",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003799",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003859",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003801",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003918",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001999",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002059",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002099",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002152",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002201",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002176",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002218",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002193",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002243",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002299",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002325",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002329",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002314",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002254",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002294",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002321",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002304",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002396",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002418",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002490",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002502",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002414",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002542",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002565",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002556",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002600",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002634",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002615",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002653",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002701",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002755",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002732",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002746",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002789",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002806",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002812",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002850",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002802",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002849",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002654",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002843",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002971",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002962",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002958",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002976",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002990",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003054",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003002",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003100",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003131",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003163",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003080",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003117",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003128",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003210",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003103",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003230",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003289",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003312",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003285",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003308",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003385",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003350",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003428",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003366",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003430",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003488",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003437",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003522",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003526",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003440",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003390",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003602",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003603",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003467",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003655",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003713",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003682",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003753",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003733",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003756",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003776",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003808",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003775",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003673",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003861",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003904",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003922",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002094",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002118",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002081",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002151",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002174",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002183",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002190",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002208",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002217",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002286",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002285",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002330",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002369",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002368",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002262",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002207",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002426",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002412",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002410",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002503",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002497",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002546",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002545",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002599",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002564",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002533",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002632",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002647",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002613",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002697",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002739",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002741",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002779",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002783",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002781",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002834",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002854",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002867",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002860",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002910",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002829",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002938",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002934",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002999",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002997",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003028",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003024",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002975",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003105",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003115",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003121",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003123",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003181",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003211",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003205",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003070",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003259",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003287",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003279",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003291",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003283",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003355",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003075",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003433",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003445",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003386",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003494",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003501",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003528",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003395",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003552",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003323",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003605",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003600",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003604",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003638",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003679",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003614",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003745",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003747",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003770",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003786",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003824",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003782",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003798",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003898",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003835",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003848",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002106",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002132",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002085",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002148",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002150",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002157",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002209",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002235",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002213",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002261",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002269",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002311",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002373",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002064",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002278",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002397",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002404",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002339",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002452",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002491",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002500",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002343",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002547",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002567",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002562",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002558",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002630",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002640",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002657",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002705",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002757",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002733",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002740",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002797",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002823",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002713",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002824",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002674",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002885",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002750",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002856",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002925",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002891",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002957",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002930",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003039",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003031",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003001",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003085",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003135",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003162",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003069",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003108",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003200",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003193",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003223",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003222",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003268",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003305",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003303",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003336",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003381",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003337",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003357",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003439",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003402",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003491",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003495",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003520",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003541",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003533",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003326",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003436",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003558",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003580",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003588",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003701",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003658",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003644",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003758",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003749",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003730",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003852",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003820",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003757",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003902",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003869",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003832",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002011",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002084",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002143",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002158",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002156",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002203",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002228",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002133",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002216",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002130",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002318",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002274",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002362",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002252",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002310",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002296",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002388",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002461",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002344",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002486",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002496",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002478",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002423",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002577",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002444",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002538",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002631",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002660",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002648",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002700",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002694",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002667",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002778",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002682",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002827",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002765",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002819",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002752",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002759",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002847",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002838",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002879",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002875",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002950",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002972",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002979",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003058",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002993",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003092",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003095",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003096",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003072",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003145",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003203",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003227",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003153",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003254",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003253",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003247",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003284",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003320",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003322",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003298",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003404",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003403",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003397",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003480",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003512",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003509",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003538",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003499",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003557",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003471",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003599",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003620",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003652",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003639",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003670",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003699",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003656",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003640",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003796",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003849",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003822",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003810",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003838",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003854",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003910",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002054",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002079",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002139",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002147",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002168",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002188",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002055",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002012",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002270",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002280",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002271",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002116",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002371",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002351",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002291",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002211",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002392",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002469",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002456",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002492",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002522",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002531",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002544",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002592",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002573",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002504",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,