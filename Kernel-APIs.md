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

## 3.2 Sync Master data-get service

### `GET /syncdata`

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
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002624",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002513",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002514",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002699",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002756",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002685",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002736",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002707",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002817",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002712",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002866",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002846",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002853",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002908",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002844",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002926",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002969",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002877",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002880",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003027",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003042",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003023",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003101",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003087",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003166",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003079",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003127",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003116",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003198",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003239",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003252",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003229",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003280",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003249",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003341",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003378",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003081",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003431",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003447",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003435",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003432",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003486",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003527",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003571",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003506",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003565",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003394",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003619",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003587",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003634",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003690",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003719",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003723",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003750",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003744",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003778",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003777",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003813",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003809",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003871",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003795",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003893",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002077",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002121",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002068",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002057",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002186",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002153",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002195",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002231",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002251",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002307",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002253",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002123",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002370",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002315",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002265",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002407",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002398",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002421",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002405",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002474",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002530",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002532",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002511",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002588",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002576",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002537",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002574",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002658",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002641",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002704",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002663",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002768",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002782",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002803",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002677",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002716",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002832",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002664",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002900",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002887",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002861",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002918",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002921",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003011",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002935",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003022",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003044",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003033",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003124",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003156",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003164",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003179",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003185",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003195",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003190",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003264",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003208",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003231",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003250",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003317",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003373",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003346",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003296",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003364",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003392",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003466",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003425",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003487",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003519",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003536",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003563",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003576",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003535",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003611",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003601",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003626",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003706",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003710",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003720",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003767",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003760",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003790",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003772",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003851",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003826",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003895",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003886",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003890",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002074",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002060",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002058",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002100",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002083",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002199",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002080",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002093",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002277",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002300",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002063",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002332",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002353",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002257",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002400",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002350",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002415",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002341",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002448",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002485",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002525",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002536",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002454",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002582",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002579",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002450",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002628",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002638",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002619",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002734",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002743",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002772",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002785",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002724",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002809",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002711",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002841",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002862",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002758",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002851",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002912",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002955",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002980",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002973",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003016",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003037",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003076",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003045",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003109",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003141",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003137",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003180",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003140",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003206",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003143",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003244",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003233",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003263",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003226",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003282",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003359",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003351",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003340",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003423",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003443",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003475",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003451",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003502",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003504",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003414",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003592",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003559",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003583",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003647",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003598",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003654",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003705",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003725",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003721",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003741",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003771",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003794",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003785",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003763",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003841",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003906",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003864",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003897",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002126",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002087",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002119",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002159",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002056",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002178",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002205",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001899",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002226",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002236",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002282",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002348",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002354",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002367",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002409",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002349",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002403",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002413",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002451",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002468",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002527",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002543",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002506",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002555",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002559",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002571",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002568",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002698",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002656",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002708",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002753",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002748",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002777",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002751",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002764",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002788",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002855",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002833",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002901",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002801",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002949",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002991",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002932",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002982",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002952",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003015",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003056",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003013",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003038",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003088",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003120",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003182",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003174",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003097",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003215",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003246",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003277",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003224",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003297",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003342",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003360",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003370",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003078",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003358",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003391",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003461",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003507",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003497",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003508",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003452",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003542",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003554",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003444",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003618",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003612",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003668",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003681",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003712",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003722",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003718",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003742",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003793",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003734",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003823",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003739",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003924",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003858",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003934",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002096",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002107",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002113",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002086",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002170",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002202",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002230",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002249",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002268",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002267",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002313",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002364",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002352",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002255",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002406",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002276",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002389",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002345",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002427",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002494",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002526",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002549",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002441",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002438",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002428",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002548",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002627",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002642",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002637",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002683",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002715",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002771",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002775",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002800",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002773",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002805",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002839",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002710",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002857",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002892",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002916",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002985",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002961",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002919",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003009",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002989",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003050",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003000",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003125",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003113",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003154",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003170",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003183",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003098",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003218",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003243",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003255",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003267",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003271",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003313",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003375",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003380",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003068",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003367",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003421",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003479",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003492",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003470",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003500",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003550",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003510",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003324",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003400",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003630",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003594",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003648",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003579",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003714",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003729",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003755",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003702",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003779",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003781",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003837",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003819",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003845",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003856",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003908",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002091",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002141",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002109",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002089",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002184",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002212",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002092",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002103",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002125",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002283",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002301",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002358",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002366",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002127",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002429",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002357",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002375",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002466",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002347",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002424",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002419",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002476",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002439",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002519",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002589",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002610",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002590",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002509",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002643",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002728",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002729",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002770",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002745",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002791",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002810",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002798",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002828",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002688",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002848",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002845",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002915",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002966",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002927",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003006",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003026",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003019",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002986",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002996",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003130",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003155",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003160",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003172",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003144",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003209",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003258",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003265",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003221",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003260",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003333",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003321",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003374",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003379",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003383",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003411",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003407",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003441",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003469",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003478",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003529",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003577",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003427",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003553",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003410",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003617",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003653",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003674",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003707",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003726",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003711",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003754",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003643",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003759",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003792",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003815",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003862",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003853",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003925",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003844",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002114",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002137",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002101",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0001988",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002171",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002197",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002225",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002238",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002129",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002289",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002247",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002365",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002326",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002241",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002124",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002372",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002395",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002390",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002479",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002473",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002528",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002540",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002453",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002586",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002581",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002411",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002626",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002515",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002650",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002692",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002720",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002676",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002723",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002668",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002813",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002722",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002869",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002719",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002822",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002905",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002917",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002948",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002883",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002922",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003055",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002988",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002937",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003046",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003138",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003146",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003171",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003175",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003173",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003118",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003261",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003270",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003099",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003245",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003331",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003306",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003372",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003300",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003354",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003408",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003413",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003459",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003516",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003518",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003458",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003555",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003544",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003388",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003463",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003582",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003629",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003677",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003695",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003717",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003666",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003764",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003686",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003662",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003791",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003784",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003805",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003731",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003866",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003867",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002117",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002098",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002145",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002155",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002049",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002187",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002223",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002191",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002284",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002320",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002128",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002328",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002293",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002384",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002379",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002258",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002338",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002467",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002464",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002498",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002524",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002534",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002432",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002483",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002623",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002446",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002633",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002616",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002659",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002680",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002742",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002747",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002774",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002793",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002807",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002852",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002864",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002735",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002893",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002906",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002946",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002760",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002984",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002951",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003043",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003029",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003020",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002939",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003094",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003147",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003168",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003184",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003188",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003189",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003061",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003240",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003228",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003275",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003316",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003334",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003315",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003387",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003335",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003472",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003393",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003426",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003455",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003511",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003530",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003547",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003591",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003401",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003422",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003627",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003606",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003650",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003683",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003691",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003737",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003464",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003752",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003732",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003728",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003735",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003736",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003847",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003842",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003933",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002122",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002138",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002105",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002175",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002196",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002221",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002134",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002180",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002259",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002245",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002260",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002363",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002272",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002383",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002275",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002399",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002391",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002460",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002342",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002475",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002523",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002471",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002575",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002584",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002557",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002595",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002561",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002517",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002612",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002669",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002721",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002689",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002794",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002776",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002816",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002731",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002826",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002889",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002884",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002799",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002923",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002987",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002941",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002909",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002942",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002974",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003036",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003052",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003126",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002970",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003165",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003186",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003207",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003066",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003237",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003266",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003214",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003290",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003330",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003295",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003311",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003347",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003362",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003419",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003484",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003412",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003468",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003503",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003540",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003556",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003569",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003325",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003608",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003609",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003632",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003589",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003667",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003696",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003628",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003584",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003663",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003765",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003789",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003664",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003872",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003802",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003873",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003870",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002111",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002142",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002164",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002181",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002200",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002222",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002232",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002233",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002069",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002237",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002312",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002360",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002335",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002376",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002394",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002402",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002401",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002463",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002443",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002488",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002529",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002420",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002437",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002603",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002597",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002607",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002570",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002644",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002639",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002687",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002662",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002737",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002761",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002693",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002763",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002787",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002837",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002888",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002858",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002890",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002914",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002940",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002882",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002983",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002936",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003034",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003047",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003057",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003090",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003111",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003176",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003136",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003194",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003213",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003104",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003257",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003064",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003278",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003332",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003319",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003348",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003376",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003329",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003415",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003483",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003399",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003396",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003485",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003546",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003562",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003581",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003549",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003417",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003649",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003636",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003623",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003687",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003700",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003693",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003762",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003657",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003727",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003766",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003740",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003863",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003865",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003860",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003917",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002112",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002144",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002146",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002185",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002177",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002220",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002264",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002204",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002246",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002115",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002306",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002361",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002316",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002356",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002382",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002281",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002385",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002442",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002447",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002487",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002346",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002512",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002541",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002518",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002583",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002602",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002554",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002652",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002618",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002666",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002727",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002672",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002795",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002825",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002808",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002730",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002865",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002886",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002859",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002902",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002943",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002959",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002965",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002994",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003041",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003017",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003005",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003035",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003084",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003082",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003060",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003119",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003202",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003059",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003242",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003262",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003217",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003274",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003273",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003345",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003301",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003363",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003368",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003456",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003481",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003473",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003416",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003515",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003514",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003573",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003574",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003534",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003418",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003578",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003596",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003621",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003724",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003688",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003698",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003716",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003692",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003708",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003831",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003804",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003889",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003875",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003880",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003920",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002082",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002065",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002163",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002179",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002198",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002104",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002234",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002242",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002240",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002210",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002324",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002355",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002323",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002381",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002422",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002417",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002416",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002449",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002480",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002482",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002472",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002551",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002585",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002587",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002622",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002596",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002635",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002645",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002651",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002726",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002686",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002691",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002792",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002811",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002836",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002690",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002871",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002897",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002894",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002903",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002931",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002954",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002924",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003008",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003025",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003049",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003048",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003077",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003040",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003159",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003149",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003142",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003192",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003197",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003238",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003232",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003219",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003318",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003272",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003338",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003307",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003356",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003365",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003405",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003477",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003409",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003496",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003513",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003532",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003568",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003590",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003570",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003624",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003615",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003476",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003685",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003641",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003661",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003635",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003642",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003738",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003797",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003811",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003780",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003868",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003787",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003877",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003836",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002061",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002140",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002162",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002182",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002149",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002224",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002263",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002229",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002214",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002295",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002308",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002292",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002333",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002287",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002288",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002273",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002408",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002455",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002499",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002493",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002521",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002507",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002569",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002606",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002591",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002563",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002646",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002617",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002516",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002709",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002684",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002725",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002678",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002717",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002835",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002673",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002863",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002895",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002874",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002907",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002928",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002878",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002944",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002929",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003053",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003018",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003032",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003074",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003122",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003129",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003178",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003102",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003204",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003093",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003063",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003241",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003220",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003134",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003248",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003292",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003328",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003382",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003343",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003446",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003420",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003498",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003465",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003517",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003545",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003566",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003564",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003548",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003610",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003616",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003646",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003625",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003678",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003680",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003672",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003783",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003715",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003788",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003814",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003839",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003833",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003907",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003857",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003881",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002067",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002136",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002166",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002169",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002167",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002108",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002192",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002227",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002131",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002256",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002317",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002336",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002309",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002378",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002387",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002430",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002440",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002445",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002462",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002484",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002489",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002535",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002436",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002435",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002566",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002605",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002560",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002578",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002598",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002702",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002670",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002675",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002718",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002762",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002695",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002814",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002842",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002870",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002872",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002655",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002904",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002947",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002920",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002981",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003003",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002881",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002945",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003014",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003073",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003132",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003158",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003167",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003187",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003196",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003106",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003083",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003256",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003216",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003286",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003299",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003293",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003339",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003302",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003071",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003424",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003457",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003493",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003482",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003524",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003543",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003561",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003572",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003460",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003586",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003622",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003651",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003675",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003676",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003665",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003768",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003769",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003751",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003825",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003800",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003807",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003806",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003846",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003909",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0002026",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003901",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003939",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003885",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003894",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003855",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003913",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003830",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003899",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003829",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003923",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003892",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003828",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003887",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003900",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003876",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003919",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003912",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003882",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003834",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003927",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003926",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003896",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003903",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003980",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003891",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003979",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003929",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003914",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003928",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003981",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003916",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003915",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003940",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003930",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003932",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003936",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003937",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003938",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003935",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003879",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003905",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003967",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003971",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003945",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003968",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003977",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003987",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003978",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003965",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003983",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003986",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003964",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003840",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003984",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003993",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004013",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003954",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004008",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003941",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003973",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003955",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003995",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003944",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003951",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004011",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003962",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003950",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003956",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003996",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003947",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003883",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004012",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003958",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003948",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003943",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003999",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004032",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004033",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003946",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003992",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004009",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004014",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003975",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004016",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003961",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003994",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003957",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003959",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003985",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003991",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003988",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003953",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004010",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004017",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003952",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003970",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004001",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004043",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004046",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004036",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004031",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004037",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004030",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004042",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004038",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004018",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004040",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004047",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004039",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004041",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003974",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003960",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004027",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004050",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004035",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003989",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003942",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003972",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003969",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003963",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004024",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004034",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004048",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003949",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003911",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003982",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004059",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003990",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004070",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004055",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004101",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003966",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004058",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004090",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004045",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004091",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004064",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004061",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004056",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004051",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003976",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004097",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004098",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004089",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004072",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004057",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004062",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004075",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004049",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004092",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004023",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004081",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004052",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004022",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004073",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004019",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004026",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004071",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004080",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004003",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004086",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004020",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003843",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004067",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004054",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004079",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004044",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004063",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004083",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004060",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004053",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003998",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004104",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004077",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004084",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004095",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004099",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004066",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004078",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004088",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004082",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004068",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004093",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004096",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004100",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004108",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004074",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004069",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004094",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004121",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004117",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004137",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004132",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003997",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004015",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004025",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004118",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004065",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004120",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004000",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004112",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004115",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004076",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004135",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004085",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004168",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004134",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004180",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004029",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004105",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004163",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004155",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004002",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004157",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004109",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004131",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004156",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004147",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004150",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004119",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004005",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004146",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004128",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004129",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004142",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004173",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004184",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004167",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004177",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004169",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004176",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004183",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004181",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004178",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004171",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004006",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004154",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004159",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004182",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004138",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004170",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004139",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004179",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004152",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004148",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004158",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004195",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004200",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004202",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004196",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004197",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004144",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004198",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004162",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004172",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004130",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004151",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004193",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004189",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004153",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004141",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004190",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004114",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004004",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004103",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004124",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004107",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004201",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004191",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004199",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004207",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004087",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004215",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004143",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004192",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004208",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004194",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004203",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004133",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004209",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004211",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004214",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004116",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004205",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004149",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004229",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004007",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004217",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004218",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004223",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004021",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004127",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004106",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004113",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004222",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004126",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004160",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004224",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004123",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004232",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004136",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004145",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0003931",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004212",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004110",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004125",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004122",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004216",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004166",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004210",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004221",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004140",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004219",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004111",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004165",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004225",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004231",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004102",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004164",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004206",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004238",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004241",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004237",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004028",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004161",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004204",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004234",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004228",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004239",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004226",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004244",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004227",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004269",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004242",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004233",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004220",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004253",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004267",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004213",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004240",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004236",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004252",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004245",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004260",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004235",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004299",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004246",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004293",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004249",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004243",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004284",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004305",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004304",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004256",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004188",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004314",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004300",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004230",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004247",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004185",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004275",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004263",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004270",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004283",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004324",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004311",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004323",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004331",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004250",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004186",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004259",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004279",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004282",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004257",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004307",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004294",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004255",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004251",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004271",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004296",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004340",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004316",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004327",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004339",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004290",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004336",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004329",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004321",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004328",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004330",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004272",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004337",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004333",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004335",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004325",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004338",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004317",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004322",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004334",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004273",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004355",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004326",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004332",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004297",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004318",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004301",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004295",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004248",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004264",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004175",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004310",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004266",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004363",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004312",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004366",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004288",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004313",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004261",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004302",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004280",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004349",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004291",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004351",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004353",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004306",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004268",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004174",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004359",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004286",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004265",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004362",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004356",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004352",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004358",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004285",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004370",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004350",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004277",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004375",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004369",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004372",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004361",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004292",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004373",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004368",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004377",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004374",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004379",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004376",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004287",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004360",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004187",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004367",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004364",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004258",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004371",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004303",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004278",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004276",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004354",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004309",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004380",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004254",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004274",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004386",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004399",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004394",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004348",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004398",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004393",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004395",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004401",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004298",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004357",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004365",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004383",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004405",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004384",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004308",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004397",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004382",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004390",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004411",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004431",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004315",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004413",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004281",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004407",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004421",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004418",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004417",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004433",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004428",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004437",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004432",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004406",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004425",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004434",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004381",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004408",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004402",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004441",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004378",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004447",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004389",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004387",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004445",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004289",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004262",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004453",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004439",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004403",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004404",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004396",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004388",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004319",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004392",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004448",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004440",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004442",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004454",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004426",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004449",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004443",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004423",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004473",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004446",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004476",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004444",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004320",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004479",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004477",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004435",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004474",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004429",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004475",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004480",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004385",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004400",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004458",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004422",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004427",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004450",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004483",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004456",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004478",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004485",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004486",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004470",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004482",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004487",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004484",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004436",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004391",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004504",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004461",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004416",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004512",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004494",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004467",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004342",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004451",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004468",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004419",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004466",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004501",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004343",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004493",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004516",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004472",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004463",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004513",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004524",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004492",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004505",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004522",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004462",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004521",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004459",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004345",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004499",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004530",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004341",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004344",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004508",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004545",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004546",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004540",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004507",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004460",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004523",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004542",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004539",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004515",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004438",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004469",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004543",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004410",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004465",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004464",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004503",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004537",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004510",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004551",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004527",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004517",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004544",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004538",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004424",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004412",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004532",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004568",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004552",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004556",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004557",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004553",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004509",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004496",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004420",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004347",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004497",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004457",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004452",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004455",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004346",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004495",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004506",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004569",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004489",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004471",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004430",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004535",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004554",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004520",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004481",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004511",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004573",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004490",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004415",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004555",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004541",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004498",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004580",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004514",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004558",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004562",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004414",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004560",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004547",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004564",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004572",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004575",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004548",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004549",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004581",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004550",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004559",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004576",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004574",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004578",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004570",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004571",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004563",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004561",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004607",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004577",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004566",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004579",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004624",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004608",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004585",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004618",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004589",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004567",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004610",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004409",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004488",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004611",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004491",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004613",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004502",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004612",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004500",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004565",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004582",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004518",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004615",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004583",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004529",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004603",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004636",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004597",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004584",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004595",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004600",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004588",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004638",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004627",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004525",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004614",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004609",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004605",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004622",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004591",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004526",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004659",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004658",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004620",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004621",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004652",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004631",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004601",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004593",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004653",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004598",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004661",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004664",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004592",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004647",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004665",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004617",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004656",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004641",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004657",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004626",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004676",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004650",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004663",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004651",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004654",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004655",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004662",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004673",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004682",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004683",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004675",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004646",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004632",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004533",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004637",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004536",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004695",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004648",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004686",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004644",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004674",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004660",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004635",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004599",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004596",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004594",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004689",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004634",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004688",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004706",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004703",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004721",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004700",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004680",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004696",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004649",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004709",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004685",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004690",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004717",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004697",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004639",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004671",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004684",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004687",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004694",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004710",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004693",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004604",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004692",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004666",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004628",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004640",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004534",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004698",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004708",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004724",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004704",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004667",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004713",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004725",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004718",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004679",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004681",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004633",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004602",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004701",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004728",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004711",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004699",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004691",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004672",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004606",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004619",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004712",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004744",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004732",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004723",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004734",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004740",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004733",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004761",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004748",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004747",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004735",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004745",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004625",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004531",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004586",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004630",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004737",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004528",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004767",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004746",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004742",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004738",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004753",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004669",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004722",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004645",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004716",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004765",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004769",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004629",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004707",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004771",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004727",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004587",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004519",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004702",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004715",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004668",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004705",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004729",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004758",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004719",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004714",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004726",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004750",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004741",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004743",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004791",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004760",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004763",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004773",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004749",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004739",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004797",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004766",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004736",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004762",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004802",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004616",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004838",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004623",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004778",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004836",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004808",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004821",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004820",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004772",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004815",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004804",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004777",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004803",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004825",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004812",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004782",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004643",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004790",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004792",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004755",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004781",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004843",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004785",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004783",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004730",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004795",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004670",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004720",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004764",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004793",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004590",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004731",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004768",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004788",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004817",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004796",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004800",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0999",
      "name": "TestN",
      "description": "TestDecs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "0004749",
      "name": "testing",
      "description": "testing",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "000",
      "name": "string",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "idTypes": [
    {
      "code": "UIN",
      "name": "Unique Identification Number",
      "descr": "National ID given to the applicant",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "PRID",
      "name": "Pre-registration ID",
      "descr": "ID assigned after Pre-registration",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RID",
      "name": "Registration ID",
      "descr": "ID assigned after registration",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "VID",
      "name": "Virtual ID",
      "descr": "ID used in replacement of UIN",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "Token ID",
      "name": "Token ID",
      "descr": "ID used by a vendor for an applicant",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "UIN",
      "name": "رقم تعريف فريد",
      "descr": "الهوية الوطنية المقدمة لمقدم الطلب",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "PRID",
      "name": "رقم التسجيل المسبق",
      "descr": "الرقم التعريفي بعد التسجيل المسبق",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RID",
      "name": "معرف تسجيل",
      "descr": "الرقم التعريفي بعد التسجيل",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "VID",
      "name": "معرف الظاهري",
      "descr": "معرف يستخدم في استبدال الهوية الوطنية",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "Token ID",
      "name": "معرف الرمز المميز",
      "descr": "معرف يستخدمه أحد البائعين لمقدم الطلب",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "UIN",
      "name": "Numéro didentification unique",
      "descr": "Carte didentité nationale fournie au demandeur",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "PRID",
      "name": "ID de pré-inscription",
      "descr": "ID attribué après la pré-inscription",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RID",
      "name": "ID denregistrement",
      "descr": "ID attribué après lenregistrement",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "VID",
      "name": "ID virtuel",
      "descr": "Identifiant utilisé en remplacement de UIN",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "Token ID",
      "name": "ID de jeton",
      "descr": "ID utilisé par un fournisseur pour un demandeur",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    }
  ],
  "titles": [
    {
      "code": "MIR",
      "titleName": "Mr",
      "titleDescription": "Male Title",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MRS",
      "titleName": "Mrs",
      "titleDescription": "Female Title",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MIS",
      "titleName": "Miss",
      "titleDescription": "Unmarried Female Title",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MIR",
      "titleName": "أستاذ",
      "titleDescription": "العنوان الذكور",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MRS",
      "titleName": "ست ",
      "titleDescription": "عنوان أنثى",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MIS",
      "titleName": "آنسة ",
      "titleDescription": "العنوان الإناث غير المتزوجات",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MIR",
      "titleName": "Monsieur",
      "titleDescription": "Titre masculin",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MRS",
      "titleName": "Madame",
      "titleDescription": "Titre féminin",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "MIS",
      "titleName": "Mademoiselle",
      "titleDescription": "Titre de femme célibataire",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    }
  ],
  "genders": [
    {
      "code": "MLE",
      "genderName": "Male",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "OTH",
      "genderName": "Others",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "MLE",
      "genderName": "الذكر",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "FLE",
      "genderName": "أنثى",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "OTH",
      "genderName": "الآخرين",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "MLE",
      "genderName": "Mâle",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "FLE",
      "genderName": "Femelle",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "OTH",
      "genderName": "Dautres",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "FLE",
      "genderName": "Female",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": false
    }
  ],
  "languages": [
    {
      "code": "eng",
      "name": "English",
      "family": "Indo-European",
      "nativeName": "English",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "ara",
      "name": "Arabic",
      "family": "Afro-Asiatic",
      "nativeName": "العَرَبِيَّة‎",
      "isDeleted": null,
      "isActive": true
    },
    {
      "code": "fra",
      "name": "French",
      "family": "Indo-European",
      "nativeName": "français",
      "isDeleted": null,
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
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "001",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "001",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "001",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "002",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "002",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "002",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "003",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "003",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "003",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "004",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "004",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "005",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "005",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "005",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "005",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "006",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "006",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "006",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "007",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "007",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "007",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "008",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "008",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "009",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "009",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "009",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "009",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "009",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "010",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "010",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "010",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "010",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "011",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "011",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "011",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "011",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "012",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "012",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "012",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "013",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "013",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "013",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "013",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "013",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "014",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "014",
      "docTypeCode": "RNC",
      "docCatCode": "POA"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "014",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "014",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "015",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "015",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "015",
      "docTypeCode": "CRN",
      "docCatCode": "POR"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "015",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "016",
      "docTypeCode": "CIN",
      "docCatCode": "POI"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "016",
      "docTypeCode": "COB",
      "docCatCode": "POB"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "appTypeCode": "016",
      "docTypeCode": "COE",
      "docCatCode": "POE"
    }
  ],
  "individualTypes": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "FR",
      "name": "Foreigner"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "code": "NFR",
      "name": "Non-Foreigner"
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "FR",
      "name": "أجنبي"
    },
    {
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true,
      "code": "NFR",
      "name": "غير أجنبي"
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "FR",
      "name": "Étranger"
    },
    {
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true,
      "code": "NFR",
      "name": "Non-étranger"
    }
  ],
  "appAuthenticationMethods": [
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "OFFICER",
      "authMethodCode": "PWD",
      "methodSequence": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "OFFICER",
      "authMethodCode": "OTP",
      "methodSequence": 2,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "SUPERVISOR",
      "authMethodCode": "PWD",
      "methodSequence": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "packet_auth",
      "roleCode": "OFFICER",
      "authMethodCode": "PWD",
      "methodSequence": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "eod_auth",
      "roleCode": "OFFICER",
      "authMethodCode": "IRIS",
      "methodSequence": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "exception_auth",
      "roleCode": "SUPERVISOR",
      "authMethodCode": "BIO",
      "methodSequence": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "exception_auth",
      "roleCode": "OFFICER",
      "authMethodCode": "FACE",
      "methodSequence": 2,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "onboard_auth",
      "roleCode": "OFFICER",
      "authMethodCode": "PWD",
      "methodSequence": 1,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "onboard_auth",
      "roleCode": "SUPERVISOR",
      "authMethodCode": "OTP",
      "methodSequence": 2,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
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
    },
    {
      "id": "10001",
      "name": "ما قبل التسجيل",
      "descr": "بوابة الويب للتسجيلات المسبقة",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10003",
      "name": "Registration Client",
      "descr": "Desktop application for Registrations",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10003",
      "name": "عميل التسجيل",
      "descr": "تطبيق سطح المكتب للتسجيلات",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10005",
      "name": "Registration Processor",
      "descr": "Application for post-registration process",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10005",
      "name": "معالج التسجيل",
      "descr": "طلب لعملية ما بعد التسجيل",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10007",
      "name": "ID Authentication",
      "descr": "Application for third party service provider authentication",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10007",
      "name": "مصادقة الهوية",
      "descr": "تطبيق لمصادقة موفر خدمة جهة خارجية",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10009",
      "name": "ID Control",
      "descr": "Web portal for configuring applications",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10009",
      "name": "التحكم في الهوية",
      "descr": "بوابة الويب لتكوين التطبيقات",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10011",
      "name": "Resident Portal",
      "descr": "Web portal for Post ID generation services",
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10011",
      "name": "بوابة المقيمين",
      "descr": "البوابة الإلكترونية لخدمات إنشاء معرف المشاركة",
      "langCode": "ara",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10001",
      "name": "Pré-inscription",
      "descr": "Portail Web pour les pré-inscriptions",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10003",
      "name": "Client dinscription",
      "descr": "Application de bureau pour les inscriptions",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10005",
      "name": "Processeur dinscription",
      "descr": "Demande de post-inscription",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10007",
      "name": "Authentification ID",
      "descr": "Application pour lauthentification du fournisseur de services tiers",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10009",
      "name": "Contrôle didentité",
      "descr": "Portail Web pour la configuration dapplications",
      "langCode": "fra",
      "isDeleted": null,
      "isActive": true
    },
    {
      "id": "10011",
      "name": "Portail Résident",
      "descr": "Portail Web pour les services de génération de post-ID",
      "langCode": "fra",
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
    },
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "SUPERVISOR",
      "priority": 2,
      "langCode": "eng",
      "isDeleted": null,
      "isActive": true
    },
    {
      "appId": "10003",
      "processId": "login_auth",
      "roleCode": "OFFICER",
      "priority": 3,
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
    },
    {
      "screenId": "loginRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "loginRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "loginRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "lostUINRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "lostUINRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "lostUINRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "newRegistrationRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "newRegistrationRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "newRegistrationRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "onBoardRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "onBoardRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "onBoardRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "registrationCorrectionRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "registrationCorrectionRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "registrationCorrectionRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "reportRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "reportRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "sendPacketServerRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "sendPacketServerRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "sendPacketServerRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "syncClientServerRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "syncClientServerRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "syncClientServerRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "syncServerClientRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "syncServerClientRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "syncServerClientRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "uinActivationRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "uinActivationRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "uinActivationRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "uinUpdateRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "uinUpdateRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "uinUpdateRoot",
      "roleCode": "SUPERADMIN",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "updateClientSoftwareRoot",
      "roleCode": "OFFICER",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "updateClientSoftwareRoot",
      "roleCode": "SUPERVISOR",
      "isPermitted": true,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "screenId": "updateClientSoftwareRoot",
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
    },
    {
      "id": "eod_auth",
      "name": "Eod authentication",
      "descr": "Eod authentication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "packet_auth",
      "name": "Packet authentication",
      "descr": "Packet authentication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "exception_auth",
      "name": "Exception authentication",
      "descr": "Exception authentication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "onboard_auth",
      "name": "Onboard authentication",
      "descr": "Onboard authentication",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "login_auth",
      "name": "مصادقة تسجيل الدخول",
      "descr": "مصادقة تسجيل الدخول",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "eod_auth",
      "name": "التخلص من الذخائر المتفجرة المصادقة",
      "descr": "التخلص من الذخائر المتفجرة المصادقة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "packet_auth",
      "name": "حزمة المصادقة",
      "descr": "حزمة المصادقة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "exception_auth",
      "name": "استثناء المصادقة",
      "descr": "استثناء المصادقة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "onboard_auth",
      "name": "مصادقة على متن الطائرة",
      "descr": "مصادقة على متن الطائرة",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "login_auth",
      "name": "Authentification de connexion",
      "descr": "Authentification de connexion",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "eod_auth",
      "name": "Authentification de nem",
      "descr": "Authentification de nem",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "packet_auth",
      "name": "Authentification de paquet",
      "descr": "Authentification de paquet",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "exception_auth",
      "name": "Authentification d’exception",
      "descr": "Authentification d’exception",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "onboard_auth",
      "name": "Authentification intégrée",
      "descr": "Authentification intégrée",
      "isDeleted": null,
      "langCode": "fra",
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
    },
    {
      "regCenterId": "10007",
      "deviceId": "3000047",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10007",
      "deviceId": "3000067",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10007",
      "deviceId": "3000087",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10007",
      "deviceId": "3000107",
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
    },
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000047",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000067",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000087",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000107",
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
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "deviceId": "3000047",
      "effectivetimes": "2019-02-27T10:50:57.589Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "deviceId": "3000067",
      "effectivetimes": "2019-02-27T10:50:57.589Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "deviceId": "3000087",
      "effectivetimes": "2019-02-27T10:50:57.589Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "deviceId": "3000107",
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
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000047",
      "effectivetimes": "2019-02-27T10:50:57.607964"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000067",
      "effectivetimes": "2019-02-27T10:50:57.607964"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000087",
      "effectivetimes": "2019-02-27T10:50:57.607964"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10007",
      "machineId": "10007",
      "deviceId": "3000107",
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


