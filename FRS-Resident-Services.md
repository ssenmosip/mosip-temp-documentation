## Table Of Content
* [Resident Services](#resident-services)
  * [1. Track Status of UIN Generation by providing Registration ID](#1-track-status-of-uin-generation-by-providing-registration-id-) _(RES_FR_1)_
  * [2. Download UIN](#2-download-uin-) _(RES_FR_2)_
  * [3. Retrieve Lost RID](#3-retrieve-lost-rid-) _(RES_FR_3)_
  * [4. Retrieve Lost UIN](#4-retrieve-lost-uin-) _(RES_FR_4)_
  * [5. Re-print Request of UIN](#5-re-print-request-of-uin-) _(RES_FR_5)_
  * [6. Initiate UIN Update](#6-initiate-uin-update-) _(RES_FR_6)_
  * [7. Track Status of UIN Update](#7-track-status-of-uin-update-) _(RES_FR_7)_
  * [8. View History of Authentication Requests (for Prescribed Days/number of requests)](#8-view-history-of-authentication-requests-for-prescribed-daysnumber-of-requests-) _(RES_FR_8)_
  * [9. Lock/Unlock UIN](#9-lockunlock-uin-) _(RES_FR_9)_
  * [10. OTP Authentication](#10-otp-authentication-) _(RES_FR_10)_


# Resident Services
## 1. Track status of UIN Generation by providing Registration ID [**[↑]**](#table-of-content)

An individual can track the stats of UIN generation by providing a Registration ID(RID). The system validates the provided RID and the mobile number/email ID associated with it and sends an OTP notifications if successfully validated. Individual provides the OTP as received; the system authenticates the individual and sends the status of UIN generation through OTP notification (UIN statuses are configurable). Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more details. During the validation of RID and mobile number/email ID, if the RID is not found or the mobile number/email ID is not associated with the RID, or the provided OTP is not correct, then the system triggers an error message.
## 2. Download UIN [**[↑]**](#table-of-content)

An individual raises a request to download his/her e-UIN by providing the UIN/VID, full name, postal code, and security code.The system validates the provided data, checks for the registered mobile number/email ID, and triggers an OTP notification.The Individual provides the OTP as received.The system validates the provided OTP and successfully authenticates the individual. Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more detailss. The system will generate the password protected (Password is configurable) e-UIN and sends a notification.During the validation of UIN/VID, Full Name, Postal Code, and Security Code and the mobile number/email ID, if the provided data are not found or the mobile number/email ID is not associated with the UIN/VID or the provided OTP is not correct, then the system triggers an error message.

## 3. Retrieve Lost RID [**[↑]**](#table-of-content)

An individual can retrieve the RID by providing the Full Name, Mobile Number/E-Mail ID, Postal Code. The system validates the provided data, checks for the registered mobile number/email ID and triggers an OTP notification. The individual provides the OTP as received. The system validates the provided OTP and successfully authenticates the individual. Please refer to the OTP Authentication for more details. The system generates the password protected (Password is configurable) RID and provides the RID to the individual and sends a notification. During the validation of Full Name, mobile number/email ID, and postal code, if the full name, mobile number/email ID and postal code are not associated with the RID or the provided OTP is not correct, then the system triggers an error notification.

## 4. Retrieve Lost UIN [**[↑]**](#table-of-content)

MOSIP allows an individual to initiate a request to retrieve the Registration ID by providing the Full Name, Mobile Number/E-Mail ID, Postal Code. The system validates the provided data, checks for the registered mobile number/email ID, and triggers an OTP notification. The individual provides the OTP as received. The system validates the provided OTP and successfully authenticates the individual. Please refer to the OTP Authentication for more details. The system generates the password protected (Password is configurable) Registration ID and sends Registration ID to the individual along with notification. During the validation of Full Name, mobile number/email ID, and postal code, if the full name, mobile number/email ID and postal code are not associated with the Registration ID or the provided OTP is not correct, then the system triggers a respective error notification.

## 5. Re-print Request of UIN [**[↑]**](#table-of-content)

MOSIP allows an individual to raise a reprint request for their UIN. The individual provides the UIN/VID for which he/she wants to reprint. The system validates the UIN/VID and checks for the registered mobile number/email ID and triggers OTP notification. The individual provides the OTP as received. The system validates the provided OTP and successfully authenticates the individual. Please refer to the OTP Authentication for more details. The system will provide the UIN to the registration processor to process the reprint request. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email, ID is not associated with the UIN/VID or the provided OTP is not correct, then the system triggers an error notification.

## 6. Initiate UIN Update [**[↑]**](#table-of-content)
MOSIP allows an individual to process a request to update the demographic data of the UIN.

The procedure for an individual to update the demographic data follows:

1. An individual provides the UIN/VID for which he/she wants to update.
1. The system validates the provided UIN/VID, checks for the registered mobile number/email ID associated with and 
triggers an OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual. Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more details.
1. The system allows the individual to update the respective demographic data.
1. The individual provides the supporting documents related to the details, which are being updated. 
1. The system provides an acknowledgement notification. 
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID or the provided OTP is not correct, and then the system triggers a respective error notification.
9. Status of an update request can further be tracked by an individual. Please refer to the
   [**Track Status of UIN Update**](#7-track-status-of-uin-update-) for more details.


## 7. Track Status of UIN Update [**[↑]**](#table-of-content)
In MOSIP, an individual will raise a request to track the status related to UIN updates based on a registration ID.

Following procedure to be followed by the individual to track the status of UIN updates:
1. An individual provides the Registration ID for which he/she wants to track the status of UIN updates.
1. The system validates the provided Registration ID, checks for the registered mobile number/email ID, and triggers an 
   OTP notification to the individual.
1. The individual provides the OTP as received.
1. The system validates the provided OTP, successfully authenticates the individual, and provides the UIN updating status 
   (Update statuses are configurable). Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more details.
1. During the validation of Registration ID and the mobile number/email ID, if the Registration ID is not found or the 
   mobile number/email ID is not associated with the Registration ID, or the provided OTP is not correct, then the system 
   triggers a respective error notification.
## 8. View History of Authentication Requests (for Prescribed Days/number of requests) [**[↑]**](#table-of-content)
In MOSIP, an individual will raise a request to view authentication- requests history for a specific UIN/VID. The system will fetch for past 6 months record from current date or maximum 50 transactions (configurable). 

Procedure to raise request to view the authentication history of the past:

1. An individual provides the UIN/VID and security code which he/she wants to view.
1. The system validates the provided UIN/VID and security code; checks for the registered mobile number/email ID, and 
   triggers an OTP notification to the individual.
1. The individual provides the OTP as received.
1. The system validates the provided OTP, successfully authenticates the individual. Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more details.
1. The system provides the history of authentication for all the authentication modalities.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID, or the provided OTP is not correct, then the system triggers a respective error notification.

## 9. Lock/Unlock UIN [**[↑]**](#table-of-content)

### A. Lock the UIN

MOSIP allows an individual to lock the authentication type(s) (Demographic, Biometrics (FP/Iris/Face/All)) associated with the UIN/VID. Only the locked authentication type(s) cannot be used for any authentication purpose.

The following procedure to be followed by an individual to lock the authentication type(s):
1. An individual provides the UIN/VID for which he/she wants to lock the authentication type(s).
1. The system validates the UIN/VID, checks for the registered mobile number/email ID, and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual. Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more details.
1. The system provides the individual with lock information related to authentication type(s).
1. The individual will lock the authentication type(s), which he/she wishes.
1. The system will disable the authentication type(s) as provided by the individual.
1. The system will also trigger a confirmation notification on successful locking.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID, or the provided OTP is not correct, then the system triggers a respective error notification.

### B. Unlock the UIN

MOSIP allows an individual to unlock the authentication type(s) (Demographic, Biometrics (FP/Iris/Face/All)) associated with the UIN/VID. Only the unlocked authentication type(s) of demographic and biometric (FP/Iris/Face/All) can be used for any required authentication purpose.

The following procedure to be followed by an individual to unlock the authentication type(s):

1. An individual provides the UIN/VID for which he/she wants to unlock the authentication type(s).
1. The system validates the UIN/VID and checks for the registered mobile number/email ID and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual. Please refer to the [**OTP Authentication**](#10-otp-authentication-) for more details.
1. The system provides the individual with unlock information related to authentication type(s).
1. The individual will unlock the authentication type(s), which he/she requires.
1. The system will enable the authentication type(s) as provided by the individual.
1. The system will also trigger a confirmation notification on successful unlocking.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID, or the provided OTP is not correct, then the system triggers a respective error notification.

## 10. OTP Authentication [**[↑]**](#table-of-content)
At the time of registration, if a mobile number is registered with more than X number (X number is configurable based on policy of a country) of UIN/VID, then the system considers OTP as weak OTP authentication at the time of OTP authentication and does not initiate any further process. System provides the notification to the respective individual to visit the registration center.

