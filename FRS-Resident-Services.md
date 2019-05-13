## Table Of Content
* [Resident Services](#resident-services)
  * [1. Track status of UIN Generation by providing Registration ID](#1-track-status-of-uin-generation-by-providing-registration-id-) _(RES_FR_1)_
  * [2. Download UIN](#2-download-uin-) _(RES_FR_2)_
  * [3. Retrieve Lost UIN - TBD](#3-retrieve-lost-uin---tbd-) _(RES_FR_3)_
  * [4. Re-print Request of UIN](#4-re-print-request-of-uin-) _(RES_FR_4)_
  * [5. Initiate UIN Update](#5-initiate-uin-update-) _(RES_FR_5)_
  * [6. Track Status of UIN Update](#6-track-status-of-uin-update-) _(RES_FR_6)_
  * [7. Generate Static PIN (WIP)](#7-generate-static-pin-wip-) _(RES_FR_7)_
  * [8. Update Static PIN (WIP)](#8-update-static-pin-wip-) _(RES_FR_8)_
  * [9. View History of Authentication Requests (for Prescribed Days/number of requests)](#9-view-history-of-authentication-requests-for-prescribed-daysnumber-of-requests-) _(RES_FR_9)_
  * [10. Lock/Unlock UIN](#10-lockunlock-uin-) _(RES_FR_10)_
  * [11. Lock/Unlock KYC Docs/Data Sharing (WIP)](#11-lockunlock-kyc-docsdata-sharing-wip-) _(RES_FR_11)_
  * [12. Lock/Unlock Biometric Auth/Other Auth (WIP)](#12-lockunlock-biometric-authother-auth-wip-) _(RES_FR_12)_

# Resident Services
## 1. Track status of UIN Generation by providing Registration ID [**[↑]**](#table-of-content)
In MOSIP, an individual will initiate a request to track the status of UIN Generation based on an Registration ID.

An individual will execute the following procedure to initiate the track status request related to UIN generation:

1. An individual provides the Registration ID for which he/she wants to track the status of UIN generation.
1. The system validates the provided Registration ID, checks for the registered mobile number/email ID, and triggers an OTP notification to the individual.
1. The individual provides the OTP as received.
1. The system validates the provided OTP, successfully authenticates the individual, and provides the UIN generation status (Statuses are configurable).
1. During the validation of Registration ID and the mobile number/email ID, if the Registration ID is not found or the mobile number/email ID is not associated with the Registration ID, or the provided OTP is not correct, then the system triggers a respective error notification.
## 2. Download UIN [**[↑]**](#table-of-content)
The system allows an individual to raise a request to download their e-UIN.

The following procedures to be followed by an individual to raise an e-UIN download request:

1. An individual provides the UIN/VID, Full Name, Postal Code, and Security Code.
1. The system validates the provided data, checks for the registered mobile number/email ID, and triggers an OTP notification.
1. The Individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual.
1. The system will generate the password protected (Password is configurable) e-UIN and successfully provides a notification.
1. During the validation of UIN/VID, Full Name, Postal Code, and Security Code and the mobile number/email ID, if the provided data are not found or the mobile number/email ID is not associated with the UIN/VID or the provided OTP is not correct, then the system triggers a respective error notification.

## 3. Retrieve Lost UIN - TBD [**[↑]**](#table-of-content)

MOSIP allows an individual to initiate a request to retrieve the Registration ID.

An individual will follow the following procedure to raise a requested related to retrieve the Registration ID: 

1. An individual provides the Full Name, Mobile Number/E-Mail ID, Postal Code.
1. The system validates the provided data, checks for the registered mobile number/email ID, and triggers an OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual.
1. The system generates the password protected (Password is configurable) Registration ID and provides the Registration ID to the individual along with notification.
1. During the validation of Full Name, mobile number/email ID, and postal code, if the full name, mobile number/email ID and postal code are not associated with the Registration ID or the provided OTP is not correct, then the system triggers a respective error notification.
## 4. Re-print Request of UIN [**[↑]**](#table-of-content)
MOSIP allows an individual to raise a reprint request for their UIN.
An individual will follow the following procedure to raise a reprint request: 
1. The individual provides the UIN/VID for which he/she wants to reprint.
1. The system validates the UIN/VID and checks for the registered mobile number/email ID and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual.
1. The system will provide the UIN to the registration processor to process the reprint request.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email, ID is not associated with the UIN/VID or the provided OTP is not correct, then the system triggers a respective error notification.

## 5. Initiate UIN Update [**[↑]**](#table-of-content)
MOSIP allows an individual to process a request to update the UIN.

The procedure for an individual to initiate a request related to UIN updates follows:

1. An individual provides the UIN/VID for which he/she wants to update.
1. The system validates the provided UIN/VID, checks for the registered mobile number/email ID associated with and 
triggers an OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual.
1. The system allows the individual to update the respective demographic data.
1. The individual provides the supporting documents related to the details, which are being updated. 
1. The system provides an acknowledgement notification. 
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the UIN/VID or the provided OTP is not correct, and then the system triggers a respective error notification.

## 6. Track Status of UIN Update [**[↑]**](#table-of-content)
In MOSIP, an individual will raise a request to track the status related to UIN updates based on a registration ID.

Following procedure to be followed by the individual to track the status of UIN updates:
1. An individual provides the Registration ID for which he/she wants to track the status of UIN updates.
1. The system validates the provided Registration ID, checks for the registered mobile number/email ID, and triggers an OTP notification to the individual.
1. The individual provides the OTP as received.
1. The system validates the provided OTP, successfully authenticates the individual, and provides the UIN updating status (Update statuses are configurable).
1. During the validation of Registration ID and the mobile number/email ID, if the Registration ID is not found or the mobile number/email ID is not associated with the Registration ID, or the provided OTP is not correct, then the system triggers a respective error notification.

## 7. Generate Static PIN (WIP) [**[↑]**](#table-of-content)
## 8. Update Static PIN (WIP) [**[↑]**](#table-of-content)
## 9. View History of Authentication Requests (for Prescribed Days/number of requests) [**[↑]**](#table-of-content)
In MOSIP, an individual will raise a request to view authentication- requests history for a specific UIN/VID. The system will fetch for past 6 months record from current date or maximum 50 transactions (configurable). 

Procedure to raise request to view the authentication history of the past:

1. An individual provides the UIN/VID and security code which he/she wants to view.
1. The system validates the provided UIN/VID and security code; checks for the registered mobile number/email ID, and triggers an OTP notification to the individual.
1. The individual provides the OTP as received.
1. The system validates the provided OTP, successfully authenticates the individual
1. The system provides the history of authentication for all the authentication modalities.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the UIN/VID, or the provided OTP is not correct, then the system triggers a respective error notification.

## 10. Lock/Unlock UIN [**[↑]**](#table-of-content)

### A. Lock the UIN

MOSIP allows an individual to lock the authentication type(s) (Demographic, Biometrics (FP/Iris/Face/All)) associated with the UIN/VID.

The following procedure to be followed by an individual to lock the authentication type(s):
1. An individual provides the UIN/VID for which he/she wants to lock the authentication type(s).
1. The system validates the UIN/VID, checks for the registered mobile number/email ID, and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual.
1. The system provides the individual with lock information related to authentication type(s).
1. The individual will lock the authentication type(s), which he/she wishes.
1. The system will disable the authentication type(s) as provided by the individual.
1. The system will also trigger a confirmation notification on successful locking.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the UIN/VID, or the provided OTP is not correct, then the system triggers a respective error notification.

### B. Unlock the UIN

MOSIP allows an individual to unlock the authentication type(s) (Demographic, Biometrics (FP/Iris/Face/All)) associated with the UIN/VID.

The following procedure to be followed by an individual to unlock the authentication type(s):

1. An individual provides the UIN/VID for which he/she wants to unlock the authentication type(s).
1. The system validates the UIN/VID and checks for the registered mobile number/email ID and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and successfully authenticates the individual.
1. The system provides the individual with unlock information related to authentication type(s).
1. The individual will unlock the authentication type(s), which he/she requires.
1. The system will enable the authentication type(s) as provided by the individual.
1. The system will also trigger a confirmation notification on successful unlocking.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the UIN/VID, or the provided OTP is not correct, then the system triggers a respective error notification.

## 11. Lock/Unlock KYC Docs/Data Sharing (WIP) [**[↑]**](#table-of-content)
## 12. Lock/Unlock Biometric Auth/Other Auth (WIP) [**[↑]**](#table-of-content)
