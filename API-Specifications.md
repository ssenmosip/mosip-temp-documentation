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
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineid|Yes|Id of the machine| | 
requestdate|Yes|Date in ISO format| | 

#### Example Request
-NA-

#### Example Response
```JSON
{
  "publickey": base_64_encoded
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
