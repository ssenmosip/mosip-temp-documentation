## Table of Contents
[Admin Services](#admin-services) 
-  [1. MOSIP Platform Setup](#1-mosip-platform-setup)
-  [2. ID Definition Setup](#2-id-definition-setup)
-  [3. ID Definition Validator](#3-id-definition-validator)
-  [4. Configuration Setup](#4-configuration-setup) 
      * [4.1 Initial Setup](#41-initial-setup) _(ASR_FR_4.1)_
      * [4.2 Configuration Validator](#42-configuration-validator) _(ASR_FR_4.2)_ 
      * [4.3 Update](#43-Update) _(ASR_FR_4.3)
      * [4.4 View Configurations](#44-view-configurations) _(ASR_FR_4.4)
-  [5. Process Flow Setup](#5-process-flow-setup)
      * [5.1 Initial Setup-Backend](#51-initial-setup-backend) _(ASR_FR_5.1)
      * [5.2 Initial Setup-UI](#52-initial-setup-ui) _(ASR_FR_5.2)
      * [5.3 Process Flow Configuration Validator](#53-process-flow-configuration-validator) _(ASR_FR_5.3)
      * [5.4 Update-Backend](#54-update-backend) _(ASR_FR_5.4)
      * [5.5 View-UI](#54-view-ui) _(ASR_FR_5.5)
-  [6. Master Data Setu](#6-master-data-setup)
      * [6.1 Creation-Initial Setup-Backend](#61-creation-initial-setup-backend) _(ASR_FR_6.1)

          [6.1.1 Creation-Subsequent additions-UI](#611-creation-subsequent-additions-ui) _(ASR_FR_6.1.1)
      * [6.2 View-UI](#62-view-ui) _(ASR_FR_6.2)
      * [6.3 List to make Updates-Activate/Deactivate-UI](#63-list-to-make-updates-activate-deactivate-ui) _(ASR_FR_6.3)
      * [6.4 Updates-Incremental Data Updates-UI](#64-updates-incremental-data-updates-ui) _(ASR_FR_6.5)
      * [6.5 View-UI](#66-view-ui) _(ASR_FR_6.5)
-  [7. Navigation](#7-Navigation) 
     * [7.1 Login-API-UI](#71-login-api-ui) _(ASR_FR_7.1)
     * [7.2 Logout-UI](#72-logout-ui) _(ASR_FR_7.2)
     * [7.3 Auto-Logout-UI](#73-Auto-logout-ui) _(ASR_FR_7.3)
     * [7.4 Home Page Dashboard UI](#74-home-page-dashboard-ui) _(ASR_FR_7.4)
     * [7.5 Profile Management-UI](#75-profile-management-ui) _(ASR_FR_7.5)

-  [8. User Management](#8-user-management)
      * [8.1 User Registration](#81-uswer-registration) _(ASR_FR_8.1)
-  [9. Account Management](#9-account-management)
-  [10. Asset Management](#10-asset-management)
-  [11. Security Policy Configuration-Backend](#11-security-policy-configuration-backend)
-  [12. UIN Activation-UI](#12-uin-activation-ui)
# Admin Services
# 1. MOSIP Platform Setup [**[↑]**](#table-of-content)
MOSIP Admin should be able to set up platform data such as list of template types, list of rejection reason etc. through a CSV. 

 For more information about platform data setup, refer 
 https://github.com/mosip/mosip/wiki/FRS-Admin-Services#113-list-of-template-types---create-

 https://github.com/mosip/mosip/wiki/FRS-Admin-Services#19-list-of-rejection-reasons---createread-

# 2. ID Definition Setup [**[↑]**](#table-of-content)
MOSIP Admin should be able to set up ID Definition. Setup activity allows the country admin to mark attributes that formulate the id for a country. For example, demographic data fields and biometric data capture attributes.
Configured through backend.

# 3. ID Definition Validator [**[↑]**](#table-of-content)
Configured through backend
# 4. Configuration Setup [**[↑]**](#table-of-content)
Configured through backend
## 4.1 Initial Setup
## 4.2 Configuration Validator
## 4.3 Update
## 4.4 View Configurations
# 5. Process Flow Setup [**[↑]**](#table-of-content)
Configured through backend process.
## 5.1 Initial Setup-Backend
## 5.2 Initial Setup-UI
## 5.3 Process Flow Configuration Validator
## 5.4 Update-Backend
## 5.5 View-UI
# 6. Master Data Setup [**[↑]**](#table-of-content)
## 6.1 Creation-Initial Setup-Backend
For more information about MDM creation, refer 
https://github.com/mosip/mosip/wiki/FRS-Admin-Services#1-master-data-management

### 6.1.1 Creation-Subsequent additions-UI
## 6.2 View-UI
## 6.3 List to make Updates-Activate/Deactivate-UI
## 6.4 List to make Updates-Activate/Deactivate-UI-TBD
## 6.5 Updates - Incremental data updates-UI
# 7. Navigation [**[↑]**](#table-of-content)
## 7.1 Login-API/UI

MOSIP Admin portal will support single factor and multi factor login including biometrics. Admin will configure the login setting related to single factor or multi-factor based on the country.
MOSIP Admin Application allows the user to login to the portal to perform the following:
1. MOSIP Admin will login the portal with valid credentials (User Name and Password). Specific to country, the password is 
   configurable to single factor or multi factor.
2. MOSIP validates the credentials and allows admin to land in main page on successful validation.
3. Credentials are blocked after unsuccessful attempt of X times (number of attempt is configurable) login.
4. Once the credentials are blocked, only the relevant user or super admin can unblock the user. Refer to section 9 Forgot 
   Password.

## 7.2 Logout-UI
MOSIP allows the user to log out from the active session.
User will perform the following to log out from MOSIP:

1. User will be in active session and on the main page.
2. Logout attributes should be always in active mood for the active session.
3. User performs logout actions from the main page.
4. The system verifies the active session and provides the logout related message within 350 milliseconds.

## 7.3 Auto-Logout-UI 
MOSIP Admin Application provides the capability to auto-logout the user as configured. For example, if system becomes idle for sometimes (idle time is configurable), then user will be auto-logout. 

## 7.4 Home Page/Dashboard-UI
MOSIP allows user to view the Home Page by following the given procedure:
1. Admin will provides the valid credentials in the relevant portal to login.
2. The system validates the credentials and allows user to login after successful validation.
3. The system allows user to land on Home page.
4. The Home Page contains the permitted functionalities to the user and those functionalities are available in main page 
   in active mode.

## 7.5 Profile Management-UI
Using MOSIP, user will be able to manage his/her profile.
Procedure to manage the profile follows:

1. User will provide the valid credential in the relevant portal to login.
2. The system validates the credentials and allows user to login after successful validation.
3. The system allows user to land on Home page.
4. The Home Page contains the permitted functionalities to the user and those functionalities are available in the main 
   page in active mode.
5. The system allows users to perform the profile management activities (updating user’s personal details and Account 
   Management).

# 8. User Management [**[↑]**](#table-of-content)
## 8.1 User Registration
Using MOSIP, Zonal Admin will register the users (registration officer, supervisor) on portal by providing the following details of the user:
1. Zonal Admin will provide the following personal details of user:
      * First Name
      * Last Name
      * Contact Number
      * Email ID
      * Date of Birth
      * VID
2. Zonal Admin will provide the username as per approved standard of a country.
3. Zonal Admin will provide activation link to the user along with username, mobile number and email ID.

**Procedure to set up User Password follows:**
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
10.User can start using his/her account by visiting to Reg. Client/Admin portal as applicable and logging in by providing 
   the username and password (Multi-factor login supported).
11.If activation link expires (expiry time configurable), the system resends the link through a batch process.


## 8.2 User Registration Approval
Using MOSIP, Zonal Approver will approve the created user on the portal. The Zonal Admin who created the users cannot be the approver. The creator and the approver must not be same person. The system validates the creator and approver for the first time when user is created and validation does not applicable for updates.
The approver will follow the following procedure: 
1. Once the Zonal Admin creates the users (RO/Supervisor), the record will available for the approver (approver is 
   configurable) for the approval.
2. Approver will approve the users within schedule time (Time is configurable).
3. If approver does not approve within the scheduled time, the system sends a reminder notification (configurable) for the 
   approval.
<The following functionalities are under WIP in the and to be updated once confirmed>
     a) Change the approver (what happens if we have only one zonal approver for that zone)
     b) Auto-Approve
     c)	Reject
     d)	Escalation Mail
     e)	Reports

## 8.3 View
MOSIP allows Zonal Admin to view the list of users on Admin Portal.
Procedure to view the registered users:
1. Zonal Admin provides valid credentials to view the users.
2. The system validates the credentials, on successful validations, allows user to land in main page.
3.<To be updated once information is available>

## 8.4 Update: User Blocking/Blacklisting
MOSIP allows the Zonal Admin to block or blacklist the users due to some reason.  
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
   password by visiting the link.

## 8.5 Whitelisting/Activating Password
MOSIP allows zonal Admin to whitelist /activate the users who are blacklisted or deactivated.  
Procedure to whitelist/activate the password:
1. Admin has authorization to activate/whitelist the users for any reason.
2. Once blocked/blacklisted, the system does not allow the user to login the system and notification is sent.
3. If user contacts Super Admin and requests to unblock/activate the account, the respective RO/Supervisor will provide 
   convincing responses, the super admin will unblock/activate the deactivated account.
4. Super Admin has authorization to reset the password and bio authentication of the supervisor on request by the 
   respective user.
5. The system will also send a link to the registered mobile number or email ID, so that the related user will reset the 
   password by accessing the link.


# 9. Account Management [**[↑]**](#table-of-content)
## 9.1 Change Password-UI
Using MOSIP, users will change the password. Based on the country, single factor or multi-factor authentication will be configured. 
Procedure to follow to change the password:
1. User visits the Reg. Client Login Page or Admin Portal Login Page and raises a request for Change Password.
2. The system provides a facility to the user to change the password.
3. User provides the information related to Old Password, New Password and, Confirm New Password as the system required. 
   During the password creation, user should follow a password creation rule (combination of characters, special 
   character, and min and max length etc.) which is configurable.
4. On successful validation, the system provides a notification to the user as “You have changed the password 
   successfully.”

## 9.2 Reset Password-UI
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

## 9.3 Forgot User Name-UI
Using MOSIP, user can retrieve the username. Based on the country, multi-factor authentication will be configured. 

To retrieve the user name, the user performs the following:
1. User visits the Reg. Client Login page or Admin Portal Login Page and requests for Forgot Password.
2. User provides the registered mobile number as require by the system.
3. The system validates the registered mobile number associated with the user and sends the User Name through an OTP 
   notification.
4. The system prompts to enter the registered mobile number.
5. Admin will enter the OTP as received.
6. System sends the user name through SMS notification to the concerned user.

## 9.4 Account Unblocking-UI
MOSIP allows Admin to unblock the account of other MOSIP users (Registration Officer/supervisor). Based on the country, multi-factor authentication will be configured. If request has been initiated through admin then only OTP authentication is active.

Procedure to unblock the account:
1. MOSIP user navigates to the login page of the portal and clicks “Unblock Account Page”.
2. User provides the registered mobile when the system requires.
3. User will enter the OTP as received
4. On successful validation, system sends SMS notification related to the unblocking of account.

# 10. Asset Management [**[↑]**](#table-of-content)
## 10.1 Registration Centers- Initial Creation/Setup-Backend
Using MOSIP, Zonal Admin will create the Registration Center and categorizes them such as Regular, Handicapped Friendly and Child Friendly and the attributes of registration center through backend process.
	
For more information about attributes of Registration Center, Refer to MDM https://github.com/mosip/mosip/wiki/FRS-Admin-Services#21-registration-center-type---createupdatedelete-

## 10.2 Machines-Subsequent Additions-UI
MOSIP allows Zonal Admin to create the Registration Center and categorizes them such as Regular, Handicapped Friendly and Child Friendly and the attributes of registration center by importing CSV/XLS.

For more information about importing the CSV.XLS through UI, Refer to MDM
https://github.com/mosip/mosip/wiki/FRS-Admin-Services#22-registration-center---createreadupdatedelete-

## 10.3 View Registration Center-UI
MOSIP Zonal Admin will view all the Registration Center available under his/her zone.
For more information about viewing registration centers, refer to https://github.com/mosip/mosip/wiki/FRS-Admin-Services#22-registration-center---createreadupdatedelete-

## 10.4 Machines-Initial Creation/Setup-Backend
Using MOSIP, Zonal Admin will register the machines for his/her zone.
Procedure to register machines follows:
1. Zonal admin will select a Machine Type and Machine Specification for the new Machine
2. Zonal admin will enter the following required details for the new machine:
     •	Machine Name
     •	Mac Address
     •	IP Address
     •	Serial Number
     •	Machine Spec ID
     •	Location Zone (Zone a Machine will belong based on Zonal Admins zone, currently not in DB)
3. Machines will be mapped to Admin Zone.
4. Zonal Admin will map the machine to the existing registration center under the jurisdiction of Admin zone.
5. Machines uniqueness will be maintained through device serial number.


## 10.5 Machines-Initial Creation/Setup-UI
Using MOSIP, Zonal Admin will register the machines through UI to his/her admin zone by importing CSV/XLS.
For more information about register machines in admin zone through UI, refer to  https://github.com/mosip/mosip/wiki/FRS-Admin-Services#23-list-of-machine-types---create-

## 10.6 Machines–View-UI
MOSIP allows Zonal Admin to view the machines through UI.
<Procedure to be updated>

## 10.7 Updating Machine Related Details
MOSIP provides the capabilities for Zonal Admin to update the machine related details.
Procedure to update the machine related details, the Zonal Admin will:
1. Update the machine details such as Serial Number and Mac-Address
2. Update the zone of a machine (If a Machine is being moved to a new zone or accidently assigned to a wrong zone).
3. The system does make the machine visible to the Zonal Admin, if previously assigned to other zone.
4. Remove the mapping of the Center and Machine  (if already mapped to a Center of another zone)
5. Assign a machine to the new zone (In case of accidently assigning the wrong zone, Zonal Admin will contact with the 
   Zonal admin of newly assigned zone to get the Machine re-assigned to the old zone)
   For more information about updating machines in admin zone through UI, refer 
   https://github.com/mosip/mosip/wiki/FRS-Admin-Services#25-list-of-machines---createreadupdatedelete-

## 10.8 Devices-Initial Creation/Setup-Backend
Using MOSIP, Zonal Admin will register the devices for his/her zone.
Procedure to register machines follows:
1.Zonal admin will select a Device Type and Device Specification for the new devices
2.The system allows Zonal admin to enter the following required details for the new devices:
     •	Device Name
     •	Mac Address
     •	IP Address
     •	Serial Number
     •	Device Spec ID
     •	Location Zone (Zone a Device will belong based on Zonal Admins zone, currently not in DB)
3. Devices will be mapped to Admin Zone.
4. Zonal Admin will map the devices to the existing registration center under the jurisdiction of his/her Admin zone.
5. Devices uniqueness will be maintained through device serial number.	
For more information about register devices in admin zone through UI, refer https://github.com/mosip/mosip/wiki/FRS-Admin-Services#29-list-of-device-types---create-

## 10.9 Devices-Subsequent Additions-UI
Using MOSIP, Zonal Admin will register the devices through UI to his/her admin zone by importing CSV/XLS.
For more information about register machines in admin zone through UI, refer to<TBD>

## 10.10 Viewing Devices
MOSIP allows Zonal Admin to view the list of devices through UI.
<TBD when information is available>
## 10.11 Updating Devices Related Details
MOSIP provides the capabilities for Zonal Admin to update the device related details.
Procedure to update the devices related details, the Zonal Admin will:
1. Update the device details such as Serial Number and Mac-Address
2. Update the zone of a device (If a device is being moved to a new zone or accidently assigned to a wrong zone).
3. The system does make the device visible to the Zonal Admin, if previously assigned to other zone.
4. Remove the mapping of the Center and device  (if already mapped to a Center of another zone)
5. Assign a machine to the new zone (In case of accidently assigning the wrong zone, Zonal Admin will contact with the 
   Zonal admin of newly assigned zone to get the Machine re-assigned to the old zone)
   For more information about updating devices related details in admin zone through UI, refer to 
   https://github.com/mosip/mosip/wiki/FRS-Admin-Services#27-list-of-devices---createreadupdatedelete-


## 10.12 View & Map: Machines to Center-UI
MOSIP allows the Zonal Admin to map the machine to the registration center based on admin zone.

Procedure to map the registration center with the machines:
1. Zonal Admin will select the registration center belongs to his/her zone.
2. The system displays the list of available machines when Zonal Admin clicks the machines to be mapped.
3. Zonal Admin will select the machines to map and clicks Save/Submit.
4. The system maps that machine to registration center and once the machine is mapped to the registration center, it is 
   not displayed in the list until unmapped.

## 10.13 View & Map: Devices to Center-UI
MOSIP allows Zonal Admin to map the devices to the registration center based on admin zone.
Procedure to map the registration center with the devices:
1. Zonal Admin will select the registration center belongs to his/her zone.
2. The system displays the list of available devices when Zonal Admin clicks the devices to be mapped.
3. Zonal Admin will select the devices to be mapped.
4. The system maps that devices to selected registration center and once the device is mapped to the registration center, 
   it is not displayed in the list until unmapped.
   For more information about mapping registration center to the devices in admin zone through UI, refer 
   https://github.com/mosip/mosip/wiki/FRS-Admin-Services#211-mappings-of-registration-center-and-device--- 
   createreaddelete-

## 10.14 Update Mapping: Center to Machine-UI
MOSIP allows Zonal Admin to update the machine to the registration center based on admin zone.
Procedure to update the registration center to the machine:
1. Zonal Admin will select the registration center belongs to his/her zone.
2. The system displays the list of available devices when Zonal Admin clicks the devices to be mapped.
3. Zonal Admin will select the devices to map.
4. The system maps that devices to selected registration center and once the device is mapped to the registration center, 
   it is not displayed in the list until unmapped.
   For more information about mapping registration center to the machines in admin zone through UI, refer to 
   https://github.com/mosip/mosip/wiki/FRS-Admin-Services#210-mappings-of-registration-center-and-machine---createdelete-

## 10.15 Update Mapping: Center to User-UI
MOSIP allows Zonal Admin to update the users to the registration center based on admin zone.
Procedure to update the registration center to the users:
1. Zonal Admin will select the registration center belongs to his/her zone.
2. The system displays the list of mapped users. 
3. Zonal Admin will select and un-assign the user. 
4. The system activates/inactivates the user to the selected registration center.

   For more information about mapping registration center to the machine and users in admin zone through UI, refer to 
   https://github.com/mosip/mosip/wiki/FRS-Admin-Services#26-mappings-of-registration-center-machine-and-user-mappings--- 
   createreaddelete-

## 10.16 Asset Management Approval-UI
MOSIP provides the capabilities to create central approver and zonal approver. 
The approver tasks include:
1. Central Approver will approve tasks done by Central Admins such as additions of Zonal Admins and Zonal Approvers.
2. Zonal Approver will approve tasks done by Zonal Admins such as additions of Users like Center Head, Supervisor, and 
   Registration Officer.
3. Zonal Approver will also approve addition of any Center, Device, Machine, mapping of Center-Device, Center-Machine, and 
   Center-User (Actions carried out by Zonal Admins).
4. Zonal Approver can only approve changes done in his/her zone.

# 11. Security Policy Configuration-Backend [**[↑]**](#table-of-content)
Using MOSIP, Zonal Admin will be able to set up security policies for each applications, which includes the following:

  * Session Time out policies
  * Password policies
  * Multi-factor authentication policies (wherever applicable)
  * Admin Portal will only be accessed through Whitelisted IP Address
  * Authenticates Users accessing the portal
  * At Role Level : Configure Level of Auth
**Default Policy:**

  * What type of Authentication
  * Which would be compulsory in case of multi factor authentication
  * Minimum number of factors of Auth (Non-Bio/Bio)
  * Feature Specific authentication overrides Role Specific Behavior for Reset Password/Forgot Username)

# 12. UIN Activation/De-activation-UI [**[↑]**](#table-of-content)
Using MOSIP, Zonal Admin/users will activate/deactivate the UIN of user based on the request by the family member due to any reason. If a UIN is deactivated, the respective VID (If created) will also be deactivated.