## 3.2 Config details-get service

This service will return back the global and registration configuration data of the MOSIP platform. 

### Resource URL
### `GET /configs`

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

/syncdata/v1.0/configs

### Example Response
```JSON
{
	"id": "mosip.sync.getconfig",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
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
		"mosip.kernel.syncdata.registration-center-config-file": "registration-${spring.profiles.active}.properties",
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




## 3.3 Get All Roles 

This service will return back the all roles of the applications. 

### Resource URL
### `GET /roles`


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
	"id": "mosip.sync.getroles",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
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

## 3.4 Get list of users and role-mapping 

This service will return back the list of users and its role-mapping based on the registration-center-id. 

### Resource URL
### `GET /userdetails/{regid}`


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
	"id": "mosip.sync.userrolesmapping",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
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
## 3.5 Public key-get service

This service will provide the public key for the specific application fetched from key manager. 

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
/syncdata/v1.0/publickey/REGISTRATION?timeStamp=2018-12-09T06%3A39%3A03.683Z

### Example Response
```JSON

{
	"id": "mosip.sync.getpublickey",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
		  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
		  "issuedAt": "2018-01-01T10:00:00",
		  "expiryAt": "2018-12-10T06:12:51.994"
	}
}	
```


# 4 UIN
## 4.1 UIN-get service

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

/uingenerator/v1.0/uin

### Example Response
```
{
	"id": "mosip.uin.getuin",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
	  "uin": "734168915279"
	}
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
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
message |Yes|Message in the SMS| | This is the sample SMS message
number |Yes|Mobile number to which the SMS have to be sent| | 743764398

