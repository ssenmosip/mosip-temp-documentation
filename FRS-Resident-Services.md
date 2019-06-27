## Table Of Content
* [1. Overview](#1-overview-)
* [2. Features](#2-features-)
  * [2.1 Track Status of UIN Generation by providing Registration ID](#21-track-status-of-uin-generation-by-providing-registration-id-) _(RES_FR_1)_
  * [2.2 Download e-UIN](#22-download-e-uin-) _(RES_FR_2)_
  * [2.3 Retrieve Lost RID](#23-retrieve-lost-rid-) _(RES_FR_3)_
  * [2.4 Retrieve Lost UIN](#24-retrieve-lost-uin-) _(RES_FR_4)_
  * [2.5 Re-print Request of UIN](#25-re-print-request-of-uin-) _(RES_FR_5)_
  * [2.6 Initiate UIN Update](#26-initiate-uin-update-) _(RES_FR_6)_
  * [2.7 Track Status of UIN Update](#27-track-status-of-uin-update-) _(RES_FR_7)_
  * [2.8 View History of Authentication Requests (for Prescribed Days/number of requests)](#28-view-history-of-authentication-requests-for-prescribed-daysnumber-of-requests-) _(RES_FR_8)_
  * [2.9 Lock/Unlock UIN](#29-lockunlock-uin-) _(RES_FR_9)_
  * [2.10 VID Service](#210-vid-service-)
    * [2.10.1 Generate a VID](#2101-generate-a-vid-) _(RES_FR_10.1)_
    * [2.10.2 Maintain the Status of a VID (WIP)](#2102-maintain-the-status-of-a-vid-wip-) _(RES_FR_10.2)_
    * [2.10.3 Regenerate a VID (WIP)](#2103-regenerate-a-vid-wip) _(RES_FR_10.3)_
    * [2.10.4 Revoke a VID](#2104-revoke-a-vid-) _(RES_FR_10.4)_
    * [2.10.5 Auto-restore a VID on Revocation and with Auto-restore Policy (WIP)](#2105-auto-restore-a-vid-on-revocation-and-with-auto-restore-policy-wip-) _(RES_FR_10.5)_
    * [2.10.6 Retrieve the UIN Corresponding to a VID (WIP)](#2106-retrieve-the-uin-corresponding-to-a-vid-wip-) _(RES_FR_10.6)_
* [Process View (WIP)](#process-view-wip-)

# 1. Overview [**[↑]**](#table-of-content)

The Resident Service module will provide a host of services to users who can avail these services after the creation of their Unique Identity Number (UIN). The list of services are as follows:
 * Update of Demographic Data (UIN update)
 * Track Request Status
 * Lock/unlock AUTH types
 * Download e-UIN
 * Retrieve Lost Registration ID(RID)/UIN
 * Reprint UIN
 * View Authentication Transaction History
 * Generate/revoke Virtual ID (VID).

All these features are detailed in the following features section.
  
# 2. Features [**[↑]**](#table-of-content)
## 2.1 Track status of UIN Generation by providing Registration ID [**[↑]**](#table-of-content)

This feature will allow a user to track status of his/her UIN generation. The user needs to provide the RID  as input. The system will first validate the user's provided RID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of UIN generation to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.2 Download e-UIN [**[↑]**](#table-of-content)

This feature will allow a user to download his/her electronic UIN. The user needs to provide the UIN/VID, full name, postal code, and security code as input. The system will validate the provided data, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send a password protected link of the pdf for download of e-UIN to the user's registered mobile number and email ID. The system will also trigger a successful notification message  to the user's registered mobile number/email id after the transaction or appropriate error message if the transaction was not successful.

## 2.3 Retrieve Lost RID [**[↑]**](#table-of-content)
After the UIN application is submitted by a user providing the required demographic, biometrics, and supporting documents and filling up the enrollment form by visiting a registration center, the system generates a 29-digit RID for future reference. If the user misplaces this RID, this feature will allow a user to retrieve his/her lost RID. The user needs to provide his/her Full Name, Mobile Number/E-Mail ID, Postal Code that was provided during registration as input. The system will validate the user's provided data and send the RID to the same mobile number and email ID. The system will display an error message if the data is not found in system.

## 2.4 Retrieve Lost UIN [**[↑]**](#table-of-content)
This feature will allow a user to retrieve his/her lost UIN. User needs to provide the Full Name, Mobile Number/E-Mail ID, Postal Code as input. The system will first validate the user's provided data, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the password protected link of the UIN  to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.5 Re-print Request of UIN [**[↑]**](#table-of-content)
This feature will allow a user to raise reprint request of his/her UIN. The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will take the UIN reprint request and acknowledge the request to the user along with a Service Request Number (SRN). The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.6 Initiate UIN Update [**[↑]**](#table-of-content)
This feature will allow a user to initiate update of demographic details (address) of his/her UIN now, but in future, other demographic details of user can also be updated. The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send the Update Request Number (URN) to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

Please refer to the [**Track Status of UIN Update**](#7-track-status-of-uin-update-) for more details.

## 2.7 Track Status of UIN Update [**[↑]**](#table-of-content)

This feature will allow a user to track status of his/her UIN update. The user needs to provide the URN as input. The system will first validate the RID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send UIN Update status to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.8 View History of Authentication Requests (for Prescribed Days/number of requests) [**[↑]**](#table-of-content)
This feature will allow a user to view the authentication request history his/her UIN. The user needs to provide the UIN/VID as input. The system will first validate the user's provided UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will display user's Authentication History. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

The system will fetch the record for past 6 months from the current date or maximum 50 transactions (configurable). 

## 2.9 Lock/Unlock UIN [**[↑]**](#table-of-content)

To protect the identity, confidentiality, and security of his/her UIN demographic or biometric information, a  user can lock/unlock his/her authentication types using Resident Service.

### 2.9.1 Lock the UIN
This feature will allow a user to lock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the locked authentication types cannot be used for any authentication purpose.
.The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of lock authentication types to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

A user can lock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the locked authentication types cannot be used for any authentication purpose.

### 2.9.2 Unlock the UIN

This feature will allow a user to unlock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the unlocked authentication types can be used for any authentication purpose.
The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of unlock authentication types to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.


## 2.10. VID Service [**[↑]**](#table-of-content)

Virtual ID is an alternative to UIN and is temporary code that can be used for authentication or for availing any service of a user. The user can provide the VID instead of UIN to authenticate themselves, obtain any service, and  protect user's UIN details from being accessed by someone else. Also VID can be used to get e-KYC done at both private and government organizations. VID validity is configurable.

VID services  include generating, regenerating, and updating VID status.

### 2.10.1 Generate a VID [**[↑]**](#table-of-content)
Virtual ID (VID) is used as a mask for UIN to protect the confidentiality and security of UIN. A user can raise a request to generate a Virtual ID via Resident Service by providing his/her UIN. The system validates the UIN via OTP authentication. On successful validation the VID is generated based on the VID policy of the respective country. The system triggers the VID generation request status to the registered mobile number/email ID.  If validation fails, then the system triggers the appropriate error message.


### 2.10.2 Maintain the status of a VID (WIP) [**[↑]**](#table-of-content)



### 2.10.3 Regenerate a VID (WIP)[**[↑]**](#table-of-content)	

A user can regenerate the VID, when the existing VID is expired or revoked. He/she provides the UIN and the system authenticates the user’s request based on the security policy of the respective country and regenerates the VID.


### 2.10.4 Revoke a VID [**[↑]**](#table-of-content)

To prevent misuse of VID, a user can request to revoke his/her VID using Resident Services if the user feels his/her VID has been compromised. The user provides the VID and the system checks for the registered mobile number/email ID, and triggers an OTP notification. The user provides the OTP as received. The system validates the provided OTP and authenticates the user. On successful authentication, the system revokes the VID and provides a new VID to the associated UIN based on VID policy of the respective country through the registered mobile number/email ID. If validation fails, the system triggers the appropriate error message.

 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

### 2.10.5 Auto-restore a VID on Revocation and with Auto-restore Policy (WIP) [**[↑]**](#table-of-content)  



### 2.10.6 Retrieve the UIN Corresponding to a VID (WIP) [**[↑]**](#table-of-content)	

When a user does not remember his/her UIN, he/she can retrieve the UIN by providing the VID that was generated against the UIN earlier. The system authenticates the user’s request as per the security policy of the respective country and retrieves the UIN. Additionally, the system triggers the UIN retrieval request status to the registered mobile number/email ID If authentication failes, the system triggers the appropriate error message.
 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/idrepository/vid-service.md)

[Refer to Wiki for more details on **VID Services API**](ID-Repository-API#vid-services-private).

### Process View (WIP) [**[↑]**](#table-of-content)
[**Link to Process View of Resident Services**](Process-view)
