This section details about the service APIs in the Registration-Processor modules

[2.9.1 Packet receiver API](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs#291-packet-receiver)

[2.9.2 Registration status API](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs#292-registration-status)

[2.9.3 Manual Adjudication API](https://github.com/mosip/mosip/wiki/Manual-Adjudication-APIs#293-manual-adjudication)

# 2.9.1 Packet Receiver API
## 2.9.1.1 Packet-receiver service
This service receives the registration packet and puts it to landing zone.

### Resource URL
### `POST /registration-processor/packet-receiver/registrationpackets`

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
  "PACKET_UPLOADED_TO_LANDING_ZONE"
}
```
#### Failure response

Example 1 : Upload packet without syncing the packet id
```JSON
{
  "message": "PACKET_NOT_YET_SYNC",
  "errorcode": "IIS_GEN_PACKET NOT YET SYNC IN REGISTRATION"
}
```
Example 2 : Packet is already present in Server
```JSON
{
  "message": "DUPLICATE_PACKET_RECIEVED",
  "errorcode": "IIS_GEN_DUPLICATE_PACKET_UPLOAD"
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
### `POST /registration-processor/registration-status/registrationstatus`

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
  "2018701130000410092012345678,2018701130000410092018110735"
}
```
### Example Response
```JSON
[
  {
    "registrationId": "2018701130000410092012345678",
    "registrationType": "NEW",
    "referenceRegistrationId": null,
    "statusCode": "PACKET_UPLOADED_TO_LANDING_ZONE",
    "langCode": "eng",
    "statusComment": "Packet is in PACKET_UPLOADED_TO_LANDING_ZONE status",
    "latestRegistrationTransactionId": "c19f1768-2aa1-494d-8d27-acbdc8e1f68d",
    "createdBy": "MOSIP_SYSTEM",
    "createDateTime": "2018-11-02T22:58:08.263",
    "updatedBy": null,
    "updateDateTime": "2018-11-02T22:58:08.264",
    "deletedDateTime": "2018-11-02T22:58:08.264",
    "retryCount": null,
    "active": true,
    "deleted": false
  },
  {
    "registrationId": "2018701130000410092018110735",
    "registrationType": "NEW",
    "referenceRegistrationId": null,
    "statusCode": "PACKET_UPLOADED_TO_LANDING_ZONE",
    "langCode": "eng",
    "statusComment": "Packet is in PACKET_UPLOADED_TO_LANDING_ZONE status",
    "latestRegistrationTransactionId": "4c26f2cd-5b64-4587-93a9-ee2198afe1da",
    "createdBy": "MOSIP_SYSTEM",
    "createDateTime": "2018-11-02T22:58:53.256",
    "updatedBy": null,
    "updateDateTime": "2018-11-02T22:58:53.256",
    "deletedDateTime": "2018-11-02T22:58:53.256",
    "retryCount": null,
    "active": true,
    "deleted": false
  }
]
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
### `POST /registration-processor/registration-status/sync`

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
[
  {
    "langCode": "eng",
    "parentRegistrationId": "",
    "registrationId": "2018701130000410092012345678",
    "statusComment": "string",
    "syncStatus": "PRE_SYNC",
    "syncType": "NEW"
  },
  {
    "langCode": "eng",
    "parentRegistrationId": "",
    "registrationId": "2018701130000410092018110735",
    "statusComment": "string",
    "syncStatus": "PRE_SYNC",
    "syncType": "UPDATE"
  }
]
```
### Example Response
```JSON
[
  {
    "registrationId": "2018701130000410092012345678",
    "status": "SUCCESS",
    "message": "Registartion Id's are successfully synched in Sync table",
    "parentRegistrationId": ""
  },
  {
    "registrationId": "2018701130000410092018110735",
    "status": "SUCCESS",
    "message": "Registartion Id's are successfully synched in Sync table",
    "parentRegistrationId": ""
  }
]
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
### `POST /registration-processor/manual-adjudication/assignment`

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
  "userId": "mono29"
}
```
### Example Response
```JSON
{
  "regId": "27847657360002520181208123456",
  "mvUsrId": "mono29",
  "statusCode": "ASSIGNED",
  "matchedRefId": "27847657360002520181208123456",
  "matchedRefType": "UIN",
  "reasonCode": null
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
### `POST /registration-processor/manual-adjudication/decision`

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
  "matchedRefId": "27847657360002520181208123987",
  "matchedRefType": "RID",
  "mvUsrId": "mono",
  "reasonCode": "Problem with biometrics",
  "regId": "27847657360002520181208123456",
  "statusCode": "APPROVED"
}
```
### Example Response
```JSON
{
  "regId": "27847657360002520181208123456",
  "mvUsrId": "mono",
  "statusCode": "APPROVED",
  "matchedRefId": "27847657360002520181208123987",
  "matchedRefType": "RID",
  "reasonCode": "Problem with biometrics"
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
### `POST /registration-processor/manual-adjudication/applicantBiometric`

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
  "fileName": "APPLICANTPHOTO",
  "regId": "27847657360002520181208123456"
}
```
### Example Response
byte array of applicant demographic information.

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
  "fileName": "DEMOGRAPHICINFO",
  "regId": "27847657360002520181208123456"
}
```
### Example Response
byte array of applicant biometric.

### Response codes
200

Description: Successfully retrieved applicant biometric

400

Description: Could not find information from packet store

500

Description: Internal server error