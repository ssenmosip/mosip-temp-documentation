## Table Of Content
- [1. Login](#1-login-) _(ASR_FR_1)_
  * [1.1 Login](#11-login) _(ASR_FR_1.1)_
  * [1.2 Logout](#12-logout)
    * [1.2.1 Manual Logout](#121-manual-logout) _(ASR_FR_1.2)_
    * [1.2.2 Auto Logout](#122-auto-logout) _(ASR_FR_1.3)_
- [2. Account Management](#2-account-management-) _(ASR_FR_2)_
  * [2.1 Edit Personal Details](#21-edit-personal-details) _(ASR_FR_2.1)_
  * [2.2 Change Password](#22-change-password-) _(ASR_FR_2.2)_
  * [2.3 Reset Password](#23-reset-password-) _(ASR_FR_2.3)_
  * [2.4 Forgot Username](#24-forgot-username-) _(ASR_FR_2.4)_
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
    * [5.1.4 Activate/Deactivate/Decommission Center (WIP)](#514-activatedeactivatedecommission-center-wip-) _(ASR_FR_5.4)_
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
    * [5.3.4 Activate/Deactivate/Decommission Device (WIP)](#534-activatedeactivatedecommission-device-wip) _(ASR_FR_5.13)_
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
    * [6.3.1 Manage Document Type (Create, Update, Activate, Deactivate)](#631-manage-document-type-create-update-activate-deactivate)) _(ASR_FR_6.3)_
    * [6.3.2 Manage Document Category to Document Mapping (Create, Update, Activate, Deactivate)(WIP)](#632-manage-document-category-to-document-mapping-create-update-activate-deactivate-wip-) _(ASR_FR_6.4)_
    * [6.3.3 Manage Location Data (Create, Update, Activate, Deactivate)](#633-manage-location-data-create-update-activate-deactivate)) _(ASR_FR_6.5)_
    * [6.3.4 Manage Blacklisted Words (Create, Update, Activate, Deactivate)](#634-manage-blacklisted-words-create-update-activate-deactivate) _(ASR_FR_6.6)_
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
  * [7.1 Approval for Resource Creation (WIP)](#71-approval-for-resource-creation-wip-)
    * [7.1.1 Center](#711-center) _(ASR_FR_7.1)_
    * [7.1.2 Machine](#712-machine) _(ASR_FR_7.2)_
    * [7.1.3 Device](#713-device) _(ASR_FR_7.3)_
    * [7.1.4 User](#714-user) _(ASR_FR_7.4)_
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
## 1. Login [**[↑]**](#table-of-content)
### 1.1 Login
The user can login to the Admin Portal by providing their credential such as Username and Password. The system validates the provided credentials and the privileges of the user. On successful validation, the system allows user to proceed further. 

Note: Based on a country requirement, single factor or multi-factor credentials can be configured.

If X number (X number is configurable) of unsuccessful attempt is made for login, then user account will be blocked and a respective notification will be sent to the user. If the user account is blocked, the system allows the relevant user or super admin to unblock the user account. 

For more details, please refer to <Reset Password, and Forgot Password link to be provided here>

### 1.2 Logout
#### 1.2.1 Manual Logout
If a user wishes to logout of the Admin Portal, he/she can opt to select the Logout option. The system validates if user is in active session and provides the logout related notification on successful validation else the system provides the respective error notification (error notification is configurable and pre-defined).
#### 1.2.2 Auto Logout
If the user is inactive for X minutes (X is configurable), the system logs out the user automatically. In such case, the system will not save any user’s data.
## 2. Account Management [**[↑]**](#table-of-content)
### 2.1 Edit Personal Details
Using the system, user will  manage his/her profile. Generally, the system users are Central Admin, Central Approver, Zonal Admin, Zonal Approver, Registration Center Head, Registration Supervisor, and Registration Officer.
Procedure to manage the profile follows:
1. User will provide the valid credential in the relevant portal to login.
2. The system validates the credentials and allows user to login after successful validation.
3. The system allows user to land on Home page.
4. The Home Page contains the permitted functionalities of the user and those functionalities are available in the main 
   page in active mode.
5. The system allows users to perform the profile management activities (updating user’s personal details and Account 
   Management).
On successful submission the updates, the system provides the notification about the updates. 

### 2.2 Change Password [**[↑]**](#table-of-content)
The system allows user to change the password. Based on the country, single factor or multi-factor authentication will be configured. User performs the following to change the password:
1. User selects the option of Change Password.
1. The system allows user to land in Change Password page.
1. User provides the information related to Old Password, New Password and, Confirm New Password as the system required. The system validates and authenticates with the policy related to password creation/change policy and sends a notification related to the status of password changes.



### 2.3 Reset Password [**[↑]**](#table-of-content)
The system allows users to reset the password. Based on the country, single factor or multi-factor authentication will be configured. If requested through Zonal Admin, then system performs only OTP authentication.

To reset the password, the user performs the following:

1. User provides the User Name and Mobile number to reset the password. 
1. The system checks the User Name, Mobile number and sends an OTP notification to the registered mobile number on successful validation.
1. User provides the OTP as received.
1. The system validates the provided OTP and the security policy of reset password, successfully authenticates the user.
1. The system allows user to provide the Old Password, New Password, and Confirm New Password (Password policy is configurable).
1. The system sends a notification to the user related to the password reset status.


### 2.4 Forgot Username [**[↑]**](#table-of-content)
Using the system, user can retrieve the username. Based on the country, multi-factor authentication will be configured. User provides the registered mobile number by selecting the Forgot Password. The system validates the registered mobile number associated with the user. On successful validation, the system provides the User Name to the registered mobile number through an OTP notification else provides the respective error notification.

### 2.5 Account Unlock
The system allows user to unlock his/her locked account.  The user account is locked due to various reason such as multiple time of wrong entry of user name or and password. Based on the country, multi-factor authentication will be configured. If request has been initiated through admin then only OTP authentication is active.

Procedure to unlock the account:

1. User provides the User Name in the system.
1. The system validates and authenticates if the mobile number is registered against this user name.
1. On successful validation, the system provides the active link through notification. 
1. User accesses the provided link


## 3. Security Policy Configuration (WIP)[**[↑]**](#table-of-content)
## 4. Notification (v1.5) (WIP) [**[↑]**](#table-of-content)
### 4.1 Approval Notifications
### 4.2 Country Specific News/Notifications
## 5. Resource Management [**[↑]**](#table-of-content)
### 5.1 Center Management 
#### 5.1.1 View Center
The system allows  Zonal Admin to provide the name of the zone or registration center ID to view the active/inactive Registration Center available in the jurisdiction of his/her zone. The system does not fetch the details of de-commissioned registration centers. The system validates the provided data, privileges allocated to Zonal Admin, and on successful validation, provides the details of registration center else triggers the respective error notification (error notification are configurable and predefined).


#### 5.1.2 Create Center
Using the system, Zonal Admin will provide all the mandatory data (ID, Name, Type, and Zone). The system validates the provided data and the privileges allocated to Zonal Admin  if validated successfully; the system creates the Registration Center with types (for example, regular, handicapped friendly, mobile etc) else trigger a respective error message. 

 The registration centers are also created though the backend. For more details, please refer to <Link will be provided for backend registration center creation> 
	
For more details, please refer to [**section**](FRS-Admin-Services#21-registration-center-type---createupdatedelete-) in Admin Service.

#### 5.1.3 Update Center [**[↑]**](#table-of-content)
Using the system, Zonal Admin will search for the registration center to be updated, open it in edit mode and update the respective data as required.  The system validates the updated data, privileges allocated to Zonal Admin, and the the date and time stamp, if validated successfully; the system updates the data related to the registration center and provides an acknowledgement notification about the updates status else triggers a respective error message. 

#### 5.1.4 Activate/Deactivate/Decommission Center (WIP)

**A. Activate the Registration Center**

The System allows Zonal Admin to activate the registration centers, which are already deactivated due to any reasons. When the registration center is created and approved, it is activated automatically. The Zonal Admin selects registration center then all the registration centers are displayed. The Zonal Admin can select one deactivated center or multiple deactivated centers at a time and selects Activate option. The system validates Zonal Admin’s privileges and activates the selected center(s). On successful validation, the system provides a notification.

**B. Deactivate the Registration Center**

The System allows Zonal Admin to deactivate the registration centers, which are already deactivated due to any reasons. The Zonal Admin selects the registration center and the all the registration centers of that zone are displayed. The Zonal Admin can select one activate center or multiple active centers at a time then selects the Deactive option. The system validates Zonal Admin’s privileges, on successful validation, deactivates the selected center(s), and the system provides a notification.

**C.Decommission the Registration Center**

Decommissioning a center means removing the center from the zone permanently. The system allows the Zonal Admin to decommission the registration centers. The Zonal Admin can un-map the resources associated with the registration center before decommissioning but he/she can also decommission the center without un-mapping the associated resources. In the situation, the associated resources are automatically un-mapped. The system validates Zonal Admin’s privileges and decommissions the selected center(s). Once the center is decommissioned, it cannot be retrieved. On successful validation, the system provides a notification.

### 5.2 Machine Management [**[↑]**](#table-of-content)
#### 5.2.1 View Machine
The system allows Zonal Admin to view the machines by providing the registration center ID. The system validates the provided data, privileges of Zonal Admin. On successful validation, the system provides the list of machines details (ID, Name, Mac Address, Serial Number, IP Address, Registration Center ID etc…), which are mapped to the registration center. If Zonal Admin searches the machine without providing the registration center ID, then the system provides all the machine registered in the country.  During the validation of registration center ID and Zonal Admin's privileges, if the registration ID/Zonal Admin's privileges are not found, then the system triggers an error notification
#### 5.2.2 Create Machine
Using the system, Zonal Admin will register the machines for his/her zone. The machine cannot be used in zone, if it is not registered.

Procedure to register machines follows:
1. Zonal admin will select a Machine Type and Machine Specification for the new Machine.
1. Zonal admin will enter the following required details for the new machine:
 * Machine ID
 * Machine Name
 * Mac Address
 * Serial Number
 * IP Address
 * Machine Spec ID
 * Language Code
 * Active (Boolean)
 * Created by
 * Created Date and Time
1. Zonal Admin creates the machine by providing all the required information related to the machine.
Machines uniqueness will be maintained through machine’s serial number.

Zonal Admin will also register the machines by importing the CSV/XLS.
For more details, please refer to [**section**](FRS-Admin-Services#23-list-of-machine-types---create-) in Admin Service.
#### 5.2.3 Update Machine [**[↑]**](#table-of-content)
The system provides the capabilities for Zonal Admin to update the machine related details. When machine was registered if any wrong entry is made, that can be rectified.
Procedure to update the machine related details, the Zonal Admin will:
1. Zonal Admin provides the mandatory information (Machine ID, Machine Name, and Zon ID).
1. The system validates the provided data and privileges of zonal Admin. On successful validation, the system allows Zonal Admin to update the required details. For example, if a Machine has been moved to a new zone or accidentally assigned to a wrong zone.
1. When the machine related information is updated, the system captures the date, date & time, Zonal Admin details who has updated the machine.
1. If the Zonal Admin selects the Delete flag, the information is updated when the registration center is updated. 
For more details, please refer to [**section**](FRS-Admin-Services#25-list-of-machines---createreadupdatedelete-) in Admin Service.

#### 5.2.4 Activate/Deactivate/Decommission Machine (WIP) [**[↑]**](#table-of-content)
**A. Activate Machine**

The System allows Zonal Admin to activate the machine, which are already deactivated due to any reasons. When the machine is created and approved, it is activated automatically. The Zonal Admin selects the machine then all the machines of that Zone are displayed. The Zonal Admin can select one deactivated machine or multiple deactivated machines at a time and selects Activate option. The system validates Zonal Admin’s privileges and activates the selected machine(s). On successful validation, the system provides a notification.

**A. Deactivate Machine**

The System allows Zonal Admin to deactivate the machine, which are already deactivated due to any reasons. The Zonal Admin selects the machine and the all the machine of that zone are displayed. The Zonal Admin can select one active machine or multiple active machine at a time then selects the Deactivate option. The system validates Zonal Admin’s privileges, on successful validation, deactivates the selected machine(s), and the system provides a notification.

**C. Decommission  Machine**

Decommissioning a machine means removing the machine from the zone permanently. The system allows the Zonal Admin to decommission the machine. The Zonal Admin can un-map the machine associated with the registration center before decommissioning the machine, but he/she can also decommission the machine  without un-mapping the associated resources. In the situation, the associated resources are automatically un-mapped. The system validates Zonal Admin’s privileges and decommissions the selected machine(s). Once the machine is decommissioned, it cannot be retrieved. On successful validation, the system provides a notification.

#### 5.2.5 Map/Un-map/Re-map Machine to a Center [**[↑]**](#table-of-content)
The system allows Zonal Admin to map the machine to the registration center under his/her zone by providing Machine ID and Registration Center ID. The machine and the Registration Center must belong to Zonal Admin’s zone. The system validates the provided data, Zonal Admin’s privileges. On successful validation, The system maps that machine to the selected registration center and once the machine is mapped to the registration center, it is not displayed in the list of available machines until un-mapped. 

If the machine is not mapped with the registration center, it cannot be recognized by the system to perform any operation in that center. The system track the machine by serial number and other attributes of the machine. If the machine is already mapped with another registration center, Zonal Admin must un-map the machine first and then map to his/her registration center. Once the mapping is completed successfully, the system provides the notification. 
 
### 5.3 Device Management [**[↑]**](#table-of-content)
#### 5.3.1 View Device
The system allows Zonal Admin to view the devices by providing the registration center ID. The system validates the provided data, privileges of Zonal Admin. On successful validation, the system provides the list of devices details (ID, Name, Mac Address, Serial Number, IP Address, Registration Center ID etc…), which are mapped to the registration center. If Zonal Admin searches the devices` without providing the registration center ID, then the system provides all the devices registered in the country.  During the validation of registration center ID and Zonal Admins privileges, if the registration ID/Zonal Admin’s privileges are not found, then the system triggers an error notification.
#### 5.3.2 Create Device
Using the system, Zonal Admin will register the devices for his/her zone. The device cannot be used in zone, if it is not registered.

Procedure to register the device follows:

1. Zonal admin will select a Device Type and Device Specification for the new device.
1. Zonal admin will provide the following required details for the new device:
 * Device ID
 * Device Name
 * Mac Address
 * Serial Number
 * IP Address
 * Device Spec ID
 * Language Code
 * Active (Boolean)
 * Created by
 * Created Date and Time
1. Zonal Admin creates the device by providing all the required information related to the device.

Device uniqueness will be maintained through device’s serial number.

Zonal Admin will also register the machines by importing the CSV/XLS.

#### 5.3.3 Update Device [**[↑]**](#table-of-content)
The system provides the capabilities for Zonal Admin to update the device related details. At the time of creating the device, if any information is not entered correctly due to any reason, 
Procedure to update the devices related details, the Zonal Admin will:
1. Update the device details such as Serial Number and Mac-Address.
1. Update the zone of a device (If a device is being moved to a new zone or accidently assigned to a wrong zone).
1. The system does make the device visible to the Zonal Admin, if previously assigned to other zone.
1. Remove the mapping of the Center and device  (if already mapped to a Center of another zone).
1. Assign a machine to the new zone (In case of accidently assigning the wrong zone, Zonal Admin will contact with the Zonal admin of newly assigned zone to get the Machine re-assigned to the old zone).

For more  details, please refer to [**section**](FRS-Admin-Services#27-list-of-devices---createreadupdatedelete-) in Admin Service.

#### 5.3.4 Activate/Deactivate/Decommission Device [**[↑]**](#table-of-content)
A.**Activate Device**

The System allows Zonal Admin to activate the device, which are already deactivated due to any reasons. When the device is created and approved, it is activated automatically. The Zonal Admin selects the device then all the devices of that Zone are displayed. The Zonal Admin can select one deactivated device or multiple deactivated devices at a time and selects Activate option. The system validates Zonal Admin’s privileges and activates the selected device(s). On successful validation, the system provides a notification.

B. **Deactivate Device**

The System allows Zonal Admin to deactivate the device, which are already deactivated due to any reasons. The Zonal Admin selects the device and the all the device of that zone are displayed. The Zonal Admin can select one active device or multiple active devices at a time then selects the Deactivate option. The system validates Zonal Admin’s privileges, on successful validation, deactivates the selected device(s), and the system provides a notification.

C.**Decommission Device**

Decommissioning a device means removing the device from the zone permanently. The system allows the Zonal Admin to decommission the device. The Zonal Admin can un-map the device associated with the registration center before decommissioning the device, but he/she can also decommission the device  without un-mapping the associated resources. In the situation, the associated resources are automatically un-mapped. The system validates Zonal Admin’s privileges and decommissions the selected device(s). Once the device is decommissioned, it cannot be retrieved. On successful validation, the system provides a notification.

#### 5.3.5 Map/Un-map/Re-map Device to a Center [**[↑]**](#table-of-content)
The system allows Zonal Admin to map the devices to the registration center by providing the Device ID and Registration Center ID. The registration center must belong to Zonal Admin’s  zone. The system validates the provide data and privileges of Zonal Admin. On successful validation, The system maps that device to the selected registration center and once the device is mapped to the registration center, it is not displayed in the list of available devices until un-mapped. 

If the device is not mapped with the registration center, it cannot be recognized by the system to perform any operation in that center. The system track the device by serial number and other attributes of the device. If the device is already mapped with another registration center, Zonal Admin must un-map the device first and then map to his/her registration center. Once the mapping is completed successfully, the system provides the notification. 


### 5.4 User Management [**[↑]**](#table-of-content)
#### 5.4.1 View User
The system allows Zonal Admin to view the list of users by providing the registration center ID. The system validates the provided data, the privileges allocated to user and provides user’s details (ID, Name, Last Name, Role, Registration Center ID, Date of Birth, Gender, Contact Number, Email ID etc…) already mapped to the specified registration center on successful validation.
#### 5.4.2 Create User
Using the system, Zonal Admin/Central Admin will register the user (registration officer, supervisor) on portal by providing the following required details of the user:
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
1. Zonal Admin will provide the username as per approved standard of a country.
1. The system triggers an activation link to the newly created user after the user is successfully created. The activation link will 
    expire after certain times (Expire time is configurable).
1. Once the user receives the link, he/she can set up the password as mentioned in the following:

 **  Procedure to set up User Password for  first time**: This featre to be checked with Aman

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
9. User receives the notification along with username and link to the portal on password generation activities completed 
   successfully. 
10. User can start using his/her account by visiting to Reg. Client/Admin portal as applicable and logging in by providing 
    the username and password (Multi-factor login supported).
11. If activation link expires (expiry time configurable), the system resends the link through a batch process.

#### 5.4.3 Update User
The system allows its users (Central Admin, Central Approver, Zonal Admin, Zonal Approver, Registration Center Head, Registration Supervisor, and Registration Officer) to update the user details. The use will provide the User ID/User Name. The system validates the provided data and privileges of user. On successful validation, the system allows updating the required user details. When the user saves the updated user details, the system captures the date & time and user’s detail who has updated the user record.

If the user selects the Delete flag at the time of updating user’s record, the delete related information is updated when the user is updated. 

#### 5.4.4 Activate/Deactivate//Whitelist User [**[↑]**](#table-of-content)
A. **Activate User**

The system allows Zonal Admin to activate the user, who is already deactivated due to any reasons. When the user is created and approved, it is activated automatically. The Zonal Admin selects the user then all the users of that Zone are displayed. The Zonal Admin can select one deactivated user or multiple deactivated users at a time and selects Activate option. The system validates Zonal Admin’s privileges and activates the selected user(s). On successful validation, the system provides a notification.

B. **Deactivate User**

The System allows Zonal Admin to deactivate the user, which are already deactivated due to any reasons. The Zonal Admin selects the user and the all the users of that zone are displayed. The Zonal Admin can select one active user or multiple active users at a time then selects the Deactivate option. The system validates Zonal Admin’s privileges, on successful validation, deactivates the selected user(s), and the system provides a notification.

C. **Blacklist User**

The system allows the Zonal Admin to block or blacklist the user due to some reason (For example, number of failed login attempt). The system does not allows the blocked user to login or perform any kind of operation except raising the request to activate/whitelist.

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

#### 5.4.5 Map/Un-map/Re-map User to a Center [**[↑]**](#table-of-content)
The system allows Zonal Admin to map/un-map/re-map the users with the registration center by providing the User ID and registration center ID. The registration center must be under the Zonal Admin’s zone. The system validates the user ID, registration center ID and the privileges of the Zonal Admin and on successful validation, provides the capability to map/un-map-re-map the user to the registration.

For more details, please please refer to [**section**](FRS-Admin-Services#26-mappings-of-registration-center-machine-and-user-mappings---createreaddelete-)
## 6. Master Data Management [**[↑]**](#table-of-content)
### 6.1 View Master Data Types
The system allows Zonal Admin to view the master data type. The master data types are configured by the backend process. The system validates the privileges of Zonal Admin who raised the request to view the master data type and provides the master data type on successful validation. During the validation, if system does not validate the allocated privileges to the user, then throws an error notification.
### 6.2 View Master Data for Each Table (WIP)
### 6.3 Manage Master Data [**[↑]**](#table-of-content)
#### 6.3.1 Manage Document Type (Create, Update, Activate/Deactivate)
A. **Create/Update Document Type**

Using the system, Zonal Admin will create the document type for his/her zone by providing the document type and document specification. The system validates the provided data and the privileges of Zonal Admin. On successful validation, the system allows the Zonal Admin to create the document type. 

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

B. **Activate the Document types**

The System allows Zonal Admin to activate the document types, which are already deactivated due to any reasons. When the document type is created and approved, it is activated automatically. The Zonal Admin selects the document type then all the document types of that Zone are displayed. The Zonal Admin can select one deactivated document type or multiple deactivated document types at a time and selects Activate option. The system validates Zonal Admin’s privileges and activates the selected document type(s). On successful validation, the system provides a notification.

C. **Deactivate the Document type**

The System allows Zonal Admin to deactivate the document type, which are already deactivated due to any reasons. The Zonal Admin selects the document type and the all the document type of that zone are displayed. The Zonal Admin can select one active document type or multiple active document type at a time then selects the Deactivate option. The system validates Zonal Admin’s privileges, on successful validation, deactivates the selected document type(s), and the system provides a notification.

D. **Map/un-Map-Re-map Document Type to Document Category**

The system allows Zonal Admin to map the document type to the document category under his/her zone by providing Document Type Code, Document Category Code, Language Code, Active(Boolean), Created by,   and Created Date & Time. The system validates the provided data, Zonal Admin’s privileges. On successful validation, the system maps the document type with the selected document category and provides a notification. During the validation, if system does not validate the provided data and the allocated privileges of the user, then throws an error notification.

#### 6.3.2 Manage Document Category to Document Mapping (Create, Update, Activate/Deactivate) [**[↑]**](#table-of-content)
#### 6.3.3 Manage Location Data (Create, Update, Activate/Deactivate) 
A. **Create/Update Location Data**
Using the system, Zonal Admin will create/update the location data by providing location data and location specification. The system validates the provided data and the privileges of Zonal Admin. During validation, if system does not find the provided data or the respective Zonal Admin’s privileges, then throws an error notification On successful validation, the system allows the Zonal Admin to create and store the location data in the database. 

Following are the mandatory location data to be provided by Zonal Admin to create the location data:
 * Location Code
 * Location Name
 * Location Hierarchy Level 
 * Location Hierarchy Level Name
 * Language Code
 * Active (Boolean)
 * Created by
 * Created Date and Time


#### 6.3.4 Manage Blacklisted Words (Create, Update, Activate, Deactivate)
A. **Create/Update Blacklisted Word**

Using the system, only Zonal Admin will create/update the Blacklisted words by providing all the mandatory data and processes it. This is also configured as a backend process. The blacklisted words database is created before updating the blacklisted words.  Zonal Admin can add only one word at a time and not more than one .  The system validates the user’s privileges and allows creating the words in the database after successful validation. When the blacklisted word related information is updated, the system captures the date & time and Zonal Admin detail who has updated the word. If the Zonal Admin selects the Delete flag, the information is updated when the blacklisted word is updated. 
During validation, if system does not find the provided data or the respective user’s privileges, then the system provides an respective error notification.   

B. **Activate the Blacklisted Word**

The System allows Zonal Admin to activate the blacklisted Word, which are already deactivated due to any reasons. When the blacklisted Word is created and approved, it is activated automatically. The Zonal Admin selects the blacklisted Word then all the blacklisted Words of that Zone are displayed. The Zonal Admin can select one deactivated blacklisted Word or multiple deactivated blacklisted Words at a time and selects Activate option. The system validates Zonal Admin’s privileges and activates the selected blacklisted Word(s). On successful validation, the system provides a notification.

C. **Deactivate the Blacklisted Word**

The System allows Zonal Admin to deactivate the blacklisted Word, which are already deactivated due to any reasons. The Zonal Admin selects the blacklisted Word and the all the blacklisted Word of that zone are displayed. The Zonal Admin can select one active blacklisted Word or multiple active blacklisted Words at a time then selects the Deactivate option. The system validates Zonal Admin’s privileges, on successful validation, deactivates the selected blacklisted Word(s), and the system provides a notification.

D. **Decommission the Blacklisted Word**

Decommissioning a blacklisted Word means removing the blacklisted Word from the zone permanently. The system allows the Zonal Admin to decommission the blacklisted Word. The Zonal Admin can un-map the blacklisted Word associated with the registration center before decommissioning the blacklisted Word, but he/she can also decommission the blacklisted Word  without un-mapping the associated resources. In the situation, the associated resources are automatically un-mapped. The system validates Zonal Admin’s privileges and decommissions the selected blacklisted Word(s). Once the blacklisted Word is decommissioned, it cannot be retrieved. On successful validation, the system provides a notification.

 
#### 6.3.5 Manage Registration Center Types (View) [**[↑]**](#table-of-content)
The system allows Zonal Admin to view the registration center types by selecting the master data. Once the user selects the master data types, all the r features associated with the master data are displayed. Again the user will select the Registration Center Type and the available registration center types are available to view.  The registration center types are configured in the backend process. The system validates the privileges of user who raised the request to view the registration center types and provides the registration center types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.6 Manage Machine Types (View)
The system allows Zonal Admin to view the machine types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again the user will select the Machine Types and the available machine types are displayed.  The machine types are configured in the backend process. The system validates the privileges of user who raised the request to view the machine types and provides the machines types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.7 Manage Machine Specifications (View) [**[↑]**](#table-of-content)
The system allows Zonal Admin to view the machine specifications by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Machine Specification and the available machine specifications are displayed. The machine specifications are configured in the backend process. The system validates the privileges of user who raised the request to view the machine specification and provides the machines types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.8 Manage Device Types (View)
The system allows Zonal Admin to view the device types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Device Types and the available Device Types are displayed.  Device Types are configured in the backend process. The system validates the privileges of user who raised the request to view the device types and provides the device types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.9 Manage Device Specifications (View) [**[↑]**](#table-of-content)
The system allows Zonal Admin to view the device specifications by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Device Specification and the available device specifications are displayed. The device specifications are configured in the backend process. The system validates the privileges of user who raised the request to view the device specification and provides the device specification on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.10 Manage Individual Types (View)
The system allows Zonal Admin to view the individual types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Individual Types and the available individual types are displayed. The individual types are configured in the backend process. The system validates the privileges of user who raised the request to view the individual types and provides the individual types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.11 Manage Document Type to Document Category Mapping (View) [**[↑]**](#table-of-content)
The system allows Zonal Admin to view the document type to document category mapping by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Document Type to Document Category Mapping and the available document type to document mapping are displayed. The document type to document category mapping are configured in the backend process. The system validates the privileges of user who raised the request to view the document type to document category mapping and provides the individual types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.

#### 6.3.12 Manage List of Holidays (View)
The system allows Zonal Admin to view the list of holidays by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Lists of Holidays and the available lists of holidays are displayed. The lists of holidays are configured in the backend process. The system validates the privileges of user who raised the request to view the lists of holidays and provides the lists of holiday on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.13 Manage List of Templates (View) [**[↑]**](#table-of-content)
The system allows Zonal Admin to view the list of holidays by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Lists of Templates and the available lists of templates are displayed. The lists of templates are configured in the backend process. The system validates the privileges of user who raised the request to view the lists of templates and provides the lists of templates on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.14 Manage List of Titles (View)
The system allows Zonal Admin to view the list of titles by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Lists of Titles and the available lists of titles are displayed. The lists of titles are configured in the backend process. The system validates the privileges of user who raised the request to view the lists of titles and provides the lists of titles on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
#### 6.3.15 Manage Gender Types (View) [**[↑]**](#table-of-content)
The system allows Zonal Admin to view the gender types by selecting the master data types. Once the user selects the master data types, all the features associated with the master data types are displayed. Again, the user will select the Gender Types and the available gender types are displayed. The gender types are configured in the backend process. The system validates the privileges of user who raised the request to view the gender types and provides the gender types on successful validation. During the validation, if system fails to validate and authenticate the allocated privileges of the user, then throws an error notification.
## 7. Approval Process [**[↑]**](#table-of-content)
### 7.1 Approval for Resource Creation (WIP)
#### 7.1.1 Center 
Using the system, Zonal Approver will approve the registered centers. The Zonal Admin who registered the center cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when the center is registered and this validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the center, the record will be available for the approver (approver is configurable) 
   for the approval.
1. Approver will approve/reject the center.
1. If approver does not approve/reject, the system sends a reminder notification (configurable) for the approval.

#### 7.1.2 Machine 
Using the system, Zonal Approver will approve the registered machines. The Zonal Admin who registered the machines cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when the machine is registered and this validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the machines, the record will be available for the approver (approver is configurable) for 
   the approval.
1. Approver will approve/reject the device.
1. If approver does not approve/reject, the system sends a reminder notification (configurable) for the approval.

#### 7.1.3 Device
Using the system, Zonal Approver will approve the registered devices. The Zonal Admin who registered the devices cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when the device is registered and this validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the devices, the record will be available for the approver (approver is configurable) for 
   the approval.
1. Approver will approve/reject the device.
1. If approver does not approve/reject, the system sends a reminder notification (configurable) for the approval.

#### 7.1.4 User
Using the system, Zonal Approver will approve the created user on the portal. The Zonal Admin who created the users cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when user is created and validation does not applicable for updates. 
The approver will follow the following procedure:
1. Once the Zonal Admin creates the users (RO/Supervisor), the record will available for the approver (approver is configurable) for the approval.
1. Approver will approve the users within schedule time (Time is configurable).
1. If approver does not approve within the scheduled time, the system sends a reminder notification (configurable) for the approval.
<The following functionalities are under WIP in the and to be updated once confirmed>
a) Change the approver (what happens if we have only one zonal approver for that zone)
b) Auto-Approve
c) Reject
d) Escalation Mail
e) Reports

### 7.2 Approval for Master Data Creation (WIP)
## 8. UIN Activation/Deactivation [**[↑]**](#table-of-content)
Using the system, Zonal Admin will provide the UIN to activate/deactivate based on the request by the UIN holder for any reason. The system validates and provides the status (active/Inactive) of UIN after successful validation.  If a UIN is deactivated, the respective VID (If created) will also be deactivated.
## 9. Packet Status Check (based on RID) (WIP) [**[↑]**](#table-of-content)
## 10. Multi-language Support (WIP) [**[↑]**](#table-of-content)
### 10.1 i18N
### 10.2 Implementation in English (Labels etc)
### 10.3 Language Specific Setup
## 11. Responsive UI (WIP) [**[↑]**](#table-of-content)
## 12. MOSIP Platform Setup (WIP) [**[↑]**](#table-of-content)
The system admin will set up platform data such as list of template types, list of rejection reason etc. through a CSV. 

For more details, please refer to
 https://github.com/mosip/mosip/wiki/FRS-Admin-Services#113-list-of-template-types---create-

https://github.com/mosip/mosip/wiki/FRS-Admin-Services#19-list-of-rejection-reasons---createread-

## 13. ID Definition Setup [**[↑]**](#table-of-content)

The system admin should be able to set up ID Definition. Setup activity allows the country admin to mark attributes that formulate the id for a country. For example, demographic data fields and biometric data capture attributes.

Configured through backend.


### 13.1 ID Definition Validator
## 14. Configuration Setup (WIP) [**[↑]**](#table-of-content)
## 15. Process Flow Setup (WIP) [**[↑]**](#table-of-content)