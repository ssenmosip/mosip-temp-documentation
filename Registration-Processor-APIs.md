This section details about the service APIs in the Registration-Processor modules

[2.9.1 Packet receiver API](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs#291-packet-receiver)

[2.9.2 Registration status API](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs#292-registration-status)

[2.9.3 Manual Adjudication API](https://github.com/mosip/mosip/wiki/Manual-Adjudication-APIs#293-manual-adjudication)

# 2.9.1 Packet Receiver API
## 2.9.1.1 Packet-receiver service
This service receives the registration packet and puts it to landing zone.

### Resource URL
### `POST /registration-processor/registrationpackets/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Request format | MULTIPART
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
MultipartFile|Yes|The encrypted zip file| |

### Example Request
![Request](_images/reg_processor/packet_receiver_sample_input.PNG)

### Example Response

#### Success response
```JSON
{
	"id" : "mosip.registration.packet",
	"version" : "1.0",
	"timestamp" : "2019-02-02T06:12:25.288Z",
	"response" : {
		"status" : "PACKET_UPLOADED_TO_VIRUS_SCAN"
	},
	"error" : null
}
```
#### Failure response

```JSON
{
  "id" : "mosip.registration.packet",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : null,
  "error" : {
		"errorcode": "RPR-PKR-005",
	    "message": "The request received is a duplicate request to upload a Packet"
	}
}
```

### Response codes
200

Description: Packet successfully uploaded to landing zone

400

Description: Packet already present in landing zone

401

Description: Unauthorized

403

Description: Forbidden

# 2.9.2 Registration Status API
## 2.9.2.1 Packet-status service
This service return the registration current status for list of input registration ids.

### Resource URL
### `POST /registration-processor/registrationstatus/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
registrationIds|Yes|List of registration ids| |

### Example Request
```JSON
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
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
### Example Response
Record found :
```JSON
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
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
```JSON
{
  "id" : "mosip.registration.status",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : []
}
```

### Response codes
200

Description: Successfully retrieved information

400

Description: Could not find information

401

Description: Unauthorized

403

Description: Forbidden

## 2.9.2.2 Sync-registration service
The registration ids has to be synced with server before uploading packet to landing zone. This service is used to syncs registration ids.

### Resource URL
### `POST /registration-processor/sync/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
List[SyncRegistrationDto]|Yes|List of SyncRegistrationDto| |

### Example Request
```JSON
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "request" : [
	  {
		"langCode": "eng",
		"parentRegistrationId": null,
		"registrationId": "80006444440002520181208094000",
		"statusComment": "string",
		"syncStatus": "PRE_SYNC",
		"syncType": "NEW"
	  }
	]
}
```
### Example Response
Success response :
```JSON
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : [
	  {
		"registrationId": "80006444440002520181208094000",
		"status": "SUCCESS",
		"message": "Registartion Id's are successfully synched in Sync table",
		"parentRegistrationId": null
	  },
	  {
		"registrationId": "27847657360002520181208183055",
		"status": "SUCCESS",
		"message": "Registartion Id's are successfully synched in Sync table",
		"parentRegistrationId": null
	  }
	]
}
```
Failure response
```JSON
{
  "id" : "mosip.registration.sync",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : [
	  {
		"registrationId": "1234575",
		"status": "FAILURE",
		"message": "RegistrationId Length Must Be 29",
		"parentRegistrationId": "string",
		"errorCode": "RPR-RGS-009"
	  },
	  {
		"registrationId": "12345678901234567890123456789",
		"status": "FAILURE",
		"message": "Invalid Time Stamp Found in RegistrationId",
		"parentRegistrationId": "string",
		"errorCode": "RPR-RGS-007"
	  },
	  {
		"registrationId": "27847657360002520181208183052",
		"status": "FAILURE",
		"message": "Parent RegistrationId Length Must Be 29",
		"parentRegistrationId": "53718436135988",
		"errorCode": "RPR-RGS-012"
	  },
	  {
		"registrationId": "27847657360002520181208aaaaaa",
		"status": "FAILURE",
		"message": "RegistrationId Must Be Numeric Only",
		"parentRegistrationId": "string",
		"errorCode": "RPR-RGS-008"
	  }
	]
}
```

### Response codes
200

Description: Successfully synced

400

Description: Could sync

401

Description: Unauthorized

403

Description: Forbidden

# 2.9.3 Manual Adjudication API
## 2.9.3.1 manual-adjudication-assignment service
This service is used to assign one single unassigned applicant record to the input user.

### Resource URL
### `POST /manual-verification/assignment/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
String|Yes|The user id| |

### Example Request
```JSON
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "request" : {
	"userId": "mono29"
  }
}
```
### Example Response
Success response
```JSON
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : {
	  "regId": "27847657360002520181208123456",
	  "mvUsrId": "mono29",
	  "statusCode": "ASSIGNED",
	  "matchedRefId": "27847657360002520181208123456",
	  "matchedRefType": "UIN",
	  "reasonCode": null
	},
	"error" : null
}
```
Failure response
```JSON
{
  "id" : "mosip.manual.verification.assignment",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : null,
	"error" : {
		"errorCode" : "RPR-FAC-003",
		"message" : "Cannot find the Registration Packet"
	}
}
```

### Response codes
200

Description: Successfully assigned applicant to manual adjudicator

400

Description: Could not assign

500

Description: Internal server error

## 2.9.3.2 manual-adjudication-decision service
This service is used to get the decision from manual adjudicator for an applicant and update the decision in table.

### Resource URL
### `POST /manual-verification/decision/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
ManualVerificationDTO|Yes|Dto containing manual adjudication info| |

### Example Request
```JSON
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
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
### Example Response
Success response
```JSON
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : {
	  "regId": "27847657360002520181208123456",
	  "mvUsrId": "mono",
	  "statusCode": "APPROVED",
	  "matchedRefId": "27847657360002520181208123987",
	  "matchedRefType": "RID",
	  "reasonCode": "Problem with biometrics"
	},
	"error" : null
}
```
Failure response
```JSON
{
  "id" : "mosip.manual.verification.decision",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "response" : null,
	"error" : {
		"errorCode" : "RPR-MVS-003"",
		"message" : "Invalid status update"
	}
}
```

### Response codes
200

Description: Successfully Updated decision

400

Description: Could update decision

500

Description: Internal server error

## 2.9.3.3 manual-adjudication-applicant-biometric service
The manual adjudicator would need to verify the applicant biometric and demographic records. This service is used to get the applicant biometric from packet store by registration id.

### Resource URL
### `POST /manual-verification/applicantBiometric/v1.0`

### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | byte[]
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
FileRequestDto|Yes|Dto containing registration id and file name| |

### Example Request
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "request" : {
	  "fileName": "APPLICANTPHOTO",
	  "regId": "27847657360002520181208123456"
	}
}
```
### Example Response
Success :
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "file": "B@629f0666"
  "error" : null
}
```
Failure :
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "file": null,
  "error" : {
	"errorCode" : "RPR-MVS-002",
	"message" : "Requested file is not present"
  }
}
```

### Response codes
200

Description: Successfully retrieved applicant demographic

400

Description: Could not find information from packet store

500

Description: Internal server error

## 2.9.3.4 manual-adjudication-applicant-demographic service
The manual adjudicator would need to verify the applicant biometric and demographic records. This service is used to get the applicant demographic from packet store by registration id.

### Resource URL
### `POST /registration-processor/manual-adjudication/applicantDemographic`

### Resource details

Resource Details | Description
------------ | -------------
Request format | JSON
Response format | byte[]
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
FileRequestDto|Yes|Dto containing registration id and file name| |

### Example Request
```JSON
{
  "id" : "mosip.manual.verification.demographic",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "request" : {
	  "fileName": "PACKETMETAINFO",
	  "regId": "27847657360002520181208123456"
	}
}
```
### Example Response
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "file": "B@629f0666"
  "error" : null
}
```
Failure :
```JSON
{
  "id" : "mosip.manual.verification.biometric",
  "version" : "1.0",
  "timestamp": "2019-02-04T13:46:39.919+0000",
  "file": null,
  "error" : {
	"errorCode" : "RPR-MVS-002",
	"message" : "Requested file is not present"
  }
}
```

### Response codes
200

Description: Successfully retrieved applicant biometric

400

Description: Could not find information from packet store

500

Description: Internal server error