### Example Request

/smsnotifier/v1.0/sms/send

```
{
	"id": "mosip.sms.send",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		"message": "Your Booking Request accepted. B-Ref BI56793",
		"number": "89900074454"

	}
}

```

### Example Response
```
{
	"id": "mosip.sms.send",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
	  "message": "Sms Request Sent",
	  "status": "success"
	}
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
Request format | Form Data
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
mailTo |Yes|Mail ID of the recepient| | mosip@mindtree.com
mailCc |No|Mail ID of the recepient| | mosip@mindtree.com
mailSubject |Yes|Mail ID of the recepient| | Sample mail subject
mailContent |No|Mail ID of the recepient| | Sample mail content
attachments |No|Mail ID of the recepient| | multipart/formdata


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
	"id": "mosip.email.send",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
	  "message": "Email Request sent",
	  "status": "success"
	}
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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		"key": "9820173642"
	}	
}
```
### Example Response
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
	  "otp": "849004",
	  "status": "GENERATION_SUCCESSFUL"
	}
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
	"id": "mosip.authentication.sendotp",
	"ver": "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
	"response": {
	  "status": "success",
	  "message": "VALIDATION SUCCESSFUL"
	}
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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"response": {
	  "status": true
	}
}
```



# 9. License Key Manager
TSPs call the IDA to authenticate the Individuals. There can be various service calls such as Demographic, biometric based authentications. Each service calls have the permission associated. When a service call comes to the IDA, a request is sent to the Kernel module to retrieve the permissions for the License Key.

This service facilitates generation of license key, mapping the license key to several permissions, and fetch permissions mapped to a license key.

## 9.1 License Key Generation

This component generates a license key for a specified TSP ID.

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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		"licenseExpiryTime": "2019-03-07T10:00:00.000Z",
		"tspId": "9837"
	}
}
```
### Example Response
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"response": {
	  "licenseKey": "gR7Mw7tA7S7qifkf"
	}
}
```
## 9.2 Mapping Permissions

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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"response": {
	  "status": "Mapped License with the permissions"
	}
}
```

