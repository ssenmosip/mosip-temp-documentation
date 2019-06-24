## Table Of Content
* [1. Overview](#1-overview-)
* [2. Features](#2-features-)
  * [2.1 Track Status of UIN Generation by providing Registration ID](#21-track-status-of-uin-generation-by-providing-registration-id-) _(RES_FR_1)_
  * [2.2 Download UIN](#22-download-uin-) _(RES_FR_2)_
  * [2.3 Retrieve Lost RID](#23-retrieve-lost-rid-) _(RES_FR_3)_
  * [2.4 Retrieve Lost UIN](#24-retrieve-lost-uin-) _(RES_FR_4)_
  * [2.5 Re-print Request of UIN](#25-re-print-request-of-uin-) _(RES_FR_5)_
  * [2.6 Initiate UIN Update](#26-initiate-uin-update-) _(RES_FR_6)_
  * [2.7 Track Status of UIN Update](#27-track-status-of-uin-update-) _(RES_FR_7)_
  * [2.8 View History of Authentication Requests (for Prescribed Days/number of requests)](#28-view-history-of-authentication-requests-for-prescribed-daysnumber-of-requests-) _(RES_FR_8)_
  * [2.9 Lock/Unlock UIN](#29-lockunlock-uin-) _(RES_FR_9)_
  * [2.10 VID Service](#10-vid-service-)
    * [2.10.1 Generate a VID](#2101-generate-a-vid-) _(RES_FR_10.1)_
    * [2.10.2 Maintain the status of a VID (WIP)](#2102-maintain-the-status-of-a-vid-wip-) _(RES_FR_10.2)_
    * [2.10.3 Regenerate a VID (WIP)](#2103-regenerate-a-vid-wip) _(RES_FR_10.3)_
    * [2.10.4 Revoke a VID](#2104-revoke-a-vid-) _(RES_FR_10.4)_
    * [2.10.5 Auto-restore a VID on Revocation and with Auto-restore Policy (WIP)](#2105-auto-restore-a-vid-on-revocation-and-with-auto-restore-policy-wip-) _(RES_FR_10.5)_
    * [2.10.6 Retrieve the UIN corresponding to a VID (WIP)](#2106-retrieve-the-uin-corresponding-to-a-vid-wip-) _(RES_FR_10.6)_


# 1. Overview [**[↑]**](#table-of-content)
The 'Resident Services' module will provide a host of services for a user which he/she can utilize after generation of his/her Unique Identity Number(UIN). These services can include update of demographic data (UIN update), track status of a request, lock/unlock AUTH types, download e-UIN, retrieve lost Registration ID(RID)/UIN, reprint UIN, view AUTH transaction history, generate/revoke Virtual ID (VID). All these features are detailed under the features section below.   
# 2. Features [**[↑]**](#table-of-content)
## 2.1 Track status of UIN Generation by providing Registration ID [**[↑]**](#table-of-content)

This feature will allow an individual to track status of his/her UIN generation. The user just needs to provide the RID  as input. The system will first validate the user's provided RID, trigger an OTP and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of UIN generation to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

## 2.2 Download UIN [**[↑]**](#table-of-content)

This feature will allow an individual to download the electronic UIN. The user just needs to provide the UIN/VID, full name, postal code, and security code as input. The system will validate the provided data, trigger an OTP and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send the e-UIN generation status to the user's registered mobile number and email ID. The system will also trigger a successful notification message  to the user's registered mobile number/email id, with a link of the pdf after successful transaction or appropriate error message if the transaction was not successful.

## 2.3 Retrieve Lost RID [**[↑]**](#table-of-content)
When an individual visits a registration center and fills up the enrollment form, or fills up the pre-registration form online specifying the mandatory fields. Once the UIN application is submitted after providing the required demographics, bio-metrics, and supporting documents, the the system generated 29-digit enrollment/RID and this RID will be used  for future reference.

This feature will allow an individual to retrieve the Lost RID. The user just needs to provide the Full Name, Mobile Number/E-Mail ID, Postal Code as input. The system will first validate the user's provided data, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send the status of retrieving lost RID  to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email id, with a link to the pdf after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.4 Retrieve Lost UIN [**[↑]**](#table-of-content)
This feature will allow an individual to retrieve his/her Lost UIN. The user just needs to provide the Full Name, Mobile Number/E-Mail ID, Postal Code as input. The system will first validate the user's provided data, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send the status of retrieving lost UIN  to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID, with a link to the pdf after a successful transaction or  appropriate error message if the transaction was not successful.

## 2.5 Re-print Request of UIN [**[↑]**](#table-of-content)
This feature will allow an individual to raise reprint request of his/her UIN . The user just needs to provide the the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send the status of UIN reprint request to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.
## 2.6 Initiate UIN Update [**[↑]**](#table-of-content)
This feature will allow an individual to initiate UIN update of his/her UIN . The user just needs to provide the the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP, and perform OTP authentication on user's mobile number/email ID. On successful authentication, the system will send the UIN update status to the user's registered mobile number and email ID. The system will also trigger a successful notification message to the registered mobile number/email ID after a successful transaction or  appropriate error message if the transaction was not successful.

<If an individual’s demographic and biometric data are mismatched or captured wrongly due to any reason, that can be updated trough registration center or Resident Services. In Resident Services, an individual can initiate a request to update the demographic data of his/her UIN. An individual provides the UIN/VID for which he/she wants to update.The system validates the provided UIN/VID, checks for the registered mobile number/email ID associated with and triggers an OTP notification. The individual provides the OTP as received.The system validates the provided OTP and  authenticates the individual. On successful authentication, the system allows the individual to update the respective demographic data.The individual provides the supporting documents related to the details, which are being updated. Additionally, the system triggers an acknowledgement  notification of UIN update request to the registered mobile number/email ID. .During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the UIN/VID or the provided OTP is not correct, and then the system triggers the appropriate error message. Status of an update request can further be tracked by an individual. Please refer to the [**Track Status of UIN Update**](#7-track-status-of-uin-update-) for more details.>

## 2.7 Track Status of UIN Update [**[↑]**](#table-of-content)
This feature will allow an individual to track status of his/her UIN update. The user just needs to provide the RID  as input. The system will first validate the user's provided RID, trigger an OTP and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send UIN Update status to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.
## 2.8 View History of Authentication Requests (for Prescribed Days/number of requests) [**[↑]**](#table-of-content)
This feature will allow an individual to view the authentication request history his/her UIN. The user just needs to provide the UIN/VID as input. The system will first validate the user's provided UIN/VID, trigger an OTP and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of View Authentication History to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

An individual can view authentication- requests history for a specific UIN/VID. The system will fetch the record for past 6 months from the current date or maximum 50 transactions (configurable). 

## 2.9 Lock/Unlock UIN [**[↑]**](#table-of-content)

To protect the identity, confidentiality, and security of his/her UIN demographic or biometric information, an  individual can lock/unlock his/her authentication types using Resident Service.

### 2.9.1 Lock the UIN
This feature will allow an individual to lock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the locked authentication types cannot be used for any authentication purpose.
.The user just needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of lock authentication types to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.

An individual can lock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the locked authentication types cannot be used for any authentication purpose.

### 2.9.2 Unlock the UIN

This feature will allow an individual to unlock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the unlocked authentication types can be used for any authentication purpose.
.The user just needs to provide the UIN/VID as input. The system will first validate the user's UIN/VID, trigger an OTP and perform OTP authentication on user's registered mobile number/email ID. On successful authentication, the system will send the status of unlock authentication types to the user's registered mobile number and email ID. The system will also send a success notification message to user’s mobile number/email ID after a successful transaction or appropriate error message if the transaction was not successful.


## 2.10. VID Service [**[↑]**](#table-of-content)

VID is an alternative to UIN and is temporary code that can be used for authentication or for availing any service of an individual. The individual can provide the VID instead of UIN to authenticate themselves, obtain any service, and  protect individual's UIN details from being accessed by someone else. Also VID can be used to get e-KYC done at both private and government organizations. VID validity is configurable.

VID services  include generating, regenerating, and updating VID status.

### 2.10.1 Generate a VID [**[↑]**](#table-of-content)
Virtual ID (VID) is used as a mask for UIN to protect the confidentiality and security of UIN. An individual can raise a request to generate a Virtual ID via Resident Service by providing his/her UIN. The system validates the UIN via OTP authentication. On successful validation the VID is generated based on the VID policy of the respective country. The system triggers the VID generation request status to the registered mobile number/email ID.  If validation fails, then the system triggers the appropriate error message.


### 2.10.2 Maintain the status of a VID (WIP) [**[↑]**](#table-of-content)



### 2.10.3 Regenerate a VID (WIP)[**[↑]**](#table-of-content)	

An individual can regenerate the VID, when the existing VID is expired or revoked. He/she provides the UIN and the system authenticates the individual’s request based on the security policy of the respective country and regenerates the VID.


### 2.10.4 Revoke a VID [**[↑]**](#table-of-content)

To prevent misuse of VID, an individual can request to revoke his/her VID using Resident Services if the individual feels his/her VID has been compromised. The individual provides the VID and the system checks for the registered mobile number/email ID, and triggers an OTP notification. The individual provides the OTP as received. The system validates the provided OTP and authenticates the individual.. On successful authentication, the system revokes the VID and provides a new VID to the associated UIN based on VID policy of the respective country through the registered mobile number/email ID. If validation fails, the system triggers the appropriate error message.

 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

### 2.10.5 Auto-restore a VID on Revocation and with Auto-restore Policy (WIP) [**[↑]**](#table-of-content)  



### 2.10.6 Retrieve the UIN corresponding to a VID (WIP) [**[↑]**](#table-of-content)	

When an individual does not remember his/her UIN, he/she can retrieve the UIN by providing the VID that was generated against the UIN earlier. The system authenticates the individual’s request as per the security policy of the respective country and retrieves the UIN. Additionally, the system triggers the UIN retrieval request status to the registered mobile number/email ID If authentication failes, the system triggers the appropriate error message.
 Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2011/Consolidated%20error%20messages%20V2.4.xlsx).

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/idrepository/vid-service.md)

[Refer to Wiki for more details on **VID Services API**](ID-Repository-API#vid-services-private).


