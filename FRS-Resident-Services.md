## Table Of Content
* [1. Overview](#1-overview-)
* [2. Features](#2-features-)
  * [2.1 Track Status of UIN Generation by providing RID (Request ID for New Registration)](#21-track-status-of-uin-generation-by-providing-registration-id-) _(RES_FR_1)_
  * [2.2 Download e-UIN](#22-download-e-uin-) _(RES_FR_2)_
  * [2.3 Retrieve Lost RID (Request ID for New Registration)](#23-retrieve-lost-rid-) _(RES_FR_3)_
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
* [List of Configurable Parameters and Processes](#list-of-configurable-parameters-and-processes-)
* [Resident Services API](#resident-services-api-)
* [Process View (WIP)](#process-view-wip-)

# 1. Overview [**[↑]**](#table-of-content)

The Resident Service module will provide a host of services to users who can avail these services after the creation of their Unique Identity Number (UIN). The list of services are as follows:
 * Update of Demographic Data (UIN update)
 * Track Request Status
 * Lock/unlock AUTH types
 * Download e-UIN
 * Retrieve Lost Request ID(RID)/UIN
 * Reprint UIN
 * View Authentication Transaction History
 * Generate/revoke Virtual ID (VID).

All these features are detailed in the following features section.
  
# 2. Features [**[↑]**](#table-of-content)
## 2.1 Track status of UIN Generation by providing Registration ID [**[↑]**](#table-of-content)

This feature will allow a user to track status of his/her UIN generation. The user needs to provide the RID  as input. The system will first validate the user's provided RID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of UIN generation to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.2 Download e-UIN [**[↑]**](#table-of-content)

This feature will allow a user to download his/her electronic UIN. The user needs to provide the UIN/VID, full name, postal code, and security code as input. The system will validate the provided data, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send a password protected link of the pdf for download of e-UIN to the user's registered mobile number and email ID. The system will also trigger a successful notification message  to the user's registered mobile number/email id after the transaction or appropriate error message if the transaction was not successful.

## 2.3 Retrieve Lost RID (Request ID for New Registration) [**[↑]**](#table-of-content)
After the UIN application is submitted by a user providing the required demographic, biometrics and supporting documents and filling up the enrollment form by visiting a registration center, the system generates a 29-digit RID (Request ID) for future reference. If the user misplaces this RID, this feature will allow a user to retrieve his/her lost RID. The user needs to provide his/her Full Name, Mobile Number/E-Mail ID, Postal Code that was provided during registration as input. The system will first validate the user's provided data, trigger an OTP, and perform OTP validation on user's registered mobile number/email ID. On successful validation, the system will send the password protected link of the RID to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.4 Retrieve Lost UIN [**[↑]**](#table-of-content)
This feature will allow a user to retrieve his/her lost UIN. User needs to provide the Full Name, Mobile Number/E-Mail ID, Postal Code as input. The system will first validate the user's provided data, trigger an OTP, and perform OTP validation on user's registered mobile number/email ID. On successful validation, the system will send the password protected link of the UIN  to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.5 Re-print Request of UIN [**[↑]**](#table-of-content)
This feature will allow a user to raise reprint request of his/her UIN. The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will take the UIN reprint request and acknowledge the request with a Request ID (RID) to the user. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.6 Initiate UIN Update [**[↑]**](#table-of-content)
This feature will allow a user to initiate update of his/her demographic details. In current implementation only address change is in scope however in future,if required, any other demographic can be changed using this service. The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will generate and send a Request ID (RID) for UIN update to user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

Please refer to the [**Track Status of UIN Update**](#7-track-status-of-uin-update-) for more details.

## 2.7 Track Status of UIN Update [**[↑]**](#table-of-content)

This feature will allow a user to track status of his/her UIN update. The user needs to provide the URN as input. The system will first validate the RID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of UIN Update to user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.8 View History of Authentication Requests [**[↑]**](#table-of-content)
This feature will allow a user to view the authentication request(s) history of his/her UIN. The user needs to provide the UIN/VID as input. The system will first validate the UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send unarchived Authentication History data of the user. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

The system will fetch the record for past 6 months from the current date or maximum 50 transactions (configurable). 

## 2.9 Lock/Unlock UIN [**[↑]**](#table-of-content)

A user can decide to lock specific Authentication types (Demographic/Biometrics) of his/her UIN/VID for security reasons. It can be for one or more Authentication types. Similarly at any point he/she may also request to unlock one or more locked Authentication types which was locked earlier.

### 2.9.1 Lock the UIN
This feature will allow a user to lock the Authentication Type (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. The locked Authentication Type(s) cannot be used for any future authentication request.
The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will first send the details of all Authentication Types to user. The user will then select which Authentication Type(s) will need to be locked. The system takes the request and accordingly locks the Authentication Type(s) and notifies the user. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

### 2.9.2 Unlock the UIN

This feature will allow a user to unlock any Authentication Types (Demographic, Biometrics (FP/Iris/Face/All)) which is/are in locked status associated with his/her UIN/VID. Once unlocked, the user can use these Authentication Type(s) for any authentication purpose. The user needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will first send the details of all Authentication Type(s) to user which is/are in locked status. The user will then select which Authentication Type(s) will need to be unlocked. The system takes the request and accordingly unlocks the Authentication Type(s) and notifies the user. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.10. VID Service [**[↑]**](#table-of-content)
To safeguard the confidentiality of an UIN and for its security, Virtual ID (VID) service is provided. Based on the VID policy (defined by a country) an user will be provided a VID during UIN registration and also he/she can create one using Resident Service. The types of VID (perpetual/temporary/etc) is defined by a country.

VID services  can include the below as described.

### 2.10.1 Generate a VID [**[↑]**](#table-of-content)
A user can request to generate a Virtual ID via Resident Service by providing his/her UIN. The system will first validate the user's UIN, trigger an OTP, and perform OTP authentication on user's registered mobile number/email ID. On successful authentication the VID is generated based on the VID policy of the respective country. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

### 2.10.2 Maintain the status of a VID (WIP) [**[↑]**](#table-of-content)

### 2.10.3 Regenerate a VID (WIP)[**[↑]**](#table-of-content)	

### 2.10.4 Revoke a VID [**[↑]**](#table-of-content)

To prevent misuse of VID, a user can request to revoke his/her VID using Resident Services if the user feels his/her VID has been compromised. The user provides the VID and the system checks for the registered mobile number/email ID, and triggers an OTP notification. The user provides the OTP as received. The system validates the provided OTP and authenticates the user. On successful authentication, the system revokes the VID and provides a new VID to the associated UIN based on VID policy of the respective country through the registered mobile number/email ID. If validation fails, the system triggers the appropriate error message.

 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

### 2.10.5 Auto-restore a VID on Revocation and with Auto-restore Policy (WIP) [**[↑]**](#table-of-content)  



### 2.10.6 Retrieve the UIN Corresponding to a VID (WIP) [**[↑]**](#table-of-content)	

When a user does not remember his/her UIN, he/she can retrieve the UIN by providing the VID that was generated against the UIN earlier. The system authenticates the user’s request as per the security policy of the respective country and retrieves the UIN. Additionally, the system triggers the UIN retrieval request status to the registered mobile number/email ID If authentication failes, the system triggers the appropriate error message.
 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/idrepository/vid-service.md)

[Refer to Wiki for more details on **VID Services API**](ID-Repository-API#vid-services-private).
### List of Configurable Parameters and Processes [**[↑]**](#table-of-content)

1. Configurable Parameters
* (Work in Progress) 
2. Configurable Processes 
* (Work in Progress) 

### Resident Services API [**[↑]**](#table-of-content)
* (Work in Progress) 


### Process View (WIP) [**[↑]**](#table-of-content)
* (Work in Progress) 
