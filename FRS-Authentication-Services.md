## Table Of Content

- [Authentication Services](#authentication-services)
- [1. Single factor Authentication](#1-single-factor-authentication)
  * [1.1 Biometric Authentication](#11-biometric-authentication) _(IDA_FR_1.1)_
  * [1.2 Demographic Authentication](#12-demographic-authentication) _(IDA_FR_1.2)_
  * [1.3 OTP Authentication](#13-otp-authentication) _(IDA_FR_1.3)_
  * [1.4 Static PIN Authentication](#14-static-pin-authentication) _(IDA_FR_1.4)_
- [2. Multi-factor Authentication](#2-multi-factor-authentication) _(IDA_FR_2)_
- [3. Offline Authentication](#3-offline-authentication)
  * [3.1 QR Code based Authentication](#31-qr-code-based-authentication) _(IDA_FR_3.1)_
- [4. KYC Service](#4-kyc-service)
  * [4.1 Profile Sharing based on Policy](#41-profile-sharing-based-on-policy) _(IDA_FR_4.1)_
- [5. Partners Authentication](#42-authorized-partners-and-authentication)
    * [5.1  MISP License Authentication](#421-misp-licensing) _(IDA_FR_5.1)_
    * [5.2  Partner Policy Authentication ](#422-partner-policy) _(IDA_FR_5.2)_
    * [5.3  MISP Partner Other Authentication](#423-partner-authentication) _(IDA_FR_5.3)_
- [6. Authentication Device Support](#5-authentication-device-support)
  * [6.1 Registered Devices and Open Devices (Architects to contribute)](#51-registered-devices-and-open-devices-architects-to-contribute) _(IDA_FR_6.1)_

# Authentication Services 
# 1. Single factor Authentication 
## 1.1 Biometric Authentication 
**A. Authenticate the face of the Individual by comparing the match score of the photo against threshold**

Upon receiving an authentication service request, the system authenticates the face of the Individual by comparing the match score of the photo against threshold as per the following steps:
1. The authentication service request should have  the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,Bio_Type,pin, otp, session key, HMAC Value,signature, otp, namePri, msPri = E /P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P,mtPri= 1 to 100, addrSec msSec= E/P,mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender,dob,age, langPri, langSec,dCode,mId, Bios(bioType, attriType) and the match score(s) 
2. The biometric data is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system retrieves the threshold level configured which is acceptable for a match and then validates if the match score is equal to greater than the threshold level and sets the status as 'Y' for authentication
4. The system then constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err
5. The system also provides id, idType, indication of type of attribute was used for Auth ( “pi->namePri” or/and “pi->nameSec” , Ad->Address line 1,etc, FAd, FID,pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1,etc, FAd, FID,pin, OTP ), reqTime, fmrCn, firCn, iirCn, fidCn, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
6. Alerts and warning messages for data type violation are sent as per data definition
7. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**B. MOSIP system can evaluate the Individual's photo match with the corresponding photo in the Auth server**

Upon receiving an authentication request, the system evaluates the Individual's photo match with the corresponding photo in the Auth server as per the following steps:
1. The authentication service request should have  the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,Bio_Type,pin, otp, session key, HMAC Value,signature, otp, namePri, msPri = E /P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P,mtPri= 1 to 100, addrSec msSec= E/P,mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender,dob,age, langPri, langSec,dCode,mId, Bios(bioType, attriType) of the Individual (data definition doc as specified below-Provide link)
2. The biometric data is sent in Base-64 encoded format
3. System validates if the time period between the current time stamp and the request time stamp is <= time period 
4. System validates that total number of face record(s) should not exceed 1
5. The faceImg record in the input parameter against the mapped UIN/VID of the resident in the auth database is matched
6. The system then generates a match score based on the level of match of the face
7. The one is to one mapping is performed by the SDK and match score is provided
8. The system then proceeds to execute compare against face threshold 
9. Alerts and warning messages for data type violation are sent as per data definition
10. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of error messages

**C. Evaluate the Individual's fingerprints with the corresponding fingerprint in the Auth server**

Upon receiving a authentication request, the system evaluates the Individual's fingerprints with the corresponding fingerprint in the Auth server as per the following steps:

1. The authentication service request has  the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,pin, OTP, session key, HMAC Value,signature, namePri, msPri , mtPri, nameSec, msSec , mtSec, dCode,mId, Bios(bioType, attriType). (Note: The specifications are detailed in the data definition doc as specified below)provide link
2. The biometric is sent in Base-64 encoded format
3. The system then validated the following
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration)
   * Validates if duplicate fingers are used in input
   * Retrieves configuration for priority between fgerMin and fgerImg . Process only priority 1 based on the configuration - only fgerMin is supported
   * Validates if single fgerMin should not contain more than one finger
   * Validates if total number of fgerMin records should not exceed 2
4. The system then matches fgerMin records in the input parameter against the mapped UIN/VID of the resident in the auth database 
5. The system then generates a match score based on the level of match of the fingerprints and proceeds to execute compare against fingerprint threshold 
6. Alerts and warning messages for data type violation are sent as per data definition
7. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of error messages

**D. Authenticate the fingerprints of the Individual by comparing the match score of the fingerprint against threshold (BioAuthService)**

Upon receiving an authentication request, the system authenticates the fingerprints of the Individual by comparing the match score of the fingerprint against threshold. The system can integrate with Fingerprint scanner and generate match score as per the following steps:
1. The authentication service request has the following parameters: id, Con, reqTime, txnId, UA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,pin, OTP, session key, HMAC Value,signature, namePri, msPri , mtPri, nameSec, msSec , mtSec, dCode,mId, Bios(bioType, attriType) and the match score
2. The biometric is sent in Base-64 encoded format
3. The system retrieves the threshold level configured which is acceptable for a match
4. The system then validates the following if the match score is equal to greater than the threshold level
5. The system constructs the response to the requesting source with status(Y/N), txnId (same as request), resTime of response, err,actn
6. The system also provides id, idType, indication of type of attribute was used for Auth ( “pi->namePri” or/and “pi->nameSec” , Ad->Address line 1,etc, FAd, fgerMin or fgerImg ,pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1,etc, FAd, fgerMin or fgerImg ,pin, OTP ), reqTime, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
7. Alerts and warning messages for data type violation are sent as per data definition
8. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of error messages.


**E. Support two finger authentication so that the quality of incoming fingerprints is better**

1. The system receives an authentication service request with the parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,pin, OTP, session key, HMAC Value,signature, namePri, msPri , mtPri, nameSec, msSec , mtSec, dCode,mId, Bios(bioType, attriType). 
2. The biometric is sent in Base-64 encoded format
3. The system validated the following
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration)
   * Validates if duplicate fingers are used in input if duplicate encoded value is used in the input for fingers - updated logic
   * Validates if single fgerMin record contains more than one finger
   * Validates if total number of fgerMin records exceed 2
4. The system then matches first fgerMin record in the input parameter against the mapped UIN/VID of the resident in the auth database.
5. Generates a match score (using SDK) based on the level of match of the fgerMin for the first fingerprint
6. Matches second fgerMin record in the input parameter against the mapped UIN/VID of the resident in the auth database.
7. Then generates a match score (using SDK) based on the level of match of the fgerMin for the second fingerprint
8. Generates a simple composite match score by summing up the match scores of the first and second fingerprint
9. The actor retrieves the composite finger threshold configured which is acceptable for a match
10. The actor validates if the composite match score is equal to greater than the composite finger threshold
11. Constructs the response to the requesting source with status(Y/N), txnId (same as request), resTime of response, err, actn
12. The system also provides id, idType, indication of type of attribute was used for Auth ( “pi->namePri” or/and “pi->nameSec” , Ad->Address line 1,etc, FAd, fgerMin ,pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1,etc, FAd, fgerMin ,pin, OTP ), reqTime, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
13. The system then  proceeds to send notifications
14. Alerts and Warning messages for data type violation are sent as per data definition
15. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of error messages


**F. Evaluate the Individual's IRIS match with the corresponding IRIS in the Auth server**

Upon receiving an authentication request, the system evaluate the Individual's IRIS match with the corresponding IRIS in the Auth server as per the following steps:

1. The authentication service request has the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,Bio_Type,pin, otp, session key, HMAC Value,signature, otp, namePri, msPri = E /P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P,mtPri= 1 to 100, addrSec msSec= E/P,mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender,dob,age, langPri, langSec,dCode,mId, Bios(bioType, attriType) of the Individual (Note: The specifications are detailed in the data definition doc as specified below)
2. The biometric is sent in Base-64 encoded format
3. The System the following
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration)
   * Validates if duplicate irises are used in input based on duplicate encoded value is used in the input for IRIS used in the input.
   * Validates if total number of Iris records should not exceed 2
   * Validates if single irisImg record is present in the input
   * The system matches irisImg record in the input parameter against the mapped UIN/VID of the resident in the auth database.
3. The system then generates a match score based on the level of match of the Irises. The SDK will provide the match score
4. The system validates if two irisImg records are present in the input
5. The system matches each of the irisImg records in the input parameter against the corresponding records of the mapped UIN/VID of the resident in the auth database and then generates a match score based on the level of match of the Irises. 
6. Match score 1 and Match score 2 are generated for each of the images. The SDK provides the match score
7. The system generates a composite match score by summing up the match scores for the first and the second iris Images}
8. The system proceeds to execute compare against Iris threshold 
9. Alerts and warning messages for data type violation are sent as per data definition
10. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of error messages


**G. Authenticate the IRIS of the Individual by comparing the match score of the IRIS against threshold (TBD)**


**H. Composite match score (TBD)**



## 1.2 Demographic Authentication  
## 1.3 OTP Authentication 
## 1.4 Static PIN Authentication 
# 2. Multi-factor Authentication
# 3. Offline Authentication 
## 3.1 QR Code based Authentication 
# 4. KYC Service 
## 4.1 Profile Sharing based on Policy
# 5 Partners Authentication and Authorisation
## 5.1 MISP License Authentication
## 5.2 Partner Policy Authentication
## 5.3 MISP Partner Other Authentication
# 6. Authentication Device Support 
## 6.1 Registered Devices and Open Devices (Architects to contribute)

