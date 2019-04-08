## Table Of Content

- [Registration Client](#registration-client)
- [Registration Services](#registration-services)
- [1. Master Data Sync](#1-master-data-sync) 
  * [1.1 Master Data, Configuration](#11-master-data-configuration-) _(REG_FR_1.1)_
  * [1.2 End of Day Process](#12-end-of-day-process-) _(REG_FR_1.2)_
- [2. Booking Data Sync](#2-booking-data-sync) 
  * [2.1 Appointments (PRIDs)](#21-appointments-prids-) _(REG_FR_2.1)_
  * [2.2 PR Packets](#22-pr-packets-) _(REG_FR_2.2)_
- [3. Registration Data Services](#3-registration-data-services) 
  * [3.1 List of Registrations](#31-list-of-registrations-) _(REG_FR_3.1)_
  * [3.2 Registration Packet Upload](#32-registration-packet-upload-) _(REG_FR_3.2)_
  * [3.3 Online / Offline Behavior(Offline data upload is covered under this) (Packet Exporter)](#33-online--offline-behavioroffline-data-upload-is-covered-under-this-packet-exporter-) _(REG_FR_3.3)_
  * [3.4 New Registration](#34-new-registration-) _(REG_FR_3.4)_
  * [3.5 UIN Updates](#35-uin-updates-) _(REG_FR_3.5)_
  * [3.6 Acknowledgement and Notifications](#36-acknowledgement-and-notifications-) _(REG_FR_3.6)_
  * [3.7 Biometric Exceptions](#37-biometric-exceptions-) _(REG_FR_3.7)_
  * [3.8 Supervisor Approval](#38-supervisor-approval-) _(REG_FR_3.8)_
- [4. User Services](#4-user-services) 
  * [4.1 User on-boarding](#41-user-on-boarding-) _(REG_FR_4.1)_
  * [4.2 Login/Authentication](#42-loginauthentication-) _(REG_FR_4.2)_
  * [4.3 Logout](#43-logout-) _(REG_FR_4.3)_
- [5. Registration Client Library](#5-registration-client-library) 
  * [5.1 Local Authentication](#51-local-authentication-) 
    * [5.1.1 Offline Authentication using Biometrics](#511-offline-authentication-using-biometrics-) _(REG_FR_5.1)_
    * [5.1.2 Biometric SDK Integration (Extract and Match)](#512-biometric-sdk-integration-extract-and-match-) _(REG_FR_5.2)_
  * [5.2 API Client](#52-api-client-) _(REG_FR_5.3)_
  * [5.3 Biometric Device Manager](#53-biometric-device-manager-)
    * [5.3.1 Vendor Device Manager Integration and Suuport](#531-vendor-device-manager-integration-and-suuport-) _(REG_FR_5.4)_
  * [5.4 Local Storage](#54-local-storage-) 
    * [5.4.1 Database](#541-database-) _(REG_FR_5.5)_
    * [5.4.2 File system](#542-file-system-) _(REG_FR_5.6)_
  * [5.5 Data Security (Take Architects Help)](#55-data-security-take-architects-help-) 
    * [5.5.1 Trust Environment](#551-trust-environment-) _(REG_FR_5.7)_
    * [5.5.2 Encryption and Decryption](#552-encryption-and-decryption-) _(REG_FR_5.8)_
    * [5.5.3 Storage Policies](#553-storage-policies-) _(REG_FR_5.9)_
    * [5.5.4 Key Management](#554-key-management-) _(REG_FR_5.10)_
  * [5.6 Business Validations](#56-business-validations-) _(REG_FR_5.11)_
  * [5.7 Data Sync](#57-data-sync-) 
    * [5.7.1 Master Data](#571-master-data-) _(REG_FR_5.12)_
    * [5.7.2 Pre-registration Data](#572-pre-registration-data-) _(REG_FR_5.13)_
    * [5.7.3 Registration Data](#573-registration-data-) _(REG_FR_5.14)_
    * [5.7.4 Analytics and Audit Logs](#574-analytics-and-audit-logs-) _(REG_FR_5.15)_
  * [5.8 Peripherals Management (Scanner, Camera,...)](#58-peripherals-management-scanner-camera-) _(REG_FR_5.16)_
  * [5.9 Software Version Upgrade](#59-software-version-upgrade-) _(REG_FR_5.17)_
  * [5.10 Cleanup](#510-cleanup-)
    * [5.10.1 Data retention policies](#5101-data-retention-policies-) _(REG_FR_5.18)_
    * [5.10.2 Device moving to new center](#5102-device-moving-to-new-center-) _(REG_FR_5.19)_
    * [5.10.3 Device retirement](#5103-device-retirement-) _(REG_FR_5.20)_
  * [5.11 Language Support](#511-language-support-) 
    * [5.11.1 Language Selection](#5111-language-selection-)  _(REG_FR_5.21)_
    * [5.11.2 Internationalization](#5112-internationalization-) _(REG_FR_5.22)_
    * [5.11.3 Transliteration](#5113-transliteration-) _(REG_FR_5.23)_
    * [5.11.4 Virtual Keyboards](#5114-virtual-keyboards-) _(REG_FR_5.24)_
    * [5.11.5 Translation??](#5115-translation-) _(REG_FR_5.25)_
  * [5.12 Health Check](#512-health-check-) 
    * [5.12.1 Disk Space Check](#5121-disk-space-check-) _(REG_FR_5.26)_
    * [5.12.2 Peripherals Check](#5122-peripherals-check-) _(REG_FR_5.27)_
    * [5.12.3 Virus Scan/Security Scan](#5123-virus-scansecurity-scan-) _(REG_FR_5.28)_
    * [5.12.4 Reports](#5124-reports-) _(REG_FR_5.29)_
- [6. Registration Client UI](#6-registration-client-ui-) _(REG_FR_6)_


# Registration Client
# Registration Services

# 1. Master Data Sync
## 1.1 Master Data, Configuration [**[↑]**](#table-of-content)

#### A. Registration Officer or Supervisor can download and unzip the client application set up kit
When a Registration Officer or Supervisor opts to download setup kit and selects the OS-specific setup kit to download, the system allows the user to download the setup kit to the storage location chosen by the user
* User then unzips the setup kit.
* Extract the files and folders from the zip file to a chosen location.
* Allows user to verify that the files and folder structure are as described in the design document.
* System captures and stores the download transaction details for audit purposes. 
#### B. Enable launching the client application on a specific machine
When a user chooses to launch the client application, the system performs validations as described below:
1. Allows the user to initiate launch by double clicking on the MOSIP icon on the dongle.
1. Validates that the mode of startup is set to ‘Dongle’ and not ‘Machine Install’.
1. Validates that the machine on which it is launched has been registered.
1. Reads the config setting that determines if a machine needs to be mapped to a Registration Centre (All the above config settings and mappings are made through the Admin portal).
   * If yes, validates that the machine is mapped.
   * If no, skips this validation.
5. Validates that the machine has sufficient RAM as defined in the design document.
1. Validates that the machine has sufficient hard disk space available as defined in the design document.
1. Checks whether updates are available on the server.
   * If yes, downloads the updates.
   * If no updates available or unable to connect to the server, proceed to the next step.
8. Launches the application and display the default landing page.
1. Displays error messages in case of exceptions for any of the validations identified above.
1. System captures and stores the launch details for audit purposes.

#### C. Update the client software from the server
When the Registration Client application is started up (launched), the system checks the server for updates to the client software.

If an update is available, it is automatically downloaded and installed as a part of the startup process.

The system follows the following steps during the update process:
1. Checks for updates during start up.
1. The client must be online to check for updates.
1. If an update is available, downloads and installs it automatically and launch the application.
1. If no updates are available, launches the application.
1. The updates are downloaded as patch updates.
1. When installation is in progress, the user cannot perform any action on the client.
1. Once installation is completed, the user can start working on the client.
1. If update is not successful, the client returns to its earlier version.
1. The client is locked for registration if x days (configuration setting) have passed since the last check for updates.
1. System captures and stores the transaction details for audit purpose.

## 1.2 End of Day Process [**[↑]**](#table-of-content)

# 2. Booking Data Sync
## 2.1 Appointments (PRIDs) [**[↑]**](#table-of-content)
## 2.2 PR Packets [**[↑]**](#table-of-content)


# 3. Registration Data Services
## 3.1 List of Registrations [**[↑]**](#table-of-content)
## 3.2 Registration Packet Upload [**[↑]**](#table-of-content)
## 3.3 Online / Offline Behavior(Offline data upload is covered under this) (Packet Exporter) [**[↑]**](#table-of-content)
## 3.4 New Registration [**[↑]**](#table-of-content)
## 3.5 UIN Updates [**[↑]**](#table-of-content)
## 3.6 Acknowledgement and Notifications [**[↑]**](#table-of-content)

**Support remapping a machine from one center to another**

When an Admin user changes the mapping of a computer from one Registration Centre (RC) to another, a sync is initiated on the client installed on that computer.

MOSIP system has the ability of completely erasing/removing data from a machine, which is not specific to the Registration Centre, considering a scenario wherein the Registration Officer (RO) moves with the machine from one center to another. In this case, data relevant to the pervious center mapped should also erased completely and a re-sync should be initiated.

The following example explains the steps system performs to support remapping a machine from one center to another:

1. Say a machine M1 is currently mapped to registration center RC1.
1. M1 contains master data related to RC1, officer on-boarding data for say RO1 and RO2, and pre-registration data, registration packets and audit logs for registrations carried out in RC1.
1. Now M1 is unmapped from RC1 and mapped to RC2 in the Admin portal.
1. When M1 comes online, the master and configuration data is synced from server to client. As a result of sync, the following occur:
   * M1 recognizes that it is mapped to RC2 instead of RC1. An alert is displayed to the user.
   * Once the client machine receives details of remapping to a new registration center, new registration, UIN update, and lost UIN cannot be initiated. The links to the above should either be hidden, disabled or display error on-click - as per UX guidelines.
   * In-progress registrations can be completed.
   * A one-time background process to push packet IDs, packets, and user onboarding data to the server will happen when the system is online and there are no pending approval packets.
   * It will then delete all the data except audit data. Deletion covers the RC1 master data, Registrations created while in RC1, user on-boarding data of RC1, and pre-registration data of RC1. Audit logs and other data, which might be used for analytics and data retention policy reasons, will not be deleted. The removal of those will be as per policy only.
   * The user from the original registration center cannot login thereafter.
   * If the one-time process has not yet run, the user will still be able to login and perform sync, end of day approval, re-register updates, export, and upload. The user cannot perform pre-registration download and user on-boarding.
5. As part of sync M1 receives the list of RC2 users. RC2 can users proceed to on-board themselves.

## 3.7 Biometric Exceptions [**[↑]**](#table-of-content)
## 3.8 Supervisor Approval [**[↑]**](#table-of-content)

# 4. User Services
## 4.1 User on-boarding [**[↑]**](#table-of-content)


#### A. Map registration officers and supervisors to a client machine.
Initially a machine will have no users on boarded. The first RO/Supervisor will be on boarded by an Administrator or from the backend. Thereafter this RO/Supervisor can onboard other users.
1. This functionality allows the system to create new mapping between registration officers and supervisors to a client machine
1. Allow the system to receive the request for mapping a registration officer / supervisor to the client machine with selected data
   * Fields selected on the UI include user, status, fingerprints, and irises.
   * The list of users should include only active users. The system does not show users who are blacklisted or decommissioned.
   * The list of users does not include users who are already mapped to the machine.
   * All 10 fingerprints are captured and authenticated with the server. The machine must be online for this authentication.
   * The system then validates the fingerprint quality threshold is met.
   * The system then validates the number of successful fingerprint authentications is greater than or equal to the config setting of fingerprint authentications required.
   * Unlimited retries are allowed.
   * Both irises are captured and authenticated with the server. Validate that the iris quality threshold is met.
   * Validate that the number of successful iris authentications is greater than or equal to the config setting of iris authentications required.
   * Unlimited retries are allowed.
3. If validations successful:
   * Save the mapping locally.
   * Successfully authenticated fingerprints and irises will be stored locally.
   * Fingerprints and irises with unsuccessful authentication will not be stored.
   * The status of the mapping is set to ‘Active’ or ‘Inactive’ as selected.
   * Mapping will be sent to the server during the next sync.
   * Biometrics will not be sent to the server.
4. If not successful: Displays error message.
5. Multiple users can be mapped to the machine by repeating the above flow. There should be no limitation to the numbers of users mapped.

#### B. Updating the mapping of registration officers and supervisors to a client machine
1. This features allow the system to receive the request to modify a mapping status from Active to Inactive or from Inactive to Active.
   * No other fields can be modified.
   * A mapping cannot be deleted.
2. Allows the system to save the changes locally. Changes will be sent to the server during the data sync process
#### C. View mapped registration officers to a client machine.
1. This feature allows the system to receive a request to view the list of mapped users
1. Fetches the locally stored details of Registration Officers and Supervisors mapped to this machine.
1. Constructs a response with the details fetched.
1. All data in the view page will be in read only mode and will be in the same sequence as defined in the data definition 
#### D. Registration client enables capturing an officer's biometrics during on-boarding in order to support login, local duplicate checks, and registration submission
1. When a Registration Officer or Supervisor enters his/her log in to registration client with their credentials the system validates that the user is mapped to the same Registration Centre as the USB dongle. System validates that the user is yet to be on-boarded to the client dongle. System directs the user to the password entry page.
1. User enters password and submits. System sends OTP to the user and directs to the OTP entry page. Lock the user account for 30 minutes if an incorrect credential (password or OTP) is entered 5 times in succession.
1. User can request the system to resend OTP if not received earlier.
1. User enters OTP and submits. System directs the user to the dashboard page with all links disabled except for ‘User on-boarding’.
1. User navigates to the User on-boarding page.
1. User marks biometric exceptions if any (system should not mandate capture and authentication of those biometrics that are marked as exceptions).
1. User scans left slap, right slap and two thumbs. System displays the result of authentication of each finger.
1. The system validates that the device is registered in the Admin portal, associated to this Registration Centre ID, and the current date lies within the validity dates of the device model.
1. User scans both irises. System displays the result of authentication of each iris. User scans face and exception photo. System displays the result of authentication of face. Exception photo is not authenticated
1. User can choose to retry each biometric capture as required. There is no limit to the number of retries.
1. User submits then opts to submit the data. System validates that the total number of successful authentications is greater than or equal to the threshold value configured. System maps the user to the client dongle and displays a pop-up confirmation message. System saves the successfully authenticated biometrics locally.
1. System validates that the total number of successful authentications is greater than or equal to the threshold value configured. For example, if 9 fingers+2 irises+face are successfully authenticated, the total number of authentications is 9+2+1=12. Validate that 12 is greater than or equal to the threshold configured (say 10). Then save the user-USB dongle mapping and the authenticated biometrics locally. Do not save the biometrics that are not authenticated.
1. The system displays the result of authentication of each biometric - 10 fingers, 2 irises and face - in a list.
1. User gets access to all links on the client according to their role.
User can update their biometrics at any time after successful on-boarding by choosing the ‘User on-boarding’ link from the menu. The biometrics provided during update will be authenticated with the server and saved locally if threshold for successful authentication is met. Updated biometrics will overwrite the biometrics stored locally earlier.

## 4.2 Login/Authentication [**[↑]**](#table-of-content)
## 4.3 Logout [**[↑]**](#table-of-content)

When a Registration Officer or Supervisor opts to logout, the system allows them to do so by provisioning the following:
1. Allows the user to choose appropriate option (button or link) in order to log out
1. Log the user out of their session.
   * While logging out, does not allow the user to perform any actions that require them to be logged in.
3. Alternatively, closing the client window will also log the user out.
1. Alternatively, if the user has remained inactive for a configured duration he will be automatically logged out.
   * Inactive/idle time is defined as the time during which the user has not submitted or retrieved data using the client application or navigated to a different page.
   * Any such action when performed resets the time to zero.
   * The auto log out duration is configured from Admin. The default value can be taken as 15 minutes.
   * Alerts the user ‘x’ minutes before reaching the auto logout time limit. Displays a countdown timer in the alert. The user can choose to dismiss the alert and continue working. This will also reset the timer to zero.
   * The duration before which to display the alert is configured by Admin. The default value can be taken as 2 minutes. That is, if auto logout time is 15 minutes then an alert will display after 13 minutes.
   * Validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
   * Validates that the user has a role or Registration Officer or Supervisor.
5. Upon logout, any unsaved data will be lost. Data will not be automatically saved in the database and will not be retained in memory.
6. The System also captures and stores the transaction details for audit purpose

# 5. Registration Client Library
## 5.1 Local Authentication [**[↑]**](#table-of-content)
### 5.1.1 Offline Authentication using Biometrics [**[↑]**](#table-of-content)
### 5.1.2 Biometric SDK Integration (Extract and Match) [**[↑]**](#table-of-content)
## 5.2 API Client [**[↑]**](#table-of-content)
## 5.3 Biometric Device Manager [**[↑]**](#table-of-content)
### 5.3.1 Vendor Device Manager Integration and Suuport [**[↑]**](#table-of-content)
## 5.4 Local Storage [**[↑]**](#table-of-content)
### 5.4.1 Database [**[↑]**](#table-of-content)
### 5.4.2 File system [**[↑]**](#table-of-content)
## 5.5 Data Security (Take Architects Help) [**[↑]**](#table-of-content)
### 5.5.1 Trust Environment [**[↑]**](#table-of-content)
### 5.5.2 Encryption and Decryption [**[↑]**](#table-of-content)
**Enable capturing an individual's face photograph—Analysis**

When a Registration Officer opts to capture photo of an individual, the system initiates a photo capture and validates the following:
1. Validates that an on-boarded camera is connected to the machine.
   * If an on-boarded camera is not found, displays an error message.
   * If more than one on-boarded camera is connected, proceeds with the first camera that the system finds as it scans the ports of the machine.
2. Displays the photo preview before capturing.
3. Allows the Registration Officer to initiate capture.
4. Sends request to the camera for photo capture.
5. Receives the photo from the camera.
6. Displays the photo on screen.
7. Allows the Registration Officer to proceed to verify quality score.
8. System captures and stores the transaction (User id or system account; Machine Details; Event Name; Application Name, and Event data) details for audit purpose. 

### 5.5.3 Storage Policies [**[↑]**](#table-of-content)
### 5.5.4 Key Management [**[↑]**](#table-of-content)

**Enable selecting the 'Fingerprint Exception' option**

When a Registration Officer sets ‘Biometric Exception’ = ‘Yes’, the system enables him/her to specify biometric exceptions.
1. The system allows the user to mark the missing finger(s) and/or missing iris(es).
1. If ‘Biometric Exception’ = ‘Yes’, at least one missing biometric must be mandatorily marked.
1. If ‘Biometric Exception’ = ‘No’, the Biometric Exception capture is skipped and exceptions cannot be marked.
1. System captures and stores the transaction (User id or system account; Machine Details; Event Name; Application Name, and Event data) details for audit purpose.

## 5.6 Business Validations [**[↑]**](#table-of-content)
## 5.7 Data Sync [**[↑]**](#table-of-content)
### 5.7.1 Master Data [**[↑]**](#table-of-content)
### 5.7.2 Pre-registration Data [**[↑]**](#table-of-content)
### 5.7.3 Registration Data [**[↑]**](#table-of-content)
### 5.7.4 Analytics and Audit Logs [**[↑]**](#table-of-content)

**Restrict access to each MOSIP feature to authorized users**

MOSIP system has role-based privileges. A user can have a single role only. For example, a user can be either a Registration Officer or Supervisor.

When a logged in user tries to access a feature on the registration client, the system determines if the user has the right privileges to use the feature.

1. If yes, system permits the user to access the requested feature.
1. If no, displays an error message or hide the link to the feature as applicable. The UX design will drive whether to hide a link or display an error on click of the link.
1. Both registration officers and supervisors can access the following features. The role to rights mapping is configurable at a country level. The list given below corresponds to the default configuration:
   * Login
   * On-board users
   * On-board devices
   * New registration
   * Registration correction
   * UIN update
   * UIN de- and re-activation
   * Lost UIN
   * Send registration packet IDs to server
   * Sync data from server to client
   * Sync data from client to server
   * Export packets to local folder
   * Upload packets through FTP
   * Virus scan
   * Update client software
4. Only supervisors can access the following features:
   * Approve registration
   * Reports
5. A Super Admin can access all features.
 
1. System should capture and store the transaction details for audit purpose.


## 5.8 Peripherals Management (Scanner, Camera,...) [**[↑]**](#table-of-content)
## 5.9 Software Version Upgrade [**[↑]**](#table-of-content)
## 5.10 Cleanup [**[↑]**](#table-of-content)
### 5.10.1 Data retention policies [**[↑]**](#table-of-content)
### 5.10.2 Device moving to new center [**[↑]**](#table-of-content)
### 5.10.3 Device retirement [**[↑]**](#table-of-content)
## 5.11 Language Support [**[↑]**](#table-of-content)
### 5.11.1 Language Selection [**[↑]**](#table-of-content)
### 5.11.2 Internationalization [**[↑]**](#table-of-content)
### 5.11.3 Transliteration [**[↑]**](#table-of-content)
### 5.11.4 Virtual Keyboards [**[↑]**](#table-of-content)
### 5.11.5 Translation?? [**[↑]**](#table-of-content)
## 5.12 Health Check [**[↑]**](#table-of-content)
### 5.12.1 Disk Space Check [**[↑]**](#table-of-content)
### 5.12.2 Peripherals Check [**[↑]**](#table-of-content)
### 5.12.3 Virus Scan/Security Scan [**[↑]**](#table-of-content)
### 5.12.4 Reports [**[↑]**](#table-of-content)

# 6. Registration Client UI [**[↑]**](#table-of-content)