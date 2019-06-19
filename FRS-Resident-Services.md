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
By using Resident Service, individual can update some specific demographics data, which were provided at the time of registration of Unique Identity Number (UIN). Government provides Unique Identity Number (UIN) to each resident of the country. Based on country, the UIN will be used as an ID card.   
# 2. Features [**[↑]**](#table-of-content)
## 2.1 Track status of UIN Generation by providing Registration ID [**[↑]**](#table-of-content)

Whenever an individual wants to know about the UIN generation status, he/she can track  status by providing the Registration ID(RID) or visiting to the registration center. The system validates the provided RID and the mobile number/email ID associated with it and sends an One Time Password (OTP) notification if successfully validated. Individual provides the OTP as received; the system authenticates the individual and on successful authentication, the system provides the status of UIN generation along with a notification (UIN statuses are configurable). During the validation of RID and mobile number/email ID, if the RID is not found or the mobile number/email ID is not associated with the RID, or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.2 Download UIN [**[↑]**](#table-of-content)

An individual can request for an electronic UIN by providing the UIN/ Virtual ID (VID), full name, postal code, and security code. The system validates the provided data, checks for the registered mobile number/email ID, and triggers an OTP notification. The Individual provides the OTP as received.The system validates the provided OTP and  authenticates the individual. On successful authentication, the system generates a password protected e-UIN in pdf format. Additionally, the system triggers a notification to the registered mobile number/email id, with a link to the pdf. During the validation of UIN/VID, Full Name, Postal Code, and Security Code and the mobile number/email ID, if the provided data are not found or the mobile number/email ID is not associated with the UIN/VID or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.3 Retrieve Lost RID [**[↑]**](#table-of-content)
When an individual visits a registration center and fill up the enrollment form, or fills up the pre-registration form online specifying the mandatory fields. Once the UIN application is submitted after providing the required demographics, bio-metrics, and supporting documents, the the system generated 29-digit enrollment/Registration ID (RID) and this registration ID will be used  for various purpose.

An individual can retrieve the RID by providing the Full Name, Mobile Number/E-Mail ID, Postal Code through Resident Services. The system validates the provided data, checks for the registered mobile number/email ID and triggers an OTP notification. The individual provides the OTP as received. The system validates the provided OTP and authenticates the individual. On successful authentication, the system generates the password protected RID in pdf format. Additionally, the system triggers a notification to the registered mobile number/email id, with a link to the pdf. During the validation of Full Name, mobile number/email ID, and postal code, if the full name, mobile number/email ID and postal code are not associated with the RID or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.4 Retrieve Lost UIN [**[↑]**](#table-of-content)

If an individual lost his/her UIN due to any reason, he/she can retrieve it by either visiting the registration center or visiting to the Resident Service. Through Resident Services, an individual can request to retrieve the Registration ID by providing the Full Name, Mobile Number/E-Mail ID, Postal Code. The system validates the provided data, checks for the registered mobile number/email ID, and triggers an OTP notification. The individual provides the OTP as received. The system validates the provided OTP and authenticates the individual. On successful authentication, the system generates the password protected UIN in pdf format. Additionally, the system triggers a notification to the registered mobile number/email id, with a link to the pdf.  During the validation of Full Name, mobile number/email ID, and postal code, if the full name, mobile number/email ID, and postal code are not associated with the UIN or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.5 Re-print Request of UIN [**[↑]**](#table-of-content)

An individual can officially receive a hard copy of his/her UIN after raising a UIN reprint request through registration center or Resident Services in case of previous UIN is misplaced/damaged or due to any other reason.
In Resident Services, an individual provides the UIN/VID for which he/she wants to reprint. The system validates the UIN/VID and checks for the registered mobile number/email ID and triggers OTP notification. The individual provides the OTP as received. The system validates the provided OTP and authenticates the individual. On successful authentication, the system will provide the UIN to the registration processor to process the reprint request. Additionally, the system triggers an acknowledgement  notification of UIN reprint request to the registered mobile number/email ID.  During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email, ID is not associated with the UIN/VID or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.6 Initiate UIN Update [**[↑]**](#table-of-content)
If an individual’s demographic and biometric data are mismatched or captured wrongly due to any reason, that can be updated trough registration center or Resident Services. In Resident Services, an individual can initiate a request to update the demographic data of his/her UIN. An individual provides the UIN/VID for which he/she wants to update.The system validates the provided UIN/VID, checks for the registered mobile number/email ID associated with and triggers an OTP notification. The individual provides the OTP as received.The system validates the provided OTP and  authenticates the individual. On successful authentication, the system allows the individual to update the respective demographic data.The individual provides the supporting documents related to the details, which are being updated. Additionally, the system triggers an acknowledgement  notification of UIN update request to the registered mobile number/email ID. .During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the UIN/VID or the provided OTP is not correct, and then the system triggers the appropriate error message. Status of an update request can further be tracked by an individual. Please refer to the [**Track Status of UIN Update**](#7-track-status-of-uin-update-) for more details.

## 2.7 Track Status of UIN Update [**[↑]**](#table-of-content)
After an individual raised UIN updates request, he/she can track the status by providing the Registration ID through Resident Services. An individual provides the Registration ID for which he/she wants to track the status of UIN updates. The system validates the provided Registration ID, checks for the registered mobile number/email ID, and triggers an OTP notification to the individual. The individual provides the OTP as received.The system validates the provided OTP, authenticates the individual, and provides the UIN updating status (Update statuses are configurable). During the validation of Registration ID and the mobile number/email ID, if the Registration ID is not found or the mobile number/email ID is not associated with the Registration ID, or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.8 View History of Authentication Requests (for Prescribed Days/number of requests) [**[↑]**](#table-of-content)
An individual can view authentication- requests history for a specific UIN/VID. The system will fetch the record for past 6 months from the current date or maximum 50 transactions (configurable). 

Procedure to raise request to view the authentication history of the past:

1. An individual provides his/her UIN/VID to view the authentication history.
1. The system validates the provided UIN/VID, checks for the registered mobile number/email ID, and 
   triggers an OTP notification to the individual.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and authenticates the individual. 
1. On successful authentication, the system provides the history of authentication for all the authentication modalities.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID, or the provided OTP is not correct, then the system triggers the appropriate error message.

## 2.9 Lock/Unlock UIN [**[↑]**](#table-of-content)
MOSIP has provided the facility to the individual to lock/unlock his/her authentication types temporarily to  put additional restriction of demographic or biometric data.

### 2.9.1 Lock the UIN

An individual can lock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with his/her UIN/VID. Only the locked authentication types cannot be used for any authentication purpose.

The following procedure to be followed by an individual to lock the authentication types:
1. An individual provides the UIN/VID for which he/she wants to lock the authentication types.
1. The system validates the UIN/VID, checks for the registered mobile number/email ID, and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and authenticates the individual.
1. On successful authentication, the system provides the individual with lock information related to authentication types.
1. The individual will lock the authentication types, which he/she wishes.
1. The system will disable the authentication types as provided by the individual.
1. The system will also trigger a confirmation notification on successful locking.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID, or the provided OTP is not correct, then the system triggers the appropriate error message.
### 2.9.2 Unlock the UIN

An individual can unlock the authentication types (Demographic, Biometrics (FP/Iris/Face/All)) associated with the UIN/VID. Only the unlocked authentication types of demographic and biometric (FP/Iris/Face/All) can be used for any required authentication purpose.

The following procedure to be followed by an individual to unlock the authentication type(s):

1. An individual provides his/her UIN/VID  to unlock the authentication types.
1. The system validates the UIN/VID and checks for the registered mobile number/email ID and triggers OTP notification.
1. The individual provides the OTP as received.
1. The system validates the provided OTP and authenticates the individual.
1. On successful authentication, The system provides the individual with unlock information related to authentication types.
1. The individual will unlock the authentication types, which he/she wishes.
1. The system will lock the authentication types as provided by the individual.
Additionally, the system triggers an acknowledgement  notification of UIN update request to the registered mobile number/email ID, The system provides an acknowledgement notification
1. Additionally, the system triggers a confirmation notification on successful unlocking the authentication types.
1. During the validation of UIN/VID, if the UIN/VID is not found or the mobile number/email ID is not associated with the 
   UIN/VID, or the provided OTP is not correct, then the system triggers the appropriate error message.

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


