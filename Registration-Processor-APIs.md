This section details about the service APIs in the Registration-Processor modules

[2.9.1 Packet receiver API](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs#291-packet-receiver)

[2.9.2 Registration status API](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs#292-registration-status)

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
    "syncType": "NEW_REGISTRATION"
  },
  {
    "langCode": "eng",
    "parentRegistrationId": "",
    "registrationId": "2018701130000410092018110735",
    "statusComment": "string",
    "syncStatus": "PRE_SYNC",
    "syncType": "NEW_REGISTRATION"
  }
]
```
### Example Response
```JSON
[
  {
    "registrationId": "2018701130000410092012345678",
    "syncType": "NEW_REGISTRATION",
    "parentRegistrationId": "",
    "syncStatus": "PRE_SYNC",
    "statusComment": "string",
    "langCode": "eng",
    "isActive": true,
    "isDeleted": false
  },
  {
    "registrationId": "2018701130000410092018110735",
    "syncType": "NEW_REGISTRATION",
    "parentRegistrationId": "",
    "syncStatus": "PRE_SYNC",
    "statusComment": "string",
    "langCode": "eng",
    "isActive": true,
    "isDeleted": false
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
