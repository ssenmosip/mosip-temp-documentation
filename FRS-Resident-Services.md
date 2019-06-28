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
_(RES_FR_10.6)_
* [List of Configurable Parameters and Processes](#list-of-configurable-parameters-and-processes-)
* [Resident Services API](#resident-services-api-)
* [Process View (WIP)](#process-view-wip-)

# 1. Overview [**[↑]**](#table-of-content)

The Resident Service module will provide a host of services to an individual which can be availed after the creation of their Unique Identity Number (UIN). The list of services are as follows:
 * Update of Demographic Data (UIN update)
 * Track Request Status
 * Lock/Unlock AUTH types
 * Download e-UIN
 * Retrieve Lost Request ID(RID)/UIN
 * Reprint UIN
 * View Authentication Transaction History
 * Generate/revoke Virtual ID (VID).

All these features are detailed in the following features section.
  
# 2. Features [**[↑]**](#table-of-content)
## 2.1 Track status of UIN Generation by providing Request ID (RID) for New Registration [**[↑]**](#table-of-content)

This feature will allow an individual to track status of his/her UIN generation. The individual needs to provide the RID (Request ID received during UIN registration) as input. The system will validate this RID. On successful validation, the system will send the status of UIN generation to the individual's registered mobile number and/or email ID. The system will also send a notification message to individual’s mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.2 Download e-UIN [**[↑]**](#table-of-content)

This feature will allow an individual to download his/her electronic UIN. The individual needs to provide the UIN/VID, full name, postal code, and security code as input. The system will validate the provided data, trigger an OTP, and perform OTP authentication of individual's mobile number and/or email ID. On successful authentication, system will send a link to password protected pdf for download of e-UIN to individual's registered mobile number and/or email ID. The system will also trigger a notification message  to the individual's registered mobile number and/or email id after the transaction or appropriate error message if the transaction was not successful.

## 2.3 Retrieve Lost RID (Request ID for New Registration) [**[↑]**](#table-of-content)
After the UIN application is submitted by an individual providing the required demographic, biometrics and supporting documents and filling up the enrollment form by visiting a registration center, the system generates a unique RID (Request ID) as an acknowledgement number. If the individual misplaces this RID, this feature will allow an individual to retrieve his/her lost RID to subsequently trace the associated UIN. The individual needs to provide his/her Full Name, Mobile Number and/or E-Mail ID, Postal Code that was provided during registration as input. The system will first validate the individual's provided data, trigger an OTP, and perform OTP validation on the given mobile number and/or email ID. On successful validation, the system will send a link to password protected pdf containing the RID to individual's registered mobile number and/or email ID. The system will also trigger a notification message to the registered mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.4 Retrieve Lost UIN [**[↑]**](#table-of-content)
This feature will allow an individual to retrieve his/her lost UIN. The individual needs to provide the Full Name, Mobile Number and/or E-Mail ID, Postal Code as input. The system will first validate the individual's provided data, trigger an OTP, and perform OTP validation on the given mobile number and/or email ID. On successful validation, the system will send a link to password protected pdf containing the UIN to individual's registered mobile number and/or email ID. The system will also trigger a notification message to the registered mobile number and/or email ID after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.5 Re-print Request of UIN [**[↑]**](#table-of-content)
This feature will allow an individual to raise reprint request of his/her UIN. The individual needs to provide the UIN/VID as input. The system will first validate the individual's UIN/VID, trigger an OTP, and perform OTP authentication of individual's registered mobile number and/or email ID. On successful authentication, the system will take the UIN reprint request and acknowledge the request with a Request ID (RID) to the individual. The system will also trigger a notification message to the registered mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.6 Initiate UIN Update [**[↑]**](#table-of-content)
This feature will allow an individual to initiate update of his/her demographic details. Currently, an individual can initiate an update of the address associated to the provided UIN/VID. However, this service can be extended to further update any other aspect of the demographic data (EG: Mobile, Email, etc). The individual needs to provide the UIN/VID as input. The system will first validate the individual's UIN/VID, trigger an OTP, and perform OTP authentication of individual's mobile number and/or email ID. On successful authentication, the system will generate and send a Request ID (RID) for UIN update to individual's registered mobile number and/or email ID. The system will also trigger a notification message to the registered mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

Please refer to the [**Track Status of UIN Update**](#7-track-status-of-uin-update-) for more details.

## 2.7 Track Status of UIN Update [**[↑]**](#table-of-content)

This feature will allow an individual to track status of his/her UIN update. The individual needs to provide the RID ( Request ID for UIN Updates) as input. The system will first validate the RID, trigger an OTP, and perform OTP authentication of individual's registered mobile number and/or email ID. On successful authentication, the system will send the status of UIN Update to individual's registered mobile number and/or email ID. The system will also send a notification message to individual’s mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.8 View History of Authentication Requests [**[↑]**](#table-of-content)
This feature will allow an individual to view history of the authentication requests associated to his/her UIN. The individual needs to provide the UIN/VID as input. The system will first validate the UIN/VID, trigger an OTP, and perform OTP authentication of individual's registered mobile number and/or email ID. On successful authentication, the system will send unarchived Authentication History data of the individual associated to the provided UIN and its associated VIDs. The system will also send a notification message to individual’s mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

The system will fetch the record for past 6 months from the current date or maximum 50 transactions (configurable). 

## 2.9 Lock/Unlock UIN [**[↑]**](#table-of-content)

An individual can decide to lock specific Authentication types (Demographic/Biometrics) of his/her UIN/VID for security reasons. It can be for one or more Authentication types. Similarly at any point he/she may also request to unlock one or more locked Authentication types which was locked earlier.

### 2.9.1 Lock the UIN
This feature will allow an individual to lock the requested Authentication Type (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. The locked Authentication Type(s) cannot be used for any future authentication request.
The individual needs to provide the UIN/VID as input. The system will first validate the individual's UIN/VID, trigger an OTP, and perform OTP authentication on individual's registered mobile number and/or email ID. On successful authentication, the system will first send the details of all Authentication Types to individual. The individual will then select which Authentication Type(s) will need to be locked. The system takes the request and accordingly locks the Authentication Type(s) and notifies the individual. The system will also send a notification message to individual’s mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

### 2.9.2 Unlock the UIN

This feature will allow an individual to unlock requested Authentication Types (Demographic, Biometrics (FP/Iris/Face/All)) which is/are in locked status associated with his/her UIN/VID. Once unlocked, the individual can use these Authentication Type(s) for any authentication purpose. The individual needs to provide the UIN/VID as input. The system will first validate the individual's UIN/VID, trigger an OTP, and perform OTP authentication of individual's registered mobile number and/or email ID. On successful authentication, the system will first send the details of all Authentication Type(s) to individual which is/are in locked status. The individual will then select which Authentication Type(s) will need to be unlocked. The system takes the request and accordingly unlocks the Authentication Type(s) and notifies the individual. The system will also send a notification message to individual’s mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.10. VID Service [**[↑]**](#table-of-content)
To safeguard the confidentiality of an UIN and for its security, Virtual ID (VID) service is provided. Based on the VID policy (defined by a country) an individual will be provided a VID during UIN registration and also he/she can create one using Resident Service. The types of VID (perpetual/temporary/etc) is defined by a country.

VID services  can include the below as described.

### 2.10.1 Generate a VID [**[↑]**](#table-of-content)
An individual can request to generate a Virtual ID via Resident Service by providing his/her UIN. The system will first validate the individual's UIN, trigger an OTP, and perform OTP authentication on individual's registered mobile number and/or email ID. On successful authentication the VID is generated based on the VID policy of the respective country. The system will also send a notification message to individual’s mobile number and/or email ID after a successful transaction or appropriate error message if the transaction was not successful.

### 2.10.2 Maintain the status of a VID (WIP) [**[↑]**](#table-of-content)

### 2.10.3 Regenerate a VID (WIP)[**[↑]**](#table-of-content)	

### 2.10.4 Revoke a VID [**[↑]**](#table-of-content)

To prevent misuse of VID, an individual can request to revoke his/her VID using Resident Services, if the individual feels his/her VID has been compromised. The individual provides the VID as input. The system will then validate the individual's VID, trigger an OTP, and perform OTP authentication on individual's registered mobile number and/or email ID. On successful authentication, the system revokes the provided VID. Based on the VID policy of the country a new VID will be generated during revocation and provided to the individual on the registered mobile number and/or email ID. If validation fails, the system triggers the appropriate error message.

 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

### 2.10.5 Auto-restore a VID on Revocation and with Auto-restore Policy (WIP) [**[↑]**](#table-of-content)  

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
