## Table Of Content
- [Resident Services](#resident-services)
  * [1. Track status of UIN Generation by providing Registration ID](#1-track-status-of-uin-generation-by-providing-registration-id) _(RES_FR_1)_
  * [2. Download e-UIN](#3-download-uin) _(RES_FR_2)_
  * [3. Retrieve Lost RID](#11-lockunlock-kyc-docsdata-sharing) _(RES_FR_3)_
  * [4. Retrieve Lost UIN](#4-retrieve-lost-uin---tbd) _(RES_FR_4)_
  * [5. Request re-print of UIN](#11-lockunlock-kyc-docsdata-sharing) _(RES_FR_5)_
  * [6. Initiate UIN Update - Address](#5-initiate-uin-update) _(RES_FR_6)_
  * [7. Track Status of UIN Update](#6-track-status-of-uin-update) _(RES_FR_7)_
  * [8. View History of Authentication Requests (for Prescribed Days/number of requests)](#9-view-history-of-authentication-requests-for-prescribed-daysnumber-of-requests) _(RES_FR_8)_
  * [9. Lock/Unlock UIN for each Authentication Type](#10-lockunlock-uin) _(RES_FR_9)_
  * [10. Generate Virtual ID](#2-generate-virtual-id) _(RES_FR_10)_
    * Virtual ID Types
  * [11. Revoke/In-activate a Virtual ID](#2-generate-virtual-id) _(RES_FR_11)_

# Resident Services
## 1. Track status of UIN Generation by providing Registration ID
In MOSIP, an individual will initiate a request to track the status of UIN Generation based on a RID.

**Procedure to initiate the track status related to UIN generation follows:**
1. Individual provides the RID for which he/she wants to track the status of UIN generation.
2. The system validates the provided RID, checks for the registered mobile number/email ID, and triggers an OTP 
   notification to the individual.
3. The individual provides the OTP as received.
4. The system validates the provided OTP, successfully authenticates the individual, and provides the UIN generation 
   status (Statuses are configurable).
1. During the validation of RID and the mobile number/email ID, if the RID is not found or the mobile number/email ID is 
   not associated with the RID, or the provided OTP is not correct, then the system triggers a respective error 
   notification.




## 2. Generate Virtual ID
## 3. Download UIN
## 4. Retrieve Lost UIN - TBD
## 5. Initiate UIN Update
## 6. Track Status of UIN Update
## 7. Generate Static PIN
## 8. Update Static PIN 
## 9. View History of Authentication Requests (for Prescribed Days/number of requests)
## 10. Lock/Unlock UIN
## 11. Lock/Unlock KYC Docs/Data Sharing 
## 12. Lock/Unlock Biometric Auth/Other Auth
