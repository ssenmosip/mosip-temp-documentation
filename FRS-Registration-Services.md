## Table Of Content

- [1. User Services](#1-user-services-)
  * [1.1 User on-boarding](#11-user-on-boarding-) _(REG_FR_1.1)_
  * [1.2 Login/Authentication](#12-loginauthentication-) _(REG_FR_1.2)_
  * [1.3 Logout](#13-logout-) _(REG_FR_1.3)_
- [2. Data Sync](#2-data-sync-)
  * [2.1 Master Data Sync](#21-master-data-sync-) _(REG_FR_2.1)_
  * [2.2 Configuration Sync](#22-configuration-sync-) _(REG_FR_2.2)_
  * [2.3 Client to Server Sync](#23-client-to-server-sync-) _(REG_FR_2.3)_
  * [2.4 Packet Status Sync](#24-packet-status-sync-) _(REG_FR_2.4)_
  * [2.5 Pre-registration Data Download](#25-pre-registration-data-download-) _(REG_FR_2.5)_
- [3. Health Check](#3-health-check-)
  * [3.1 Peripherals Check](#31-peripherals-check-) _(REG_FR_3.1)_
  * [3.2 Disk Space Check](#32-disk-space-check-) _(REG_FR_3.2)_
  * [3.3 Virus Scan/Security Scan](#33-virus-scansecurity-scan-) _(REG_FR_3.3)_
- [4. Registration Data Services](#4-registration-data-services-)
  * [4.1 New Registration](#41-new-registration-) _(REG_FR_4.1)_
  * [4.2 UIN Update](#42-uin-update-) _(REG_FR_4.2)_
  * [4.3 Lost UIN](#43-lost-uin-) _(REG_FR_4.3)_
  * [4.4 Acknowledgement and Notifications](#44-acknowledgement-and-notifications-) _(REG_FR_4.4)_
  * [4.5 Biometric Capture (SDK Integration, Extract and Match) (WIP)](#45-biometric-capture-sdk-integration-extract-and-match-wip-) _(REG_FR_4.5)_
  * [4.6 Biometric Exceptions](#46-biometric-exceptions-) _(REG_FR_4.6)_
  * [4.7 Registration Officer and Supervisor Approval](#47-registration-officer-and-supervisor-approval-) _(REG_FR_4.7)_
  * [4.8 End of Day Process](#48-end-of-day-process-) _(REG_FR_4.8)_
- [5. Geo-location](#5-geo-location-) _(REG_FR_5)_
- [6. Language Support](#6-language-support-)
  * [6.1 Translation](#61-translation-) _(REG_FR_6.1)_
  * [6.2 Transliteration](#62-transliteration-) _(REG_FR_6.2)_
- [7. Packet Upload](#7-packet-upload-)
  * [7.1 Registration Packet Upload](#71-registration-packet-upload-) _(REG_FR_7.1)_
  * [7.2 Offline upload (Packet Exporter)](#72-offline-upload-packet-exporter-) _(REG_FR_7.2)_
- [8. Analytics and Audit Logs](#8-analytics-and-audit-logs-) _(REG_FR_8)_
- [9. Data Security](#9-data-security-)
  * [9.1 Key Management](#91-key-management-) _(REG_FR_9.1)_
- [10. Software Version Upgrade](#10-software-version-upgrade-) _(REG_FR_10)_
- [11. Clean up](#11-clean-up-)
  * [11.1 Data retention policies](#111-data-retention-policies-) _(REG_FR_11.1)_
  * [11.2 Machine Retirement](#112-machine-retirement-) _(REG_FR_11.2)_

## 1. User Services [**[↑]**](#table-of-content)
### 1.1 User on-boarding [**[↑]**](#table-of-content)

When a registration officer or supervisor logs in a client machine for the first time, they provide their biometric details, which will be stored and mapped to the client machine locally. This locally stored data helps to authenticate a supervisor or registration officer to work in offline mode (when the client is not connected to the server).
#### A. Map registration officers and supervisors to a client machine.
Initially, a machine will have no users on boarded. The first user will be on boarded by an administrator or from the backend. Thereafter this user can onboard other users.
1. This functionality allows the system to create new mapping between registration officers and supervisors to a client machine.
1. Allows the system to receive the request for mapping a registration officer / supervisor to the client machine with selected data.
   * Fields selected on the UI include user, status, fingerprints, and irises.
   * The list of users will include only active users. The system does not show users who are blacklisted or decommissioned.
   * The list of users do not include those users, who are already mapped to the machine.
   * All 10 fingerprints are captured and authenticated with the server. The machine must be online for this authentication.
   * The system then validates the fingerprint quality threshold is met.
   * The system then validates the number of successful fingerprint authentications is greater than or equal to the config setting of fingerprint authentications required.
   * Unlimited attempts are allowed.
   * Both irises are captured and authenticated with the server. Validate that the iris quality threshold is met.
   * Validate that the number of successful iris authentications is greater than or equal to the config setting of iris authentications required.
   * Unlimited attempts are allowed.
3. If validations are successful, then the system performs the following:
   * Saves the mapping locally.
   * Successfully authenticated fingerprints and irises will be stored locally.
   * Fingerprints and irises with unsuccessful authentication will not be stored.
   * The status of the mapping is set to ‘Active’ or ‘Inactive’ as selected.
   * Mapping will be sent to the server during the next sync.
   * Biometrics will not be sent to the server.
4. If not successful: Triggers an error message.
5. Multiple users can be mapped to the machine by repeating the above flow. There is no limitation to the numbers of users mapped.

#### B. Registration Client enables capturing an officer's biometrics during on-boarding to support login, local duplicate checks, and registration submission
The system performs the following steps:
1. Captures all the biometrics of the officer's as an input.
1. Generates a match score for each individual biometric
1. Generates an average match score
1. Compares the average match score with the configured threshold match score 
1. Returns one single response i.e. return success if average >= threshold 

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registrtaion-on-board-user.md)

### 1.2 Login/Authentication [**[↑]**](#table-of-content)

#### A. Allows biometric login of the Registration Officer or Supervisor to the client application

MOSIP supports single factor and multi factor login including iris and face capture. An Admin config setting determines the mode of login. 

1. The registration officer or supervisor opts to login to Registration Client application
   * System enables user to login by entering username, and submit iris and face photo.
2. The user provides their username.
3. The user scans any one iris through the iris capture device.
4. The user then captures face photo using the face photo capture-device.
5. On successful authentication, the system allows a user to log in.

#### B. Temporarily lock the user account after five unsuccessful login attempts.
1. The MOSIP system temporarily locks the user’s account in case he/she provides an invalid password for five times continuously to login.
1. Upon the fifth unsuccessful attempt to login, displays an error message 
1. The temporarily account lock lasts for 30 minutes (configured by an admin).
1. The same error message is displayed for any subsequent login attempt within 30 minutes.
1. After 30 minutes, the lock is released and the count of invalid login attempts is reset to zero.
1. The same is implemented if the fingerprint, iris, face, or multifactor login fails five times.
1. System captures and stores the transaction details for audit purpose (except PII data).

#### C. Authenticate online/offline login of the Supervisor to the client application [**[↑]**](#table-of-content)
If the Registration Client is offline, then system allows the supervisor to log in the client machine only with a password-based login. Whereas, if the Registration Client is online, the supervisor can log in to the client machine with all various type of login such as Password-based login, OTP based login, etc.

When a supervisor opts to log in the client machine, the system displays the appropriate options as per the mode of login.

* If the mode of login is username and password, displays the password-based login.
* If the mode of login is username and OTP, display the OTP based login 


**(i) Password-based login**

The mode of login is configured by admin, if the login is configured as Password-based login, the supervisor will be able to login the client machine in both online and offline mode using their password.

1. System allows the user to provide their credential and submit.
1. System validates that the username belongs to an on boarded registration officer or supervisor on that client.
1. System validates that the password matches with the user’s password stored locally. The local password will be fetched from the server during sync.
1. System validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
1. System validates that the user has a role of registration officer or supervisor. 

**(ii) OTP based login**

If the client machine is online and the supervisor is mapped to the client machine, then the system allows supervisor to login with the OTP. The system allows supervisor to enter their username and authenticate himself or herself with OTP.

1. Allows the user to enter their username and submit.
1. Validates that the username belongs to an on-boarded registration officer or supervisor on that client.
1. The system generates and sends an OTP by SMS to the user’s registered mobile number. Use the template defined in Admin for the OTP message. 
1. Allows the user to enter the OTP and submit.
   * Alternatively, allows the user to change entered username.
   * Alternatively, allows the user to request for resending the OTP.
5. Validates that the OTP submitted matches with the one that was generated and is submitted within its validity period.
6. Validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
7. Validates that the user has a role of registration officer or supervisor.
8. On successful validation of all conditions above, displays the logged in screen to the user

#### D. Restrict access to each MOSIP feature to authorized users. [**[↑]**](#table-of-content)

In MOSIP system, a user can have multiple role. When a user is registered on admin portal, the system allows a user to assign multiple roles.

When a logged in user tries to access a feature on the Registration Client, the system determines if the requested feature is accessible to the role(s) mapped to the user.
1. If yes, permits the user to access the requested feature.
1. If no, displays an error message or hide the link to the feature as applicable. The UX design will drive whether to hide a link or display an error by clicking the link.
1. Both registration officers and supervisors can access the following features. The role to rights mapping is configurable at a country level. The list given below corresponds to the default configuration.
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
1. If a user is not authorized to access a feature, the system notifies the user by a message. 

[**Link to design for Login**](/mosip/mosip/tree/master/docs/design/registration/registration-login.md)

[**Link to design for Multi-authentication**](/mosip/mosip/tree/master/docs/design/registration/registration-multi-authentication.md)

[**Link to design for authorization**](/mosip/mosip/tree/master/docs/design/registration/registration-authorization.md)

### 1.3 Logout [**[↑]**](#table-of-content)
When a registration officer or supervisor opts to logout, the system allows them to do so by provisioning the following:
1. Allows the user to choose appropriate option (button or link) in order to log out
1. Logs out the user of their session.
   * While logging out, does not allow the user to perform any actions that require them to be logged in.
1. Alternatively, closing the client window will also log out the user.
1. Alternatively, if the user has remained inactive for a configured duration, he/she will be automatically logged out.
   * Inactive/idle time is defined as the time during which the user has not submitted or retrieved data using the client application or navigated to a different page.
   * Any such action when performed resets the time to zero.
   * The auto log out duration is configured by Admin. The default value can be taken as 15 minutes.
   * Alerts the user ‘x’ minutes before reaching the auto logout time limit. The system displays a countdown timer in the alert. The user can choose to dismiss the alert and continue working. This will also reset the timer to zero.
   * The duration before which to display the alert is configured by Admin. The default value can be taken as 2 minutes. That is, if auto logout time is 15 minutes then an alert will display after 13 minutes.
5. Upon logout, any unsaved data will be lost. Data will not be automatically saved in the database and will not be retained in memory.
1. The System also captures and stores the transaction details for audit purpose (except PII data).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-login.md)

## 2. Data Sync [**[↑]**](#table-of-content)
### 2.1 Master Data Sync [**[↑]**](#table-of-content)

The Registration Client can work both in online and offline mode. When the client machine is switching from offline to online mode, the locally saved data will be synced with the server.
The data sync can happen through an automated process at a set frequency or a user can manually initiate a sync.

Please refer to [**Git**](/mosip/mosip/blob/master/docs/requirements/MOSIP%20Masterdata%20Types.xlsx) for more details on the type of master data that is synced.


### 2.2 Configuration Sync [**[↑]**](#table-of-content)

Please refer [**Git**]() for a detailed list of parameters that can be configured as ON and OFF by a country while commencing a [**new registration**](#41-new-registration-).
Based on the configuration (turn on or turn off), the system allows a user to capture applicable biometrics, authenticates, and completes the registration. 

### 2.3 Client to Server Sync [**[↑]**](#table-of-content)

1. The Registration Client receives a request to sync data (through manual trigger or scheduled job) from client to server.
2. Client in turn sends request with the applicable data to server.
   * User on-boarding data is synced.
   * Only the additions, deletions, and modifications made since the last sync are sent.
3. Client receives response from server as a success or failure message.
4. Client displays a success or failure message on the UI
5. User on-boarding data such as User ID, USB device ID and Computer ID will be synced
6. Alternatively, if the client machine is not online
   * Displays an error message and does not sync when a user tries to initiate a manual sync.
   * Does not sync when an automatic sync is triggered.

### 2.4 Packet Status Sync [**[↑]**](#table-of-content)

The system performs the following steps to ensure packet status sync from server to client to read the status of the registration packets sent:
1. The system allows a registration officer to either sync manually or automatically based on configured frequency.
1. The system allows the application to request using registration packet ID and receive the registration packet status from the server
1. The system displays the status (in progress/completed) of the operation to pull registration packet IDs from registration server.

### 2.5 Pre-registration Data Download [**[↑]**](#table-of-content)


#### A. Register a pre-registered individual by searching & fetching pre-registration data associated to a pre-registration ID from local system or server

When a registration officer starts a new registration by entering a pre-registration ID of an individual, the system checks if an exact match for the ID available in local database.
1. If available, checks if an updated pre-registration packet for that ID is available on the server.
   * If available, downloads the pre-registration packet from the server and pre-populate on screen.
   * If update is not available on server, the system displays the data from local database.
   * If client if offline, the system displays the data from the local database.
1. If data are not available in local database, checks if data for that ID are available on the server.
   * If available, downloads the pre-registration packet from the server and pre-populate on screen.
   * If data are not available on server, the system displays the data from local database.
1. Based on the availability of data, the system populates the demographic details of the individual and pre-populates the registration form.
1. The demographic details can still be edited at this stage.
1. The registration officer can then view the documents, which were uploaded during pre-registration
1. If no matching PRID available in local system and server, the system displays an error message.

#### B. Registration Client allows downloading of pre-registration data in real time or manually for a specific PRID
**(i) Real time downloads of Pre-registration data**

1. When a registration officer starts a new registration by entering a pre-registration ID and opts to fetch pre-registration data, the system checks if the pre-registration ID entered has a match in the local system
1. The system then fetches the demographic details of the individual and pre populate the registration form if there is exactly one match for pre-registration ID in the local system

**(ii) Manual downloads of Pre-registration data**

A registration officer can download the pre-registration data while being online. It is possible to download the demographic data of an individual only and the system does not allow to download the documents, which were uploaded by the applicant. 

The system also enables a user to view the progress of download.

The pre-registration data can be downloaded only for that particular registration center, where the pre-registration data download is initiated

It is possible to download the pre-registration data from current date plus 1 to current date plus 7. This date range is  configurable

The downloaded pre-registration data overwrites the previously downloaded data for the same pre-registration ID

The downloaded pre-registration data is stored in its stipulated path as defined

[**Link to design**](/mosip/mosip/blob/master/docs/design/registration/registration-sync-job.md)

## 3. Health Check [**[↑]**](#table-of-content)
### 3.1 Peripherals Check [**[↑]**](#table-of-content)
The system allows a registration officer or supervisor to view whether a  biometric devices (such as fingerprint & iris capture devices, face camera) is connected correctly or not connected to the client machine. If a biometric device is configured as "turned OFF" by admin, then the system does not display the availability of the device.

The system also has the provision to show if the client machine has internet connectivity or not. 

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-device-integration.md)


### 3.2 Disk Space Check [**[↑]**](#table-of-content)
If disk space is insufficient, system displays an error message and data entered by registration officer will be not be saved. Then registration officer will clean up to make sufficient space on the client machine and try the registration again.

Upon receiving a request to create a registration packet at the end of data capture and authentication steps, the system validates the disk space available on the client machine to store the registration packet as follows:
1. Calculates the size of the registration packet based on the data captured.
   * Data includes demographic, biometric, photographs, OSI authentication, registration metadata, audit data, and acknowledgement scan.
2. Calculates the disk space, which is available in the configured packet storage location.
1. Validates if the storage location is sufficient to store the registration packet.
1. In case of successful validation, responds with success message and proceeds further. 
1. In case of unsuccessful validation, responds with an appropriate error message.
1. System captures and stores the transaction details for audit purpose (except PII data).

### 3.3 Virus Scan/Security Scan [**[↑]**](#table-of-content)

Upon receiving a request to perform a virus scan of the registration packets on the client machine, the system performs the following steps:
1. When the client application is open, the system scans the registration packets at a configured frequency.
1. Checks if viruses are available in the registration packets, which are stored on the client machine.
   * All registration packets on the machine will be scanned.
3. At the end of the scan, displays an alert message (Security scan detected viruses in the following files [List of files]. Please take necessary action or contact the administrator) on screen if a virus is detected.
1. If the client application is not open at the configured time, the scan will be queued up and runs only when the client application is open.

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-virus-scanner.md)

## 4. Registration Data Services [**[↑]**](#table-of-content)
### 4.1 New Registration [**[↑]**](#table-of-content)

Registration officer initiates a new registration for a non pre-registered individual or a pre-registered individual (by entering the PRID) and follows the below process to complete registration:

#### A. Capture consent from the individual for data storage and utilization				
1. For every registration, the system provides an option for the registration officer to mark an individual's consent as Yes or No
1. The registration officer marks consent after confirming with the individual offline.
1. Whether the consent is marked as Yes/No, it will not have any impact on issuance of UIN for that individual and the system will not execute any validations in this regard during packet processing.

#### B. Transliteration

Refer to the section related to [**Transliteration**](#62-transliteration-).
#### C. Mark an individual's date of birth as 'Verified' (Not Specified for Morocco)
1. For new registration or UIN update, the system provides an option for the registration officer to mark an individual's date of birth as ‘Verified’.
1. For a new registration, the ‘Verified’ field is displayed as an option next to Date of Birth field. The default state is unchecked. When checked, it indicates that the registration officer has verified the date of birth of the individual.
1. For a UIN update, the ‘Verified’ field is applicable only when the Age/Date of Birth field is selected for update.
#### D. Register an individual who is less than 5 years old.
1. MOSIP does not have an explicit ‘Category’ for registering children less than five years. However, the date of birth will automatically determine the category of the applicant, which can be setup by the country as required.
1. When a registration officer starts a new registration, the system intuitively determines if the registration is for a child using the date of birth.
1. If the date of birth indicates that the registration is for a child is less than 5 years on the date of registration, and if parent/guardian’s UIN exists. Then the system captures parent/guardian's details: UIN/Name/Biometrics/Proof of relationship. 
1. If the date of birth indicates that the registration is for a child is less than 5 years and if parent/guardian’s UIN does not exist then the system ensures parent/guardian is registered first and at least RID is available.
1. The system captures parent/guardian's details: Registration ID/Name/-Biometrics/PoR (Processor will pick up parent/guardian's registration first prior to child)
#### E. Mark an individual as Foreigner or Non-Foreigner
For every new registration, the system provides an option on the demographic details page for the registration officer to mark an individual as either a citizen of that country or a Foreigner. 

If the registration officer selects the desired option, indicates that the individual is a Foreigner. If option is not selected, indicates that the individual is a citizen of that country.
#### F. Register a non-pre-registered individual 
When a registration officer starts a new registration for a non-pre-registered individual (an individual who does not have PRID), the registration officer will capture the demographic and biometric details to register the individuals.

If registration officer determines that the non-pre-registered individual’s date of birth is less than 5 years old, then refer to the feature related to [**Register an individual who is less than 5 years old**](#d-register-an-individual-who-is-less-than-5-years-old).
#### G. Enter the demographic details for registration

**(i) The Registration Officer opts to initiate a new registration**
1. The system allows the registration officer to enter the individual’s demographic details such as Name, Gender, DOB, Residential Address, and other fields based on the [**ID Object Definition**](MOSIP-ID-Object-definition). 
1. The system validates the entered demographic fields.
1. If demographic fields validation fails, the system displays an error message.
1. On successful validation, the system proceeds to next step.

**(ii) The Registration Officer selects a pre-registration for registration**

1. Registration officer enters the PRID provided by a pre-registered individual. 
1. The registration officer enters demographic details or edits pre-filled demographic details (details rendered from the provided PRID).
1. The Registration Client validates the entered demographic data as per the [**field definition document**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/Reg.%20Client/MOS-1220%20New%20Registration%20Field%20Definition.docx).
1. Displays error message(s) on screen in case of validation failure.
1. On successful validation, proceeds to next step.
#### H. Copy address from the previous registration
When the address details of the previous registration and the current registration is same, the system allows the registration officer to copy the same address as previous registration. This feature helps the registration officer to save the time while registering the individual who has the same address as previous registration.

Upon receiving a request to copy address details from the previous registration to the current registration, the system performs the following steps:
1. Fetches the address details such as city, state or province, country and postal code of the previous registration from the cache.
   * If the cache does not contain any of those address details, responds with an error message. 
2. The address details will be pre-populated in the respective fields for the current registration and will be further editable. 
1. This feature is applicable to new registrations, pre-registered and non-pre-registered applicants but does not applies to registration correction such as UIN update, lost UIN and deactivate UIN.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### I. Scan and upload of POI, POA and POR
1. The registration officer can input three types of documents- POA, POI and POR while registering an individual
   * POA refers to Proof of Address, POI is Proof of Identity and POR is Proof of Relationship
   * Document type is configurable by admin based on the country level.
2. The registration officer collects these documents from individual and scans them
1. The scan and upload works in such a way that copy of documents is not saved in system or any external device.
1. The scanner scans the documents and uploads them to the Registration Client machine
1. The following parameters will be met while uploading the documents:
   * System lists various document categories as configured by admin
   * For each document category, system enables selection of the list of valid documents
   * The system validates if the document is pdf file format.
   * The system does not allow user to upload more than one document per category
   * The system performs size check after document upload and revert the user to upload again if the document size is more than 1MB (document size is configurable)
   * The system displays the name of the document adjacent to the Document Category for which the document is uploaded 
6. The registration officer can delete files uploaded by mistake.
1. The system allows to view the uploaded file(s)
1. The system allows to download the uploaded file(s)
#### J. Capture an individual's fingerprints as per specification

Registration officer captures an individual’s fingerprints using fingerprint device to authenticate an individual. Fingerprint capture is configurable by the admin at the country level.

**Turn ON or OFF fingerprints capture**

1. If fingerprints capture is turned ON, registration officer captures the individual’s fingerprints using fingerprint device.
1. Alternatively, if fingerprint capture is turned OFF, the system does not show any provision for fingerprint capture and proceeds to the next step.

When the registration officer uses fingerprint capture device to capture the individual left and right hand palm, the left thumb and the right thumb simultaneously, the system performs the following steps:
1. Displays the quality score and threshold score for each captured image.
1. Allows the registration officer to re-try each capture up to a maximum number of times (as configured) if threshold score is not met for one or more fingers.
1. Rejects further capture if the number of capture attempts are greater than the configured limits.
1. Determines and displays rank for each finger. The finger with the highest quality score is ranked 1 and so on till 10 (excluding exceptions)
1. Validates all the available fingerprints that have been captured, the fingerprints, which are above threshold quality and the maximum retries attempted.
1. Retains only that capture which has the highest quality score.
1. Captures and stores the transaction details for audit purpose (except PII data).

#### K. Enable capturing an individual's face photograph

When a registration officer opts to capture photo of an individual, the system initiates a photo capture and performs the following steps:
1. Validates that an on-boarded camera is connected to the machine.
   * If an on-boarded camera is not found, displays an error message.
   * If more than one on-boarded camera is connected, proceeds with the first camera that the system finds as it scans the ports of the machine.
2. Displays the photo preview before capturing.
1. Allows the registration officer to initiate capture.
1. Sends request to the camera for photo capture.
1. Receives the photo from the camera.
1. Displays the photo on screen.
1. Allows the registration officer to proceed to verify quality score.
1. System captures and stores the transaction (User ID or system account; Machine Details; Event Name; Application Name, and Event data) details for audit purpose (except PII data). 
#### L. Capture an individual's face photograph and exception photograph.
1. When a registration officer opts to capture the face photograph or exception photograph of an individual during the registration process, the system validates that an on-boarded camera is connected to the machine.
   * If an on-boarded camera is not found, display an error message.
   * If more than one on-boarded camera is connected, proceed with the first camera that the system finds as it scans the ports of the machine.
1. Displays the face photo preview before capturing.
1. Allows the registration officer to initiate face capture.
1. Sends request to the camera for face photo capture.
1. Receives the face photo from the camera.
1. Display the face photo on screen.
1. Allows the registration officer to proceed to verify quality score.
1. Allows exception photo capture only if an exception has been marked.
   * Step 2 to 7 must be performed to capture the exception photo.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### M. Retry capture of face photo as configured
While registering an individual, a registration officer captures the face photo of the individual. If the quality score of the photo captured is less than the threshold score, the system allows registration officer to retry face capture
1. The system displays the quality score and the threshold score for the capture.
1. The registration officer proceeds to the next step if the quality score >= threshold or if the maximum number of retry attempts as configured is reached.
1. The system validates that:
   * the photo has been captured, and
   * the photo quality score is above threshold quality (or) the maximum retries (as configured) have been attempted.
4. The system maintains a count of the number of retries of face photo for the current registration.
1. Every time a retry is captured, the earlier quality score and threshold score are replaced by the current quality score and threshold score on screen.
1. A retry is allowed only after at least x seconds since the previous capture. The value x is configurable (default value is 10 seconds)
1. The quality score is determined by the SDK and the threshold limits are configured by the admin.
1. The system does not allow further capture if the number of capture attempts are greater than the configured limits and displays an alert message that the retry limit is reached and photo of sufficient quality is not obtained.
1. When the retry limit is reached and photo of sufficient quality is not obtained, the best quality photo is retained. The best photo will be displayed on screen along with its quality score.
1. All the above rules apply to exception photo capture as well.

#### N. Capture Iris as per defined specifications
When the registration officer scans the individual’s irises either individually or together, the system performs the following steps:
1. Displays the quality score and threshold for each captured iris.
1. Allows the registration officer to re-try each capture up to a maximum number of times (as configured) if threshold score is not met for one or both irises.
1. The quality score is determined and the threshold limits are configured.
1. If the quality score meets threshold, a re-capture is not allowed.
1. Validates all available irises that have been captured, the irises, which are above threshold quality and the maximum retries attempted.
1. Retains only the capture, which has the highest quality score.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### O. Restrict registration if the duration since the last export or upload is more than the configured limit
When the registration officer opts to start a new registration or UIN update. The system determines the time of the most recent export or upload (automatic uploads and manual uploads) of registration packets.
If the duration since the last export or upload is not more than the configured limit, then system displays the demographic details page or UIN update page. If exceeded the configured limit, then system displays an error message.

#### P. Choose the 'Opt to Register' option. 

Upon receiving a request to start a new registration, the system performs the following steps:
1. Validates the time since the last sync from server to client has not exceeded the maximum duration permitted (configured from Admin portal).
   * Sync includes Master data, Login credentials, Pre-registration data, Registration center config, Registration center setup, User role setup, Policies, Registration packet status.
2. Validates the time since the last export of registration packets from client to server has not exceeded the maximum duration permitted, if applicable (configured from Admin portal).
1. Validates the number of registration packets on the client yet to be exported to server has not exceeded the maximum limit, if applicable (configured from Admin portal).
1. Reads the config setting that determines if the geo-location of the machine needs to be captured before every registration or captured at beginning of day only.
1. Before every registration, the system captures geo-location of the machine and validates that the captured location is within x meters of the registration center location (Both x and the center location are configured from the Admin portal).
1. If captured at beginning of day only, validates that the beginning-of-day location is within x meters of the registration center location.
1. On successful validation, sends a response and proceeds to the next step of choosing a pre-registered or non pre-registered applicant.
1. In case of failures validation, triggers appropriate error messages.
1. System sends a success response and allows it to proceed to the next step.
1. System captures and stores the transaction details for audit purpose (except PII data).

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/registration/registration-New.md)

### 4.2 UIN Update [**[↑]**](#table-of-content)
When an individual visits the registration center to update their demographic or biometric details, the registration officer captures the updated data as provided by the individual in the system. Refer the following process: 
#### A. UIN Updates Turn ON or OFF

The UIN update feature is configurable by a country. Admin can turn either ON or OFF the UIN update feature.

When an individual approaches the registration officer for UIN update, the following scenarios may arise:

1. If UIN update is turned ON by a country, the registration officer can proceeds to capture the individual’s updated details.
1. Alternatively, if UIN Update is turned OFF by a country the registration officer will not be able to carry out the UIN Update process.

#### B. Registration Client allows update to UIN data only for configured fields
1. An admin can configure the fields that are available for update through the Registration Client. The configuration applies at a country level.
2. The Admin can set the following fields to be update-able at a country level through the admin portal:
   * Name
   * Age/DoB
   * Gender
   * Address
   * Contact details
   * CNIE/EC Number
   * Parent/Guardian details
   * Biometrics-Exception
   * Biometrics-Fingerprint
   * Biometrics-Iris
3. If none of the fields is set up to be update-able, then the system does not allow a registration officer to update any field\s 

#### C. UIN Update
1. The registration officer selects the fields to update for an individual seeking modification of UIN data. Select one or more of the following fields to update the corresponding data: Name, Age or Date of Birth, Gender, Foreigner/National, Address, Email ID, Phone Number, CNIE/PIN/Residence Card Number, parent/guardian Details, Biometrics.
1. Registration officer captures the mandatory demographic attributes (individual's name is captured) and other demographic fields selected for update. In case of update of parent/guardian details, the applicable fields that are updated will be ‘Parent/Guardian Name’ and ‘Parent/Guardian UIN’. The system at this stage also validates that the parent/guardian’s UIN is different from the individual’s UIN. If they are same, displays an error message 
1. Registration officer then uploads documents. The applicable documents are determined by the system based on configuration
1. If biometrics were selected for update, the registration officer marks exceptions and scans all biometrics. Else scans any one biometric.
1. Registration officer captures face photo and exception photo.
1. After capturing all the biometric and demographic details the registration officer can see a preview of the data captured and performs user authentication.
1. If biometric exceptions were marked, supervisor performs authentication.
1. A unique RID (registration ID is generated) on successful completion of registration process. Please refer to [**Wiki**](FRS-Data-Services#4-id-generator-and-validator) for more details.
1. System initiates the process to update UIN after the RID is generated.
   * Receiving a RID do not mean UIN update is successful.
1. Registration officer views and prints acknowledgement. 
1. SMS and/or email notifications are sent to the individual if the contact details are entered during the update process.
1. Refer to the [**Track Status of UIN Update**](FRS-Resident-Services#7-track-status-of-uin-update-) in Resident Services.

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-update-UIN.md)

### 4.3 Lost UIN [**[↑]**](#table-of-content)

When an individual has lost his UIN and visits registration center for retrieval of UIN, the registration officer captures the biometric and demographic details of the individual and processes a request to retrieve the lost UIN. The system sends a notification to the individual upon successful creation of the UIN retrieval request.

The registration officer performs the following steps to retrieve a lost UIN of the individual:

1. Enters demographic details such as name, age or date of birth, etc. of the individual who has lost their UIN. 
   * None of the demographic fields is mandatory.
2. Marks biometric exceptions and captures all fingerprints, irises, face photo and exception photo of the individual.
1. Views a preview of details captured of the individual.
1. Performs user authentication by providing credentials in the configured mode.
1. Supervisor performs supervisor authentication for individuals with exceptions.
1. Views acknowledgement of Lost UIN request with a Registration ID assigned to it.
1. System initiates the process to retrieve a lost UIN after the RID is provided to the individual.
   * Receiving a RID do not mean UIN is successfully retrieved.
8. Prints acknowledgement of the UIN, then SMS and email notifications are sent to the individual if contact details of the individual are entered.
1. The individual will be informed after a Lost UIN gets retrieve. Refer to [**Notification**](FRS-Registration-Processor#331-notification-pluggable-by-si-)
1. System captures and stores the transaction details for audit purpose (except PII data).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-lost-UIN.md)

### 4.4 Acknowledgement and Notifications [**[↑]**](#table-of-content)

#### A. Printing the registration receipt.
1. Upon completion of a registration, the system generates a unique RID 
1. The system generates the registration receipt.
1. The registration receipt contains details in a print-friendly format.
   * Receipt includes labels and data in two languages - the default language and the secondary language as configured. 
   * All labels and fields are in the default language. Only name and address labels and fields are shown in the secondary language
   * Receipt displays the 2D bar code.
4. This print friendly receipt can then be printed using a printer

#### B. Acknowledgement receipt sent by email on completion of registration process [**[↑]**](#table-of-content)
1. When a registration is completed, that is, a Registration ID has been generated and assigned the system. Based on the notification language, the system sends an acknowledgement email to the individual.
   * Notification language is set by a country's admin, who determines in which language, a notification is sent to the individual. Notification language can be either primary language or combination of both primary and secondary language.
   * In case of UIN Update or Lost UIN, the system sends a notification to the individual.
2. The email template is defined by the admin at country level.
3. Email is sent to the email address entered during registration.
4. The subject and the body of the acknowledgement email are configured by admin.
5. No email is sent under the following scenario
   * If mode of confirmation is not set to ‘email’ or ‘email and SMS’
   * If an email address is not provided during registration
   * If the client is not online during registration completion
#### C. Acknowledgement receipt sent by SMS on completion of registration process
1. When a registration is completed, that is, a Registration ID has been generated and assigned the system. Based on the notification language, the system sends an acknowledgement SMS to the individual.
   * Notification language is set by a country's admin, who determines in which language, a notification is sent to the individual. Notification language can be either primary language or combination of both primary and secondary language.
   * In case of UIN Update or Lost UIN, the system sends a notification to the individual.
2. The template of the SMS is defined by the admin at the country level.
3. The “from” ID of the SMS will be set up by the System Integrator.
4. The system triggers the SMS to the mobile number provided during registration.
5. The SMS contains the details as per the template configured by a country.
6. An SMS is triggered regardless of the applicant being an adult or child as determined by the date of birth.
7. The system will not be able to send SMS, if the client is not online at the time of registration completion.

#### D. Sending email and SMS acknowledgements to additional recipients
This feature enables Registration Client to send SMS and email acknowledgements to additional recipient\s (other than the individual’s primary email ID and mobile number).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-acknowledgement-notification.md)

### 4.5 Biometric Capture (SDK Integration, Extract and Match) (WIP) [**[↑]**](#table-of-content)

Registration Client performs a local duplicate check for irises and face of an individual against the mapped registration officers' biometrics
1. The registration officer captures the irises of the individual and opts to proceed further in the registration process
1. The system performs a local duplicate check of the individual’s irises with the irises of all the users on-boarded to the client.
1. In case of forced capture, the system uses only the best capture for local duplicate check
1. The iris images of the individual are compared with the irises of the users mapped to the client.
1. Each iris is matched individually.
1. The two captured irises are also compared against each other to identify a potential duplicate.
1. The SDK determines the match score, and this is compared with the threshold match score. If match score >= threshold then it is a match.
1. If at least one iris match is found, the system displays an alert, sets retry count to zero, and requires recapture of both irises.
1. If a match is not found, allows the user to proceed to the face capture step
1. The registration officer captures the face photo and opts to proceed further in the registration process
1. On force capture/successful capture of face performs a local duplicate check of face of the individual against faces of all users on-boarded to the client.
1. In case of forced capture uses only the best capture for local duplicate check
1. The system performs a local duplicate check of the individual’s face with the faces of all the users on-boarded to the client.
1. If a match is found, the system displays an error message and require individual to provide the face scan again.
1. When no match is found, the system proceeds to the next step (Registration Preview).
1. The number of recapture attempts due to local duplicate check failures is not capped.

Please refer to [**Wiki**](MOSIP-Biometric-APIs) for more details on the MOSIP Biometric APIs.

[**Link to design**](/mosip/mosip/blob/master/docs/design/registration/registration-MOSIP-bio-device-integration.md)

### 4.6 Biometric Exceptions [**[↑]**](#table-of-content)
If the required biometric quality is not achieved while a registration officer is capturing biometrics of an individual (e.g., missing finger(s), missing iris(es), etc.), then the system mandates to capture a biometric exception for that individual. Refer the following process:
#### A. Low quality biometrics marked as reason for exceptions

1. During a registration process while capturing biometrics, if the configured threshold is not met for fingerprints and/or irises in spite of the x attempts (configurable) to capture the biometrics, then system mandates capture of exception photo 
1. Also, system automatically flags the reason for exception as ‘Low Quality of biometrics’. 
1. If the individual has missing biometrics and low quality of biometrics, both the reasons are auto-associated. Here also the system mandates capture of exception photo.

#### B. Mark fingerprint and iris exceptions for an individual

1. During a registration process after the demographic details and documents have been captured, the system allows a registration officer to mark biometric exceptions for missing finger(s) and missing iris(es) if the individual has any such exceptions.
1. If ‘Biometric Exception’ is ‘Yes’, at least one missing biometric must be mandatorily marked.
1. The registration officer can mark the missing finger(s) and missing iris(es).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-registrationscreen.md)

### 4.7 Registration Officer and Supervisor Approval [**[↑]**](#table-of-content)

When a registration officer captures biometric exceptions of an individual, then a supervisor has to validate/approve that biometric exception. This approval is required to authenticate the captured biometric exception of the individual.

**Supervisor authentication for biometric exceptions**

1. The 'supervisor authentication for exceptions' process is configurable and can be switched ON or OFF at a country level by the Admin 
1. A registration officer completes user authentication at the end of registering an individual with exceptions.
1. If a country has opted to turned on supervisor authentication, a supervisor is required to enter their credentials
1. The mode of supervisor authentication is a configurable at the country level. It can be set to password, OTP, fingerprint, or multifactor.
1. In case of OTP authentication, the client first sends a request to server to generate the OTP, then allows the supervisor to provide OTP and requests the server to match the input value with the generated OTP.
1. In case of multifactor authentication, the client prompts the supervisor to provide credentials in the order configured and authenticates each input before proceeding to the entry of the next credential.
1. On successful validation, the system proceeds to the next step of Registration ID generation and displays of registration acknowledgement.
1. If the validation fails, the system displays an error message and allows user to try again. Unlimited attempts are allowed.
1. Based on country-specific requirements, it is also possible for the registration officer and supervisor to be the same person. In this case, the registration officer and supervisor will be required to provide biometrics twice in succession, once as part of the Officer authentication and once for supervisor authentication of exceptions.
1. Alternatively, if supervisor authentication is turned OFF, system does not show the supervisor authentication option at all and a registration officer may proceed to the next step (acknowledgement).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-registrationscreen.md)

### 4.8 End of Day Process [**[↑]**](#table-of-content)

#### A. Approval of registrations through an end of day process.

As a process, MOSIP enables a designated user to review/approve every registration at the end of day before the packet is sent to Registration Processor. This process is done to prevent fraudulent of the packets.

Supervisor can log in to the Registration Client application and view a list of Registration ID that are awaiting for approval

The supervisor may opt to see the details of one or many Registration ID. The supervisor can view the details on the right hand side pane 

The supervisor then chooses to either approve or reject the registration.

The supervisor must provide a reason in case of rejection. 

The supervisor then authenticates the registration by providing any one biometric - fingerprint, iris, or face.
The system then confirms on successful approval.

1. In case of authentication failure, the supervisor can try again by providing the same or different biometric.
1. The packet status will change only when supervisor completes authentication. Else, the packet status will revert to its original status.
1. The packets, which are approved or rejected followed by successful authentication are removed from the ‘Pending Approval’ list.
1. The approved and rejected packets are placed in the upload location on the client and will be sent to server during the next upload.

#### B. Supervisor can inform individuals to 'Re-register'
When the Registration Processor finds an error in the packet such as registration failure (incorrect or duplicate demographic and biometric information), the status of the packet is marked as Re-register. After receiving a status as Re-register, a supervisor then informs an individual to re-visit the registration center to re-register the application. Refer below for the process:

1. A supervisor can view the packets whose status has been received from the processor as ‘Re-register’.
1. The system displays the list of Registration IDs that have been flagged as ‘re-register’ during packet status sync from the processor.
1. The supervisor can see the registration details (the acknowledgement slip) for Registration ID\s
1. Supervisor informs the individual by phone, email, physical mail, or physical visit to re-register. This is an offline process.
1. Supervisor also records it in the system that he has ‘Informed’ the individual
   * If unable to contact the individual, the supervisor records it as ‘Can’t inform'.
6. The supervisor then authenticates by providing biometric data -fingerprint, Iris, or face. Further, selects the specific finger or iris being provided.
1. The supervisor authenticates with locally stored biometric and with the results.
   * On successful authentication, the actioned packets are removed from the ‘-Re-register’ list.
   * On unsuccessful authentication, the user can retry their authentication with the same or a different biometric

#### C. Authenticated registrations report (WIP)
The system allows the supervisor to view a report of approved registrations for the past 15 days.

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-eod-process.md)

## 5. Geo-location [**[↑]**](#table-of-content)
Upon receiving a request to geotag a registration machine, the system performs the following steps:
1. Validates that an on-boarded GPS device is connected to the machine.
   * If an on-boarded GPS device is not found, then displays an error message.
   * If more than one on-boarded GPS device is connected, then proceeds with the first GPS device that the system finds as it scans the ports of the machine.
2. Requests the GPS device to capture a location.
1. Receives the latitude and longitude from the GPS device.
   * If signal is weak and GPS device is unable to capture location, then displays an error message.
4. Proceeds to perform following validations:
   * If location capture is required only at the beginning of day, the co-ordinates are stored and validations are performed when opting to start a new registration.
   * If location capture is required only at the beginning of day and location could not be captured at beginning of the day, then attempts to capture the location during the first registration of the day.
   * The latitude and longitude will be stored in the packet when the packet is created.
5. System captures and stores the transaction details for audit purpose (except PII data).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-device-integration.md)

## 6. Language Support [**[↑]**](#table-of-content)
The Registration Client supports two languages, a primary language in which all pages of the application are rendered, and a secondary language in which select pages such as demographic details are also rendered for convenience of the individual. French and Arabic are the default primary and secondary languages, which are driven by an admin (configurable) and can be setup by the admin as required. Transliteration from the primary to secondary language is supported for user entered text fields.
### 6.1 Translation [**[↑]**](#table-of-content)

**A Registration Officer can view static data translated to secondary language**

1. In MOSIP, the primary and secondary languages are configured by the admin 
1. All static data (headers, labels, action buttons, and alert messages) is set up by the admin in both languages so that the registration officer can view all pages in the client application in both the default (primary) language and translated (secondary) language. 
1. If configured translation language is same as default language, the system displays text in default language only.

### 6.2 Transliteration [**[↑]**](#table-of-content)

**Registration Client enables viewing transliterated data other than French and Arabic**

The Registration Client application will support two type of languages: Primary language (the language in which the registration officer enters data) and secondary language (transliteration language). The secondary language is country specific and is set by the administrator

When a registration officer starts a new registration, update or lost UIN process and enters data in the primary language for the demographic fields such as: Full Name, Address Line 1, Address Line 2, Address Line 3, and parent/guardian Name.

System transliterates the data and displays in the corresponding secondary language fields.

The following data are transliterated into the secondary language in addition to being shown in the primary language.
1. Demographic details page: Data for Full Name, Address Line 1, Address Line 2, Address Line 3 and parent/guardian Name.
1. Registration preview page: Data for Full Name, Address Line 1, Address Line 2, Address Line 3 and parent/guardian Name.
1. Registration confirmation page: Data for Full Name, Address Line 1, Address Line 2, Address Line 3 and parent/guardian Name.

Registration officer can invoke the virtual keyboard to edit transliterated data and proceeds with registration. The following rules are followed during transliteration.
1. Editing transliterated fields does not change the data entered in the primary language field
1. The system also validates the maximum character length in the transliterated field and ensures that it is same as the limits defined for the primary language field.
1. If no secondary language is set, system does not do any transliteration and will display empty space instead.
1. Numeric fields are not transliterated. The same numerals are displayed in the secondary language section of the page and are not editable.

Master data selections are not transliterated. Instead, the master data as setup in the secondary language is displayed in the relevant section. 

The registration officer can then view the preview page

The system then enables a registration officer to view the registration confirmation page. The fields as transliterated and edited earlier are also shown in the secondary language.

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/registration/registration-muti-lingual-support.md)
## 7. Packet Upload [**[↑]**](#table-of-content)
### 7.1 Registration Packet Upload [**[↑]**](#table-of-content) 

#### A. Upload the packet
1. The registration officer views a list of packets.
1. The registration officer may opt to upload one or multiple packets from a list of packets.
1. After the registration officer selects the packet/s, he/she can upload the selected packet/s to server.

   NOTE: If any packets are selected, the ‘Export’ feature will be disable because the selection of packets is applicable only for ‘Upload’ feature.

#### B. Push those packets that are marked 'Resend' to the server

1. When the registration officer or supervisor navigates to the ‘Upload Packets’ page, the list of RIDs that are pending packets to upload will be displayed.
   * Pending packets are those packets, which are not sent to the server due to various reasons (e.g. Sanity Check and Validation failure in the Registration Processor) and have been marked for resending.
2. When the registration officer or supervisor selects the ‘Upload’ option, the pending packets will be uploaded to the server.
3. The result of each packet uploaded will be displayed as ‘Success’ or ‘Failure’.
   * Packets that are successfully sent or resent will not be sent again unless the server requests for them.
   * Packets for which upload fails will continue to be in pending state.
4. System captures and stores the transaction details for audit purpose (except PII data).

#### C. Enable a real time packet upload when system is online upon registration submission

**(i) When EoD process is turned ON**

1. Registration Client checks if the system is online as soon as the assigned approver (such as supervisor) approves or rejects a new registration or UIN update.
1. If client is online, the Registration Client sends Registration ID to server and then the packets are marked as “Ready to upload” and auto uploaded to server.
1. If client is offline or on low bandwidth, then when the client next comes online, the Registration ID’s are sent to server through scheduled or manual sync and the packets are then marked as “ready to upload”.
1. Once the packets are ready for upload, packets are uploaded in two ways:
   * The registration officer can initiate upload to server using upload function.
   * Export to external storage device for subsequent upload as required.
5. System captures and stores the transaction details for audit purpose (except PII data).

**(ii) When EoD process is turned OFF**

1. Registration Client checks if system is online as soon as the registration officer submits a new registration or UIN update.
1. If client is online, the Registration Client sends Registration Id to server and then the packets are marked as “Ready to upload” and auto uploaded to server.
1. If client is offline or on low bandwidth, then when the client next comes online, the Registration ID’s are sent to server through scheduled or manual sync and the packets are then marked as “ready to upload”.
1. Once the packets are ready for upload, packets are uploaded in two ways:
   * The registration officer can initiate upload to server using client’s upload function.
   * Export to external storage device for subsequent upload as required.
5. System captures and stores the transaction details for audit purpose (except PII data).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration-packetupload.md)

### 7.2 Offline upload (Packet Exporter) [**[↑]**](#table-of-content)

System exports registration packet data from client machine to an external device as follows:
1. Allows the registration officer to select a destination folder.
   * The destination folder includes the laptop/desktop, an external hard drive or a remote location.
   * External storage devices are not necessary to be MOSIP-registered devices.
1. When the destination folder is selected, user initiates export of packets.
1. System exports the packets to the selected folder and performs the following steps:
   * Identifies the packets in ‘Ready to Upload’ state.
   * If EoD process is turned ON, packets that have been approved or rejected and packet ID sync is completed are considered ‘Ready to Upload’.
   * If EoD process is turned OFF, packets are considered ‘Ready to Upload’ as soon as the registration is submitted and packet ID sync is completed.
   * Puts the packets in the destination folder.
1. Once the server acknowledges that the packets have been received, which is uploaded from the external device to the server, the packets in the client will be marked as ‘Uploaded’.
   * Packets that remain in ‘Ready to Upload’ status will be exported again when the next export is executed.
   * Packets in ‘Uploaded’ or any other status will not be exported again.
1. All the Registration Officers and supervisors on-boarded to the client machine are able to export all packets.
1. Supports the partial export. If the system is able to export some packets to the folder and no other files due to lack of storage space or unavailability of the folder, the successfully exported packets will remain on the destination folder.
1. For partial or full failure, the system displays error message.
1. System captures and stores the transaction details for audit purpose (except PII data).

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registrtaion-packet_export.md)

## 8. Analytics and Audit Logs [**[↑]**](#table-of-content) 
System captures and stores details of each transaction during registration process for audit purpose (except PII data). The audit data is stored in the audit database. When the client machine is working in an offline mode, the audit log is synced with the server as when the client machine is online. 
## 9. Data Security [**[↑]**](#table-of-content)
Registration Client integrates with Trusted Platform Model (TPM) data integrity. For enhanced security and integrity purposes, data captured from individuals are saved securely in local system and then shared to server. The details saved locally will be encrypted. Database encryption is also mandatory.

MOSIP performs the following:

1. Signing the data (This process is called as Signature) using Private Key provided by the TPM
   * This process will ensure that the request to the server has been dispatched from a registered or trusted Registration Client machine
2. Validates the signature against the actual data using the Public Key or Public Part. The application does not connect or access the underlying TPM to validate the Signature. This validation ensures that the request is from a registered or trusted Registration Client machine
1. Encrypts and decrypts the data using RSA algorithm in TPM

### 9.1 Key Management [**[↑]**](#table-of-content)

The data captured and stored in to the client machine during different process (such as new registration, update UIN, lost UIN, pre-registration) will be encrypted with the different set of keys. The keys have a different set of expiry policies, based on which it will be refreshed. The keys are securely managed into the database.

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/registration/registration-key-management.md)

## 10. Software Version Upgrade [**[↑]**](#table-of-content)

#### A. Registration Officer or Supervisor can download and unzip the client application set up kit

Initial installation of the client software on a particular machine, supervisor or registration officer will download an installable software (setup kit) from an admin portal. Then unzip the setup kit and install it in the client machine.

When a registration officer or supervisor opts to download setup kit and selects the OS-specific setup kit to download, the system allows the user to download the setup kit to the storage location chosen by the user

1. User then unzips the setup kit.
1. Extract the files and folders from the zip file to the chosen location.
1. Allows the user to verify that the files and folder structure are as described in the design document.
1. System captures and stores the download transaction details for audit purpose (except PII data). 

#### B. Update the client software from the server
If a software update is available, then the system will provide an option to supervisor or registration officer to update either immediately or later. If the maximum number of days without software update has been exceeded, then the system will mandate a user to update the software.

The system follows the following steps during the update process:
1. When the client is online, the system automatically checks for updates if available.
1. If an update is available, the system displays a message “Updates are available” and provides two options to the registration officer 
   * Update now or 
   * Update later.
1. If the registration officer opts to select “Update now” option, then the registration officer can download and installs software and launches the application.
1. The updates are downloaded as patch updates.
1. When installation is in progress, the user cannot perform any action on the client.
1. Once installation is completed, the user can start working on the client.
1. If update is not successful, the system provides error message and provides both the options (Update Now or Update Later) again.
1. If the registration officer opts to select “Update later” option, then the system checks if the freeze period has been reached.
   * If the freeze period has not been reached, the system allows the registration officer to continue with registration
   * If freeze period has been reached, the system does not allow the registration officer for registration without updating the software.
   * The client will be locked for registration, if x days (configuration setting) have passed since the last check for updates and mandates the registration officer to update the software.
1. If updates are not available, the system launches the application.
1. If update is not successful, the client returns to its earlier version.
1. System captures and stores the transaction details for audit purpose (except PII data).

Refer to [**Wiki**](Registration-Client-Setup) for more details.


## 11. Clean up [**[↑]**](#table-of-content)

Pre-registration and registration data are automatically deleted from the client machine upon consumption and upon intimation from the server respectively. 
* Pre-registration data is deleted from the client machine immediately after consumption for a registration.
* Registration packets that are identified as ‘processed’ are deleted by a periodic process.
* Audit data is deleted after it is sent to the server.
* All deletion is executed by a periodic process after retention of the data for a configured duration.

### 11.1 Data retention policies [**[↑]**](#table-of-content)

#### A. Read packet status and delete packets
When the Registration Client receives a request through manual trigger or scheduled job to sync data, the system performs the following steps to read a packet status and delete the packets:
1. Sends request to server for sync.
1. Receives response from server with packet statuses.
   * Server sends status of those registration packets that were created in the specific machine, and that status that has changed since the last sync.
1. Saves the statuses ‘Processing’, ‘Processed’ or ‘Resend’ as received for each packet. Statuses of other packets are not updated.
1. Sends success or failure message to the UI.
1. Immediately deletes the packets from the local machine whose status is received as ‘Processed’.
1. Displays an alert in case of sync failure.
   * The on-screen message is only indicated if the sync was a success or failure.
   * Detailed errors can be viewed in the transaction logs.
1. When a sync is running, the system does not allow the user to perform any other action.
1. If the Registration Client is not online or not open during a scheduled sync, the sync will be queued up and executed later. When the Registration Client is next launched and is online, checks if the previous scheduled sync was executed. If not executed earlier then immediately starts the sync.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### B. Delete transaction history (audit logs) post sync with server and the retention period
When a set of audit data is uploaded to the server and the server has acknowledged receipt of the audit data, the system performs the following steps to delete transaction history (audit logs) post sync with server and the retention period:
1. Runs on a daily process to identify audit data that has been sent to the server and acknowledgement is received from the server.
   * The audit data acknowledgement received from the server >= x hours ago. X is configured at a country level.
2. Deletes the identified audit data from the client machine.
1. Executes at a time and frequency as configured. 
   * The process takes place only when the Registration Client is in open and running situation. If the Registration Client is not open during a scheduled run, it is executed as soon as the client is next started up.
4. Does not delete audit data if that is yet to be sent to the server.
1. System captures and stores the transaction details.

[**Link to design**](/mosip/mosip/tree/master/docs/design/registration/registration_packet_deletion_job.md)

### 11.2 Machine Retirement [**[↑]**](#table-of-content)

Machine is termed as machine retirement due to following reason:
* If the machine has obsolete specification.
* When the machine is moved from one center to another, then the machine will retire from that old center.

Before the machine is decommissioned, the following checks must be performed:

1. All packets created must either be uploaded to server or exported to external device.
2. All data locally saved in the machine must be cleaned up.


