## Table Of Content
- [Common Services](#common-services)
  * [1. OTP Manager](#1-otp-manager)
  * [2. QR Code Generator](#2-qr-code-generator)
  * [3. Crypto Services](#3-crypto-services)
    * [3.1 Key Generator](#31-key-generator)
    * [3.2 Key Management](#32-key-management)
    * [3.3 Crypto Utility](#33-crypto-utility)
    * [3.4 Hash Utility](#34-hash-utility)
    * [3.5 HMAC Utility/Checksum Utility](#35-hmac-utilitychecksum-utility)
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
    * [6.5 Date Utility](#65-date-utility)
    * [6.6 File Utility](#66-file-utility)
    * [6.7 Json Utility](#67-json-utility)
    * [6.8 Math Utility](#68-math-utility)
    * [6.9 String Utility](#69-string-utility)
    * [6.10 UUID Utility](#610-uuid-utility)
    * [6.11 Zip-Unzip Utility](#611-zip-unzip-utility)
# Common Services
## 1. OTP Manager
### A. OTP Generation
1. OTP Manager Component handles OTP Generation and OTP Validation


1. For OTP generation, system receives a request to generate an OTP along with a Key in input parameter. 


1. This key can be a Mobile number, Email ID or a combination of Mobile Number and Email ID. 

1. The component will generate an OTP as per the configured length and responds back with to the source with the OTP. OTP manager maps an expiry period with the OTP as configured by the Admin.

### B. OTP Validation
1. For OTP Validation, system receives a request to validate an OTP with a Key and OTP in input parameter. 

1. The component validates the OTP against the expiry and then validates the OTP against the Key if the OTP is not expired. 

1. If the OTP is not expired and is valid against the Key, it will respond with message “Valid” else responds with “Invalid”. 

1. A user will have a maximum configured number of tries to get the OTP wrong after which he/she will be blocked for a configured amount of time. During this blocked period, he/she cannot generate or validate another OTP.


## 2. QR Code Generator
QR code generator takes the content received along with the version number and converts the content into a QR code. The version number is configurable and determines how much data a QR code can store. The more the version number, the more data can be stored in a QR Code.
## 3. Crypto Services
Crypto service encrypt or decrypt data across MOSIP with the help of Public/Private Keys.

#### A. For Encryption
The Crypto Service receives a request from an application with input parameters – Application ID, Reference ID, Timestamp and Data that needs to be encrypted. It calls the Key Generator API for a symmetric key and encrypt data using that symmetric Key. It then calls Key Manager Service and get the public key for the Application ID and Timestamp received in the input parameter. Encrypt the symmetric key using the Public key and joins the Encrypted data and Encrypted Symmetric Key using a Key splitter and respond to the source with the joined data.
#### B. For Decryption
The Crypto Service will receive a request from an application with input parameters – Application ID, Reference ID, Timestamp and Data that needs to be decrypted. 


The Application ID received will be the one, which was sent for encryption of data in the above flow. 


The Crypto Service then splits the received data into Encrypted Content and Encrypted Symmetric Key using the Key Splitter and then calls the Key Manager Service with the Encrypted Symmetric Key, Application ID and Timestamp to decrypt the data using private key.


The Key Manager instead of responding with the private key, decrypts the symmetric itself and send it back to the crypto service. The service then uses this symmetric key to decrypt data and send the decrypted data back to the source.

### 3.1 Key Generator
This component receives a request to generate Symmetric and Asymmetric (Public/Private Keys). It receives a request to generate a Key. It generates and responds with the Key to the source.

### 3.2 Key Management

The Key Manager Service works together with the Crypto Service. 


It receives a request from Crypto Service from Public Key with the Application ID and Timestamp. Key Manager Service then sends a valid Public key against the application ID received to Crypto Service. In case, the public key is expired against that Application ID, it will generate a new Public Key and respond with it.


For a request to receive private key, The Key manager will not respond with Private Key but instead takes the encrypted data from the source and decrypts it itself and responds with decrypted content

### 3.3 Crypto Utility 

The crypto utility is used to perform encryption and decryption 

#### A. Encryption

1. On receiving a  request to encrypt data with input parameters (Application ID, Reference ID, Timestamp, data) the system gets the public key by calling the Key Manager Webservice with the input parameters received in the request (Application ID, Reference ID, Timestamp, data)
1. Get the Public key in response from the Key Manager Webservice.
1. Generates the Symmetric Key by using the Symmetric Key generator API.
1. Encrypts the data received in the request with the Symmetric key using the Cryptography JAVA API.
1. Encrypts the symmetric key received using the public key using the Cryptography JAVA API.
1. Combines the Encrypted data and Encrypted Symmetric Key using Crypto Utility
1. Responds to the source with the Encrypted data and Encrypted Symmetric key combined in a Byte array.

#### B. Decryption

1. On receiving  a request to decrypt data with input parameters (Application ID, Reference ID, Timestamp, Encrypted Byte array) the system Extracts the encrypted Data and Encrypted public key from the Byte Array received using Crypto Utility
1. Decrypts the encrypted symmetric received in the request using the Key Management WebService.
1. Decrypts the encrypted data with the decrypted symmetric using Cryptography JAVA API.
1. Responds to the source with the Encrypted data and Encrypted Symmetric key combined in a Byte array.

### 3.4 Hash Utility
1. Identifies hash util methods
1. Creates wrapper class for methods defined in apache-commons hash util
1. Raises an alert in case of listed
### 3.5 HMAC Utility/Checksum Utility

A HMAC/checksum function is a way to create a compact representation of an arbitrarily large amount of data 

## 4. Notification
### 4.1 OTP Notification Services
OTP Notification Service is a combined service, which receives a request to generate an OTP and responds directly to the User using SMS or Email Notification. 


The service receives a request to generate and send OTP with Notification Type (SMS and/or Email), Template (SMS and/or Email) and Mobile Number (SMS and/or Email). It then calls OTP Generator Service to generate an OTP against a Key (Mobile Number or Email). Its calls the Template Merger Service to merge OTP with the Template (SMS and/or Email). It will then call SMS and/or Email Notification Service to send the notification as per the template. The choice of sending SMS and/or Email will depend on the Notification Type Flag received in Input.

### 4.2 Email Notification
This service triggers an Email Notification upon receiving a request to trigger notification with Recipient Email-ID, CC Recipients Email-IDs, Subject, Email Content, and Attachment as input parameter. The restriction on Attachment and its size is configurable. The Third-Party Email Vendor is configurable and any country specific vendor can be used.

### 4.3 SMS Notification

This service triggers an SMS Notification upon receiving a request to trigger notification with Phone Number and Content as input parameter. The third-party SMS Vendor is configurable and any country specific vendor can be used.

### 4.4 PDF Generator
This utility enables created of PDF from the content received. It will receive a content in input parameter, convert it into a PDF document, and respond with it to the source.

### 4.5 Template Merger
This utility merges a Template with Placeholders with the dynamic values to form the content to be sent as Notifications or Acknowledgement. The Utility will receive a template and dynamic values from a source. It will merge the values and template and respond with the processed content.
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

## <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
|Mobile no is valid	|"Valid"	|NA|

## <p align="left">**2. Type : Error/Failure – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
|MosipInvalidPhoneNumberException|Phone number should not be empty or null|KER-MOV-001|
|MosipInvalidPhoneNumberException|Phone length should be specified number of digits|KER-MOV-002|
|MosipInvalidPhoneNumberException|Phone number should not contain any special characters except specified|KER-MOV-003|
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
MOSIP system provides base exception framework.
### 6.4 Calendar Utility 
1. Identifies Calendar util methods
1. Creates wrapper class for methods defined in apache-commons Calendar util
1. Raises an alert in case of listed exceptions 

### 6.5 Date Utility
1. Identifies File util methods
1. Creates wrapper class for methods defined in apache-commons date and time util
1. Raises an alert in case of listed exceptions 
### 6.6 File Utility
1. Identifies File util methods
1. Creates wrapper class for methods defined in apache-commons File util
1. Raises an alert in case of listed exceptions 
### 6.7 Json Utility
1. Identifies jason util methods
1. Creates wrapper class for methods defined in apache-commons jason util
1. Raises an alert in case of listed exceptions 
### 6.8 Math Utility
1. Identifies Math util methods
1. Creates wrapper class for methods defined in apache-commons Math util
1. Raises an alert in case of listed exceptions 
### 6.9 String Utility
1. Identifies String util methods
1. Creates wrapper class for methods defined in apache-commons String util
1. Raises an alert in case of listed exceptions
### 6.10 UUID Utility
1. Upon receiving a request to generate UUID the system generates UUID as per default UUID generation logic
1. UUID generated should be as per UUID Version 5
1. UUID generated should be of 36 characters (32 alphanumeric characters and four hyphens e.g. 123e4567-e89b-12d3-a456-426655440000)
1. Any application in MOSIP can use this UUID utility
1. Responds with the UUID to the source
1. Raises an alert in case of listed exceptions
### 6.11 Zip-Unzip Utility
1. Identifies Zip-Unzip util methods
1. Creates wrapper class for methods defined in apache-commons Zip-Unzip util
1. Raises an alert in case of listed exceptions