## 9.3 Fetching Permissions 

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
	"id": "mosip.license.permission",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"response": {
	  "permissions": [
		"OTP Trigger",
		"OTP Authentication"
	  ]
	}
}
```


## 9.4 Change license key status

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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
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
	"id":"mosip.license.status",			
	"version":"1.0",	
	"responsetime":"2007-12-03T10:15:30Z",	
	"response" : {
		"message":"The status had been changed successfully. "
	}
}	
```


Sample Error Response:

```JSON
{
	"id":"mosip.license.status",			
	"version":"1.0",	
	"responsetime":"2007-12-03T10:15:30Z",	
	"errors":[
		"errorCode": "PRG_PAM_APP_001",
		"message": "License key not found"
	  }	
	]
}
```




# 10. OTP Notification

This service facilitates sending the generated OTP through sms/email/both.

## 10.1 OTP Notification[Both Email and SMS]

When OTP needs to be notified both through email and sms.

### Resource URL
### `POST /otp/send`

### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
emailBodyTemplate|Yes|The email content with $otp as the placeholder which represents the OTP| |Your OTP is $otp 
emailId|Yes|Email ID to be notified| |testmail@tmail.com
emailSubjectTemplate|Yes|Subject for the email to be notified||OTP Notification through Email
mobileNumber|Yes|Mobile number to be notified||1234567890
notificationTypes|Yes|When opted for both types of notification,both should be mentioned||sms,email
smsTemplate|Yes|The SMS content with $otp as the placeholder which represents the OTP||Your OTP is $otp

