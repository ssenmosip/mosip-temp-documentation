This section details about the service APIs in the Registration-Processor modules

[1. Packet receiver Service](#1-packet-receiver-service)

[2. Registration status Service](#2-registration-status-service)

[3. Manual Adjudication Service](#3-manual-adjudication-service)

[4. Bio Dedupe Service](#4-bio-dedupe-service)

[5. Packet Generator Service](#5-packet-generator-service)

# 1 Packet Receiver Service
## 1.1 Packet-receiver service

- #### `POST /registrationprocessor/v1/packetreceiver/registrationpackets`

This service receives the registration packet frm client. Before moving packet to landing zone it is sent for virus scan and then trustworthiness of the packet is validated using hashvalue and size.


#### Resource URL
https://mosip.io/registrationprocessor/v1/packetreceiver/registrationpackets

#### Resource details

Resource Details | Description
------------ | -------------
Request format | MULTIPART
Response format | JSON
Requires Authentication | Yes

#### Request Path Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
MultipartFile|Yes|The encrypted zip file| 

#### Request
![Request](_images/reg_processor/packet_receiver_sample_input.PNG)

#### Response

##### Success response

######Status Code: 200
######Description: Packet is in PACKET_RECEIVED status

```JSON
{
	"id" : "mosip.registration.packet",
	"version" : "1.0",
	"responsetime" : "2019-02-02T06:12:25.288Z",
	"response" : {
		"status" : "Packet is in PACKET_RECEIVED status"
	}
}
```
#### Failure response

###### Status Code: 200
######Description: The request received is a duplicate request to upload a Packet

```JSON
{
  "id" : "mosip.registration.packet",
  "version" : "1.0",
  "responsetime": "2019-02-02T06:12:25.288Z",
  "errors" : [{
		"errorcode": "RPR-PKR-005",
	    "message": "The request received is a duplicate request to upload a Packet"
	}]
}
```

# 2 Registration Status Service
## 2.1 Packet-status service

- ### `GET /registrationprocessor/v1/registrationstatus/search`

This service return the registration current status for list of input registration ids.

#### Resource URL
https://mosip.io/registrationprocessor/v1/registrationstatus/search

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment |
-----|----------|-------------|---------------|
registrationIds|Yes|List of registration ids|

#### Request
```JSON
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : [
	{
		"registrationId" : "2018701130000410092012345678"
	},
	{
		"registrationId" : "2018701130000410092012345678"
	}
  ]
}
```
#### Response
Record found :
######Status Code: 200
######Description: Successfully retrieved information

```JSON
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : [
  {
    "registrationId": "2018701130000410092012345678",
    "statusCode": "PROCESSING"
  },
  {
    "registrationId": "2018701130000410092018110735",
    "statusCode": "PROCESSED"
  }
]
}
```
Record not found :
######Status Code: 200
######Description: Successfully retrieved information
```JSON
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : []
}
```


## 2.2 Sync-registration service
The registration ids has to be synced with server before uploading packet to landing zone. This service is used to syncs registration ids.

- #### `POST /registrationprocessor/v1/registrationstatus/sync`

#### Resource URL
https://mosip.io/registrationprocessor/v1/registrationstatus/sync

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
id|Yes|the id for sync|mosip.registration.sync
version|Yes|the version for sync|1.0
requesttime|Yes|the requesttime for sync|2019-02-14T12:40:59.768Z
request|Yes|the request object|1.0
registrationId|Yes|the registration id|80006444440002520181208094000
registrationType|Yes|the type of the registration|NEW, UPDATE, LOST, ACTIVATE, DEACTIVATE, RES_UPDATE
packetHashValue|Yes|the hash value of the encrypted packet|D7C87DC5D3A759D77433B02B80435CFAB5087F1A942543F51A5075BC441BF7EB
packetSize|Yes|size of encrypted packet in bytes|5242880
supervisorStatus|Yes|supervisor decision|APPROVED, REJECTED
supervisorComment|No|supervisor comments|rejected because of error
optionalValues|No|additional values to be passed during sync|key, value pair
langCode|Yes|language code used |eng or ara


#### Request Header
##### Center-Machine-RefId = `10011_10011`
##### timestamp = `2019-02-14T12:40:59.768Z`

#### Request
```JSON
{
	"id": "mosip.registration.sync",
	"version": "1.0",
	"requesttime": "2019-02-14T12:40:59.768Z",
	"request": [{
			"registrationId": "80006444440002520181208094000",
			"registrationType": "NEW",
			"packetHashValue": "D7C87DC5D3A759D77433B02B80435CFAB5087F1A942543F51A5075BC441BF7EB",
			"packetSize": 5242880,
			"supervisorStatus": "APPROVED",
			"supervisorComment": "Approved, all good",
			"longCode": "eng",
			"optionalValues": [{
				"key": "CNIE",
				"value": "122223456"
			}]
		},
		{
			"registrationId": "10011100110002520181208094000",
			"registrationType": "UPDATE",
			"packetHashValue": "D7C87DC5D3A759D77433B02B80435CFAB5087F1A942543F51A5075BC441BF7EB",
			"packetSize": 4242880,
			"supervisorStatus": "REJECTED",
			"supervisorComment": "Rejected due to error",
			"longCode": "eng",
			"optionalValues": [{
				"key": "CNIE",
				"value": "3456789o"
			}]
		}
	]
}
```
#### Response

######Response Code: 200
######Description: Successfully synced

Success response :
```JSON
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : [
	  {
		"registrationId": "1234575",
		"status": "SUCCESS"
	  },
	  {
		"registrationId": "12345678901234567890123456789",
		"status": "SUCCESS"
	  },
	  {
		"registrationId": "27847657360002520181208183052",
		"status": "SUCCESS"
	  }
	]
}
```
Failure response
```JSON
// response 1 : decryption failed
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "errors" : [
	  {
		"status": "FAILURE",
                "errorCode": "RPR-RGS-001",
		"errorMessage": "Decryption failed"
	  }
	]
}

// response 2 : validation failed

{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "errors" : [
	  {
		"registrationId": "1234575",
		"status": "FAILURE",
                "errorCode": "RPR-RGS-009",
		"errorMessage": "RegistrationId Length Must Be 29"
	  },
	  {
		"registrationId": "12345678901234567890123456789",
		"status": "FAILURE",
		"errorCode": "RPR-RGS-007",
                "errorMessage": "Invalid Time Stamp Found in RegistrationId"
	  },
	  {
		"registrationId": "27847657360002520181208183052",
		"status": "FAILURE",
		"errorCode": "RPR-RGS-012",
		"errorMessage": "Parent RegistrationId Length Must Be 29"
	  }
	]
}
```

# 3 Manual Adjudication Service
## 3.1 manual-adjudication-assignment service

- #### `POST /registrationprocessor/v1/manualverification/assignment`
This service is used to assign one single unassigned applicant record to the input user.

#### Resource URL
https://mosip.io/registrationprocessor/v1/manualverification/assignment

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
String|Yes|The user id|

#### Request
```JSON
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : {
	"userId": "mono29"
  }
}
```
#### Response
######Status Code: 200
######Description : response code is always 200 if server receives the request.

Success response
```JSON
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : {
	  "regId": "27847657360002520181208123456",
	  "mvUsrId": "mono29",
	  "statusCode": "ASSIGNED",
	  "matchedRefId": "27847657360002520181208123456",
	  "matchedRefType": "UIN",
	  "reasonCode": null
	}
}
```
Failure response
```JSON
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
	"errors" : [{
		"errorCode" : "RPR-FAC-003",
		"message" : "Cannot find the Registration Packet"
	}]
}
```


## 3.2 manual-adjudication-decision service

- #### `POST /registrationprocessor/v1/manualverification/decision`

This service is used to get the decision from manual adjudicator for an applicant and update the decision in table.

#### Resource URL
https://mosip.io/registrationprocessor/v1/manualverification/decision

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
ManualVerificationDTO|Yes|Dto containing manual adjudication info|

#### Request
```JSON
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : {
	  "matchedRefId": "27847657360002520181208123987",
	  "matchedRefType": "RID",
	  "mvUsrId": "mono",
	  "reasonCode": "Problem with biometrics",
	  "regId": "27847657360002520181208123456",
	  "statusCode": "APPROVED"
	}
}
```
#### Response
######Status Code: 200
######Description : response code is always 200 if server receives the request.

Success response
```JSON
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : {
	  "regId": "27847657360002520181208123456",
	  "mvUsrId": "mono",
	  "statusCode": "APPROVED",
	  "matchedRefId": "27847657360002520181208123987",
	  "matchedRefType": "RID",
	  "reasonCode": "Problem with biometrics"
	}
}
```
Failure response
```JSON
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
	"errors" : [{
		"errorCode" : "RPR-MVS-003"",
		"message" : "Invalid status update"
	}]
}
```

## 3.3 manual-adjudication-applicant-biometric service

- #### `POST /registrationprocessor/v1/manualverification/applicantBiometric`

The manual adjudicator would need to verify the applicant biometric and demographic records. This service is used to get the applicant biometric from packet store by registration id.

#### Resource URL

https://mosip.io/registrationprocessor/v1/manualverification/applicantBiometric

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | byte[]
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
FileRequestDto|Yes|Dto containing registration id and file name|

#### Example Request
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : {
	  "fileName": "APPLICANTPHOTO",
	  "regId": "27847657360002520181208123456"
	}
}
```
#### Example Response
######Status Code: 200
######Description : response code is always 200 if server receives the request.

Success :
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : {
	  "file": "B@629f0666"
  }
}
```
Failure :
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "errors" : [{
	"errorCode" : "RPR-MVS-002",
	"message" : "Requested file is not present"
  }]
}
```

## 3.4 manual-adjudication-applicant-demographic service

- #### `POST /registrationprocessor/v1/manualverification/applicantDemographic`

The manual adjudicator would need to verify the applicant biometric and demographic records. This service is used to get the applicant demographic from packet store by registration id.

#### Resource URL
https://mosip.io/registrationprocessor/v1/manualverification/applicantDemographic


#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | byte[]
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
FileRequestDto|Yes|Dto containing registration id and file name|

#### Request
```JSON
{
  "id" : "mosip.manual.verification.demographic",
  "version" : "1.0",
  "requesttime": "2019-02-14T12:40:59.768Z",
  "request" : {
	  "fileName": "PACKETMETAINFO",
	  "regId": "27847657360002520181208123456"
	}
}
```
#### Response
######Status Code: 200
######Description : response code is always 200 if server receives the request.
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "response" : {
	  "file": "B@629f0666"
  }
}
```
Failure :
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "responsetime": "2019-02-14T12:40:59.768Z",
  "errors" : [{
	"errorCode" : "RPR-MVS-002",
	"message" : "Requested file is not present"
  }]
}
```


# 4 Bio Dedupe Service
## 4.1 Bio Dedupe service

- #### `POST /registrationprocessor/v1/bio-dedupe/{referenceid}`

The abis would call bio-dedupe service to get the biometric cbeff file.

#### Resource URL
https://mosip.io/registrationprocessor/v1/bio-dedupe/{referenceid}

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | byte[]
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
byte[]|Yes|byte array of CBEFF file|

#### Response
###### Status codes: 200
######Description : response code is always 200 if server receives the request.
```JSON
// byte array of CBEFF xml file
```

# 5 Packet Generator Service
## 4.1 Packet Generator Service
- #### `POST /registrationprocessor/v1/packetgenerator/registrationpacket`
The abis would call bio-dedupe service to get the biometric cbeff file.

#### Resource URL
https://mosip.io/registrationprocessor/v1/packetgenerator/registrationpacket

#### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | byte[]
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Comment
-----|----------|-------------|---------------|
PacketGeneratorRequestDto|Yes|Dto containing information required for activate or deactivate packet|

#### Request
```JSON
{
  "id": "mosip.packet.generator",
  "version": "1.0",
  "requesttime": "2019-02-02T06:12:25.288Z",
  "request": {
    "centerId": "10031",
    "machineId": "10011",
    "reason": "something",
    "registrationType": "DEACTIVATED",
    "uin": "4215839851"
  }
}
```
#### Response
######Status Code:200
######Description : response code is always 200 if server receives the request.

```JSON
{
  "id": "mosip.packet.generator",
  "version": "1.0",
  "responsetime": "2019-02-02T06:12:25.288Z",
  "response": {
    "registrationId": "10031100110005020190313110030",
    "status": "RECEIVED",
    "message": "Packet created and uploaded"
  }
}
```

