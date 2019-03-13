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

Upon receiving an authentication service request, the system authenticates the face of the Individual by comparing the match score of the photo against threshold as per the following steps
1. The authentication service request should have  the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio,Bio_Type,pin, otp, session key, HMAC Value,signature, otp, namePri, msPri = E /P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P,mtPri= 1 to 100, addrSec msSec= E/P,mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender,dob,age, langPri, langSec,dCode,mId, Bios(bioType, attriType) and the match score(s) 
2. The biometric data is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system retrieves the threshold level configured which is acceptable for a match and then validates if the match score is equal to greater than the threshold level and sets the status as 'Y' for authentication
4. The system then constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err
5. The system also provides id, idType, indication of type of attribute was used for Auth ( “pi->namePri” or/and “pi->nameSec” , Ad->Address line 1,etc, FAd, FID,pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1,etc, FAd, FID,pin, OTP ), reqTime, fmrCn, firCn, iirCn, fidCn, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
6. Alerts and warning messages for data type violation are sent as per data definition
7. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).


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

