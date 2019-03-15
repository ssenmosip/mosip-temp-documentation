## Table Of Content

- [Authentication Services](#authentication-services)
- [1. Single factor Authentication](#1-single-factor-authentication)
  * [1.1 Biometric Authentication](#11-biometric-authentication) _(IDA_FR_1.1)_
  * [1.2 Demographic Authentication](#12-demographic-authentication) _(IDA_FR_1.2)_
  * [1.3 OTP Authentication](#13-otp-authentication) _(IDA_FR_1.3)_
- [2. Multi-factor Authentication](#2-multi-factor-authentication) _(IDA_FR_2)_
- [3. Offline Authentication](#3-offline-authentication)
  * [3.1 QR Code based Authentication](#31-qr-code-based-authentication) _(IDA_FR_3.1)_
- [4. KYC Service](#4-kyc-service)
  * [4.1 Profile Sharing based on Policy](#41-profile-sharing-based-on-policy) _(IDA_FR_4.1)_
- [5. Partners Authentication and Authorisation](#5-partners-authentication-and-authorisation)
    * [5.1 MISP License Authentication](#51-misp-license-authentication) _(IDA_FR_5.1)_
    * [5.2 Partner Policy Authentication](#52-partner-policy-authentication) _(IDA_FR_5.2)_
- [6. Authentication Device Support](#6-authentication-device-support)
  * [6.1 Registered Devices and Open Devices TBD](#61-registered-devices-and-open-devices-tbd) _(IDA_FR_6.1)_

# Authentication Services 
# 1. Single factor Authentication 
## 1.1 Biometric Authentication 
**A. Authenticate the face of the Individual by comparing the match score of the photo against the threshold**

Upon receiving an authentication service request, the system authenticates the face of the Individual by comparing the match score of the photo against the threshold as per the following steps:

1. The authentication service request should have the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio, Bio_Type, pin, otp, session key, HMAC Value, signature, otp, namePri, msPri= E/P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P, mtPri= 1 to 100, addrSec msSec= E/P, mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender, dob, age, langPri, langSec, dCode, mId, Bios (bioType, attriType) and the match score(s)
2. The biometric data is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system retrieves the threshold level configured which is acceptable for a match and then validates if the match score is equal to greater than the threshold level and sets the status as 'Y' for authentication
4. The system then constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err
5. The system also provides id, idType, indication of type of attribute was used for Auth (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, FID, pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, FID, pin, OTP), reqTime, fmrCn, firCn, iirCn, fidCn, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
6. Alerts and warning messages for data type violation are sent as per data definition
7. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**B. MOSIP system can evaluate the Individual's photo match with the corresponding photo in the Auth server**

Upon receiving an authentication request, the system evaluates the Individual's photo match with the corresponding photo in the Auth server as per the following steps:
1. The authentication service request should have the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio, Bio_Type, pin, otp, session key, HMAC Value, signature, otp, namePri, msPri = E /P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P, mtPri= 1 to 100, addrSec msSec= E/P, mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender, dob, age, langPri, langSec, dCode, mId, Bios (bioType, attriType) of the Individual _**(data definition doc as specified below-Provide link)**_
2. The biometric data is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. System validates if the time period between the current time stamp and the request time stamp is <= time period
4. System validates that total number of face record(s) should not exceed 1
5. The faceImg record in the input parameter against the mapped UIN/VID of the resident in the auth database is matched
6. The system then generates a match score based on the level of the match of the face
7. The one is to one mapping is performed by the SDK and match score is provided
8. The system then proceeds to execute compare against face threshold
9. Alerts and warning messages for data type violation are sent as per data definition
10. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**C. Evaluate the Individual's fingerprints with the corresponding fingerprint in the Auth server**

Upon receiving an authentication request, the system evaluates the Individual's fingerprints with the corresponding fingerprint in the Auth server as per the following steps:

1. The authentication service request has the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio, pin, OTP, session key, HMAC Value, signature, namePri, msPri, mtPri, nameSec, msSec, mtSec, dCode, mId, Bios (bioType, attriType). _**(Note: The specifications are detailed in the data definition doc as specified below)provide link**_
2. The biometric is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system then validated the following:
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration)
   * Validates if duplicate fingers are used in input
   * Retrieves configuration for priority between fgerMin and fgerImg. Process only priority 1 based on the configuration - only fgerMin is supported
   * Validates if single fgerMin should not contain more than one finger
   * Validates if total number of fgerMin records should not exceed 2
4. The system then matches fgerMin records in the input parameter against the mapped UIN/VID of the resident in the auth database 
5. The system then generates a match score based on the level of the match of the fingerprints and proceeds to execute compare against fingerprint threshold 
6. Alerts and warning messages for data type violation are sent as per data definition
7. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**D. Authenticate the fingerprints of the Individual by comparing the match score of the fingerprint against the threshold (BioAuthService)**

Upon receiving an authentication request, the system authenticates the fingerprints of the Individual by comparing the match score of the fingerprint against the threshold. The system can integrate with Fingerprint scanner and generate match score as per the following steps:
1. The authentication service request has the following parameters: id, Con, reqTime, txnId, UA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio, pin, OTP, session key, HMAC Value, signature, namePri, msPri, mtPri, nameSec, msSec, mtSec, dCode, mId, Bios (bioType, attriType) and the match score
2. The biometric is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system retrieves the threshold level configured which is acceptable for a match
4. The system then validates the following if the match score is equal to greater than the threshold level
5. The system constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err, actn
6. The system also provides id, idType, indication of type of attribute was used for Auth (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, fgerMin or fgerImg, pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, fgerMin or fgerImg, pin, OTP), reqTime, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
7. Alerts and warning messages for data type violation are sent as per data definition
8. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).


**E. Support two-finger authentication so that the quality of incoming fingerprints is better**

1. The system receives an authentication service request with the parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio, pin, OTP, session key, HMAC Value, signature, namePri, msPri, mtPri, nameSec, msSec, mtSec, dCode, mId, Bios (bioType, attriType). 
2. The biometric is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system validated the following:
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration)
   * Validates if duplicate fingers are used in input if duplicate encoded value is used in the input for fingers - updated logic
   * Validates if single fgerMin record contains more than one finger
   * Validates if total number of fgerMin records exceed 2
4. The system then matches first fgerMin record in the input parameter against the mapped UIN/VID of the resident in the auth database.
5. Generates a match score (using SDK) based on the level of the match of the fgerMin for the first fingerprint
6. Matches second fgerMin record in the input parameter against the mapped UIN/VID of the resident in the auth database.
7. Then generates a match score (using SDK) based on the level of the match of the fgerMin for the second fingerprint
8. Generates a simple composite match score by summing up the match scores of the first and second fingerprint
9. The actor retrieves the composite finger threshold configured which is acceptable for a match
10. The actor validates if the composite match score is equal to greater than the composite finger threshold
11. Constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err, actn
12. The system also provides id, idType, indication of type of attribute was used for Auth (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, fgerMin, pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, fgerMin, pin, OTP), reqTime, API_Version, SHA-256 hash value of UA code, SHA-256 hash value of SA code
13. The system then proceeds to send notifications
14. Alerts and warning messages for data type violation are sent as per data definition
15. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).


**F. Evaluate the Individual's IRIS match with the corresponding IRIS in the Auth server**

Upon receiving an authentication request, the system evaluates the Individual's IRIS match with the corresponding IRIS in the Auth server as per the following steps:

1. The authentication service request has the following parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, pi, ad, fad, bio, Bio_Type, pin, otp, session key, HMAC Value, signature, otp, namePri, msPri= E/P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P, mtPri= 1 to 100, addrSec msSec= E/P, mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender, dob, age, langPri, langSec, dCode, mId, Bios (bioType, attriType) of the Individual _**(Note: The specifications are detailed in the data definition doc as specified below)**_
2. The biometric is sent in [**Base-64 encoded format**](https://en.wikipedia.org/wiki/Base64)
3. The system validated the following:
   * Validates if the time period between the current time stamp and the request time stamp is <= time period (n is an admin configuration)
   * Validates if duplicate irises are used in input based on duplicate encoded value is used in the input for IRIS used in the input.
   * Validates if total number of Iris records should not exceed 2
   * Validates if single irisImg record is present in the input
   * The system matches irisImg record in the input parameter against the mapped UIN/VID of the resident in the auth database.
4. The system then generates a match score based on the level of the match of the Irises. The SDK will provide the match score
5. The system validates if two irisImg records are present in the input
6. The system matches each of the irisImg records in the input parameter against the corresponding records of the mapped UIN/VID of the resident in the auth database and then generates a match score based on the level of the match of the Irises.
7. Match score 1 and Match score 2 are generated for each of the images. The SDK provides the match score
8. The system generates a composite match score by summing up the match scores for the first and the second iris Images
9. The system proceeds to execute compare against Iris threshold
10. Alerts and warning messages for data type violation are sent as per data definition
11. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).


_**G. Authenticate the IRIS of the Individual by comparing the match score of the IRIS against the threshold (TBD)**_


_**H. Composite match score (TBD)**_



## 1.2 Demographic Authentication

**A. Strategy for Authentication**

MOSIP supports only exact match for the demographic authentication of the individual and does not perform any validations related to partial match and phonetics match. No error messages related to partial match and phonetics match are triggered.

**B. Demographic (Address) Authentication**

No weightage is provided to any field\s but exact match strategy is adopted for demographic address

The system receives authentication service request with the parameters: id, Con, reqTime, txnId, UA code, API_Version, UA_Licensekey, SA_license key, idType, Id, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, addrLine1Pri, addrLine2Pri, addrLine3Pri cityPri, statePri,, countryPri, pcPri, msPri = E (Exact), LangPri, addrLine1Sec, addrLine2Sec, addrLine3Sec, citySec, stateSec, countrySec, pcSec, msSec = E (Exact), LangSec. _**Address validate data definition link**_

1. Validate if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system validates if each of the address line items (addrLine1Pri, addrLine2Pri, addrLine3Pri, cityPri, statePri, countryPri, pcPri) in the i/p parameter is same as the address line items (saved in the primary language) against the mapped UIN/VID of the resident in the auth database
3. The system validates if each of the address line items (addrLine1Sec, addrLine2Sec, addrLine3Sec, citySec, stateSec, countrySec, pcSec) in the i/p parameter is same as the address line items (saved in the secondary language) against the mapped UIN/VID of the resident in the auth database
4. Constructs the response to the requesting source with Res (Y/N), txnId (same as request), timestamp_Res of response, error code
5. Provides UIN token, idType, indication of type of attribute was used for Auth (“Id->Name_Primary” or/and “Id->Name_Secondary”, ad->Address line 1, ad->Address line 2, ad->city, ad->state, ad->country, ad->pc etc, fad, Bio, Bio_Type, pin, OTP) and what attribute matched (“Id->namePri” or/and “Id->nameSec”, ad->addrLine1Pri, ad->addrLine2Pri, ad->addrLine3Pri, ad->cityPri, ad->statePri, ad->countryPri, ad->pcPri, ad->addrLine1Sec, ad->addrLine2Sec, ad->addrLine3Sec, ad->citySec, ad->stateSec, ad->countrySec, ad->pcSec, fad, Bio, Bio_Type, pin, OTP), reqTime, API_Version, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
6. The system proceeds to send  Notification -SMS and ‘E-mail’ user stories.
_**Provide link to error msgs.MOS-231**_



**C. Multi-System Authentication**

MOSIP sends a positive response only if all configured parameters match

In case of multi-system authentication, MOSIP responds back with e-KYC data based on alternate preferred business rules, as preferred by an SI. It is feasible for a Country/SI to accommodate business rule to send a positive response if 2 out of 3 systems match, to clear authentication – Without Code change by SI

**D. Verify the Age of the individual so that the individual is authenticated**

The system receives authentication request from TSP with the parameters: id, Con, reqTime, txnId, MUA code, API_Version, MUA_Licensekey, MSA_license key, idType, pi, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, age of the Individual.
_**Please refer Git for more details on the parameters (Provide link)**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system retrieves the DOB of the individual in the auth DB based on the mapped UIN/VID
3. The system calculates the age of the individual based on the DOB.
4. Validates if the Age of the individual is greater than or equal to the Age in the i/p parameter
5. Constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err
6. The system also provides UIN token, idType, indication of type of attribute was used for Auth (“pi->age”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (pi->age, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
7. The system proceeds to execute ‘Notification SMS’ and ‘Notification E-mail’. _**Please refer Git for for details on the type of error messages.**_

**E. Match Name of the individual in the database so that the individual is authenticated**

The system receives authentication service request with the parameters: id, Con, reqTime, txnId, UA code, API_Version, MUA_Licensekey, MSA_license key, idType, id, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, namePri, msPri = P (Partial), mtPri= 1 to 100, nameSec, msSec = P (Partial), mtSec= 1 to 100 _**Link to name data validation**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system compares the namePri in the i/p parameter with the Name saved in the primary language ‘Lang’ in the auth database
3. The system generates the match value
4. Validates if the match valve calculated in step 3 is equal to or above the match threshold_Prim in the input parameter
5. Compares the nameSec in the i/p parameter with the Name saved in the secondary language ‘Lang’ in the auth database
6. The system generates the match value
7. Validates if the match valve calculated in step 7 is equal to or above the match threshold_Second in the input parameter
8. Constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
9. The system also provides UIN token, IdType, indication of type of attribute was used for Auth (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (“pi->namePri” or/and “pi->nameSec”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), ReqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
10. Encoded Data (48 bit rep of Hexadecimal) will be used to indicate type of attribute was used for Auth and type of attribute matched for Auth - To be finalised with Technical team
11. The system proceeds to execute Notification SMS, E-mail. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx)


**F. Match phone number of the individual in the database so that the individual is authenticated**

The system receives authentication request from TSP with the parameters: id, Con, reqTime, txnId, MUA code, API_Version, MUA_Licensekey, MSA_license key, idType, pi, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, phone of the Individual. _**Phone number validation data Git link-Req-223**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system matches the phone number in the input parameter with the phone number of the individual in the auth DB based on the mapped UIN/VID
3. Constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
4. Provides UIN token, idType, indication of type of attribute was used for Auth (“pi->phone”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (pi->phone, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
5. The system proceeds to execute Notification SMS/E-mail _**(Link to be attached)**_


**G. Match e-mail ID of the individual in the database so that the individual is authenticated**

The system receives an authentication request from TSP with the parameters: id, Con, reqTime, txnId, MUA code, API_Version, MUA_Licensekey, MSA_license key, idType, pi, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, email of the Individual.
 _**Please refer Git for more details on the parameters. Email ID data validation**_

1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system matches the e-mail id in the input parameter with the phone no of the individual in the auth DB based on the mapped UIN/VID
3. The system constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
4. The system also provides UIN token, idType, indication of type of attribute was used for Auth (“pi->email”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (pi->email, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
5. The system proceeds to execute Notification -SMS/E-mail. Please refer wiki for to know more about the type error messages based on scenario. _** Link to be attached)**_


**H. Match gender of the individual in the database so that the individual is authenticated**

The system receives authentication request from TSP with the parameters: id, Con, reqTime, txnId, MUA code, ver, MUA_Licensekey, MSA_license key, idType, Id, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, gender of the Individual.
_**Please refer Git for more details on the parameters. Gender data validation**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system matches the Gender in the input parameter with the Gender of the individual in the auth DB based on the mapped UIN/VID
3. The system constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
4. Provides UIN token, idType, indication of type of attribute was used for Auth (“pi->gender”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (pi->gender, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
5. The system proceeds to execute Notification - SMS/E-mail. Please refer wiki for to know more about the type error messages based on scenario. _**Link to be attached)**_

**I. Match DOB of the individual in the database so that the individual is authenticated**

The system receives authentication request from TSP with the parameters: id, Con, reqTime, transaction id, MUA code, API_Version, MUA_Licensekey, MSA_license key, idType, pi, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, dob of the Individual. _**Please refer Git for more details on the parameters.**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system matches the DOB in the input parameter with the dob of the individual in the auth DB based on the mapped UIN/VID
3. Constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
4. The system also provides UIN token, idType, indication of type of attribute was used for Auth (“pi->dob”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (pi->dob, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
5. The system proceeds to execute Notification SMS/E-mail. Please refer wiki for to know more about the type error messages based on scenario. _**Link to be attached)**_


**J. Support country specific address ID attributes for an individual**

**(i) Complete Address and Exact Match**

The system receives authentication service request with the parameters: id, Con, reqTime, txnId, UA code, API_Version, MUA_Licensekey, MSA_license key, idType, Id, ad, fad, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, msPri = E (Exact), langPri, addrSec, msSec = E (Exact), langSec _**Please refer Git for more details on the parameters**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. Validates if the addrPri in the i/p parameter is same as the Address (saved in the primary language) against the mapped UIN/VID of the resident in the auth database
3. Validates if the addrSec in the i/p parameter is same as the Address (saved in the secondary language) against the mapped UIN/VID of the resident in the auth database
4. Constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
5. The system also provides UIN token, idType, indication of type of attribute was used for Auth (“Id->Name_Primary” or/and “Id->Name_Secondary”, fad->addrPri or/and fad->addrSec, etc, fad, Bio, Bio_Type, pin, OTP) and what attribute matched (“Id->Name_Prim” or/and “Id->Name_Second”, fad->addrPri, or/and fad->addrSec, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, API_Version, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
6. The system proceeds to execute Notification SMS/E-mail. Please refer wiki for to know more about the type error messages based on scenario. _**Link to be attached)**_

**(ii) Address as individual line items and Complete Match**

1. The system receives authentication service request with the parameters: id, Con, reqTime, txnId, UA code, API_Version, UA_Licensekey, SA_license key, idType, Id, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, addrLine1Pri, addrLine2Pri, addrLine3Pri loc1Pri, loc2Pri, loc3Pri, pcPri, msPri = E (Exact), LangPri, addrLine1Sec, addrLine2Sec, addrLine3Sec, loc1Sec, loc2Sec, loc3Sec, pcSec, msSec = E (Exact), LangSec
2. Validate if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
3. The system validates if each of the address line items (addrLine1Pri, addrLine2Pri, addrLine3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri) in the i/p parameter is same as the Address line items (saved in the primary language) against the mapped UIN/VID of the resident in the auth database
4. The system validates if each of the address line items (addrLine1Sec, addrLine2Sec, addrLine3Sec, loc1Sec, loc2Sec, loc3Sec, pcSec) in the i/p parameter is same as the Address line items (saved in the secondary language) against the mapped UIN/VID of the resident in the auth database
5. The system constructs the response to the requesting source with Res (Y/N), txnId (same as request), timestamp_Res of response, error code
6. The system also provides UIN token, idType, indication of type of attribute was used for Auth (“Id->Name_Primary” or/and “Id->Name_Secondary”, ad->Address line 1, ad->Address line 2, ad->city, ad->state, ad->country, ad->pc etc, fad, Bio, Bio_Type, pin, OTP) and what attribute matched (“Id->namePri” or/and “Id->nameSec”, ad->addrLine1Pri, ad->addrLine2Pri, ad->addrLine3Pri, ad->loc1Pri, ad->loc2Pri, ad->loc3Pri, ad->pcPri, ad->addrLine1Sec, ad->addrLine2Sec, ad->addrLine3Sec, ad->loc1Sec, ad->loc2Sec, ad->loc3Sec, ad->pcSec, fad, Bio, Bio_Type, pin, OTP), reqTime, API_Version, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
7. The system proceeds to execute ‘Notification SMS’ and ‘Notification E-mail’ user stories. _**(Links to be attached)**_

**K. Match DOB Type for an individual in the Auth database so that an individual can be authenticated**

The system receives authentication request from TSP with the parameters: id, Con, reqTime, transaction id, MUA code, API_Version, MUA_Licensekey, MSA_license key, idType, pi, Ad, FAd, Bio, Bio_Type, pin, OTP, session key, HMAC Value, signature, dobType of the Individual _**Please refer Git for more details on the parameters**_
1. Validates if the time period between the current time stamp and the request time stamp is <= time period (n - admin config)
2. The system matches the DOB Type in the input parameter with the dobType of the individual in the auth DB based on the mapped UIN/VID
3. The system constructs the response to the requesting source with status (Y/N), txnId (same as request), resTimeof response, err
4. The system also provides UIN token, idType, indication of type of attribute was used for Auth (“pi->dobType”, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (pi->dobType, Ad->Address line 1, etc, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver, SHA-256 hash value of MUA code, SHA-256 hash value of MSA code
5. The system proceeds to execute Notification SMS/E-mail. Please refer wiki for to know more about the type error messages based on scenario. _**Link to be attached)**_




  
## 1.3 OTP Authentication 
# 2. Multi-factor Authentication
# 3. Offline Authentication 
## 3.1 QR Code based Authentication 
# 4. KYC Service 
## 4.1 Profile Sharing based on Policy


**A. Respond back to TSP with KYC details, as configured - KycAuth - Add KycFilter, decode authRequest**

Upon receiving a request for authentication from TSP, the system responds back to TSP with KYC details, as configured as per the following steps:

1. The system receives authentication request from TSP with the parameters: reqTime, ver, eCon, rqSec, rqPfr, eAuthType and also the encoded version of Auth request **(Refer MOS-41 for OTP based Authentication request parameters)**
2. Decodes the authentication request and obtain all the input parameters of the auth request
3. Validates eAuthType and compare the data in the PID block in the auth request
4. Validates if the MUA has permission for e-KYC
5. Validates if the mode of authentication in the input for e-KYC is as per the configuration of a permissible mode of authentication for e-KYC for the MUA
6. The system performs all the validation of the OTP Validation process and encodes the auth response
7. Validates the status of the auth response based on auth response and proceed only if the status is successful
8. The system proceeds to construct the e-KYC response element, which is encoded and encrypted.
9. The system then proceeds to execute tokenization
10. Retrieves the configured demVal parameter configured for the country
11. Constructs the response with the fields eResp, demVal, actn, txnId, resTime, err. Out of these elements eResp, txnId, resTime, err will also be available out of the encrypted block for audit purpose of the AUA
12. Validates MUA permissions for e-KYC (if MUA e-KYC permissions = ‘limited KYC’ retrieve the demo fields configured to be part of the response)
13. The system retrieves the PDF template configured for the limited KYC to construct ePri element of the response
14. Retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the limited KYC from the admin config to be part of ePri
15. The system retrieves the configured id fields (from id, masked id, tokenid) for the limited KYC from the admin config to be part of the response
16. The system validates the rqSec flag
17. The system returns masked id, tokenid, namePri, gender, DOB, langPri addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, loc1Sec, loc2Sec, loc3Sec, pcSec, signature as per the validations in step 13, 14 and 15
18. Validates MUA permissions for e-KYC - else (MUA e-KYC permissions = ‘Full KYC')
19. The system retrieves the PDF template configured for the Full KYC to construct ePri element
20. The system retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the full KYC from the admin config to be part of ePri
21. Retrieves the configured id fields (out of id, masked id, tokenid) for the full KYC from the admin config to be part of the response
22. The system also provides id, tokenId, and the retrieved epi and ead demo fields out of namePri, gender, DOB, langPri, addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, citySec, stateSec, countrySec, pcSec, signature, as per the validations in step 15, 19, 20
23. The system then proceeds to execute Notification SMS/E-mail
24. Alerts and warning messages for data type violation are sent as per data definition
25. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**B. Support returns additional e-KYC data to social protection system (TBD)**

MOSIP to provide an additional API to fetch specific data of an individual based on UIN number (evaluate security aspect, as linking of HoF and maintenance of a family relationship will be required as a security imperative) and send to Social Protection Data System

MOSIP to provide a mechanism to record the consent of HoF

This is required to accommodate Household Program of GoM

**C. Integrate Fingerprint Authentication with e-KYC**

Upon receiving an authentication request from TSP with the parameters: reqTime, ver, eCon, rqSec, rqPfr, eAuthType and also the encoded version of Auth request, the system performs the following steps:

1. Decodes the authentication request and obtains all the input parameters of the auth request
2. Validates eAuthType and compare the data in the PID block in the auth request
3. Validates if the MUA has permission for e-KYC
4. Validates if the mode of authentication in the input for e-KYC is as per the configuration of a permissible mode of authentication for e-KYC for the MUA
5. The system performs fingerprint validation as per defined standards and encodes the auth response
6. Validates the status of the auth response based on auth response and proceeds only if the status is successful
7. The system proceeds to construct the e-KYC response element, which will be encoded and encrypted.
8. The proceeds to execute tokenization user story
9. The system then retrieves the configured demVal parameter configured for the country
10. Constructs the response with the fields eResp, demVal, actn, txnId, resTime, err. Out of these elements eResp, txnId, resTime, err will also be available out of the encrypted block for audit purpose of the MUA
11. Validates MUA permissions for e-KYC (if MUA e-KYC permissions = ‘limited KYC’ retrieve the demo fields configured to be part of the response)
12. Retrieves the PDF template configured for the limited KYC to construct ePri element of the response
13. The system retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the limited KYC from the admin config to be part of ePri
14. The actor retrieves the configured id fields (from id, masked id, tokenid) for the limited KYC from the admin config to be part of the response
15. Validates the rqSec flag
16. Returns masked id, tokenid, namePri, gender, DOB, langPri addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, loc1Sec, loc2Sec, loc3Sec, pcSec, signature as per the validations in step 13, 14 and 15
17. Validates MUA permissions for e-KYC - else (MUA e-KYC permissions = ‘Full KYC')
18. Retrieves the PDF template configured for the Full KYC to construct ePri element
19. Retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the full KYC from the admin config to be part of ePri
20. Retrieves the configured id fields (out of id, masked id, tokenid) for the full KYC from the admin config to be part of the response
21. The system also provides id, tokenId, and the retrieved epi and ead demo fields out of namePri, gender, DOB, langPri, addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, citySec, stateSec, countrySec, pcSec, signature, as per the validations in step 15, 19, 20
22. The system then proceeds to execute Notification-SMS/E-mail
23. Alerts and warning messages for data type violation are sent as per data definition
24. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**D. Integrate IRIS Authentication with e-KYC**

Upon receiving an authentication request from TSP with the parameters: reqTime, ver, eCon, rqSec, rqPfr, eAuthType and also the encoded version of Auth request, the system perform the following steps:

1. Decodes the authentication request and obtain all the input parameters of the auth request
2. Validates eAuthType and compares the data in the PID block in the auth request
3. Validates if the MUA has permission for e-KYC
4. Validates if the mode of authentication in the input for e-KYC is as per the configuration of a permissible mode of authentication for e-KYC for the MUA
5. The system performs all the validation of the IRIS Validation Story as per defined standards and encodes the auth response
6. Validate the status of the auth response based on auth response from _**MOS-1154**_ and proceed only if the status is successful
7. The system proceeds to construct the e-KYC response element, which will be encoded and encrypted.
8. The system proceeds to execute tokenization user story
9. Retrieves the configured demVal parameter configured for the country
10. Constructs the response with the fields eResp, demVal, actn, txnId, resTime, err. Out of these elements eResp, txnId, resTime, err will also be available out of the encrypted block for audit purpose of the MUA
11. Validates MUA permissions for e-KYC (if MUA e-KYC permissions = ‘limited KYC’ retrieve the demo fields configured to be part of the response)
12. Retrieves the PDF template configured for the limited KYC to construct ePri element of the response
13. Retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the limited KYC from the admin config to be part of ePri
14. Retrieves the configured id fields (from id, masked id, tokenid) for the limited KYC from the admin config to be part of the response
15. Validates the rqSec flag
16. Returns masked id, tokenid, namePri, gender, DOB, langPri addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, loc1Sec, loc2Sec, loc3Sec, pcSec, signature as per the validations in step 13, 14 and 15
17. Validates MUA permissions for e-KYC - else (MUA e-KYC permissions = ‘Full KYC')
18. Retrieves the PDF template configured for the Full KYC to construct ePri element
19. Retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the full KYC from the admin config to be part of ePri
20. Retrieves the configured id fields (out of id, masked id, tokenid) for the full KYC from the admin config to be part of the response
21. The system also provides id, tokenId, and the retrieved epi and ead demo fields out of namePri, gender, DOB, langPri, addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, citySec, stateSec, countrySec, pcSec, signature, as per the validations in step 15, 19, 20
22. The actor proceeds to execute Notification-SMS/E-mail
23. Alerts and warning messages for data type violation are sent as per data definition
24. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

**E. Integrate static pin authentication with e-KYC**

Upon receiving an authentication request from TSP with the parameters: reqTime, ver, eCon, rqSec, rqPfr, eAuthType and also the encoded version of Auth request, the system performs the following steps:

1. Decodes the authentication request and obtain all the input parameters of the auth request
2. Validates eAuthType and compare the data in the PID block in the auth request
3. Validates if the MUA has permission for e-KYC
4. Validates if the mode of authentication in the input for e-KYC is as per the configuration of a permissible mode of authentication for e-KYC for the MUA
5. The system performs all the validation of the IRIS Validation standards and encodes the auth response
6. Validates the status of the auth response based on auth response and proceeds only if the status is successful
7. The system proceeds to construct the e-KYC response element, which will be encoded and encrypted.
8. Proceeds to execute tokenization user story
9. Retrieves the configured demVal parameter configured for the country
10. Constructs the response with the fields eResp, demVal, actn, txnId, resTime, err. Out of these elements eResp, txnId, resTime, err will also be available out of the encrypted block for audit purpose of the MUA
11. Validates MUA permissions for e-KYC (if MUA e-KYC permissions = ‘limited KYC’ retrieve the demo fields configured to be part of the response)
12. Retrieves the PDF template configured for the limited KYC to construct ePri element of the response
13. Retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the limited KYC from the admin config to be part of ePri
14. Retrieves the configured id fields (from id, masked id, tokenid) for the limited KYC from the admin config to be part of the response
15. Validates the rqSec flag
16. The system then returns masked id, tokenid, namePri, gender, DOB, langPri addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, loc1Sec, loc2Sec, loc3Sec, pcSec, signature as per the validations in step 13, 14 and 15
17. Validates MUA permissions for e-KYC - else (MUA e-KYC permissions = ‘Full KYC')
18. Retrieves the PDF template configured for the Full KYC to construct ePri element
19. Retrieves the configured demographic fields (out of name, address, dob, dob Type, gender, phone no, e-mail) for the full KYC from the admin config to be part of ePri
20. Retrieves the configured id fields (out of id, masked id, tokenid) for the full KYC from the admin config to be part of the response
21. The system also provides id, tokenId, and the retrieved epi and ead demo fields out of namePri, gender, DOB, langPri, addrline1Pri, addrline2Pri, addrline3Pri, loc1Pri, loc2Pri, loc3Pri, pcPri, ePht, ePri, langSec, nameSec, addrline1Sec, addrline2Sec, addrline3Sec, citySec, stateSec, countrySec, pcSec, signature, as per the validations in step 15, 19, 20
22. The system then proceeds to execute Notification -SMS/E-mail
23. Alerts and warning messages for data type violation are sent as per data definition
24. All the error and warning messages are configurable via a configurable file. Please refer Git for more details on the type of [**error messages**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Consolidated%20error%20messages%20V2.1.xlsx).

# 5. Partners Authentication and Authorisation
## 5.1 MISP License Authentication

**Authenticate and authorize the MOSIP Infrastructure Service Provider (MISP)**

MOSIP can authenticate and authorize the MOSIP Infrastructure Service Provider (MISP) as per the following steps listed below:
1. Receives a pin based authentication request with the parameters: id, Con, reqTime, txnId, partnerID, ver, MISP-LK, idType, pi, ad, fad, bio, Bio_Type, pin, otp, pin, session key, HMAC Value, signature, otp, namePri, nameSec, addrPri, addrSec, addrLine1, addrLine2, city, state, country, pc, phone, email, gender, dob, age, langPri, langSec, dCode, mId, Bios (bioType, attriType), pinval of the Individual 
**Please refer [**data definition doc**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Error_Messages_Validate%20MISP%20Partner_MOS-1123_MOS-1129_MOS-1098.docx)
2. Validates if the MISP-LK has not expired
3. Validates if the MISP-LK belongs to a registered MISP (Note: All the MISPs will be registered through MOSIP admin portal and the MISP-LK should belong to one of the registered MISP entities)
4. Validates if the MISP-LK status is active
5. Proceeds to execute e-KYC/Auth partner authentication and authorization as per defined standards
6. Captures and stores the transaction details for audit purpose.
7. Alerts and warning messages for data type violation are sent as per [**definition Link**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Error_Messages_Validate%20MISP%20Partner_MOS-1123_MOS-1129_MOS-1098.docx) _**(Link to be updated)**_
8. The alert and warning messages are configurable via a configurable file.

## 5.2 Partner Policy Authentication

**A. Authenticate and authorize Auth Partner**

The system receives authentication request with the parameters: id, Con, reqTime, txnId, partnerID, ver, MISP-LK, idType, pi, ad, fad, bio, Bio_Type, pin, otp, pin, session key, HMAC Value, signature, otp, namePri, msPri= E/P, mtPri= 1 to 100, nameSec, msSec= E/P, mtSec= 1 to 100, addrPri, addrSec, addrLine1, addrLine2, city, state, country, pc, phone, email, gender, dob, age, langPri, langSec, dCode, mId, Bios (bioType, attriType), pinval of the Individual 
(Note: The specifications are detailed in the [**data definition doc**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Error_Messages_Validate%20MISP%20Partner_MOS-1123_MOS-1129_MOS-1098.docx))

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
11. The system constructs the response to the requesting source with status (Y/N), txnId (same as request), resTime of response, err
12. The system also provides id, idType, indication of what type of attribute was used for Auth (Id, Ad, FAd, Bio, Bio_Type, pin, OTP) and what attribute matched (Id, Ad, FAd, Bio, Bio_Type, pin, OTP), reqTime, ver.
13. The system proceeds to execute Notification SMS
14. _**Alerts and Warning messages for data type violation are sent as per [**data definition**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Error_Messages_Validate%20MISP%20Partner_MOS-1123_MOS-1129_MOS-1098.docx) (Link to be updated)**_
15. The alert and warning messages are configurable via a configurable file.

**B. Authenticate and authorize e-KYC partner - proxy implementation**

The system receives pin based authentication request with the parameters: id, Con, reqTime, txnId, partnerID, ver, MISP-LK, idType, Signature, pi, ad, fad, bio, Bio_Type, pin, otp, pin, session key, HMAC Value, signature, otp, namePri, msPri= E/P, mtPri= 1 to 100, nameSec, msSec = E/P, mtSec= 1 to 100, addrPri, msPri= E/P, mtPri= 1 to 100, addrSec msSec= E/P, mtSec= 1 to 100, addrLine1, addrLine2, city, state, country, pc, phone, email, gender, dob, age, langPri, langSec, dCode, mId, Bios (bioType, attriType), pinval of the Individual (Note: The specifications are detailed in the data definition doc)

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
14. Constructs the response with the fields eResp, demVal, actn, txnId, resTime, err.
15. Validate e-KYC permissions for e-KYC partner as per the e-KYC policies retrieved and identify the demo fields configured to be part of the response
16. Retrieves the configured id fields as per the e-KYC policy and identifies the id fields configured to be part of the response
17. Appends the response with the demographic and id fields as per the policy
18. The system validates the sec_language attribute in the request and appends the response with the demographic fields in language requested.
19. The system proceeds to execute Notification-SMS
20. _**Alerts and Warning messages for data type violation are sent as per [**data definition**](https://github.com/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%209/Error_Messages_Validate%20MISP%20Partner_MOS-1123_MOS-1129_MOS-1098.docx) (Link to be updated)**_
21. The alert and warning messages are configurable via a configurable file.

**C. Support multiple license keys (policies) for a single TSP (Partner) (Feature Roadmap-TBD)**

**License Key Generation**

1. License key generation to be invoked through admin portal with an approval process > Key to be associated to the TSP ID > TSP should have a mechanism to access the key
2. MOSIP should support multiple license keys per TSP. There will be a separate license key per use case/application with associated policy
3. Once a TSP is authorized, they should ideally have a self-service (TSP Portal) mechanism to get their keys and regenerate them on need basis. In the absence of a Self-service portal, it should be possible for the admin to generate the key and email it to the TSP. This can be done as part of the approval process, as well as on an ad hoc basis when the key needs to be replaced

# 6. Authentication Device Support 
## 6.1 Registered Devices and Open Devices TBD 

Technical story (Architects to contribute)



