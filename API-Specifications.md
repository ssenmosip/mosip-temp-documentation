# MOSIP API List
This page and its sub-pages will have the API specifications of various features of MOSIP

## Kernel
### Public key-get service

This service will provides the public key of the Enrolment client. 

#### Resource URL
#### `GET /publickey`

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description |  Example
-----|----------|-------------|--------
applicationId |Yes|Id of the application| REGISTRATION,IDA
referenceId|Yes|Id of the Machine/TSP|
requestdate|Yes|Date-time without time-zone in ISO-8601| 2007-12-03T10:15:30

#### Example Request
/publickey/REGISTRATION?referenceId=1001&timeStamp=2018-11-29T12%3A00

#### Example Response
```JSON
{
  "publicKey": "publicKey",
  "keyExpiryTime": "keyExpiryTime",
  "keyGenerationTime": "keyGenerationTime"
}
```

## Authentication
AM: Put auth list here
* Auth API 1
* Auth API 2

## Pre-Registration
* [Service APIs](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs)

## Registration-Processor
* [Registration-Processor APIs](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs) 

## Registration
* [Registration APIs](https://github.com/mosip/mosip/wiki/Registration-APIs) 

# ABIS APIs

https://github.com/mosip/mosip/wiki/ABIS-APIs
