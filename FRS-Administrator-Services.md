## Table Of Contents
- [1. Login](#1-login-) _(ASR_FR_1)_
  * [1.1 Login](#11-login) _(ASR_FR_1.1)_
  * [1.2 Logout](#12-logout)
    * [1.2.1 Manual Logout](#121-manual-logout) _(ASR_FR_1.2)_
    * [1.2.2 Auto Logout](#122-auto-logout) _(ASR_FR_1.3)_
- [2. Account Management](#2-account-management-) _(ASR_FR_2)_
  * [2.1 Edit Personal Details](#21-edit-personal-details) _(ASR_FR_2.1)_
  * [2.2 Change Password](#22-change-password-) _(ASR_FR_2.2)_
  * [2.3 Reset Password](#23-reset-password-) _(ASR_FR_2.4)_
  * [2.5 Account Unlock](#25-account-unlock) _(ASR_FR_2.5)_
- [3. Security Policy Configuration (WIP)](#3-security-policy-configuration-wip-) _(ASR_FR_3)_
- [4. Notification V1.5 (WIP)](#4-notification-v15-wip-) _(ASR_FR_4)_
  * [4.1 Approval Notifications](#41-approval-notifications) _(ASR_FR_4.1)_
  * [4.2 Country Specific News/Notifications](#42-country-specific-newsnotifications) _(ASR_FR_4.2)_
- [5. Resource Management](#5-resource-management-) _(ASR_FR_5)_
  * [5.1 Center Management](#51-center-management)
    * [5.1.1 View Center](#511-view-center) _(ASR_FR_5.1)_
    * [5.1.2 Create Center](#512-create-center) _(ASR_FR_5.2)_
    * [5.1.3 Update Center](#513-update-center-) _(ASR_FR_5.3)_
    * [5.1.4 Activate/Deactivate/Decommission Center](#514-activate-deactivate-decommission-center-) _(ASR_FR_5.4)_
  * [5.2 Machine Management](#52-machine-management-)
    * [5.2.1 View Machine](#521-view-machine) _(ASR_FR_5.5)_
    * [5.2.2 Create Machine](#522-create-machine) _(ASR_FR_5.6)_
    * [5.2.3 Update Machine](#523-update-machine-) _(ASR_FR_5.7)_
    * [5.2.4 Activate/Deactivate/Decommission Machine](#524-activatedeactivatedecommission-machine-) _(ASR_FR_5.8)_
    * [5.2.5 Map/Un-map/Re-map Machine to a Center](#525-mapun-mapre-map-machine-to-a-center-) _(ASR_FR_5.9)_
  * [5.3 Device Management](#53-device-management-)
    * [5.3.1 View Device](#531-view-device) _(ASR_FR_5.10)_
    * [5.3.2 Create Device](#532-create-device) _(ASR_FR_5.11)_
    * [5.3.3 Update Device](#533-update-device-) _(ASR_FR_5.12)_
    * [5.3.4 Activate/Deactivate/Decommission Device](#534-activatedeactivatedecommission-device-) _(ASR_FR_5.13)_
    * [5.3.5 Map/Un-map/Re-map Device to a Center](#535-mapun-mapre-map-device-to-a-center-) _(ASR_FR_5.14)_
  * [5.4 User Management](#54-user-management-)
    * [5.4.1 View User](#541-view-user) _(ASR_FR_5.15)_
    * [5.4.2 Create User](#542-create-user) _(ASR_FR_5.16)_
    * [5.4.3 Update User](#543-update-user) _(ASR_FR_5.17)_
    * [5.4.4 Activate/Deactivate/Blacklist/Whitelist User](#544-activatedeactivateblacklistwhitelist-user-) _(ASR_FR_5.18)_
    * [5.4.5 Map/Un-map/Re-map User to a Center](#545-mapun-mapre-map-user-to-a-center-) _(ASR_FR_5.19)_
- [6. Master Data Management](#6-master-data-management-) _(ASR_FR_6)_
  * [6.1 View Master Data Types](#61-view-master-data-types) _(ASR_FR_6.1)_
  * [6.2 View Master data for each table (WIP)](#62-view-master-data-for-each-table-wip-) _(ASR_FR_6.2)_
  * [6.3 Manage Master Data](#63-manage-master-data-)
    * [6.3.1 Manage Document Type (Create, Update, Activate/Deactivate)](#631-manage-document-type-create-update-activate-deactivate-) _(ASR_FR_6.3)_
    * [6.3.2 Manage Document Category to Document Mapping (Create, Update, Activate/Deactivate)(WIP)](#632-manage-document-category-to-document-mapping-create-update-activate-deactivate-wip-) _(ASR_FR_6.4)_
    * [6.3.3 Manage Location Data (Create, Update, Activate/Deactivate)](#633-manage-location-data-create-update-activate-deactivate-) _(ASR_FR_6.5)_
    * [6.3.4 Manage Blacklisted Words (Create, Update, Activate/Deactivate)](#634-manage-blacklisted-words-create-update-activate-deactivate) _(ASR_FR_6.6)_
     * [6.3.5 Manage Registration Center Types (View)](#635-manage-registration-center-types-view-) _(ASR_FR_6.7)_ 
     * [6.3.6 Manage Machine Types (View)](#636-manage-machine-types-view) _(ASR_FR_6.8)_ 
     * [6.3.7 Manage Machine Specifications (View)](#637-manage-machine-specifications-view-) _(ASR_FR_6.9)_ 
     * [6.3.8 Manage Device Types (View)](#638-manage-device-types-view) _(ASR_FR_6.10)_ 
     * [6.3.9 Manage Device Specifications (View)](#639-manage-device-specifications-view-) _(ASR_FR_6.11)_ 
     * [6.3.10 Manage Individual Types (View)](#6310-manage-individual-types-view) _(ASR_FR_6.12)_ 
     * [6.3.11 Manage Document Type to Document Category Mapping (View)](#6311-manage-document-type-to-document-category-mapping-view-) _(ASR_FR_6.13)_ 
     * [6.3.12 Manage List of Holidays (View)](#6312-manage-list-of-holidays-view) _(ASR_FR_6.14)_ 
     * [6.3.13 Manage List of Templates (View)](#6313-manage-list-of-templates-view-) _(ASR_FR_6.15)_ 
     * [6.3.14 Manage List of Titles (View)](#6314-manage-list-of-titles-view) _(ASR_FR_6.16)_ 
     * [6.3.15 Manage Gender Types (View)](#6315-manage-gender-types-view-) _(ASR_FR_6.17)_ 
- [7. Approval Process](#7-approval-process-) _(ASR_FR_7)_
  * [7.1 Approval for Resource Creation](#71-approval-for-resource-creation-)
    * [7.1.1 Approval of Center](#711-approval-of-center) _(ASR_FR_7.1)_
    * [7.1.2 Approval of Machine](#712-approval-of-machine) _(ASR_FR_7.2)_
    * [7.1.3 Approval of Device](#713-approval-of-device) _(ASR_FR_7.3)_
    * [7.1.4 Approval of User](#714-approval-of-user) _(ASR_FR_7.4)_
  * [7.2 Approval for Master Data Creation (WIP)](#72-approval-for-master-data-creation-wip) _(ASR_FR_7.5)_
- [8. UIN Activation/Deactivation](#8-uin-activationdeactivation-) _(ASR_FR_8)_
- [9. Packet Status Check (based on RID)(WIP)](#9-packet-status-check-based-on-rid-wip) _(ASR_FR_9)_
- [10.Multi-language Support (WIP)](#10-multi-language-support-wip-) _(ASR_FR_10)_
    * [10.1 i18N](#101-i18n) _(ASR_FR_10.1)_
    * [10.2 Implementation in English (Labels etc)](#102-implementation-in-english-labels-etc) _(ASR_FR_10.2)_
    * [10.3 Language Specific Setup](#103-language-specific-setup) _(ASR_FR_10.3)_
- [11. Responsive UI](#11-responsive-ui-) _(ASR_FR_11)
- [12. MOSIP Platform Setup (WIP)](#12-mosip-platform-setup-wip-) _(ASR_FR_12)
- [13. ID Definition Setup](#13-id-definition-setup-) _(ASR_FR_13)
    * [13.1 ID Definition Validator](#131-id-definition-validator) _(ASR_FR_13.1)_
- [14. Configuration Setup (WIP)](#14-configuration-setup-wip-) _(ASR_FR_14)
- [15. Process Flow Setup (WIP)](#15-process-flow-setup-wip-) _(ASR_FR_15)
- [List of Configurable Parameters and Processes](#list-of-configurable-parameters-and-processes-)
- [Administrator Services API](#administrator-services-api-)
- [Process View](#process-view-)
## 1. Login [**[↑]**](#table-of-contents)
### 1.1 Login
The Admin Portal integrates with the Key Cloak IAM to store users and provides login functionality. 
When an Administrator access the Homepage or any page on the Admin portal through a browser, the portal detects if the Administrator is already logged-in or not. If not, the system re-directs the Administrator to the Key Cloak Login User Interface (UI) which requests the Administrator for his/her Username and Password. 
After getting the credentials, KeyCloak verifies the Administrator’s credentials and Role. It also validates whether the Administrator is not deactivated.After successful validation of the credentials, the system then re-directs the Administrator to the page he/she initially landed on.

### 1.2 Logout
#### 1.2.1 Manual Logout
If an Administrator wishes to logout of the Admin Portal, he/she can opt to select the Logout option from the profile menu on the Administrator UI. The system logs out the Administrator.
#### 1.2.2 Auto Logout
If the user is inactive for X minutes (X is configurable), the system logs out the user automatically. In such case, the system will not save any user’s data.
## 2. Account Management(WIP) [**[↑]**](#table-of-contents)
Using the portal, user will  manage his/her profile. The  portal users are Central Admin, Central Approver, Zonal Admin, Zonal Approver, Registration Center Head, Registration Supervisor, and Registration Officer.

### 2.1 Edit Personal Details (WIP)

### 2.2 Change Password (WIP) [**[↑]**](#table-of-contents)

### 2.3 Reset Password (WIP) [**[↑]**](#table-of-contents)

### 2.4 Forgot User Name (WIP) [**[↑]**](#table-of-contents)

### 2.5 Account Unlock (WIP)

## 3. Security Policy Configuration(WIP)[**[↑]**](#table-of-contents)
Using the portal, Zonal Admin will be able to set up security policies for each applications, which includes the following:
 * Session Time out policies
 * Password policies
    * Use of both upper-case and lower-case letters atleast once
    * Use of at least one numerical digit
    * Use of at least one of the special characters, such as @, #, $
    * Restriction on passwords with words found in the User Name and Emaid ID
    * Should not match last three old passwords
    * Minimum character length should be 8
 * Multi-factor authentication policies (wherever applicable)
 * Admin Portal will only be accessed through Whitelisted IP Address
 * Authenticates Users accessing the portal
 * At Role Level : Configure Level of Auth

Default Policy:

 * What type of Authentication
 * Which would be compulsory in case of multi factor authentication
 * Minimum number of factors of Auth (Non-Bio/Bio)
 * Feature Specific authentication overrides Role Specific Behavior for Reset Password/Forgot User Name)


## 4. Notification (v1.5) (WIP) [**[↑]**](#table-of-contents)
### 4.1 Approval Notifications
### 4.2 Country Specific News/Notifications
## 5. Resource Management [**[↑]**](#table-of-contents)
### 5.1 Center Management 
Admin Portal allows an Administrator to manage Registration Centers the Country will have for taking Registrations of the Residents. Center management includes Viewing, Creating, Editing, Activating, Deactivating and Decommission of Centers. An Administrator should have the role of a Zonal Admin to do this. A Zonal Admin can manage only Centers under his/her administrative zone.

#### 5.1.1 View Center
The Admin portal allows Zonal Admin to view the list of all Registration Centers available in the jurisdiction of his/her administrative zone. The system does not fetch the details of Decommissioned Registration Centers but only Active and Inactive Centers. 
Admin portal UI shows the list of Registration Centers in only the country configured Primary Language. Besides the list view, an administrator can also view the detail of a Registration Center by clinking on a Center Name in the List view. This Detail view shows all the details of a Registration Center in all the country configured languages.

#### 5.1.2 Create Center
A Zonal Admin can create a Center by providing necessary mandatory details. A Center needs to be created in both configured Primary and Secondary languages. Although the Portal will allow creation of the Center in only primary language but will not allow activation of that Center until data for that Center is not updated for all the languages.
 
A Center is created with the following attributes: 
Center name, Center Type, Address, Latitude, Longitude, Location, Contact Phone, Contact Person, Working Hours, No. of Kiosk, Center Start Time, Center End Time, Lunch Start Time, Lunch End Time, Time Zone and Holiday Zone and Administrative Zone the Center belongs to. A Center can only be mapped to the Administrative Zonal at the lowest Zonal hierarchy.

While entering data through UI in multiple languages, the dropdown values and numeric values entered in primary language gets automatically captured in all language. But the text fields (e.g., Center Name) needs to be manually input in all the languages.
	
For more details, please refer to [**section**](FRS-Admin-Services#21-registration-center-type---createupdatedelete-) in Admin Service.

#### 5.1.3 Update Center [**[↑]**](#table-of-contents)
Once a Center is created, a Zonal admin can edit a Center later if required. The Update can include adding the details in another required language that were missed during creation of the Center or changing the details of a Center itself.  

#### 5.1.4 Activate/Deactivate/Decommission Center

A Zonal admin can Deactivate or Decommission a Center through the Admin Portal.

Deactivation refers to a temporary shut down while Decommission refers to a permanent shut down of the Center. Both Deactivated or Decommissioned Center does not show up in the Pre-Registration UI and thus no appointments can be booked for such Centers. 

Another difference between Deactivated and Decommissioned center is that a Deactivated center can later be Activated through Admin Portal after a period as required by the country. But a Decommissioned Center cannot be bought into commission again as decommission refers to a permanent shutdown. To reactivate such a Center (if decommissioned by mistake), the Admin must directly update the database through the backend scripts.

### 5.2 Machine Management [**[↑]**](#table-of-contents)
Admin Portal allows an Administrator to manage Machines the Country will use for taking Registration of the Residents. The definition of Machine is the device on which the registration Client is installed. Machine management includes Viewing, Creating, Editing, Activating, Deactivating and Decommission of Machines. An Administrator should have the role of a Zonal Admin to do this. A Zonal Admin can manage only Machines under his/her administrative zone.

#### 5.2.1 View Machine

The Admin portal allows Zonal Admin to view the list of all Machines available in the jurisdiction of his/her administrative zone. The system does not fetch the details of Decommissioned Machines but only Active and Inactive Machines. 
Admin portal UI shows the list of Machines in only the country configured Primary Language. Besides the list view, an Administrator can also view the detail of a Machine by clinking on a Machine Name in the List view. This Detail view shows all the details of a Machine in all the country configured languages.

#### 5.2.2 Create Machine
A Zonal Admin can create a Machine by providing necessary mandatory details. A Machine needs to be created in both configured Primary and Secondary languages. Although the Portal will allow creation of the Machine in only primary language but will not allow activation of that Machine until data for that Machine is not updated for all the languages. 

A Machine is created with the following attributes: 
Machine ID, Machine Name, Mac Address, Serial Number, Machine Spec ID and Administrative Zone the Machine belongs to.

While entering data through UI in multiple languages, the dropdown values and numeric values entered in primary language gets automatically captured in all language. But the text fields (e.g., Machine Name) needs to be manually input in all the languages. A Machine can be mapped to the Administrative Zone which is at the any Zonal hierarchy.

For more details, please refer to [**section**](FRS-Admin-Services#23-list-of-machine-types---create-) in Admin Service.

#### 5.2.3 Update Machine [**[↑]**](#table-of-contents)
Once a Machine is created, a Zonal admin can edit a Machine later if required. The Update can include adding the details in another required language that were missed during creation of the Machine or changing the details of a Machine itself. 

For more details, please refer to [**section**](FRS-Admin-Services#25-list-of-machines---createreadupdatedelete-) in Admin Service.

#### 5.2.4 Activate/Deactivate/Decommission Machine [**[↑]**](#table-of-contents)
A Zonal admin can Deactivate or Decommission a Machine through the Admin Portal.

Deactivation refers to a temporary shut down while Decommission refers to a permanent shut down of the Machine. 
Another difference between Deactivated and Decommissioned Machine is that a Deactivated Machine can later be Activated through Admin Portal after a period as required by the country. But a Decommissioned Machine cannot be bought into commission again as decommission refers to a permanent shutdown. To reactivate such a Machine (if decommissioned by mistake), the Admin must directly update the database through the backend scripts.

#### 5.2.5 Map/Un-map/Re-map Machine to a Center [**[↑]**](#table-of-contents)
Admin portal allows a Zonal Admin to map each Machine to a Center. This mapping specifies as to which Center can the Machine be used in. A Machine can only be mapped to a Center which belongs to the Machines’ Administrative Zone or a child Administrative Zone of the Machines’ Administrative Zone.

A Machine can later be un-mapped from the Center in cases where a Machine is needed to be moved to another Center. In such cases, the Machine will later need to be mapped to the new Center. In case the Machine is required to be mapped to a Registration Center outside the Administrative Zonal Restriction, the Administrative Zone of the Machine must be changed. 

### 5.3 Device Management [**[↑]**](#table-of-contents)
Admin Portal allows an Administrator to manage Devices the Country will use for taking Registration of the Residents. These includes Device for bio-metric capture (Fingerprint, Iris, Web camera etc.) Device management includes Viewing, Creating, Editing, Activating, Deactivating and Decommission of Devices. An Administrator should have the role of a Zonal Admin to do this. A Zonal Admin can manage only Devices under his/her administrative zone.

#### 5.3.1 View Device
The Admin portal allows Zonal Admin to view the list of all Devices available in the jurisdiction of his/her administrative zone. The system does not fetch the details of Decommissioned Devices but only Active and Inactive Devices. 
Admin portal UI shows the list of Devices in only the country configured Primary Language. Besides the list view, an Administrator can also view the detail of a Device by clinking on a Device Name in the List view. This Detail view shows all the details of a Device in all the country configured languages.

#### 5.3.2 Create Device
A Zonal Admin can create a Device by providing necessary mandatory details. A Device needs to be created in both configured Primary and Secondary languages. Although the Portal will allow creation of the Device in only primary language but will not allow activation of that Device until data for that Device is not updated for all the languages. 

A Device is created with the following attributes: 
Device ID, Device Name, Mac Address, Serial Number, Device Spec ID and Administrative Zone the Device belongs to. A Machine can be mapped to the Administrative Zone which is at the any Zonal hierarchy.

While entering data through UI in multiple languages, the dropdown values and numeric values entered in primary language gets automatically captured in all language. But the text fields (e.g., Device Name) needs to be manually input in all the languages..

#### 5.3.3 Update Device [**[↑]**](#table-of-contents)
Once a Device is created, a Zonal admin can edit a Device later if required. The Update can include adding the details in another required language that were missed during creation of the Device or changing the details of a Device itself. 

For more  details, please refer to [**section**](FRS-Admin-Services#27-list-of-devices---createreadupdatedelete-) in Admin Service.

#### 5.3.4 Activate/Deactivate/Decommission Device [**[↑]**](#table-of-contents)
A Zonal admin can Deactivate or Decommission a Device through the Admin Portal.

Deactivation refers to a temporary shut down while Decommission refers to a permanent shut down of the Device. 
Another difference between Deactivated and Decommissioned Device is that a Deactivated Device can later be Activated through Admin Portal after a period as required by the country. But a Decommissioned Device cannot be bought into commission again as decommission refers to a permanent shutdown. To reactivate such a Device (if decommissioned by mistake), the Admin must directly update the database through the back-end scripts.

#### 5.3.5 Map/Un-map/Re-map Device to a Registration Center [**[↑]**](#table-of-contents)
Admin portal allows a Zonal Admin to map each Device to a Center. This mapping specifies as to which Center can the Device be used in. A Device can only be mapped to a Center which belongs to the Devices’ Administrative Zone or a child Administrative Zone of the Devices’ Administrative Zone.

A Device can later be un-mapped from the Center in cases where a Device is needed to be moved to another Center. In such cases, the Device will later need to be mapped to the new Center. In case the Device is required to be mapped to a Registration Center outside the Administrative Zonal Restriction, the Administrative Zone of the Device must be changed.
Refer to section on more details of CRUD APIs used in above mentioned features

For more details, please refer to [link](FRS-Admin-Services#211-mappings-of-registration-center-and-device---createreaddelete-)

### 5.4 User Management(WIP) [**[↑]**](#table-of-contents)
#### 5.4.1 View User
MOSIP uses KeyCloak IAM for managing Users. KeyCloak also provides its native UI for managing Users. These Users include Registration Operators, Supervisors, Registration Admins, Zonal Admins etc. User management includes Viewing, Creating, Editing, Activating, Deactivating and Blacklisting of Users. An Administrator should have the role of a Zonal Admin to do this. A Zonal Admin can manage Users under his/her administrative zone only. 
#### 5.4.2 Create User
Using the portal, Zonal Admin/Central Admin will register the user (registration officer, supervisor) on portal by providing the following required details of the user:
 * User ID
 * First Name
 * Date of Birth
 * Gender
 * Contact Number
 * Email ID
 * Address
 * Activation Status
 * Blacklisted Status
 * Created by
 * Created Time Stamp
1. Zonal Admin will provide the user name as per approved standard of a country.
1. The system triggers an activation link to the newly created user after the user is successfully created. The activation link will expire after certain times (Expire time is configurable).
1. Once the user receives the link, he/she can set up the password as mentioned in the following:

 **  Procedure to set up User Password for  first time**: This feature to be checked with Aman

1. Once the user receives the link, he/she will generate the password by accessing the link.
2. User will provide his/her VID/UIN as required by the system.
3. The system allows the user to provide the registered mobile number and receives an OTP.
4. User will provide the OTP as received.
5. System will validate the user’s UIN, perform demographic authentication and check whether the user is child or adult. 
6. On successful validation, system allows user to generate the password.
7. User will provide password and confirm the password.
   The system validates the password based on the password policy (Password policy is configurable).
8. On successful validation, the system maps the RID with the user in IAM. If the user has multiple VID, the VID, which is 
   mapped by the system, is considered as the latest VID of user.
9. User receives the notification along with user name and link to the portal on password generation activities completed 
   successfully. 
10. User can start using his/her account by visiting to Reg. Client/Admin portal as applicable and logging in by providing 
    the user name and password (Multi-factor login supported).
11. If activation link expires (expiry time configurable), the system resends the link through a batch process.

#### 5.4.3 Update User
The portal allows its users (Central Admin, Central Approver, Zonal Admin, Zonal Approver, Registration Center Head, Registration Supervisor, and Registration Officer) to update the user details. The use will provide the User ID/User Name. The system validates the provided data and user's role. On successful validation, the system allows updating the required user details. When the user saves the updated user details, the system captures the date & time and user’s detail who has updated the user record.

If the user selects the Delete flag at the time of updating user’s record, the delete related information is updated when the user is updated. 

#### 5.4.4 Activate/Deactivate//Whitelist User [**[↑]**](#table-of-contents)
#### A. Activate User

The portal allows Zonal Admin to activate the user, who is already deactivated due to any reasons. When the user is created and approved, it is activated automatically. The Zonal Admin selects the user then all the users of that zone are displayed. The Zonal Admin can select a deactivated user or multiple deactivated users at a time and selects Activate option. The system validates user's role and activates the selected user(s). On successful validation, the system provides a notification.

#### B. Deactivate User

The portal allows Zonal Admin to deactivate the users, who are already active. The Zonal Admin selects the user and all the users of that zone are displayed. The Zonal Admin can select one active user or multiple active users at a time then selects the Deactivate option. The system validates user’s role, on successful validation, deactivates the selected user(s), and the system provides a notification.

#### C. Blacklist User

The portal allows the Zonal Admin to block or blacklist the user due to some reason (For example, number of failed login attempt). The system does not allows the blocked user to login or perform any kind of operation except raising the request to activate/whitelist.

Procedure to block/blacklist:

1. Zonal Admin has authorization to block or blacklist the users for any reason.
2. Once blocked/blacklisted, the system does not allow the users to login the system and notification related to 
   block/blacklist is sent to the respective user.
3. Due to some reason or If user exceeds numbers of attempt (number of attempt is configurable) to login, the system locks 
  the account and respective user will contact admin to unlock. 
4. User contacts Super Admin and requests to unblock/activate the account, the respective user will provide convincing 
   responses regarding blocking, the super admin will block/deactivate the active account.
5. Super Admin has authorization to reset the password and bio authentication of the supervisor on request by the 
  respective user.
6. The system will also send a link to the registered mobile number or email ID, so that the related user will reset the 
   password by visiting the link. For more details, please refer to [**Reset Password**](#23-reset-password-) 

#### 5.4.5 Map/Un-map/Re-map User to a Center [**[↑]**](#table-of-contents)
#### A. Map User to a Registration Center
The portal allows Zonal Admin to map users to the registration center by providing the User ID and registration center ID. The registration center must be under the Zonal Admin’s zone. The system validates the user ID, registration center ID and the user's role. On successful validation, the system maps the user to a registration center.

For more details, please please refer to [**section**](FRS-Admin-Services#26-mappings-of-registration-center-machine-and-user-mappings---createreaddelete-)

#### B. Un-map User to a Registration Center
The portal allows Zonal Admin to un-map users to the registration center by providing the User ID and registration center ID. The registration center must be under the Zonal Admin’s zone. The system validates the user ID, registration center ID and the user's role. On successful validation, the system un-maps the user to a registration center.Once user is un-mapped, he/she will be displayed in the available list of users.
#### C. Re-map User to a Registration Center
The portal allows Zonal Admin to re-map users to the registration center by providing the User ID and registration center ID. The registration center must be under the Zonal Admin’s zone. The system validates the user ID, registration center ID and the user's role. On successful validation, the system re-maps the user to a registration center.Once user is re-mapped, he/she will be not displayed in the available list of users. 

## 6. Master Data Management [**[↑]**](#table-of-contents)
### 6.1 View Master Data Types
The portal allows Zonal Admin to view the master data type. The master data types are configured by admin console. The system validates the user's role who raised the request to view the master data type and provides the master data type on successful validation. During the validation, if system does not validate the user's role, then provides an error notification.
### 6.2 View Master Data for Each Table (WIP)
The portal allows the Administrator to view the list of any Masterdata which are required by the country. The Administrator can access these list views by clicking on a type of Masterdata in the Masterdata Types Screen.
Each List view consumes the same UI template and follows following criteria:
1.	List view shows data of a Masterdata Type only in the country configured Primary Language. 
2.	An Administrator can access pagination functionalities on each list screens. Pagination functionality included selecting no. of rows to be displayed on the list view and options to jump to next or previous set of records. 
3.	An Administrator can sort the data by any column
4.	An Administrator can also perform certain actions from the list view which includes activating or deactivating a record in Masterdata.

Besides the list view, an Administrator can also view the details of a Masterdata record from the Masterdata List view. This can be done by clicking on record. The detail view shows all the details of a Masterdata record in multiple languages. The Administrator can access all the actions for a Master record which are available on the List view.

### 6.3 Manage Master Data [**[↑]**](#table-of-contents)
#### 6.3.1 Manage Document Types (Create, Update, Activate/Deactivate)
#### A. Create/Update Document Types

Using the portal, Zonal Admin will create the document type for his/her zone by providing the document type and document specification. The system validates the provided data and user's role. On successful validation, the system allows the Zonal Admin to create the document type. 

Procedure to create document type follows:


1. Zonal Admin will provide the following required details for the new document type:
 * Document Code
 * Document  Name
 * Language Code
 * Active (Boolean)
 * Created by
 * Created Date and Time
2. Zonal Admin creates the document type by providing all the required information related to the document type.
   Zonal Admin will register the document types  by importing CSV/XLS.

#### B. Activate Document types

The portal allows Zonal Admin to activate the document types, which are already deactivated due to any reasons. When the document type is created and approved, it is activated automatically. The Zonal Admin selects the document type then all the document types of that Zone are displayed. The Zonal Admin can select a deactivated document type or multiple deactivated document types at a time and selects Activate option. The system validates user's role and activates the selected document type(s). On successful validation, the system provides a notification.

#### C. Deactivate Document type

The portal allows Zonal Admin to deactivate the document type, which are already active. The Zonal Admin selects the document type and the all the document type of that zone are displayed. The Zonal Admin can select one active document type or multiple active document types at a time then selects the Deactivate option. The system validates user's role, on successful validation, deactivates the selected document type(s), and the system provides a notification.

#### D. Map Document Type to Document Category
The portal allows Zonal Admin to map the document type to the document category under his/her zone by providing Document Type Code, Document Category Code, Language Code, Active(Boolean), Created by,   and Created Date & Time. The system validates the provided data and user's roles. On successful validation, the system maps the document type with the selected document category and provides a notification. During the validation, if system does not validate the provided data and the user's role then provides a respective error notification.

#### E. Un-map Document Type to Document Category
The portal allows Zonal Admin to un-map the document type to the document category under his/her zone by providing Document Type Code, Document Category Code, Language Code, Active(Boolean), Created by,   and Created Date & Time. The system validates the provided data and user’s role. On successful validation, the system un-maps the document type with the selected document category and provides a notification. During the validation, if system does not validate the provided data and the allocated privileges of the user’s role, then throws provides an error notification.
#### F. Re-map Document Type to Document Category
The portal allows Zonal Admin to re-map the document type to the document category under his/her zone by providing Document Type Code, Document Category Code, Language Code, Active(Boolean), Created by,   and Created Date & Time. The system validates the provided data and user’s role. On successful validation, the system re-maps the document type with the selected document category and provides a notification. During the validation, if system does not validate the provided data and the allocated privileges of the user’s role, then throws provides an error notification.

#### 6.3.2 Manage Document Category to Document Mapping (WIP) (Create, Update, Activate/Deactivate) [**[↑]**](#table-of-contents)

#### 6.3.3 Manage Location Data (Create, Update, Activate/Deactivate) 
#### A. Create/Update Location Data
Using the portal, Zonal Admin will create/update the location data by providing location data and location specification. The system validates the provided data and the user's role. During validation, if system does not find the provided data or the respective user's role, then provides a respective error notification. On successful validation, the system allows the Zonal Admin to create and store the location data in the database. 

Following are the mandatory location data to be provided by Zonal Admin to create the location data:
 * Location Code
 * Location Name
 * Location Hierarchy Level 
 * Location Hierarchy Level Name
 * Language Code
 * Active (Boolean)
 * Created by
 * Created Date and Time
#### B. Activate Location data

The portal allows Zonal Admin to activate the location data, which are already deactivated due to any reasons. When the location data is created and approved, it is activated automatically. The Zonal Admin selects the location data then all the location data of that Zone are displayed. The Zonal Admin can select one deactivated location data or multiple deactivated location data at a time and selects Activate option. The system validates user's role and activates the selected location data(s). On successful validation, the system provides a notification.

#### C. Deactivate Location data

The portal allows Zonal Admin to deactivate the location data, which are already active. The Zonal Admin selects the location data and the all the location data of that zone are displayed. The Zonal Admin can select one active location data or multiple active location data at a time then selects the Deactivate option. The system validates user's role, on successful validation, deactivates the selected location data(s), and the system provides a notification.


#### 6.3.4 Manage Blacklisted Words (Create, Update, Activate, Deactivate)
#### B. Create/Update Blacklisted Word

Using the portal, only Zonal Admin will create/update the Blacklisted words by providing all the mandatory data and processes it. This is also configured through admin console. The blacklisted words database is created before updating the blacklisted words.  Zonal Admin can add only one word at a time and not more than one .  The system validates the user’s role and allows creating the words in the database after successful validation. When the blacklisted word related information is updated, the system captures the date & time and Zonal Admin detail who has updated the word. If the Zonal Admin selects the Delete flag, the information is updated when the blacklisted word is updated. 
During validation, if system does not find the provided data or the respective user’s role, then the system provides a respective error notification.   

#### C. Activate Blacklisted Word

The portal allows Zonal Admin to activate the blacklisted Word, which are already deactivated due to any reasons. When the blacklisted Word is created and approved, it is activated automatically. The Zonal Admin selects the blacklisted Word then all the blacklisted Words of that Zone are displayed. The Zonal Admin can select one deactivated blacklisted Word or multiple deactivated blacklisted Words at a time and selects Activate option. The system validates user’s role and activates the selected blacklisted Word(s). On successful validation, the system provides a notification.

#### D. Deactivate Blacklisted Word

The portal allows Zonal Admin to deactivate the blacklisted Word, which are already active . The Zonal Admin selects the blacklisted Word and the all the blacklisted Words of that zone are displayed. The Zonal Admin can select one active blacklisted Word or multiple active blacklisted Words at a time then selects the Deactivate option. The system validates user's roles, on successful validation, deactivates the selected blacklisted Word(s), and the system provides a notification.

#### E. Decommission Blacklisted Word

Decommissioning a blacklisted Word means removing the blacklisted Word from the zone permanently. The portal allows the Zonal Admin to decommission the blacklisted Word. The Zonal Admin can un-map the blacklisted Word associated with the registration center before decommissioning the blacklisted Word, but he/she can also decommission the blacklisted Word  without un-mapping the associated resources. In the situation, the associated resources are automatically un-mapped. The system validates user's role and decommissions the selected blacklisted Word(s). Once the blacklisted Word is decommissioned, it cannot be retrieved. On successful validation, the system provides a notification.

 
#### 6.3.5 Manage Registration Center Types (View) [**[↑]**](#table-of-contents)
The portal allows Zonal Admin to view the registration center types by selecting the master data. Once the user selects the master data types, all the r features associated with the master data are displayed. Again the user will select the Registration Center Type and the available registration center types are available to view.  The registration center types are configured through admin console. The system validates the user's role who raised the request to view the registration center types and provides the registration center types on successful validation. During the validation, if system fails to validate and authenticate the  user's role, then provides a respective error notification.
#### 6.3.6 Manage Machine Types (View)
The portal allows Zonal Admin to view the machine types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again the user will select the Machine Types and the available machine types are displayed.  The machine types are configured through admin console. The system validates the user's who raised the request to view the machine types and provides the machines types on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides an error notification.
#### 6.3.7 Manage Machine Specifications (View) [**[↑]**](#table-of-contents)
The portal allows Zonal Admin to view the machine specifications by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Machine Specification and the available machine specifications are displayed. The machine specifications are configured through admin console. The system validates user's role who raised the request to view the machine specification and provides the machines types on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides a respective error notification.
#### 6.3.8 Manage Device Types (View)
The portal allows Zonal Admin to view the device types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Device Types and the available Device Types are displayed.  Device Types are configured through admin console. The system validates the user's role who raised the request to view the device types and provides the device types on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides a respective error notification.
#### 6.3.9 Manage Device Specifications (View) [**[↑]**](#table-of-contents)
The portal allows Zonal Admin to view the device specifications by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Device Specification and the available device specifications are displayed. The device specifications are configured through admin console. The system validates the user's who raised the request to view the device specification and provides the device specification on successful validation. During the validation, if system fails to validate and authenticate user's role, then provides a respective error notification.
#### 6.3.10 Manage Individual Types (View)
The portal allows Zonal Admin to view the individual types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Individual Types and the available individual types are displayed. The individual types are configured through admin console. The system validates the user's role who raised the request to view the individual types and provides the individual types on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides a respective error notification.
#### 6.3.11 Manage Document Type to Document Category Mapping (View) [**[↑]**](#table-of-contents)
The portal allows Zonal Admin to view the document type to document category mapping by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Document Type to Document Category Mapping and the available document type to document mapping are displayed. The document type to document category mapping are configured through admin console. The system validates the user's role who raised the request to view the document type to document category mapping and provides the individual types on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides a respective error notification.

#### 6.3.12 Manage List of Holidays (View)
The portal allows Zonal Admin to view the list of holidays by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Lists of Holidays and the available lists of holidays are displayed. The lists of holidays are configured through admin console. The system validates the user's role who raised the request to view the lists of holidays and provides the lists of holiday on successful validation. During the validation, if system fails to validate and authenticate the user' role, then provides a respective error notification.
#### 6.3.13 Manage List of Templates (View) [**[↑]**](#table-of-contents)
The portal allows Zonal Admin to view the list of holidays by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Lists of Templates and the available lists of templates are displayed. The lists of templates are configured through admin console. The system validates the user's role who raised the request to view the lists of templates and provides the lists of templates on successful validation. During the validation, if system fails to validate and authenticate the  user's role, then provides a respective error notification.
#### 6.3.14 Manage List of Titles (View)
The portal allows Zonal Admin to view the list of titles by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Lists of Titles and the available lists of titles are displayed. The lists of titles are configured through admin console. The system validates the user's role who raised the request to view the lists of titles and provides the lists of titles on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides a respective error notification.
#### 6.3.15 Manage Gender Types (View) [**[↑]**](#table-of-contents)
The portal allows Zonal Admin to view the gender types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Gender Types and the available gender types are displayed. The gender types are configured through admin console. The system validates the user's role who raised the request to view the gender types and provides the gender types on successful validation. During the validation, if system fails to validate and authenticate the user's role, then provides a respective error notification.
## 7. Approval Process [**[↑]**](#table-of-contents)
### 7.1 Approval for Resource Creation
#### 7.1.1 Approval of Center 
Using the portal, Zonal Approver will approve the registered centers. The Zonal Admin who registered the center cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when the center is registered and this validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the center, the record will be available for the approver (approver is configurable) 
   for the approval.
1. Approver will approve/reject the center.
1. If approver does not approve/reject, the system sends a reminder notification (configurable) for the approval.

#### 7.1.2 Approval of Machine 
Using the portal, Zonal Approver will approve the registered machines. The Zonal Admin who registered the machines cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when the machine is registered and this validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the machines, the record will be available for the approver (approver is configurable) for 
   the approval.
1. Approver will approve/reject the device.
1. If approver does not approve/reject, the system sends a reminder notification (configurable) for the approval.

#### 7.1.3 Approval of Device
Using the portal, Zonal Approver will approve the registered devices. The Zonal Admin who registered the devices cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when the device is registered and this validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the devices, the record will be available for the approver (approver is configurable) for 
   the approval.
1. Approver will approve/reject the device.
1. If approver does not approve/reject, the system sends a reminder notification (configurable) for the approval.

#### 7.1.4 Approval of User
Using the portal, Zonal Approver will approve the created user on the portal. The Zonal Admin who created the users cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when user is created and validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the users (RO/Supervisor), the record will available for the approver (approver is configurable) for the approval.
1. Approver will approve the users within schedule time (Time is configurable).
1. If approver does not approve within the scheduled time, the system sends a reminder notification (configurable) for the approval.
The following functionalities are under WIP in the and to be updated once confirmed
a) Change the approver (what happens if we have only one zonal approver for that zone)
b) Auto-Approve
c) Reject
d) Escalation Mail
e) Reports

### 7.2 Approval for Master Data Creation (WIP)
## 8. UIN Activation/Deactivation [**[↑]**](#table-of-contents)
Using the portal, Zonal Admin will provide the UIN to activate/deactivate based on the request by the UIN holder for any reason. The system validates and provides the status (active/inactive) of UIN after successful validation.  If a UIN is deactivated, the respective VID (If created) will also be deactivated.
## 9. Packet Status Check (based on RID) (WIP) [**[↑]**](#table-of-contents)
## 10. Multi-language Support (WIP) [**[↑]**](#table-of-contents)
### 10.1 i18N
### 10.2 Implementation in English (Labels etc)
### 10.3 Language Specific Setup
## 11. Responsive UI (WIP) [**[↑]**](#table-of-contents)
## 12. MOSIP Platform Setup (WIP) [**[↑]**](#table-of-contents)
The system admin will set up platform data such as list of template types, list of rejection reason etc. through a CSV. 

For more details, please refer to
 [link](FRS-Admin-Services#113-list-of-template-types---create-)

[link](FRS-Admin-Services#19-list-of-rejection-reasons---createread-)

## 13. ID Definition Setup [**[↑]**](#table-of-contents)

The system admin will configure ID Definition. The configuration activity allows the country admin to mark attributes that formulate the id for a country. For example, demographic data fields and biometric data capture attributes.This is
configured through admin console.


### 13.1 ID Definition Validator
## 14. Configuration Setup (WIP) [**[↑]**](#table-of-contents)
## 15. Process Flow Setup (WIP) [**[↑]**](#table-of-contents)

### List of Configurable Parameters and Processes [**[↑]**](#table-of-contents)

1. Configurable Parameters

   [**Link to Configurable Parameters of Administrator Services**](/mosip/mosip-config/blob/master/config/admin.properties)

2. Configurable Processes 
* (Work in Progress) 
### Administrator Services API [**[↑]**](#table-of-contents)
* (Work in Progress) 


## Process View [**[↑]**](#table-of-contents)
* (Work in Progress) 