## Table Of Content
- [Data Services](#data-services) 
  * [1. Data mapper](#1-data-mapper) _(DAT_FR_1)_
  * [2. Data Access Manager](#2-data-access-manager) _(DAT_FR_2)_
  * [3. Sync Handler](#3-sync-handler) _(DAT_FR_3)_
  * [4. ID Generator and Validator](#4-id-generator-and-validator) 
    * [4.1 ID Generator](#41-id-generator) 
      * [4.1.1 Machine ID Generator](#411-machine-id-generator) _(DAT_FR_4.1)_
      * [4.1.2 Registration Center ID Generator](#412-registration-center-id-generator) _(DAT_FR_4.2)_
      * [4.1.3 MISP ID Generator](#413-misp-id-generator) _(DAT_FR_4.3)_
      * [4.1.4 PRID Generator](#414-prid-generator) _(DAT_FR_4.4)_
      * [4.1.5 VID Generator](#415-vid-generator) _(DAT_FR_4.5)_
      * [4.1.6 Token ID Generator](#416-token-id-generator) _(DAT_FR_4.6)_
      * [4.1.7 Partner ID Generator](#417-partner-id-generator) _(DAT_FR_4.12)_
      * [4.1.8 License Key Generator](#418-license-key-generator) _(DAT_FR_4.13)_
    * [4.2 ID Validator](#42-id-validator) 
      * [4.2.1 Static Pin Validator](#421-static-pin-validator) _(DAT_FR_4.7)_
      * [4.2.2 UIN Validator](#422--uin-validator) _(DAT_FR_4.8)_
      * [4.2.3 PRID Validator](#423-prid-validator) _(DAT_FR_4.9)_
      * [4.2.4 VID Validator](#424-vid-validator) _(DAT_FR_4.10)_
      * [4.2.5 RID Validator](#425-rid-validator) _(DAT_FR_4.11)_
      * [4.2.6 Partner ID Validator](#426-partner-id-validator) _(DAT_FR_4.14)_
      * [4.2.7 License Key Status Validator](#427-license-key-status-validator) _(DAT_FR_4.15)_

# Data services
## 1. Data mapper
Data mapper is used across MOSIP to facilitate mapping between DTO (Data Transfer Object) and entity. 

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-datamapper.md)

## 2. Data Access Manager
Data Access Manager provides a DAO (Data Access Object) interface to do the following
1. Provide an interface for connection to a Database
1. Provide an interface to support Database CRUD (Create, Read, Update, Delete) operation
1. Provide an interface to support a custom SQL
1. Provide an interface to call Database functions.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-dataaccess.md)

## 3. Sync Handler
1. Sync Handler allows registration client to sync Master data, List of User, Roles and Respective Mappings and Configurations (Registration Client specific and Global Configs).
1. Sync Handler also allows Registration Client to push data from Client local database to Master Database.
1. As part of Masterdata Sync, the service receives a Machine ID and Timestamp, looks for a mapped Center ID to that Machine ID and responds to the Registration Client with the Center specific Master data for the following tables.
   * Registration Center Type
   * List of Registration Center
   * Template File Format
   * Template Type
   * Templates
   * Reason Category
   * List of Reasons
   * Document Category
   * Document Type
   * Mapping of Applicant Type-Document Category-Document Type (refer table "Valid Documents")
   * Machine Type
   * Machine Specifications
   * List of Machines
   * Device Types
   * Device Specifications
   * List of Devices
   * Location Hierarchy
   * List of Languages
   * List of Genders
   * Biometric Authentication Type
   * Biometric Attribute
   * Center-Machine Mapping
   * Center-Device Mapping
   * Center-Machine-Device Mapping
   * Center-Machine-User Mapping
   * Center-User Mapping
4. The Sync Handler service only sends incremental changes based on the Timestamp received by the service.
1. For configuration, sync handler receives a request to sync configurations and will respond back with Registration Client specific and Global Configurations.
1. For User, Roles and Respective User-Role mappings, Sync handler receives Center ID and Timestamp and will respond to the Registration Client with Center specific incremental changes.

[**Link to design**](https://github.com/mosip/mosip/blob/0.8.0_FIT3_KERNEL/docs/design/kernel/kernel-syncservices.md)
## 4. ID Generator and Validator
### 4.1 ID Generator
#### 4.1.1 Machine ID Generator

Upon receiving a request to generate Machine ID, the system generates Machine ID as per default Machine ID generation logic as mentioned below:
1. Machine ID should only be numeric
1. Machine ID generated should be of length of 5 digits
1. Each new Machine ID should be incremented by 1 for each new request
1. Machine ID generation should start from 10000
1. The number should not contain the restricted numbers defined by the ADMINs.

Responds with the Machine ID to the source.

Raises an alert in case of exceptions. 

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/Kernel-idgenerator-MachineID.md)

#### 4.1.2 Registration Center ID Generator

Upon receiving a request to generate Registration Center ID, the system generates it as per default Registration Center ID generation logic

Refer below for the process:
1. Registration Center ID is generated as per the defined logic mentioned below
   * Registration Center ID should only be numeric
   * Registration Center ID generated should be of length of 5 digits
   * Each new Registration Center ID should be incremented by 1 for each new request
   * Registration Center ID generation should start from 10000
   * The number should not contain the restricted numbers defined by the ADMIN
2. In case of Exceptions, system triggers relevant error messages
1. Responds with the Registration Center ID to the source
1. Raises an alert in case of exceptions.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-RegistrationCenterIDGenerator.jpg)

#### 4.1.3 MISP ID Generator

Upon receiving a request to generate MISP ID, the system generates it as per default MISP ID generation logic.

Refer below for the process:

1. MISP ID should be generated as per the defined logic mentioned below
   * MISP ID should only be numeric
   * MISP ID generated should be of length of 3 digits (Configurable)
2. MISP ID generation should start from 100
3. Each new MISP ID should be incremented by one for each new request
4. The number should not contain the restricted numbers defined by the ADMIN
5. Responds with the MISP ID to the source
6. Raises an alert in case of exceptions and triggers the messages.

[**Link to design**]() _**update the link**_

#### 4.1.4 PRID Generator

Upon receiving a request to generate PRID with input parameters, the system generates PRID as per default PRID generation logic.

Refer below for the process:
1. PRID generated should contain number of digits as configured by the ADMIN
1. PRID is generated as per the defined logic mentioned below
   * The number should not contain any alphanumeric characters
   * The number should not contain any repeating numbers for 2 or more than 2 digits
   * The number should not contain any sequential number for 3 or more than 3 digits
   * The numbers should not be generated sequentially
   * The number should not have repeated block of numbers for 2 or more than 2 digits
   * The number should not contain the restricted numbers defined by the ADMIN
   * The last digit in the number should be reserved for a checksum
   * The number should not contain '0' or '1' as the first digit
4. Responds with the PRID to the source
1. Raises an alert in case of exceptions. 

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/Kernel-idgenerator-PRID.md)

#### 4.1.5 VID Generator

Upon receiving a request to generate VID, the system generates PRID as per default PRID generation logic

Refer below for the process:
1. VID should be generated as per the defined logic mentioned below
1. Responds with the VID to the source
4. Raises an alert in case of exceptions. 

**VID generation policy**
1. VID generated should contain the number of digits as configured.
1. Validates if the VID is generated as per the defined logic mentioned below
   * The number should not contain any alphanumeric characters
   * The number should not contain any repeating numbers for 2 or more than 2 digits
   * The number should not contain any sequential number for 3 or more than 3 digits
   * The numbers should not be generated sequentially
   * The number should not have repeated block of numbers for 2 or more than 2 digits
   * The number should not contain the restricted numbers defined by the ADMIN
   * The last digit in the number should be reserved for a checksum
   * The number should not contain '0' or '1' as the first digit.
4. Expired VID should not be sent in response.


[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/VID%20Generator.md)
#### 4.1.6 Token ID Generator

Upon receiving a request to generate Token ID (with input para meters (TSP ID, UIN), the system generates token ID as per default Token ID generation logic

Refer below for the process:
1. The numbers is not be generated sequentially
1. Token ID generated is of the length of 36 digits
1. The length of Token ID is configurable by the ADMIN
1. Token ID is generated as per the defined logic mentioned below
   * The number does not contain any alphanumeric characters and contains only numeric characters
   * The last digit in the number is reserved for a checksum
   * ID is unique for a combination of TSP ID and UIN received
   * ID is untraceable to both TSP ID and UIN received
5. Responds with the Token ID to the source
1. Raises an alert in case of exceptions.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/TokenID%20Generator.md)

### 4.2 ID Validator
#### 4.2.1 Static Pin Validator

Upon receiving a request to perform data validation on Static PIN with input parameters (Static PIN), the system validates Static PIN as per the Static PIN generation logic and responds with the required result (Valid/Invalid).

Refer below for the process:
1. Validates if the request has the following input parameters.
   * Static PIN
2. Validates if the Static PIN is of configured length. (Current configured length = 6)
1. Validates if the Static PIN is only numerical.
1. In case of Exceptions, system triggers relevant error messages. 

#### 4.2.2  UIN Validator

Upon receiving a request to validate the UIN, the system validates the UIN against the defined policy

Refer below for the process:
1. Validates if the UIN is of configured length.
1. Validates the UIN by verifying the checksum
1. Validates if the UIN received as per the UIN generation logic
1. Responds to the source with an appropriate message 
1. Raises an alert in case of exceptions. 

#### 4.2.3 PRID Validator

Upon receiving a request to validate the PRID, the system validates the PRID against the defined policy

Refer below for the process:
1. Validates if the received PRID contains number of digits as configured by the ADMIN
1. Validates the PRID received as per the PRID generation logic 
1. Responds to the source with an appropriate message 
1. Raises an alert in case of exceptions. 

#### 4.2.4 VID Validator

Upon receiving a request to validate the VID with input parameters (UIN), the system validates the VID against the defined VID policy

Refer below for the process:
1. Validates if the VID is of configured length.
1. Validates the VID by verifying the checksum
1. Validates if the VID received as per the VID generation logic
1. Responds to the source with an appropriate message and raises an alert in case of exceptions.

#### 4.2.5 RID Validator

RID is generated in the following manner:
* First 5 Digit: Registration Center ID
* Next 5 Digits: Machine ID
* Next 5 Digits: Running sequence
* Last 14 Digits: Timestamp
* Total: 29 Digits

RID Validation performs pattern validation on RID and provides three methods to validate RID.
1. Receive a RID, check whether RID is of configured length or not and respond with whether RID is valid or invalid
1. Receive a RID along with Registration Center ID and Machine ID. Check whether RID is of configured length or not and whether Registration Center ID and Machine ID are attached to the RID or not. Respond with whether RID is valid or invalid
1. Receive a RID along with Registration Center ID, Machine ID, Sequence Length and Timestamp Length. Check whether RID is proper or not as per the input received. Respond with whether RID is valid or invalid.

#### 4.2.6 TSP ID Validator

Upon receiving a request to perform data validation on TSP ID with input parameters (TSP ID), the system validates TSP ID as per the TSP ID generation logic

Refer below for the process:
1. Validates if the request has the following input parameters.
   * TSP ID
2. Validates TSP ID as per the TSP ID generation Policy
1. Responds with the required result (Valid/Invalid)
1. Raises an alert in case of exceptions. 

[**Link to ID validator design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-idvalidator.md)