### Example Request
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		"emailBodyTemplate": "Your OTP is $otp",
		"emailId": "testmail@tmail.com",
		"emailSubjectTemplate": "Test Mail",
		"mobileNumber": "1234567890",
		"notificationTypes": [
			"email","sms"
		],
		"smsTemplate": "Test SMS $otp"
	}
}
```
### Example Response
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"response": {
	  "status": "success",
	  "message": "Otp notification request submitted"
	}
}
```
## 10.2 OTP Notification[Only Email]

When OTP needs to be notified only through email.

### `POST /otp/send`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
emailBodyTemplate|Yes|The email content with $otp as the placeholder which represents the OTP| |Your OTP is $otp 
emailId|Yes|Email ID to be notified| |testmail@tmail.com
emailSubjectTemplate|Yes|Subject for the email to be notified||OTP Notification through Email
mobileNumber|No|||
notificationTypes|Yes|When opted for email notification,only email should be mentioned||email
smsTemplate|No|||

### Example Request
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		"emailBodyTemplate": "Your OTP is $otp",
		"emailId": "testmail@tmail.com",
		"emailSubjectTemplate": "Test Mail",
		"mobileNumber": "",
		"notificationTypes": [
			"email"
		],
		"smsTemplate": ""
	}
}
```
### Example Response
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
	  "status": "success",
	  "message": "Otp notification request submitted"
	}
}	
```

