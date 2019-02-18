## Table Of Content
- [Common Services](#common-services)
  * [1. OTP manager](#1-otp-manager)
  * [2. QR Code Generator](#2-qr-code-generator)
  * [3. Crypto](#3-crypto)
    * [3.1 Key Generator](#31-key-generator)
    * [3.2 Key Management](#32-key-management)
    * [3.3 Crypto Utility](#33-crypto-utility)
    * [3.4 Hash Utility](#34-hash-utility)
    * [3.5 HMAC Utility](#35-hmac-utility)
  * [4. Notification](#4-notification)
    * [4.1 OTP Notification Services](#41-otp-notification-services)
    * [4.2 Email Notification](#42-email-notification)
    * [4.3 SMS Notification](#43-sms-notification)
    * [4.4 PDF Generator](#44-pdf-generator)
    * [4.5 Template Merger](#45-template-merger)
  * [5. Transliteration](#5-transliteration)
  * [6. MOSIP Utils](#6-mosip-utils)
    * [6.1 Mobile Data Validator](#61-mobile-data-validator)
    * [6.2 Email Data Validator](#62-email-data-validator)
    * [6.3 Exception Framework](#63-exception-framework)
    * [6.4 Calendar Utility](#64-calendar-utility)
    * [6.5 Checksum Utility](#65-checksum-utility)
    * [6.6 Date Utility](#66-date-utility)
    * [6.7 File Utility](#67-file-utility)
    * [6.8 Json Utility](#68-json-utility)
    * [6.9 Math Utility](#69-math-utility)
    * [6.10 String Utility](#610-string-utility)
    * [6.11 UUID Utility](#611-uuid-utility)
# Common Services
## 1. OTP manager
## 2. QR Code Generator
## 3. Crypto
### 3.1 Key Generator
### 3.2 Key Management
### 3.3 Crypto Utility 
### 3.4 Hash Utility
### 3.5 HMAC Utility 
## 4. Notification
### 4.1 OTP Notification Services
### 4.2 Email Notification
### 4.3 SMS Notification
### 4.4 PDF Generator
### 4.5 Template Merger
## 5. Transliteration
MOSIP system can be able to facilitate transliteration by integrating with a third party service provider. Receive a request for transliteration with the required input parameters (Word, Input Language Code, and Output Language Code)
1. Validate if all required input parameters have been received as listed below for each specific request
* User Input Word - Mandatory
* Input Language Code - Mandatory
* Output Language Code - Mandatory
2. Transliterate the Word received from Input Language to Output Language
1. In case of Exceptions, system triggers relevant error messages as specified below
## <p align="left">**Type : Error / Failure – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
|TRANSLITERATION_INVALID_ID|Transliteration not possible|KER-TRL-001|
|TRANSLITERATION_INVALID_LANGUAGE_CODE|Language code not supported|KER-TRL-002|
## 6. MOSIP Utils
### 6.1 Mobile Data Validator
MOSIP system, can validate a mobile number based on a defined policy

Upon receiving a request to validate a mobile number against configured mobile number policy, the system validates the mobile number against the policy
1. Validate if all required input parameters have been received as listed below for each specific request
* Mobile number
2. Validate if the mobile no. against the following policies
* Mobile no. should contain no of digits configured by the ADMIN
* Mobile no. should only be numerical.
3. In case of Exceptions, system should trigger relevant error messages. Refer “Messages” section

Respond to the source with the result (Valid/Invalid)

Raise an alert in case of listed exceptions as follows










### 6.2 Email Data Validator
MOSIP system, can validate an Email ID based on a defined policy

Upon receiving a Request to validate an Email ID against the standard Email ID policy, system validate the Email ID against the Standard Email ID format

1. Validate if all required input parameters have been received as listed below for each specific request
* Email ID
2. Validate if the Email ID contains the minimum no. of characters as configured
1. Validate if the Email ID contains less than 254 max length
1. Validate if the Email ID only contains following characters
* Digits 0 to 9
* Uppercase and lowercase English letters (a–z, A–Z)
* Characters ! # $ % & ' * + - / = ? ^ _ ` { | }
* ~ .
5. Validate if the Email ID contains "@" and domain name within the Email ID.
1. Respond to the source with the result (Valid/Invalid)

Raise an alert in case of listed exceptions (Refer “messages” section)

## <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
|Email ID is valid	|Valid	|NA|

## <p align="left">**2. Type : Error/Failure – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
|MosipInvalidEmailException|	Email should not be empty or null|	KER-EMV-001|
|MosipInvalidEmailException|	Email length should be specified number of characters|	KER-EMV-002|
|MosipInvalidEmailException|	Email Domain extension length should be specified number of characters|	KER-EMV-003|
|MosipInvalidEmailException|	Invalid Email ID|	KER-EMV-004|
### 6.3 Exception Framework
### 6.4 Calendar Utility 
### 6.5 Checksum Utility 
### 6.6 Date Utility
### 6.7 File Utility
### 6.8 Json Utility
### 6.9 Math Utility
### 6.10 String Utility
### 6.11 UUID Utility
