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
  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
  "issuedAt": "2018-01-01T10:00:00",
  "expiryAt": "2018-12-10T06:12:51.994"
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
  "applicationId": "REGISTRATION",
  "encryptedSymmetricKey": "encryptedSymmetricKey",
  "referenceId": "REF01",
  "timeStamp": "2018-12-10T06:12:52.994Z"
}
```



### Example Response
```JSON

{
  "symmetricKey": "decryptedSymmetricKey"
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

/syncdata/v1.0/masterdata/10001

### Example Response
```JSON
{
"lastSyncTime": "2019-03-04T12:34:15.477Z",
  "registrationCenter": [
    {
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
    },
    {
      "id": "10001",
      "name": "Centre A Ben Mansour",
      "centerTypeCode": "REG",
      "addressLine1": "P4238",
      "addressLine2": "Ben Mansour",
      "addressLine3": "Maroc",
      "latitude": "36.52117",
      "longitude": "-6.453277",
      "locationCode": "14022",
      "holidayLocationCode": "KTA",
      "contactPhone": "993556086",
      "numberOfStations": null,
      "workingHours": "8:00:00",
      "numberOfKiosks": 1,
      "perKioskProcessTime": "00:15:00",
      "centerStartTime": "09:00:00",
      "centerEndTime": "17:00:00",
      "timeZone": "GTM + 01h00) HEURE EUROPEENNE CENTRALE",
      "contactPerson": "John Doe",
      "lunchStartTime": "13:00:00",
      "lunchEndTime": "14:00:00",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "id": "10001",
      "name": "Center A Ben Mansour",
      "centerTypeCode": "REG",
      "addressLine1": "P4238",
      "addressLine2": "Ben Mansour",
      "addressLine3": "Morroco",
      "latitude": "34.52117",
      "longitude": "-6.453275",
      "locationCode": "14022",
      "holidayLocationCode": "KTA",
      "contactPhone": "779517433",
      "numberOfStations": null,
      "workingHours": "8:00:00",
      "numberOfKiosks": 1,
      "perKioskProcessTime": "00:15:00",
      "centerStartTime": "09:00:00",
      "centerEndTime": "17:00:00",
      "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
      "contactPerson": "John Doe",
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
    },
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
      "id": "3000021",
      "name": "Finger Print Scanner 1",
      "serialNum": "SZ5912878988",
      "deviceSpecId": "165",
      "macAddress": "85:bb:97:4b:14:05",
      "ipAddress": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000041",
      "name": "IRIS Scanner 1",
      "serialNum": "JN7935692567",
      "deviceSpecId": "327",
      "macAddress": "11:fb:cf:6a:bf:29",
      "ipAddress": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000061",
      "name": "Web Camera 1",
      "serialNum": "H483Y8886310688",
      "deviceSpecId": "736",
      "macAddress": "b3:62:78:07:d4:d1",
      "ipAddress": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000081",
      "name": "Document Scanner 1",
      "serialNum": "YZ492N3059198",
      "deviceSpecId": "801",
      "macAddress": "7d:8b:8c:f7:26:bb",
      "ipAddress": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "3000101",
      "name": "Printer 1",
      "serialNum": "BS563Q2230804",
      "deviceSpecId": "920",
      "macAddress": "79:2f:a1:5b:dc:ec",
      "ipAddress": null,
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "deviceTypes": [
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
      "name": "Caméra",
      "description": "Pour capturer une photo",
      "isDeleted": null,
      "langCode": "fra",
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
      "code": "FRS",
      "name": "Finger Print Scanner",
      "description": "For scanning fingerprints",
      "isDeleted": null,
      "langCode": "eng",
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
      "code": "FRS",
      "name": "ماسح بصمة الأصبع",
      "description": "لمسح بصمات الأصابع",
      "isDeleted": null,
      "langCode": "ara",
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
      "name": "Scanner dIris",
      "description": "Pour scanner liris",
      "isDeleted": null,
      "langCode": "fra",
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
      "code": "PRT",
      "name": "Imprimante",
      "description": "Pour imprimer des documents",
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
      "code": "SCN",
      "name": "Document Scanner",
      "description": "For scanning documents",
      "isDeleted": null,
      "langCode": "eng",
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
      "code": "SCN",
      "name": "وثيقة الماسح الضوئي",
      "description": "لمسح المستندات ضوئيًا",
      "isDeleted": null,
      "langCode": "ara",
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
      "code": "PSP",
      "name": "Passport",
      "description": "Proof of Idendity",
      "isDeleted": null,
      "langCode": "eng",
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
      "name": "Passeport",
      "description": "Preuve didentité",
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
      "docTypeCode": "CRN",
      "docCategoryCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "docTypeCode": "PSP",
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
      "id": "1125",
      "name": "Template for Onscreen Acknowledgment",
      "description": "Template for Onscreen Acknowledgment",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Name                 :$Individual Name\nPre Registration ID    :$PRID\nRegistration Centre    :$Registration Centre\nCentre Contact Number  :$Contact Number\nAppointment Date & Time:$Appointment Date and Time\n\nImportant Guidelines\n1.$Guideline 1\n2.$Guideline 2\n3.$Guideline 3\n4.$Guideline 4\n5.$Guideline 5\n6.$Guideline 6\n7.$Guideline 7\n8.$Guideline 8\n9.$Guideline 9\n10.$Guideline 10\n",
      "moduleId": "10001",
      "moduleName": "Pre-Registration",
      "templateTypeCode": "Onscreen-Acknowledgement",
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
      "id": "1125",
      "name": "قالب للشاشة شكر وتقدير",
      "description": "قالب للشاشة شكر وتقدير",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "اسم                           : $Individual Name\nمعرف التسجيل المسبق: $PRID\nمركز التسجيل: $Registration Centre\nرقم الاتصال بالمركز: $Contact Number\nتاريخ ووقت الموعد: $Appointment Date and Time\n\nإرشادات هامه\n1. $Guideline 1\n2. $Guideline 2\n3. $Guideline 3\n4. $Guideline 4\n5. $Guideline 5\n6. $Guideline 6\n7. $Guideline 7\n8. $Guideline 8\n9. $Guideline 9\n01. $Guideline 10\n",
      "moduleId": "10001",
      "moduleName": "ما قبل التسجيل",
      "templateTypeCode": "Onscreen-Acknowledgement",
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
      "id": "1125",
      "name": "On-screen recognition template",
      "description": "On-screen recognition template",
      "fileFormatCode": "txt",
      "model": null,
      "fileText": "Nom                           : $Individual Name\nID de pré-inscription: $PRID\nCentre d'inscription: $Registration Centre\nNuméro de contact du Centre: $Contact Number\nDate et heure de la nomination: $Appointment Date and Time\n\nDirectives importantes\n1.$Guideline 1\n2.$Guideline 2\n3.$Guideline 3\n4.$Guideline 4\n5.$Guideline 5\n6.$Guideline 6\n7.$Guideline 7\n8.$Guideline 8\n9.$Guideline 9\n10.$Guideline 10",
      "moduleId": "10001",
      "moduleName": "Pré-inscription",
      "templateTypeCode": "Onscreen-Acknowledgement",
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
      "id": "1131",
      "name": "قالب بطاقة UIN",
      "description": "قالب بطاقة UIN",
      "fileFormatCode": "html",
      "model": null,
      "fileText": "<!DOCTYPE html>\r\n<html>\r\n<head>\r\n\t<meta charset=\"utf-8\">\r\n\t<meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\r\n\t<title>UIN Card</title>\r\n<style>\r\n.main-table {\r\n\tmargin-left: 60px;;\r\n\twidth: 600px;\r\n\theight: 350px;\r\n\tborder: 1px solid black;\r\n}\r\n.cir {\r\n\tdisplay: inline-block;\r\n\tborder-radius: 60px;\r\n\tbox-shadow: 0px 0px 2px #000000;\r\n\tpadding: 0.5em 0.6em;\r\n}\r\n.name-head-color {\r\n\tcolor: black;\r\n}\r\n.head-title {\r\n\tmargin-left: -85px;\r\n}\r\n\r\n.bar-code-padding {\r\n\tmargin-top: 20px;\r\n\tmargin-left: 20px;\r\n}\r\n.top-buffer {\r\n\tmargin-left:10px;\r\n}\r\n</style>\r\n</head>\r\n\r\n<body>\r\n\t<table class=\"main-table\">\r\n\t\t<tr>\r\n\t\t\t<td>&nbsp;\r\n\t\t\t\t<div class=\"cir\">\r\n\t\t\t\t\t<font size=\"1\">Logo</font>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t\t<td><label class=\"name-head-color\"> <font size=\"5\"\r\n\t\t\t\t\tclass=\" head-title\"> &nbsp;&nbsp; Kingdom of Morocco\r\n\t\t\t\t\t\t&nbsp;&nbsp;&nbsp; </font>\r\n\t\t\t</label></td>\r\n\t\t\t<td rowspan=\"4\">\r\n\t\t\t\t<div>\r\n\t\t\t\t\t<div\r\n\t\t\t\t\t\tstyle=\"border: solid black 1px; height: 150px; width: 120px; margin-right: -30px;\">\r\n\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>UIN&nbsp;:&nbsp;</b></label> <span\r\n\t\t\t\t\t\tclass=\"name-color\"> $UIN </span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Name&nbsp;:&nbsp;</b></label> <span\r\n\t\t\t\t\t\tclass=\"name-color\"> $name_eng</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>اسم&nbsp;:&nbsp;</b></label> <span>\r\n\t\t\t\t\t\t$name_ara</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Date/تاريخ&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t<span>$dob</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td colspan=\"2\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Gender&nbsp;:&nbsp;</b></label> <span>$gender_eng</span>\r\n\t\t\t\t\t&nbsp;&nbsp; <label class=\"name-head-color\"><b>جنس&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t<span>$gender_ara</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td colspan=\"3\">\r\n\t\t\t\t<div class=\"row\" style=\"margin-right: 0px; margin-left: -10px;\">\r\n\t\t\t\t\t<div class=\"col-md-2 top-buffer\">\r\n\t\t\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t\t\t<table>\r\n\t\t\t\t\t\t\t\t<tr>\r\n\t\t\t\t\t\t\t\t\t<td><label class=\"name-head-color\"><b>Address&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t\t<td><span>$addressLine1_eng, $addressLine2_eng,\r\n\t\t\t\t\t\t\t\t\t\t\t$addressLine3_eng, $region_eng, $province_eng, $city_eng,\r\n\t\t\t\t\t\t\t\t\t\t\t$postalCode </span></td>\r\n\t\t\t\t\t\t\t\t</tr>\r\n\t\t\t\t\t\t\t\t<tr>\r\n\t\t\t\t\t\t\t\t\t<td><label class=\"name-head-color\"><b>عنوان&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t\t<td><span>$addressLine1_ara, $addressLine2_ara,\r\n\t\t\t\t\t\t\t\t\t\t\t$addressLine3_ara, $region_ara, $province_ara, $city_ara,\r\n\t\t\t\t\t\t\t\t\t\t\t$postalCode </span>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t</tr>\r\n\t\t\t\t\t\t\t</table>\r\n\t\t\t\t\t\t</div>\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t</table>\r\n\t<div>&nbsp;</div>\r\n\t<table class=\"main-table\" style=\"height: 300px\">\r\n\t\t<tr>\r\n\t\t\t<td>\r\n\t\t\t\t<div\r\n\t\t\t\t\tstyle=\"margin-left: 10px; margin-right: 10px; border: solid black 1px; height: 250px; width: 250px;\">\r\n\t\t\t\t\t<div class=\"col-md-6\">\r\n\t\t\t\t\t\t<div class=\"bar-code-padding\"></div>\r\n\t\t\t\t\t\t<img src=\"QrCode.png\"\r\n\t\t\t\t\t\t\tstyle=\"width: 250px; height: 250px; margin-top: -20px\">\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t\t<td>\r\n\t\t\t\t<div class=\"name-head-color col-md-6\">\r\n\t\t\t\t\t<br> For any issues please contact us at<br>\r\n\t\t\t\t\t<br> Registration Proccessor,Hanging Gardens,Global Village\r\n\t\t\t\t\tTech Park, Mysore Rd,RVCE,Bengaluru, Karnataka 560059<br>\r\n\t\t\t\t\t<br> لأية مشاكل يرجى الاتصال بنا على <br>التسجيل المعالج،\r\n\t\t\t\t\tالحدائق المعلقة ، القرية العالمية Tech Park, Mysore Rd,RVCE 560059\r\n\t\t\t\t\tبنغالورو، كارناتاكا <br>\r\n\t\t\t\t\t<br>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t</table>\r\n</body>\r\n</html>",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_CARD_TEMPLATE",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "id": "1131",
      "name": "UIN Card Template",
      "description": "UIN Card Template",
      "fileFormatCode": "html",
      "model": null,
      "fileText": "<!DOCTYPE html>\r\n<html>\r\n<head>\r\n\t<meta charset=\"utf-8\">\r\n\t<meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\r\n\t<title>UIN Card</title>\r\n<style>\r\n.main-table {\r\n\tmargin-left: 60px;;\r\n\twidth: 600px;\r\n\theight: 350px;\r\n\tborder: 1px solid black;\r\n}\r\n.cir {\r\n\tdisplay: inline-block;\r\n\tborder-radius: 60px;\r\n\tbox-shadow: 0px 0px 2px #000000;\r\n\tpadding: 0.5em 0.6em;\r\n}\r\n.name-head-color {\r\n\tcolor: black;\r\n}\r\n.head-title {\r\n\tmargin-left: -85px;\r\n}\r\n\r\n.bar-code-padding {\r\n\tmargin-top: 20px;\r\n\tmargin-left: 20px;\r\n}\r\n.top-buffer {\r\n\tmargin-left:10px;\r\n}\r\n</style>\r\n</head>\r\n\r\n<body>\r\n\t<table class=\"main-table\">\r\n\t\t<tr>\r\n\t\t\t<td>&nbsp;\r\n\t\t\t\t<div class=\"cir\">\r\n\t\t\t\t\t<font size=\"1\">Logo</font>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t\t<td><label class=\"name-head-color\"> <font size=\"5\"\r\n\t\t\t\t\tclass=\" head-title\"> &nbsp;&nbsp; Kingdom of Morocco\r\n\t\t\t\t\t\t&nbsp;&nbsp;&nbsp; </font>\r\n\t\t\t</label></td>\r\n\t\t\t<td rowspan=\"4\">\r\n\t\t\t\t<div>\r\n\t\t\t\t\t<div\r\n\t\t\t\t\t\tstyle=\"border: solid black 1px; height: 150px; width: 120px; margin-right: -30px;\">\r\n\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>UIN&nbsp;:&nbsp;</b></label> <span\r\n\t\t\t\t\t\tclass=\"name-color\"> $UIN </span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Name&nbsp;:&nbsp;</b></label> <span\r\n\t\t\t\t\t\tclass=\"name-color\"> $name_eng</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>اسم&nbsp;:&nbsp;</b></label> <span>\r\n\t\t\t\t\t\t$name_ara</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Date/تاريخ&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t<span>$dob</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td colspan=\"2\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Gender&nbsp;:&nbsp;</b></label> <span>$gender_eng</span>\r\n\t\t\t\t\t&nbsp;&nbsp; <label class=\"name-head-color\"><b>جنس&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t<span>$gender_ara</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td colspan=\"3\">\r\n\t\t\t\t<div class=\"row\" style=\"margin-right: 0px; margin-left: -10px;\">\r\n\t\t\t\t\t<div class=\"col-md-2 top-buffer\">\r\n\t\t\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t\t\t<table>\r\n\t\t\t\t\t\t\t\t<tr>\r\n\t\t\t\t\t\t\t\t\t<td><label class=\"name-head-color\"><b>Address&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t\t<td><span>$addressLine1_eng, $addressLine2_eng,\r\n\t\t\t\t\t\t\t\t\t\t\t$addressLine3_eng, $region_eng, $province_eng, $city_eng,\r\n\t\t\t\t\t\t\t\t\t\t\t$postalCode </span></td>\r\n\t\t\t\t\t\t\t\t</tr>\r\n\t\t\t\t\t\t\t\t<tr>\r\n\t\t\t\t\t\t\t\t\t<td><label class=\"name-head-color\"><b>عنوان&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t\t<td><span>$addressLine1_ara, $addressLine2_ara,\r\n\t\t\t\t\t\t\t\t\t\t\t$addressLine3_ara, $region_ara, $province_ara, $city_ara,\r\n\t\t\t\t\t\t\t\t\t\t\t$postalCode </span>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t</tr>\r\n\t\t\t\t\t\t\t</table>\r\n\t\t\t\t\t\t</div>\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t</table>\r\n\t<div>&nbsp;</div>\r\n\t<table class=\"main-table\" style=\"height: 300px\">\r\n\t\t<tr>\r\n\t\t\t<td>\r\n\t\t\t\t<div\r\n\t\t\t\t\tstyle=\"margin-left: 10px; margin-right: 10px; border: solid black 1px; height: 250px; width: 250px;\">\r\n\t\t\t\t\t<div class=\"col-md-6\">\r\n\t\t\t\t\t\t<div class=\"bar-code-padding\"></div>\r\n\t\t\t\t\t\t<img src=\"QrCode.png\"\r\n\t\t\t\t\t\t\tstyle=\"width: 250px; height: 250px; margin-top: -20px\">\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t\t<td>\r\n\t\t\t\t<div class=\"name-head-color col-md-6\">\r\n\t\t\t\t\t<br> For any issues please contact us at<br>\r\n\t\t\t\t\t<br> Registration Proccessor,Hanging Gardens,Global Village\r\n\t\t\t\t\tTech Park, Mysore Rd,RVCE,Bengaluru, Karnataka 560059<br>\r\n\t\t\t\t\t<br> لأية مشاكل يرجى الاتصال بنا على <br>التسجيل المعالج،\r\n\t\t\t\t\tالحدائق المعلقة ، القرية العالمية Tech Park, Mysore Rd,RVCE 560059\r\n\t\t\t\t\tبنغالورو، كارناتاكا <br>\r\n\t\t\t\t\t<br>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t</table>\r\n</body>\r\n</html>",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_CARD_TEMPLATE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "id": "1131",
      "name": "Modèle de carte UIN",
      "description": "Modèle de carte UIN",
      "fileFormatCode": "html",
      "model": null,
      "fileText": "<!DOCTYPE html>\r\n<html>\r\n<head>\r\n\t<meta charset=\"utf-8\">\r\n\t<meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\r\n\t<title>UIN Card</title>\r\n<style>\r\n.main-table {\r\n\tmargin-left: 60px;;\r\n\twidth: 600px;\r\n\theight: 350px;\r\n\tborder: 1px solid black;\r\n}\r\n.cir {\r\n\tdisplay: inline-block;\r\n\tborder-radius: 60px;\r\n\tbox-shadow: 0px 0px 2px #000000;\r\n\tpadding: 0.5em 0.6em;\r\n}\r\n.name-head-color {\r\n\tcolor: black;\r\n}\r\n.head-title {\r\n\tmargin-left: -85px;\r\n}\r\n\r\n.bar-code-padding {\r\n\tmargin-top: 20px;\r\n\tmargin-left: 20px;\r\n}\r\n.top-buffer {\r\n\tmargin-left:10px;\r\n}\r\n</style>\r\n</head>\r\n\r\n<body>\r\n\t<table class=\"main-table\">\r\n\t\t<tr>\r\n\t\t\t<td>&nbsp;\r\n\t\t\t\t<div class=\"cir\">\r\n\t\t\t\t\t<font size=\"1\">Logo</font>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t\t<td><label class=\"name-head-color\"> <font size=\"5\"\r\n\t\t\t\t\tclass=\" head-title\"> &nbsp;&nbsp; Kingdom of Morocco\r\n\t\t\t\t\t\t&nbsp;&nbsp;&nbsp; </font>\r\n\t\t\t</label></td>\r\n\t\t\t<td rowspan=\"4\">\r\n\t\t\t\t<div>\r\n\t\t\t\t\t<div\r\n\t\t\t\t\t\tstyle=\"border: solid black 1px; height: 150px; width: 120px; margin-right: -30px;\">\r\n\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>UIN&nbsp;:&nbsp;</b></label> <span\r\n\t\t\t\t\t\tclass=\"name-color\"> $UIN </span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Name&nbsp;:&nbsp;</b></label> <span\r\n\t\t\t\t\t\tclass=\"name-color\"> $name_eng</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>اسم&nbsp;:&nbsp;</b></label> <span>\r\n\t\t\t\t\t\t$name_ara</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\r\n\t\t<tr>\r\n\t\t\t<td rowspan=\"1\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Date/تاريخ&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t<span>$dob</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td colspan=\"2\">\r\n\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t<label class=\"name-head-color\"><b>Gender&nbsp;:&nbsp;</b></label> <span>$gender_eng</span>\r\n\t\t\t\t\t&nbsp;&nbsp; <label class=\"name-head-color\"><b>جنس&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t<span>$gender_ara</span>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t\t<tr>\r\n\t\t\t<td colspan=\"3\">\r\n\t\t\t\t<div class=\"row\" style=\"margin-right: 0px; margin-left: -10px;\">\r\n\t\t\t\t\t<div class=\"col-md-2 top-buffer\">\r\n\t\t\t\t\t\t<div class=\"block top-buffer\">\r\n\t\t\t\t\t\t\t<table>\r\n\t\t\t\t\t\t\t\t<tr>\r\n\t\t\t\t\t\t\t\t\t<td><label class=\"name-head-color\"><b>Address&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t\t<td><span>$addressLine1_eng, $addressLine2_eng,\r\n\t\t\t\t\t\t\t\t\t\t\t$addressLine3_eng, $region_eng, $province_eng, $city_eng,\r\n\t\t\t\t\t\t\t\t\t\t\t$postalCode </span></td>\r\n\t\t\t\t\t\t\t\t</tr>\r\n\t\t\t\t\t\t\t\t<tr>\r\n\t\t\t\t\t\t\t\t\t<td><label class=\"name-head-color\"><b>عنوان&nbsp;:&nbsp;</b></label>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t\t<td><span>$addressLine1_ara, $addressLine2_ara,\r\n\t\t\t\t\t\t\t\t\t\t\t$addressLine3_ara, $region_ara, $province_ara, $city_ara,\r\n\t\t\t\t\t\t\t\t\t\t\t$postalCode </span>\r\n\t\t\t\t\t\t\t\t\t</td>\r\n\t\t\t\t\t\t\t\t</tr>\r\n\t\t\t\t\t\t\t</table>\r\n\t\t\t\t\t\t</div>\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t</table>\r\n\t<div>&nbsp;</div>\r\n\t<table class=\"main-table\" style=\"height: 300px\">\r\n\t\t<tr>\r\n\t\t\t<td>\r\n\t\t\t\t<div\r\n\t\t\t\t\tstyle=\"margin-left: 10px; margin-right: 10px; border: solid black 1px; height: 250px; width: 250px;\">\r\n\t\t\t\t\t<div class=\"col-md-6\">\r\n\t\t\t\t\t\t<div class=\"bar-code-padding\"></div>\r\n\t\t\t\t\t\t<img src=\"QrCode.png\"\r\n\t\t\t\t\t\t\tstyle=\"width: 250px; height: 250px; margin-top: -20px\">\r\n\t\t\t\t\t</div>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t\t<td>\r\n\t\t\t\t<div class=\"name-head-color col-md-6\">\r\n\t\t\t\t\t<br> For any issues please contact us at<br>\r\n\t\t\t\t\t<br> Registration Proccessor,Hanging Gardens,Global Village\r\n\t\t\t\t\tTech Park, Mysore Rd,RVCE,Bengaluru, Karnataka 560059<br>\r\n\t\t\t\t\t<br> لأية مشاكل يرجى الاتصال بنا على <br>التسجيل المعالج،\r\n\t\t\t\t\tالحدائق المعلقة ، القرية العالمية Tech Park, Mysore Rd,RVCE 560059\r\n\t\t\t\t\tبنغالورو، كارناتاكا <br>\r\n\t\t\t\t\t<br>\r\n\t\t\t\t</div>\r\n\t\t\t</td>\r\n\t\t</tr>\r\n\t</table>\r\n</body>\r\n</html>",
      "moduleId": "10003",
      "moduleName": "Registration Processor",
      "templateTypeCode": "RPR_UIN_CARD_TEMPLATE",
      "isDeleted": null,
      "langCode": "fra",
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
      "code": "RPR_UIN_CARD_TEMPLATE",
      "description": "قالب بطاقة UIN",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "RPR_UIN_CARD_TEMPLATE",
      "description": "UIN card template ",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "RPR_UIN_CARD_TEMPLATE",
      "description": "Modèle de carte UIN",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "RPR_UIN_CARD_TEMPLATE",
      "description": "قالب بطاقة UIN ",
      "isDeleted": null,
      "langCode": "taa",
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
      "description": "Fichier html",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "html",
      "description": "html file",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "html",
      "description": "ملف html",
      "isDeleted": null,
      "langCode": "ara",
      "isActive": true
    },
    {
      "code": "html",
      "description": "ملف html",
      "isDeleted": null,
      "langCode": "taa",
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
    }
  ],
  "locationHierarchy": [
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
      "langCode": "eng",
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
      "langCode": "ara",
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
      "code": "LIF",
      "name": "Left Index Finger",
      "description": "Print of Left Index Finger",
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
    }
  ],
  "applications": [
    {
      "code": "1111",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1112",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1113",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1114",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1115",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1116",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1117",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1118",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1119",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1120",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1121",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1122",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1123",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1124",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1125",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1126",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1127",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1128",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1129",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1130",
      "name": "Pre_Reg",
      "description": "string",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "${CodeId}",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "0999999",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "1000000",
      "name": "app1",
      "description": "decs",
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
      "code": "0100001",
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
      "code": "7777",
      "name": "app1",
      "description": "${decs}",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "8888",
      "name": "app1",
      "description": "${decs}",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "9999",
      "name": "app1",
      "description": "${decs}",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "2222",
      "name": "app1",
      "description": "${decs}",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "code": "987456",
      "name": "app1",
      "description": "decs",
      "isDeleted": null,
      "langCode": "fra",
      "isActive": true
    },
    {
      "code": "${CodeId}",
      "name": "app1",
      "description": "decs",
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
      "code": "FLE",
      "genderName": "Female",
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
      "appTypeCode": "001",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "001",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "001",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "001",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "002",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "002",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "002",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "003",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "003",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "003",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "004",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "004",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "005",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "005",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "005",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "005",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "006",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "006",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "006",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "007",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "007",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "007",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "008",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "008",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "009",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "009",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "009",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "009",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "009",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "010",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "010",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "010",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "010",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "011",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "011",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "011",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "011",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "012",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "012",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "012",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "013",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "013",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "013",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "013",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "013",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "014",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "014",
      "docTypeCode": "RNC",
      "docCatCode": "POA",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "014",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "014",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "015",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "015",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "015",
      "docTypeCode": "CRN",
      "docCatCode": "POR",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "015",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "016",
      "docTypeCode": "CIN",
      "docCatCode": "POI",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "016",
      "docTypeCode": "COB",
      "docCatCode": "POB",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "appTypeCode": "016",
      "docTypeCode": "COE",
      "docCatCode": "POE",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
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
  "registrationCenterMachines": [
    {
      "regCenterId": "10001",
      "machineId": "10001",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterDevices": [
    {
      "regCenterId": "10001",
      "deviceId": "3000021",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "deviceId": "3000041",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "deviceId": "3000061",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "deviceId": "3000081",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "deviceId": "3000101",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    }
  ],
  "registrationCenterMachineDevices": [
    {
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000021",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000041",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000061",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000081",
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true
    },
    {
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000101",
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
      "cntrId": "10001",
      "machineId": "10001",
      "usrId": "110001"
    }
  ],
  "registrationCenterUsers": [
    {
      "regCenterId": "10001",
      "userId": "110001",
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
      "regCenterId": "10001",
      "machineId": "10001",
      "effectivetimes": "2019-02-28T10:24:38.460784"
    }
  ],
  "registrationCenterDeviceHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "deviceId": "3000021",
      "effectivetimes": "2019-02-28T10:24:38.420Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "deviceId": "3000041",
      "effectivetimes": "2019-02-28T10:24:38.420Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "deviceId": "3000061",
      "effectivetimes": "2019-02-28T10:24:38.420Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "deviceId": "3000081",
      "effectivetimes": "2019-02-28T10:24:38.420Z"
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "deviceId": "3000101",
      "effectivetimes": "2019-02-28T10:24:38.420Z"
    }
  ],
  "registrationCenterMachineDeviceHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000021",
      "effectiveDateTime": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000041",
      "effectiveDateTime": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000061",
      "effectiveDateTime": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000081",
      "effectiveDateTime": null
    },
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCenterId": "10001",
      "machineId": "10001",
      "deviceId": "3000101",
      "effectiveDateTime": null
    }
  ],
  "registrationCenterUserMachineMappingHistory": [
    {
      "cntrId": "10001",
      "machineId": "10001",
      "usrId": "110001",
      "effectivetimes": "2019-02-28T10:24:38.496Z"
    }
  ],
  "registrationCenterUserHistory": [
    {
      "isDeleted": null,
      "langCode": "eng",
      "isActive": true,
      "regCntrId": "10001",
      "userId": "110001",
      "effectDateTimes": "2019-02-28T10:24:38.478467"
    }
  ]
}
```

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
  "publicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwUAubI0cMDZMlalDYbzZj4G2UrWY0QDtmZQyqU_ER5CA1gbxlHDQIesm1DVyp6kf1sG-RcosKPqKIhe9vKLPx5pzQXinGdl_8e5bkPpg2RLlDoNju1ycohPrCk0VOd4eNU90-SRJZH_62QE1_MG2yIohI7e7cuC93Q9SHMD8jmJ7DX2zTui4zbo-c5g7vFAtzDgxJg0vSPGbap682xkWZNgzRA_ctrnHF_9_JMzP_6Equ8E_g5BaI3jkWnVmDNjDzzseBH9zHpfbx6wNYrzQZy8iqqywbUtbHWtM0ALkH7nLi4atVbL6a-ryFt6Tq7qfGzYhLtWN47t4GxwyOJC99QIDAQAB",
  "issuedAt": "2018-01-01T10:00:00",
  "expiryAt": "2018-12-10T06:12:51.994"
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
  "licenseExpiryTime": "2019-03-07T10:00:00.000Z",
  "tspId": "9837"
}
```
### Example Response
```JSON
{
  "licenseKey": "gR7Mw7tA7S7qifkf"
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
  "licenseKey": "gR7Mw7tA7S7qifkf",
  "permissions": [
    "OTP Trigger","OTP Authentication"
  ],
  "tspId": "9837"
}
```
### Example Response
```JSON
{
  "status": "Mapped License with the permissions"
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
  "permissions": [
    "OTP Trigger",
    "OTP Authentication"
  ]
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
	"id":"mosip.license.status",			
	"version":"1.0",	
	"requesttime":"2007-12-03T10:15:30Z",
	"request" : {
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
  "emailBodyTemplate": "Your OTP is $otp",
  "emailId": "testmail@tmail.com",
  "emailSubjectTemplate": "Test Mail",
  "mobileNumber": "1234567890",
  "notificationTypes": [
    "email","sms"
  ],
  "smsTemplate": "Test SMS $otp"
}
```
### Example Response
```JSON
{
  "status": "success",
  "message": "Otp notification request submitted"
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
  "emailBodyTemplate": "Your OTP is $otp",
  "emailId": "testmail@tmail.com",
  "emailSubjectTemplate": "Test Mail",
  "mobileNumber": "",
  "notificationTypes": [
    "email"
  ],
  "smsTemplate": ""
}
```
### Example Response
```JSON
{
  "status": "success",
  "message": "Otp notification request submitted"
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
  "emailBodyTemplate": "",
  "emailId": "",
  "emailSubjectTemplate": "",
  "mobileNumber": "1234567890",
  "notificationTypes": [
    "sms"
  ],
  "smsTemplate": "Your OTP is $otp"
}
```
### Example Response
```JSON
{
  "status": "success",
  "message": "Otp notification request submitted"
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

