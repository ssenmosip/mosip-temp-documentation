## Table Of Content

- [Authentication Services](#authentication-services)
- [1. Single factor Authentication](#1-single-factor-authentication)
  * [1.1 Biometric Authentication](#11-biometric-authentication-) _(IDA_FR_1.1)_
  * [1.2 Demographic Authentication](#12-demographic-authentication-) _(IDA_FR_1.2)_
  * [1.3 OTP Authentication](#13-otp-authentication-) _(IDA_FR_1.3)_
  * [1.4 Common Features for all Authentication Types](#14-common-features-for-all-authentication-types-) _(IDA_FR_1.4)_
- [2. Multi-factor Authentication (WIP)](#2-multi-factor-authentication-wip-) _(IDA_FR_2)_
- [3. Offline Authentication](#3-offline-authentication)
  * [3.1 QR Code based Authentication (WIP)](#31-qr-code-based-authentication-wip-) _(IDA_FR_3.1)_
- [4. KYC Service](#4-kyc-service)
  * [4.1 Profile Sharing based on Policy](#41-profile-sharing-based-on-policy-) _(IDA_FR_4.1)_
- [5. Partners Authentication and Authorisation](#5-partners-authentication-and-authorisation)
    * [5.1 MISP License Authentication](#51-misp-license-authentication-) _(IDA_FR_5.1)_
    * [5.2 Partner Policy Authentication](#52-partner-policy-authentication-) _(IDA_FR_5.2)_
- [6. Authentication Device Support](#6-authentication-device-support)
  * [6.1 Registered Devices and Open Devices TBD](#61-registered-devices-and-open-devices-tbd-) _(IDA_FR_6.1)_

# Authentication Services 
# 1. Single factor Authentication 
## 1.1 Biometric Authentication [**[↑]**](#table-of-content)
**A. MOSIP system can evaluate the Individual's photo match with the corresponding photo in the Auth server**

Upon receiving an authentication request, the system evaluates the Individual's photo match with the corresponding photo in the Auth server as per the following steps:

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
2. The biometric data is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64)
3. System validates if the time period between the current time stamp and the request time stamp is <= time period. Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
4. System validates that total number of face record(s) should not exceed 1
5. The face record in the input parameter against the mapped UIN/VID of the resident in the auth database is matched. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
6. The system then generates a match score based on the level of the match of the face
7. The one is to one mapping is performed by the SDK and match score is provided
8. The system then proceeds to execute compare against face threshold
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Biometric Authentication API**](ID-Authentication-APIs#authentication-service-public)
for more details.

**B. Authenticate the face of the Individual by comparing the match score of the photo against the threshold**

Upon receiving an authentication service request, the system authenticates the face of the Individual by comparing the match score of the photo against the threshold as per the following steps:

1. The authentication service request should have the following parameters: individualId, individualIdType,consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, demo, bio, Bio_Type, otp, requestSessionKey, requestHMAC, signature,  dCode, mId, Bios (bioType, attriType) and the match score(s)
2. The biometric data is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64).
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
1. The system retrieves the threshold level configured which is acceptable for a match and then validates if the match score is equal to greater than the threshold level and sets the status as 'Y' for authentication
1. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-). 
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

**C. Evaluate the Individual's fingerprints with the corresponding fingerprint in the Auth server** [**[↑]**](#table-of-content)

Upon receiving an authentication request, the system evaluates the Individual's fingerprints with the corresponding fingerprint in the Auth server as per the following steps:

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
2. The biometric is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64).
1. The system then validated the following:
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
   * Validates if duplicate fingers are used in input
   * Validates if total number of finger print records exceed 2
4. The system then matches finger print records in the input parameter against the mapped UIN/VID of the resident in the auth database. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
1. The system then generates a match score based on the level of the match of the fingerprints and proceeds to execute compare against fingerprint threshold 
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).
 
Please refer to the [**Biometric Authentication API**](ID-Authentication-APIs#authentication-service-public)
for more details.

**D. Authenticate the fingerprints of the Individual by comparing the match score of the fingerprint against the threshold (BioAuthService)**

Upon receiving an authentication request, the system authenticates the fingerprints of the Individual by comparing the match score of the fingerprint against the threshold. The system can integrate with Fingerprint scanner and generate match score as per the following steps:
1. The authentication service request has the following parameters: individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio, Bio_Type, otp, requestSessionKey, requestHMAC, signature, dCode, mId, Bios (bioType, attriType) and the match score(s)
2. The biometric is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64).
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
1. The system retrieves the threshold level configured which is acceptable for a match
1. The system then validates the following if the match score is equal to greater than the threshold level
1. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-). 
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).


**E. Support two-finger authentication so that the quality of incoming fingerprints is better** [**[↑]**](#table-of-content)

Upon receiving an authentication request, the system support two-finger authentication so that the quality of incoming fingerprints gets better. Refer to below process:

1. The system receives an authentication service request with the parameters: individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio, Bio_Type, otp, requestSessionKey, requestHMAC, signature, dCode, mId, Bios (bioType, attriType) 
2. The biometric is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64)
3. The system validated the following:
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
   * Validates if duplicate fingers are used in input if duplicate encoded value is used in the input for fingers - updated logic
   * Validates if single fgerMin record contains more than one finger
   * Validates if total number of fgerMin records exceed 2
4. The system then matches first fgerMin record in the input parameter against the mapped UIN/VID of the resident in the auth database. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
5. Generates a match score (using SDK) based on the level of the match of the fgerMin for the first fingerprint
6. Matches second fgerMin record in the input parameter against the mapped UIN/VID of the resident in the auth database. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
7. Then generates a match score (using SDK) based on the level of the match of the fgerMin for the second fingerprint
8. Generates a simple composite match score by summing up the match scores of the first and second fingerprint
9. The actor retrieves the composite finger threshold configured which is acceptable for a match
10. The actor validates if the composite match score is equal to greater than the composite finger threshold
11. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err

1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).


**F. Evaluate the Individual's IRIS match with the corresponding IRIS in the Auth server** [**[↑]**](#table-of-content)

Upon receiving an authentication request, the system evaluates the Individual's IRIS match with the corresponding IRIS in the Auth server as per the following steps:

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
2. The biometric is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64)
3. The system validated the following:
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
   * Validates if duplicate irises are used in input based on duplicate encoded value is used in the input for IRIS used in the input.
   * Validates if total number of Iris records should not exceed 2
   * Validates if single irisImg record is present in the input
   * The system matches irisImg record in the input parameter against the mapped UIN/VID of the resident in the auth database. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
4. The system then generates a match score based on the level of the match of the Irises. The SDK will provide the match score
5. The system validates if two irisImg records are present in the input
6. The system matches each of the irisImg records in the input parameter against the corresponding records of the mapped UIN/VID of the resident in the auth database and then generates a match score based on the level of the match of the Irises. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
7. Match score 1 and Match score 2 are generated for each of the images. The SDK provides the match score
8. The system generates a composite match score by summing up the match scores for the first and the second iris Images
9. The system proceeds to execute compare against Iris threshold
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Biometric Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.


**G. Authenticate the IRIS of the Individual by comparing the match score of the IRIS against the threshold** [**[↑]**](#table-of-content)

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. The system retrieves generated score match
1. The biometric is sent in [**Base-64 encoded format**](//en.wikipedia.org/wiki/Base64).
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
1. The system then validated the following:
   * Validates if single irisImg records are present in the input
   * Retrieves the threshold level configured which is acceptable for a match
   * Validates if the match score is equal to greater than the threshold level
   * Validates if two irisImg records are present in the input
   * Retrieves the composite threshold level configured which is acceptable for a match
   * Validates if the composite match score is equal to greater than the composite threshold
6. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err 
1. The system proceeds to execute compare against Iris threshold
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).  
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
1. Alerts and Warning messages for data type violation are sent as per data definition. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx)

Please refer to the [**Biometric Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.


[**Link to design**](/mosip/mosip/blob/master/docs/design/authentication/Bio_Auth_Request_REST_Service.md)

## 1.2 Demographic Authentication [**[↑]**](#table-of-content)

**A. Strategy for Authentication**

MOSIP supports only exact match for the demographic authentication of the individual and does not perform any validations related to partial match and phonetics match. No error messages related to partial match and phonetics match are triggered.

**B. Demographic (Address) Authentication**

No weightage is provided to any field\s but exact match strategy is adopted for demographic address

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition)
in Git for more details on required parameters.
1. Validate if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
1. The system validates if each of the address line items  in the i/p parameter is same as the address line items against the mapped UIN/VID of the resident in the auth database in the respective language for each address element. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
1. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.


NOTE:

1. The address attributes are generalized as location 1, location 2 and location 3 
1. The SI has to define and map the address specific attributes against addressLine2, addressLine3,  and location specific attributes against location1, location2, location3 of a country. For example: addrLine1 means House No, addrLine2 means Street No, and addrLine3 means Locality; similarly loc1 means Local Administrative Authority, loc2 means Province and loc3 means Region.

Please refer Git for the address based [**Normalization Rules**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%20FIT-4/Address%20Normalization%20BR.docx)



**C. Verify the Age of the individual so that the individual is authenticated**

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
1. The system retrieves the DOB of the individual in the auth DB based on the mapped UIN/VID. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
1. The system calculates the age of the individual based on the DOB.
4. Validates if the Age of the individual is greater than or equal to the Age in the i/p parameter
5. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.

**D. Match Name of the individual in the database so that the individual is authenticated**

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
2. The system compares the name in the i/p parameter with the Name saved in the respective language in the auth database
3. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx)

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.

**E. Match phone number of the individual in the database so that the individual is authenticated** [**[↑]**](#table-of-content)

1. The authentication service request should have a defined set of parameters. Please refer to  [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
2. The system matches the phone number in the input parameter with the phone number of the individual in the auth DB based on the mapped UIN/VID. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
3. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx)

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.



**F. Match e-mail ID of the individual in the database so that the individual is authenticated** [**[↑]**](#table-of-content)

1. The authentication service request should have a defined set of parameters. Please refer to  [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.

1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
2. The system matches the e-mail id in the input parameter with the phone no of the individual in the auth DB based on the mapped UIN/VID. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
3. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.



**G. Match gender of the individual in the database so that the individual is authenticated** [**[↑]**](#table-of-content)

1. The authentication service request should have a defined set of parameters. Please refer to  [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.

1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
2. The system matches the Gender in the input parameter with the Gender of the individual in the auth DB based on the mapped UIN/VID. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
3. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-). 
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.


**H. Match DOB of the individual in the database so that the individual is authenticated**

1. The authentication service request should have a defined set of parameters. Please refer to  [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
2. The system matches the DOB in the input parameter with the dob of the individual in the auth DB based on the mapped UIN/VID. Refer to the features related to [**Map VID to UIN**](#c-map-vid-to-uin-of-the-individual-in-the-auth-database-so-that-the-individual-can-be-authenticated-).
3. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
1. Integrates the response with the static token generated for the authentication request. Refer to features related to generate a [**Static Token**]( #d-generate-a-static-token-id-for-each-mosip-authentication-request-to-facilitate-authentication-).
1. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**Demographic Authentication API**](ID-Authentication-APIs#authentication-service-public) for more details.



[**Link to design**](/mosip/mosip/blob/0.8.0/docs/design/authentication/Demo_Auth_Request_REST_Service.md)


  
## 1.3 OTP Authentication [**[↑]**](#table-of-content)

**A. Trigger OTP to an individual so that the individual can be authenticated based on OTP**

1. The authentication service request should have a defined set of parameters. Please refer to  [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.

1. Validates if the Timestamp of OTP generation request is older than 20 min. Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
2. The system generates the OTP for the request. (Use < product_id >_< encoded token_id >_< txn_id > < MUA Code >logic to generate a unique key for this OTP generation request; The system calls the Core kernel OTP generator component by passing the unique key; The system receives the OTP from the Core kernel component)
3. Retrieves the mode of communication (i.e) e-mail or phone no configured for sending the OTP
4. The system validates if the configured mode of communication is also registered
5. The system triggers OTP to the configured and registered mode of the individual
6. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err, masked mobile and masked e-mail
8. The system proceeds to execute Validate OTP as per the defined standards
9. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**OTP Authentication API**](ID-Authentication-APIs#otp-request-service-public) for more details.


**B. Validate OTP provided by an Individual so that the individual can be authenticated based on OTP**

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. The system validates if the transaction id matches with transaction id value of OTP Generate Request
2. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config). Refer to the features related to [**time stamp validation**](#a-validate-the-timestamp-of-the-authentication-request).
3. Validates if the OTP in the i/p parameter is same as the OTP triggered for the individual to the registered phone number and/or e-mail
4. The system validates the validity of the OTP 
5. Constructs the authentication response based on validation results
6. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
8. The system proceeds to send “Notification SMS” and Notification E-mail. Refer to features related to [**Trigger SMS**](#e-trigger-sms-to-the-individuals-mobile-for-every-authentication-request) and [**Trigger E-mail**](#f-trigger-e-mail-to-the-individuals-e-mail-id-for-every-authentication-request-).
Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**OTP Authentication API**](ID-Authentication-APIs#otp-request-service-public) for more details.

**C. Trigger SMS to the Individual's mobile for OTP Trigger request** [**[↑]**](#table-of-content)

1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
1. The system retrieves the mode of communication (i.e) e-mail or phone no configured for sending the notification
2. Validates if the configured mode of communication is also registered
3. The system fetches the notification template as per admin configuration
4. Triggers notification as per the defined and configured template and in the default language English. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

Please refer to the [**OTP Authentication API**](ID-Authentication-APIs#otp-request-service-public) for more details.


**D. Respond with masked e-mail and masked phone no for OTP trigger request so that the partner can intimate the individual on the mode of communication of the OTP**

The system follows the following steps to include masked e-mail and phone in the info object in the response
1. Retrieves the mode to which OTP will be sent based on the validation for modes 
   * Validates if the configured mode of communication is also registered
   * If the configured mode is also registered
   * Send OTP to the configured and registered mode
   * If the configured mode = e-mail and Registered Mode is Mobile; then
   * Send OTP to Mobile
   * If the configured mode = phone and Registered Mode is e-mail; then
   * Send OTP to e-mail
   * If registered mode is none, then
   * Send error code. 

Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

2. If the communication mode = mobile
3. Mask the mobile no of the individual as per logic below and include the masked mobile in info object of response
4. If the communication mode = e-mail
5. Mask the e-mail of the individual as per the logic below and include the masked e-mail in info object of response
6. If the communication mode = mobile and e-mail
7. Mask both the mobile no and the email as per the logic below and include the both in info object of response
 
**Logic for masking mobile** [**[↑]**](#table-of-content)

1. No of digits in the mobile number to be retrieved – say n
2. Mask first {(50% of the n digits) + 1} digits of the mobile number

Note: 50% in case of decimal means rounded to the greatest whole number

Eg:

Original phone no: 8347899201

Masked phone no: XXXXXX9201

**Logic for masking e-mail**

1. Consider the characters prior to the symbol ‘@’
2. Assign a position to each character
3. Mask every alternate 2 characters starting from position 1

Eg:

```Original e-mail: umamahesh@gmail.com```

```Masked e-mail: XXaXXhXXh@gmail.com```

**E. Trigger e-mail to the Individual's mail-ID for OTP Trigger request**

1. The system receives OTP service request with the parameters: individualId, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, signature and OTP channel
2. The system then retrieves the mode of communication (i.e) e-mail or phone no configured for sending the notification
3. Validates if the configured mode of communication is also registered
4. Fetches the notification template as per admin configuration
5. Triggers notification as per the defined and configured template and in the default language English
6. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

## 1.4 Common Features for all Authentication Types [**[↑]**](#table-of-content)

#### A. Validate the timestamp of the authentication request

The system receives authentication request from partner with the following parameters: individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio,  otp, requestSessionKey, requestHMAC, signature, <bio/demo/otp> attribute of the Individual

The system then validates the following:
1. Validates if the time period between the current time stamp and the request time stamp is <= 20 min
2. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)---> Default value-24 hrs
3. The system proceeds to execute mode of authentication validation as per the defined standards
4. Then triggers error messages as configured.

MOSIP supports standard time for timestamps of authentication requests and responses
1. The timestamp of the Authentication, e-KYC, OTP trigger requests and responses will support IS0-8601 standard.
2. The partners in a country are expected to send the timestamp (reqTime) in the request in UTC with time zone
3. MOSIP returns the timestamp (resTime) in the response in UTC with Time zone

#### B. Locate the UIN of the resident in the Auth database so that the individual can be authenticated

The system receives authentication request from partner with the following parameters:  individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio,  otp, requestSessionKey, requestHMAC, signature, <bio/demo/otp> attribute of the Individual


1. The system matches the input UIN from the individual with the UIN in the auth database (Complete match)

2. The system proceeds match Input UIN from the individual matches with the UIN in the auth database
3. The system proceeds to execute match depending on the parameter using which the individual has to be authenticated.
4. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx). 


#### C. Map VID to UIN of the individual in the Auth database so that the individual can be authenticated [**[↑]**](#table-of-content)

The system receives authentication request from partner with the following parameters: individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio,  otp, requestSessionKey, requestHMAC, signature, <bio/demo/otp> attribute of the Individual

1. The system then validates if the VID is mapped to an UIN in the database and retrieve the UIN
2. The system proceeds to Match UIN as per defined standards
3. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

#### D. Generate a static token ID for each MOSIP authentication request, to facilitate authentication [**[↑]**](#table-of-content)

The system receives authentication service request with the following parameters: 
individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio,  otp, requestSessionKey, requestHMAC, signature, <bio/demo/otp> attribute of the Individual

The system then performs the following steps to generate a static token ID

The system retrieves the parameters relevant for token Id generation

1. Validates if idType = VID is used in the input and retrieves the UIN mapped to the VID (id)
1. Validates if idType = UIN is used in the input and retrieves the UIN (id)
1. The system retrieves the partnerid
1. Generates tokenID based on the retrieved parameters and based on the defined standards
1. The tokenID is unique for a UIN and partnerId combination. The same id should be returned if any auth request is received from the same UIN and partnerId combination
1. The tokenID is generated for every authentication request
1. The length of tokenID is configurable by the ADMIN. The tokenID generated can be of the default length of 36 digits
1. The UIN and partnerid are not be derivable from the tokenId
1. The tokenID is a random number generated
1. The tokenId does not contain any alphanumeric characters and should contain only numeric characters
1. The number does not contain the restricted numbers defined by the ADMIN
1. The generated tokenid is integrated to the authentication response along with other parameters.

Note: The Authentication is integrated for both successful and failure authentications (i.e) in all cases where authentication notifications are triggered.

13. The system then captures and stores the transaction details for audit purpose.

#### E. Trigger SMS to the Individual's mobile for every authentication request


The system receives authentication request from partner with the following parameters:
individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio,  otp, requestSessionKey, requestHMAC, signature, <bio/demo/otp> attribute of the Individual

The system then performs the following steps to Trigger SMS to the Individual's mobile for every authentication request

1. Retrieves the mode of communication (i.e) mobile configured for sending the notification
2. Validates if the configured mode of communication is also registered
3. Validates the response for Auth Type 
4. Fetches the notification template as per admin configuration
5. The system triggers notification as per the defined and configured template and in the default language English
6. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).


#### F. Trigger e-mail to the Individual's e-mail ID for every authentication request [**[↑]**](#table-of-content)

The system receives authentication request from partner with the following parameters: individualId, consentObtained, requestTime, transactionID, Auth-Partner-ID, version, MISP-LicenseKey, individualIdType, demo, bio,  otp, requestSessionKey, requestHMAC, signature, <bio/demo/otp> attribute of the Individual

1. The system retrieves the mode of communication (i.e) e-mail configured for sending the notification
2. The system validates if the configured mode of communication is also registered
3. Validates the response by Auth Type as per the defined standards
4. Fetches the notification template as per admin configuration
5. The system triggers notification as per the defined and configured template and in the default language English
6. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).


[**Link to design**](/mosip/mosip/blob/master/docs/design/authentication/OTP_Request_REST_service.md)

[**Link to design**](/mosip/mosip/blob/0.8.0/docs/design/authentication/Auth_Request_REST_service.md)

# 2. Multi-factor Authentication (WIP) [**[↑]**](#table-of-content)

# 3. Offline Authentication 
## 3.1 QR Code based Authentication (WIP) [**[↑]**](#table-of-content)
# 4. KYC Service 
## 4.1 Profile Sharing based on Policy [**[↑]**](#table-of-content)

**KYC Service is offered based on the individual’s consent using OTP or Biometric (Fingerprint/IRIS/Face) Authentication in the authentication request.**

The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.

The system then validates the following:

1. Validates digital signature in the certificate
2. Validates the certificate
3. Validates if the partnerID belongs to a registered partner
4. Validates if the partner status is active
5. Retrieves the policy constituting for the partnerID
6. Validates if the auth type specified in the request is one of the policies retrieved.
7. Validates if the auth type specified in the request is one of the permissible auth types for e-KYC for the country as per the set configuration
8. Validates if the retrieved policy contains one e-KYC policy (the policy containing demographic attributes to be returned)
9. The system performs all the validation of the "auth" as per standards and encodes the auth response
10. Validate the status of the auth response and proceed only if the status is successful
11. The system proceeds to construct the e-KYC response element, which will be encoded and encrypted.
12. The system integrates the response with the static token generated for the authentication request 
13. Retrieves the configured demVal parameter configured for the country
14. Constructs the response with the fields kycStatus, ttl, actn, transactionID, responseTime, err.
15. Validate e-KYC permissions for e-KYC partner as per the e-KYC policies retrieved and identify the demo fields configured to be part of the response
17. Appends the response with the demographic and id fields as per the policy
18. The system validates the sec_language attribute in the request and appends the response with the demographic fields in language requested.
19. The system proceeds to execute Notification-SMS
20. Alerts and Warning messages for data type violation are sent as per [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition)

Please refer to the [**eKYC API**](ID-Authentication-APIs#ekyc-service-public) for more details.

[**Link to design**](/mosip/mosip/blob/master/docs/design/authentication/eKYC_Auth_Request_REST_service.md)


# 5. Partners Authentication and Authorisation
## 5.1 MISP License Authentication [**[↑]**](#table-of-content)

**Authenticate and authorize the MOSIP Infrastructure Service Provider (MISP)**

MOSIP can authenticate and authorize the MOSIP Infrastructure Service Provider (MISP) as per the following steps listed below:
1. The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.
2. Validates if the MISP-LK has not expired
3. Validates if the MISP-LK belongs to a registered MISP (Note: All the MISPs will be registered through MOSIP admin portal and the MISP-LK should belong to one of the registered MISP entities)
4. Validates if the MISP-LK status is active
5. Proceeds to execute e-KYC/Auth partner authentication and authorization as per defined standards
6. Captures and stores the transaction details for audit purpose.
7. Alerts and warning messages for data type violation are sent as per [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition).

Please refer to the [**Authentication Service API**](ID-Authentication-APIs#users-of-authentication-service--) for more details.


## 5.2 Partner Policy Authentication [**[↑]**](#table-of-content)

**Authenticate and authorize Auth Partner- proxy implementation**

The authentication service request should have a defined set of parameters. Please refer to [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition) in Git for more details on required parameters.

The system then validates the following:
1. Validates the digital signature in the certificate
2. Validates the certificate
3. Validates if the partnerID belongs to a registered partner
4. The system also validates if the partner status is active
5. Retrieves all the policies constituting the partnerID
6. Validates if the auth type specified in the request is one of the policies retrieved for the partner
7. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
8. Validates if the "authvalue" in the i/p parameter is same "authval" stored in the database for the mapped UIN and VID
9. The system constructs the authentication response based on validation results and sets the authentication status as 'Y' only if the pinval matches.
10. The system then integrates the response with the static token generated for the authentication request  
11. The system then constructs the response to the requesting source with status (true/False), transactionID(same as request), responseTime of response, err
13. The system proceeds to execute Notification SMS
14. Alerts and Warning messages for data type violation are sent as per [**data definition**](/mosip/mosip/tree/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Data%20Definition)

Please refer to the [**Authentication Service API**](ID-Authentication-APIs#users-of-authentication-service--) for more details.


# 6. Authentication Device Support 
## 6.1 Registered Devices and Open Devices TBD [**[↑]**](#table-of-content)

Technical story (Architects to contribute)



