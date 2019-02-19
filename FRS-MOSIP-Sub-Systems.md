## Table Of Content
- [Sub-Systems](#sub-systems)
  * [1. UIN Generation](#1-uin-generation)
  * [2. Configuration Manager](#2-configuration-manager)
  * [3. Audit Manager](#3-audit-manager)
  * [4. Log Manager](#4-log-manager)
  * [5. LDAP / Authorization](#5-ldap--authorization)
# Sub-Systems
## 1. UIN Generation
MOSIP will generate a pool of UINs before the registration process and stores them. The number of UINs to be generated in a pool depends on a configuration to be done by the country depending on the peak registration requirements. UIN generation service will receive a request by Registration Processor to get a UIN. The service will respond with an unallocated UIN from the generated Pool. When the pool reaches a configured number of minimum UINs, MOSIP will generate another pool of UIN. 


The UINs generated follows the following policies:


1. UIN should not contain any alphanumeric characters
1. UIN should not contain any repeating numbers for 2 or more than 2 digits
1. UIN should not contain any sequential number for 3 or more than 3 digits
1. UIN should not be generated sequentially
1. UIN should not have repeated block of numbers for 2 or more than 2 digits
1. The last digit in the number should be reserved for a checksum
1. The number should not contain '0' or '1' as the first digit.
1. First 5 digits should be different from the last 5 digits (E.g. 4345643456)
1. First 5 digits should be different to the last 5 digits reversed (E.g. 4345665434)
1. UIN should not be an ascending or descending cyclic figure (E.g. 4567890123, 6543210987)
1. UIN should be different from the repetition of the first two digits 5 times (E.g. 3434343434)
1. UIN should not contain three even adjacent digits (E.g. 3948613752)
1. UIN should not contain ADMIN defined restricted number

## 2. Configuration Manager
## 3. Audit Manager
Audit Manager takes data from different Modules and stores it in the Audit DB. It needs to receive following attribute against each audit record. 
1. Audit Event ID - Mandatory
1. Audit Event name - Mandatory
1. Audit Event Type - Mandatory
1. Action DateTime Stamp - Mandatory
1. Host Name - Mandatory
1. Host IP - Mandatory
1. Application Id - Mandatory
1. Application Name - Mandatory
1. Session User Id - Mandatory
1. Session User Name - Mandatory
1. Module Name – Optional
1. Module Id - Optional
1. ID - Mandatory
1. ID Type - Mandatory
1. Logged Timestamp - Mandatory
1. Audit Log Description - Optional
1. Created By, (Actor who has done the event) - Mandatory
1. Created Date and Time Stamp (When this row is inserted into DB) – Mandatory
## 4. Log Manager
Log manager will provide following functionalities
1. Generate logs across the application
1. Store generated logs in configured location
1. Support for reading the logger configurations through as external file
1. Support addition log level to a particular logger dynamically

## 5. LDAP / Authorization
MOSIP system can handle Authorization across core services and restricts access to Web-services as per the roles defined below

1. OTP manager: To be defined
1. SMS Notification Manager API : To be defined
1. Email Notification Manager API : To be defined
1. Software Updater API - Master Data : To be defined
1. Software Updater API - Configurations : To be defined
1. Software Updater API - Public Keys : To be defined
1. Crypto Service API : To be defined
1. Key Manager API : To be defined
1. Master Data APIs (All Create/Update/Delete) : To be defined
1. UIN Generator : To be defined
1. Audit Manager : To be defined
1. OTP Notification Service : To be defined
1. ID Repo Service : To be defined
