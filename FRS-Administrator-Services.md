## Table Of Content
- [1. Login](#1-login) _(ASR_FR_1)_
  * [1.1 Login](#11-login) _(ASR_FR_1.1)_
  * [1.2 Logout](#12-logout)
    * [1.2.1 Manual](#121-manual) _(ASR_FR_1.2)_
    * [1.2.2 Auto](#122-auto) _(ASR_FR_1.3)_
- [2. Account Management](#2-account-management) _(ASR_FR_2)_
  * [2.1 Edit Personal Details](#21-edit-personal-details) _(ASR_FR_2.1)_
  * [2.2 Change Password](#22-change-password) _(ASR_FR_2.2)_
  * [2.3 Reset Password](#23-reset-password) _(ASR_FR_2.3)_
  * [2.4 Forgot Username](#24-forgot-username) _(ASR_FR_2.4)_
  * [2.5 Account Unlock](#25-account-unlock) _(ASR_FR_2.5)_
- [3. Security Policy Configuration](#3-security-policy-configuration) _(ASR_FR_3)_
- [4. Notification (WIP)](#4-notification-wip-) _(ASR_FR_4)_
  * [4.1 Approval Notifications](#41-approval-notifications) _(ASR_FR_4.1)_
  * [4.2 Country Specific News/Notifications](#42-country-specific-newsnotifications) _(ASR_FR_4.2)_
- [5. Resource Management](#5-resource-management) _(ASR_FR_5)_
  * [5.1 Center Management](#51-center-management)
    * [5.1.1 View Center](#511-view-center) _(ASR_FR_5.1)_
    * [5.1.2 Create Center](#512-create-center) _(ASR_FR_5.2)_
    * [5.1.3 Update Center](#513-update-center) _(ASR_FR_5.3)_
    * [5.1.4 Activate/Deactivate/Decommission Center](#514-activate-fdeactivate-decommission-center) _(ASR_FR_5.4)_
  * [5.2 Machine Management](#52-machine-management)
    * [5.2.1 View Machine](#521-view-machine) _(ASR_FR_5.5)_
    * [5.2.2 Create Machine](#522-create-machine) _(ASR_FR_5.6)_
    * [5.2.3 Update Machine](#523-update-machine) _(ASR_FR_5.7)_
    * [5.2.4 Activate/Deactivate/Decommission Machine](#524-activatedeactivatedecommission-machine) _(ASR_FR_5.8)_
    * [5.2.5 Map/Un-map/Re-map Machine to a Center](#525-mapun-mapre-map-machine-to-a-center) _(ASR_FR_5.9)_
  * [5.3 Device Management](#53-device-management)
    * [5.3.1 View Device](#531-view-device) _(ASR_FR_5.10)_
    * [5.3.2 Create Device](#532-create-device) _(ASR_FR_5.11)_
    * [5.3.3 Update Device](#533-update-device) _(ASR_FR_5.12)_
    * [5.3.4 Activate/Deactivate/Decommission Device](#534-activatedeactivatedecommission-device) _(ASR_FR_5.13)_
    * [5.3.5 Map/Un-map/Re-map Device to a Center](#535-mapun-mapre-map-device-to-a-center) _(ASR_FR_5.14)_
  * [5.4 User Management](#54-user-management)
    * [5.4.1 View User](#541-view-user) _(ASR_FR_5.15)_
    * [5.4.2 Create User](#542-create-user) _(ASR_FR_5.16)_
    * [5.4.3 Activate/Deactivate/Blacklist/Whitelist User](#543-activatedeactivateblacklistwhitelist-user) _(ASR_FR_5.17)_
    * [5.4.4 Map/Un-map/Re-map User to a Center](#544-mapun-mapre-map-user-to-a-center) _(ASR_FR_5.18)_
- [6. Master Data Management](#6-master-data-management) _(ASR_FR_6)_
  * [6.1 View Master Data Types](#61-view-master-data-types) _(ASR_FR_6.1)_
  * [6.2 View Master data for each table](#62-view-master-data-for-each-table) _(ASR_FR_6.2)_
  * [6.3 Manage Master Data](#63-manage-master-data)
    * [6.3.1 Manage Document Type (Create, Update, Activate, Deactivate)](#631-manage-document-type-create-update-activate-deactivate)) _(ASR_FR_6.3)_
    * [6.3.2 Manage Document Category to Document Mapping (Create, Update, Activate, Deactivate)](#632-manage-document-category-to-document-mapping-create-update-activate-deactivate)) _(ASR_FR_6.4)_
    * [6.3.3 Manage Location Data (Create, Update, Activate, Deactivate)](#633-manage-location-data-create-update-activate-deactivate)) _(ASR_FR_6.5)_
    * [6.3.4 Manage Blacklisted Words (Create, Update, Activate, Deactivate)](#634-manage-blacklisted-words-create-update-activate-deactivate) _(ASR_FR_6.6)_
     * [6.3.5 Manage Registration Center Types (View)](#635-manage-registration-center-types-view) _(ASR_FR_6.7)_ 
     * [6.3.6 Manage Machine Types (View)](#636-manage-machine-types-view) _(ASR_FR_6.8)_ 
     * [6.3.7 Manage Machine Specifications (View)](#637-manage-machine-specifications-view) _(ASR_FR_6.9)_ 
     * [6.3.8 Manage Device Types (View)](#638-manage-device-types-view) _(ASR_FR_6.10)_ 
     * [6.3.9 Manage Device Specifications (View)](#639-manage-device-specifications-view) _(ASR_FR_6.11)_ 
     * [6.3.10 Manage Individual Types (View)](#6310-manage-individual-types-view) _(ASR_FR_6.12)_ 
     * [6.3.11 Manage Document Type to Document Category Mapping (View)](#6311-manage-document-type-to-document-category-mapping-view) _(ASR_FR_6.13)_ 
     * [6.3.12 Manage List of Holidays (View)](#6312-manage-list-of-holidays-view) _(ASR_FR_6.14)_ 
     * [6.3.13 Manage List of Templates (View)](#6313-manage-list-of-templates-view) _(ASR_FR_6.15)_ 
      * [6.3.14 Manage List of Titles (View)](#6314-manage-list-of-titles-view) _(ASR_FR_6.16)_ 
     * [6.3.15 Manage Gender Types (View)](#6315-manage-gender-types-view) _(ASR_FR_6.17)_ 
- [7. Approval Process](#7-approval-process) _(ASR_FR_7)_
  * [7.1 Approval for Resource Creation (WIP)](#71-approval-for-resource-creation-wip-)
    * [7.1.1 Center](#711-center) _(ASR_FR_7.1)_
    * [7.1.2 Machine](#712-machine) _(ASR_FR_7.2)_
    * [7.1.3 Device](#713-device) _(ASR_FR_7.3)_
    * [7.1.4 User](#714-user) _(ASR_FR_7.4)_
  * [7.2 Approval for Master Data Creation (WIP)](#72-approval-for-master-data-creation-wip) _(ASR_FR_7.5)_
- [8. UIN Activation/Deactivation](#8-uin-activationdeactivation) _(ASR_FR_8)_
- [9. Packet Status Check (based on RID)](#9-packet-status-check-based-on-rid) _(ASR_FR_9)_
- [10.Multi-language Support)](#10-multi-language-support) _(ASR_FR_10)_
    * [10.1 i18N](#101-i18n) _(ASR_FR_10.1)_
    * [10.2 Implementation in English (Labels etc)](#102-implementation-in-english-labels-etc) _(ASR_FR_10.2)_
    * [10.3 Language Specific Setup](#103-language-specific-setup) _(ASR_FR_10.3)_
- [11. Responsive UI](#11-responsive-ui) _(ASR_FR_11)
- [12. MOSIP Platform Setup](#12-mosip-platform-setup) _(ASR_FR_12)
- [13. ID Definition Setup](#13-id-definition-setup) _(ASR_FR_13)
    * [13.1 ID Definition Validator](#131-id-definition-validator) _(ASR_FR_13.1)_
- [14. Configuration Setup](#14-configuration-setup) _(ASR_FR_14)
- [15. Process Flow Setup](#15-process-flow-setup) _(ASR_FR_15)
## 1. Login
### 1.1 Login
MOSIP Admin portal will support single factor and multi factor login including biometrics. Admin will configure the login setting related to single factor or multi-factor based on the country.
MOSIP Admin Application allows the user to login to the portal to perform the following:
1. MOSIP Admin will login the portal with valid credentials (User Name and Password). Specific to country, the password is 
   configurable to single factor or multi factor.
2. MOSIP validates the credentials and allows admin to land in main page on successful validation.
3. Credentials are blocked after unsuccessful attempt of X times (number of attempt is configurable) login.
4. Once the credentials are blocked, only the relevant user or super admin can unblock the user. 
### 1.2 Logout
#### 1.2.1 Manual
MOSIP allows the user to log out from the active session.
User will perform the following to log out from MOSIP:
1. User will be in active session and on the main page.
2. Logout attributes should be always in active mood for the active session.
3. User performs logout actions from the main page.
4. The system verifies the active session and provides the logout related message within 350 milliseconds.

#### 1.2.2 Auto
MOSIP Admin Application provides the capability to auto-logout the user as configured. For example, if system becomes idle for sometimes (idle time is configurable), then user will be auto-logout. 
## 2. Account Management
### 2.1 Edit Personal Details
Using MOSIP, user will  manage his/her profile. Generally MOSIP users are Central Admin, Central Approver, Zonal Admin, Zonal Approver, Registration Center Head, Registration Supervisor, and Registration Officer.

Procedure to manage the profile follows:
1. User will provide the valid credential in the relevant portal to login.
2. The system validates the credentials and allows user to login after successful validation.
3. The system allows user to land on Home page.
4. The Home Page contains the permitted functionalities of the user and those functionalities are available in the main 
   page in active mode.
5. The system allows users to perform the profile management activities (updating user’s personal details and Account 
   Management).
On successful submission the updates, the system provides the notification about the updates. 

### 2.2 Change Password
Using MOSIP, users will change the password. Based on the country, single factor or multi-factor authentication will be configured. 
Procedure to follow to change the password:
1. User visits the Reg. Client Login Page or Admin Portal Login Page and raises a request for Change Password.
2. The system provides a facility to the user to change the password.
3. User provides the information related to Old Password, New Password and, Confirm New Password as the system required. 
   During the password creation, user should follow a password creation rule (combination of characters, special 
   character, and min and max length etc.) which is configurable.
4. On successful validation, the system provides a notification to the user as “You have changed the password 
   successfully.”

### 2.3 Reset Password
MOSIP allows users to reset the password. Based on the country, single factor or multi-factor authentication will be configured. If requested through Zonal Admin, then system performs only OTP authentication.
To reset the password, the user performs the following:

1. User visits to the Reg. Client Login page or Admin Portal Login Page and requests for Forgot Password.
2. The system allows user to provide the User Name.
3. The system checks the User Name and sends an OTP notification to the registered mobile number of this User Name.
4. User provides the OTP as received.
5. The system validates the provided OTP and successfully authenticates the user.
6. The system allows user to provide the Old Password, New Password, and Confirm New Password (Password policy is 
   configurable).
7. The system sends a notification to the user related to the password update status.

### 2.4 Forgot Username
Using MOSIP, user can retrieve the username. Based on the country, multi-factor authentication will be configured. 
To retrieve the user name, the user performs the following:

1. User visits the Reg. Client Login page or Admin Portal Login Page and requests for Forgot Password.
2. User provides the registered mobile number as require by the system.
3. The system validates the registered mobile number associated with the user and sends the User Name through an OTP 
   notification.
4. The system prompts to enter the registered mobile number.
5. Admin will enter the OTP as received.
6. System sends the user name through SMS notification to the concerned user.

### 2.5 Account Unlock
MOSIP allows Admin to unlock the account of other MOSIP users (Registration Officer/supervisor). Based on the country, multi-factor authentication will be configured. If request has been initiated through admin then only OTP authentication is active.

Procedure to unblock the account:

1. MOSIP user navigates to the login page of the portal and clicks “Unblock Account Page”.
2. User provides the registered mobile when the system requires.
3. User will enter the OTP as received
4. On successful validation, system sends SMS notification related to the unblocking of account.

## 3. Security Policy Configuration
## 4. Notification (v1.5) (WIP)
### 4.1 Approval Notifications
### 4.2 Country Specific News/Notifications
## 5. Resource Management
### 5.1 Center Management
#### 5.1.1 View Center
#### 5.1.2 Create Center
#### 5.1.3 Update Center
#### 5.1.4 Activate/Deactivate/Decommission Center
### 5.2 Machine Management
#### 5.2.1 View Machine
#### 5.2.2 Create Machine
#### 5.2.3 Update Machine
#### 5.2.4 Activate/Deactivate/Decommission Machine
#### 5.2.5 Map/Un-map/Re-map Machine to a Center
### 5.3 Device Management
#### 5.3.1 View Device
#### 5.3.2 Create Device
#### 5.3.3 Update Device
#### 5.3.4 Activate/Deactivate/Decommission Device
#### 5.3.5 Map/Un-map/Re-map Device to a Center
### 5.4 User Management
#### 5.4.1 View User
#### 5.4.2 Create User
#### 5.4.3 Activate/Deactivate/Blacklist/Whitelist User
#### 5.4.4 Map/Un-map/Re-map User to a Center
## 6. Master Data Management
### 6.1 View Master Data Types
### 6.2 View Master Data for Each Table
### 6.3 Manage Master Data
#### 6.3.1 Manage Document Type (Create, Update, Activate, Deactivate)
#### 6.3.2 Manage Document Category to Document Mapping (Create, Update, Activate, Deactivate)
#### 6.3.3 Manage Location Data (Create, Update, Activate, Deactivate) 
#### 6.3.4 Manage Blacklisted Words (Create, Update, Activate, Deactivate)
#### 6.3.5 Manage Registration Center Types (View)
#### 6.3.6 Manage Machine Types (View)
#### 6.3.7 Manage Machine Specifications (View)
#### 6.3.8 Manage Device Types (View)
#### 6.3.9 Manage Device Specifications (View)
#### 6.3.10 Manage Individual Types (View)
#### 6.3.11 Manage Document Type to Document Category Mapping (View)
#### 6.3.12 Manage List of Holidays (View)
#### 6.3.13 Manage List of Templates (View)
#### 6.3.14 Manage List of Titles (View)
#### 6.3.15 Manage Gender Types (View)
## 7. Approval Process
### 7.1 Approval for Resource Creation (WIP)
#### 7.1.1 Center 
#### 7.1.2 Machine 
#### 7.1.3 Device
#### 7.1.4 User
### 7.2 Approval for Master Data Creation (WIP)
## 8. UIN Activation/Deactivation
## 9. Packet Status Check (based on RID)
## 10. Multi-language Support
### 10.1 i18N
### 10.2 Implementation in English (Labels etc)
### 10.3 Language Specific Setup
## 11. Responsive UI
## 12. MOSIP Platform Setup
## 13. ID Definition Setup
### 13.1 ID Definition Validator
## 14. Configuration Setup
## 15. Process Flow Setup