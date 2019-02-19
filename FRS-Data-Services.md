## Table Of Content
- [Data services](#data-services)
  * [1. Data mapper](#1-data-mapper)
  * [2. Data Access Manager](#2-data-access-manager)
  * [3. Sync Handler](#3-sync-handler)
  * [4. ID Generator and Validator](#4-id-generator-and-validator)
    * [4.1 ID Validator](#41-id-validator)
      * [4.1.1 Static Pin Validator](#411-static-pin-validator)
      * [4.1.2  UIN Validator](#412--uin-validator)
      * [4.1.3 PRID Validator](#413-prid-validator)
      * [4.1.4 VID Validator](#414-vid-validator)
      * [4.1.5 RID Validator](#415-rid-validator)
      * [4.1.6 TSP ID Validator](#416-tsp-id-validator)
    * [4.2 ID Generator](#42-id-generator)
      * [4.2.1 RID Generator](#421-rid-generator)
      * [4.2.2 Machine ID Generator](#422-machine-id-generator)
      * [4.2.3 Registration Center ID Generator](#423-registration-center-id-generator)
      * [4.2.4 TSP ID Generator](#424-tsp-id-generator)
      * [4.2.5 PRID Generator](#425-prid-generator)
      * [4.2.6 VID Generator](#426-vid-generator)
      * [4.2.7 Token ID Generator](#427-token-id-generator)
# Data services
## 1. Data mapper
Data mapper is used across MOSIP to facilitate mapping between DTO and entity 

## 2. Data Access Manager
Data Access Manager provides a DAO (Data access object) interface to do the following
1. Provide an interface for connection to a DB
1. Provide an interface to support DB CRUD operation
1. Provide an interface to support a custom SQL
1. Provide an interface to call DB functions

## 3. Sync Handler
Sync Handler allows registration client to sync Master data, List of User, Roles and respective mappings and Configurations (Registration Client specific and Global configs).


Sync Handler also allows Registration Client to push data from Client local database to Master Database.


As part of Masterdata Sync, the service will receive a Machine ID and Timestamp, looks for a mapped Center id to that Machine ID and responds to the Registration Client with the Center specific Master data for the following tables.


1. Registration Center Type
1. List of Registration Center
1. Template File Format
1. Template Type
1. Templates
1. Reason Category
1. List of Reasons
1. Document Category
1. Document Type
1. Mapping of Document Category-Type (refer table "Valid Documents")
1. Machine Type
1. Machine Specifications
1. List of Machines
1. Device Types
1. Device Specifications
1. List of Devices
1. Location Hierarchy
1. List of Languages
1. List of Genders
1. Biometric Authentication type - (refer table "Biometric Type")
1. Biometric Attribute
1. Center-Machine Mapping
1. Center-Device Mapping
1. Center-Machine-Device Mapping
1. Center-Machine-User Mapping
1. Center-User Mapping


The Sync Handler service will only send incremental changes based on the Timestamp received by the service.


For configuration, sync handler will receive a request to sync configurations and will respond back with Registration Client specific and Global Configurations


For User, Roles and Respective User-Role mappings, Sync handler will receive Machine ID and Timestamp and will respond to the Registration Client will Center specific incremental changes.

## 4. ID Generator and Validator
### 4.1 ID Validator
#### 4.1.1 Static Pin Validator
MOSIP system can perform Static PIN validation against a defined Static PIN logic.

Upon receiving a request to perform data validation on Static PIN with input parameters (Static PIN), the system validate Static PIN as per the Static PIN generation logic and responds with the required result (Valid/Invalid).

1. Validate if the request has the following input parameters.
* Static PIN
2. Validate if the Static PIN is of configured length. (Current configured length = 6)
1. Validate if the Static PIN is only numerical.

In case of Exceptions, system should trigger relevant error messages. Refer “Messages” section
### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|Static PIN is Valid|True|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|Static PIN in Invalid|Static PIN length Must be <Length configured>|KER-IDV-501|
|Static PIN in not numeric|	Static PIN length must be numeric>|	KER-IDV-502|
|Static PIN input parameter is missing	|Input parameter is missing	|KER-IDV-503|





#### 4.1.2  UIN Validator
MOSIP system can perform UIN validation against a defined ID policy

Upon receive a Request to validate the UIN the system validates the UIN against the defined policy

Validates if the UIN is of configured length.

If no length is configured, validate if UIN length is of 12 digits

Validates the UIN by verifying the checksum

Validates if the UIN received follows the UIN generation logic

Responds to the source with appropriate message 

Raises an alert in case of listed exceptions as listed below

### <p align="left"> **1. Type: Success – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
UIN is Valid|	"Valid"|	NA|
UIN is invalid|	"Invalid"	|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
MosipInvalidIDException	|Entered UIN should not be empty or null.|	COK-IDV-UIN-001
MosipInvalidIDException	|Entered UIN should not contain any sequential and repeated block of number for 2 or more than two digits	|COK-IDV-UIN-002
MosipInvalidIDException	|Entered UIN length should be 12 digit|	COK-IDV-UIN-003
MosipInvalidIDException	|Entered UIN should not contain any alphanumeric characters|	COK-IDV-UIN-004
MosipInvalidIDException|	Entered UIN should match checksum|	COK-IDV-UIN-005
MosipInvalidIDException	|Entered UIN should not contain Zero or One as first Digit|	COK-IDV-UIN-006
UIN_VAL_ILLEGAL_REVERSE	|UIN First configured no.of digits should be different from the reverse of last configured no.of digits|	KER-IDV-207
UIN_VAL_ILLEGAL_EQUAL_LIMIT|	UIN First configured no.of digits should be different from the last configured no.of digits	|KER-IDV-208







#### 4.1.3 PRID Validator
As the MOSIP system can validate PRID as per a defined PRID generation logic

Upon receiving a request to validate the PRID the system validates the PRID against the defined policy

1. Validates if the received PRID contains number of digits as configured by the ADMIN
1. In absence of the configured length, validates if the PRID received should contain 14 digits
1. Validates the PRID received follows the PRID generation logic 
In case of Exceptions, triggers relevant error messages

Responds to the source with appropriate message 

Raise an alert in case of listed exceptions as defined below
### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
PRID is valid|	"Valid"|	NA|
PRID is invalid|	"Invalid"|	NA|


### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
MosipInvalidIDException	|Entered PRID should not be empty or null.|	KER-IDV-101
MosipInvalidIDException|	Entered PRID should not contain any sequential and repeated block of number for 2 or more than two digits	|KER-IDV-102
MosipInvalidIDException	|Entered PRID length should be 14 digit	|KER-IDV-103
MosipInvalidIDException	|Entered PRID should not contain any alphanumeric characters|	KER-IDV-104
MosipInvalidIDException	|Entered PRID should match checksum	|KER-IDV-105
MosipInvalidIDException	|Entered PRID should not contain Zero or One as first Digit|	KER-IDV-106



#### 4.1.4 VID Validator
MOSIP system can perform VID validation against a defined VID policy

Upon receiving a request to validate the VID with input parameters (UIN), the system validates the VID against the defined VID policy
1. Validates if the VID is of configured length.
1. If no length is configured, validate if VID length is of 16 digits
1. Validates the VID by verifying the checksum
1. Validates if the VID received follows the VID generation logic listed in User Story

Respond to the source with appropriate message and Raise an alert in case of listed exceptions 

### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|VID is Valid|"Valid"|NA|
|VID is Invalid|"Invalid"|NA|



### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|------|:------:|
|MosipInvalidIDException|Entered VID should not be empty or null.|KER-IDV-VID-001|
|MosipInvalidIDException|Entered VID should not contain any sequential and repeated block of number for 2 or more than two digits|KER-IDV-VID-002
|MosipInvalidIDException|Entered VID length should be 16 digit|	KER-IDV-VID-003|
|MosipInvalidIDException|Entered VID should not contain any alphanumeric characters|KER-IDV-VID-004|
|MosipInvalidIDException|Entered VID should match checksum|KER-IDV-VID-005|
|MosipInvalidIDException|Entered VID should not contain Zero or One as first Digit|KER-IDV-VID-006|






#### 4.1.5 RID Validator

RID is generated in the following manner:
* First 5 Digit: Registration Center ID
* Next 5 Digits: Machine ID
* Next 5 Digits: Running sequence
* Last 14 Digits: Timestamp
* Total: 29 Digits

RID Validation performs pattern validation on an RID and provides three methods to validate an RID.
1. Receive a RID, check whether RID is of configured length or not and respond with whether RID is valid or invalid
1. Receive a RID along with Registration Center ID and Machine ID. Check whether RID is of configured length or not and whether Registration Center ID and Machine ID is attached to the RID or not. Respond with whether RID is valid or invalid
1. Receive a RID along with Registration Center ID, Machine ID, Sequence Length and Timestamp Length. Check whether RID is proper or not as per the input received. Respond with whether RID is valid or invalid 


#### 4.1.6 TSP ID Validator
MOSIP system can perform TSP ID validation against a defined TSP ID policy

Upon receiving a request to perform data validation on TSP ID with input parameters (TSP ID), the system validate TSP ID as per the TSP ID generation logic
1. Validates if the request has the following input parameters.
* TSP ID
2. Validates TSP ID as per the TSP ID generation Policy
1. In case of Exceptions system triggers relevant error messages 

Respond with the required result (Valid/Invalid)

Raise an alert in case of listed exceptions as defined below:

### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|TSP ID is Valid|	True	|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|------|:------:|
|TSP ID in Invalid	|TSP ID length Must be <Length configured)	|KER-IDV-401|

### 4.2 ID Generator
#### 4.2.1 RID Generator
#### 4.2.2 Machine ID Generator
MOSIP system can generate Machine ID as per defined Machine ID generation logic

Upon receiving a request to generate Machine ID the system generates Machine ID as per default Machine ID generation logic as mentioned below
1. Machine ID should only be numeric
1. Machine ID generated should be of length of 5 digits
1. Each new Machine ID should be incremented by 1 for each new request
1. Machine ID generation should start from 10000
1. The number should not contain the restricted numbers defined by the ADMINs

Responds with the Machine ID to the source

Raise an alert in case of listed exceptions as specified below
* All confirmation, warning, and error messages are listed below. The message text is configurable.

### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|NA|	NA	|NA|


### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|------|:------:|
|MachineIdException|	Error occured while fetching ID	|KER-MNG-001|
|MachineIdException|	Error occured while inserting ID|	KER-MNG-002|


#### 4.2.3 Registration Center ID Generator
MOSIP system can generate Registration Center ID as per defined Registration Center ID generation logic

Upon receiving a request to generate Registration Center ID the system generates it as per default Registration Center ID generation logic

Registration Center ID is generated as per the defined logic mentioned below

1. Registration Center ID should only be numeric
1. Registration Center ID generated should be of length of 5 digits
1. Each new Registration Center ID should be incremented by 1 for each new request
1. Registration Center ID generation should start from 10000
1. The number should not contain the restricted numbers defined by the ADMIN
In case of Exceptions, system triggers relevant error messages

Responds with the Registration Center ID to the source

Raises an alert in case of listed exceptions

### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|NA|	NA	|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|------|:------:|
RegistrationCenterIdException|	Error occured while fetching ID|	KER-RCG-001
RegistrationCenterIdException|	Error occured while inserting ID|	KER-RCG-002


#### 4.2.4 TSP ID Generator
MOSIP system can generate TSP ID as per defined TSP ID generation logic

Upon receiving a request to generate TSP ID, the system generates it as per default TSP ID generation logic

TSP ID should be generated as per the defined logic mentioned below
1. TSP ID should only be numeric
1. TSP ID generated should be of length of 4 digits
1. Each new TSP ID should be incremented by 1 for each new request
1. TSP ID generation should start from 1000
1. The number should not contain the restricted numbers defined by the ADMIN

Responds with the TSP ID to the source

Raise an alert in case of listed exceptions and triggers the following messages as listed below
### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|NA|	NA	|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|------|:------:|
|NA	|TSP ID Generation Failed|	NA|

#### 4.2.5 PRID Generator
MOSIP system can generate PRID as per a defined PRID generation logic

Upon receiving a request to generate PRID with input parameters the system generates PRID as per default PRID generation logic

PRID generated should contain number of digits as configured by the ADMIN
In absence of the configured length, the PRID generated should contain 14 digits
PRID is generated as per the defined logic mentioned below
* The number should not contain any alphanumeric characters
* The number should not contain any repeating numbers for 2 or more than 2 digits
* The number should not contain any sequential number for 3 or more than 3 digits
* The numbers should not be generated sequentially
* The number should not have repeated block of numbers for 2 or more than 2 digits
* The number should not contain the restricted numbers defined by the ADMIN
* The last digit in the number should be reserved for a checksum
* The number should not contain '0' or '1' as the first digit.

Respond with the PRID to the source

Raise an alert in case of listed exceptions as listed below
### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|NA|NA|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
PridGenerationexception	|Unable to connect to the database|	KER-PRD-001|


#### 4.2.6 VID Generator
MOSIP system can  generate VID as per a defined VID generation logic

Upon receiving a request to generate VID with input parameters (UIN) the system checks if a VID is already generated, validates if the existing VID is active based on the defined VID expiry policy

If the generated VID is active, responds with the same VID

If the generated VID is inactive:

1. Generate new VID based on the VID generation policy defined below
1. Responds with the new VID generated
1. Maps the new VID against the received UIN

If no VID is generated against the UIN:
1. Generates new VID based in the policy defined
1. Map the new VID against the received UIN
1. Raise an alert in case of listed exceptions as listed below

### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|NA|NA|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
INVALID_UIN_EXCEPTION|	Invalid UIN	|KER-VID-001|
VID_GENERATION_FAILED_EXCEPTION	|VID Generation Failed|	KER-VID-002|

**VID generation policy**
1. VID generated should contain the number of digits as configured
1. In absence of configured length, VID generated should have 16 digits
1. Validate if the VID is generated as per the defined logic mentioned below
* The number should not contain any alphanumeric characters
* The number should not contain any repeating numbers for 2 or more than 2 digits
* The number should not contain any sequential number for 3 or more than 3 digits
* The numbers should not be generated sequentially
* The number should not have repeated block of numbers for 2 or more than 2 digits
* The number should not contain the restricted numbers defined by the ADMIN
* The last digit in the number should be reserved for a checksum
* The number should not contain '0' or '1' as the first digit.
4. Expired VID should not be sent in response


#### 4.2.7 Token ID Generator
MOSIP system can generate Token ID as per defined Token ID generation logic

Upon receiving a request to generate Token ID (with input para meters (TSP ID, UIN) the system generate token ID as per default Token ID generation logic

The numbers is not be generated sequentially

Token ID generated is of the length of 36 digits

The length of Token ID is configurable by the ADMIN

Token ID is generated as per the defined logic mentioned below
* The number does not contain any alphanumeric characters and contains only numeric characters
* The last digit in the number is reserved for a checksum
* ID is unique for a combination of TSP ID and UIN received
* ID is untraceable to both TSP ID and UIN received

Responds with the Token ID to the source

Raise an alert in case of listed exceptions as listed below
### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|NA|NA|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
Database	|Connection|	Exception	|unable to connect To db|	KER-TIG-001|
|:------:|:------:|:------:|:------:|:------:|