## 10.3 OTP Notification[Only SMS]

When OTP needs to be notified only through SMS.

### `POST /otp/send`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
emailBodyTemplate|No|||
emailId|No|||
emailSubjectTemplate|No|||
mobileNumber|Yes|Mobile number to be notified||1234567890
notificationTypes|Yes|When opted for SMS notification,only sms should be mentioned||sms
smsTemplate|Yes|The SMS content with $otp as the placeholder which represents the OTP||Your OTP is $otp

### Example Request
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"request": {
		"emailBodyTemplate": "",
		"emailId": "",
		"emailSubjectTemplate": "",
		"mobileNumber": "1234567890",
		"notificationTypes": [
			"sms"
		],
		"smsTemplate": "Your OTP is $otp"
	}
}
```
### Example Response
```JSON
{
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
	"response": {
	  "status": "success",
	  "message": "Otp notification request submitted"
	}
}	
```

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
	"id": "mosip.applicanttype.getApplicantType",
	"version": "1.0",
	"requesttime": "2007-12-03T10:15:30Z",
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
	"id": "mosip.applicanttype.getApplicantType",
	"ver" : "1.0",
	"responsetime": "2007-12-03T10:15:30Z",
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
	"id": "mosip.applicanttype.getDocCatAndTyp",
	"ver" : "1.0",
	"timestamp" : "2007-12-03T10:15:30Z",
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
	"id": "mosip.applicanttype.getDocCatAndTyp",
	"ver" : "1.0",
	"timestamp" : "2007-12-03T10:15:30Z",
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
	"id": "mosip.applicanttype.isApplicantTypeExists",
	"ver" : "1.0",
	"timestamp" : "2007-12-03T10:15:30Z",
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
	"id": "mosip.individualtype.getAllIndividualTypes",
	"ver": "1.0",
	"timestamp": "2007-12-03T10:15:30Z",
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
	"id": "mosip.individualtype.getIndividualTypes",
	"ver" : "1.0",
	"timestamp" : "2007-12-03T10:15:30Z",
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


# 13. UIN acknowledgement service

This service is called when an UIN is assigned to the invidual. 

## 13.1 Acknowledge the usage or UIN

This service is called when an UIN is assigned to the invidual. 

### Resource URL
### `POST /uinacknowledgement/acknowledgeuinassignment`

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
{
	"id":"mosip.uinacknowledgement.acknowledgeuinassignment",			
	"version":"1.0",	
	"requesttime":"2007-12-03T10:15:30Z",
	"request" : {
		"uin":"33983987329832"
	}
}
```
### Example Response
```JSON
{
	"id": "mosip.individualtype.getAllIndividualTypes",
	"ver": "1.0",
	"timestamp": "2007-12-03T10:15:30Z",
	"response": {
		"result":true
	}
}
```

