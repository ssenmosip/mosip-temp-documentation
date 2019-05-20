## Table Of Content

- [1. User Services](#1-user-services-)
  * [1.1 User on-boarding](#11-user-on-boarding-) _(REG_FR_1.1)_
  * [1.2 Login/Authentication](#12-loginauthentication-) _(REG_FR_1.2)_
  * [1.3 Logout](#13-logout-) _(REG_FR_1.3)_
- [2. Data Sync](#2-data-sync-)
  * [2.1 Master Data Sync](#21-master-data-sync-) _(REG_FR_2.1)_
  * [2.2 Configuration Sync](#22-configuration-sync-) _(REG_FR_2.2)_
  * [2.3 Packet ID Sync](#23-packet-id-sync-) _(REG_FR_2.3)_
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
  * [4.5 Biometric Capture (SDK Integration, Extract and Match)](#45-biometric-capture-sdk-integration-extract-and-match-) _(REG_FR_4.5)_
  * [4.6 Biometric Exceptions](#46-biometric-exceptions-) _(REG_FR_4.6)_
  * [4.7 Operator and Supervisor Approval](#47-operator-and-supervisor-approval-) _(REG_FR_4.7)_
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

Initially, when a Registration Officer or Supervisor logs in to a client machine, the Registration Officer or Supervisor provides their biometric details, which will be stored and mapped to the client machine locally. Which in further, helps Registration Officer or Supervisor to work when the server is offline.

#### A. Map registration officers and supervisors to a client machine.
Initially a machine will have no users on boarded. The first Registration Officer/Supervisor will be on boarded by an Administrator or from the backend. Thereafter this Registration Officer/Supervisor can onboard other users.
1. This functionality allows the system to create new mapping between registration officers and supervisors to a client machine
1. Allow the system to receive the request for mapping a registration officer / supervisor to the client machine with selected data
   * Fields selected on the UI include user, status, fingerprints, and irises.
   * The list of users will include only active users. The system does not show users who are blacklisted or decommissioned.
   * The list of users does not include users who are already mapped to the machine.
   * All 10 fingerprints are captured and authenticated with the server. The machine must be online for this authentication.
   * The system then validates the fingerprint quality threshold is met.
   * The system then validates the number of successful fingerprint authentications is greater than or equal to the config setting of fingerprint authentications required.
   * Unlimited retries are allowed.
   * Both irises are captured and authenticated with the server. Validate that the iris quality threshold is met.
   * Validate that the number of successful iris authentications is greater than or equal to the config setting of iris authentications required.
   * Unlimited retries are allowed.
3. If validations are successful, then the system performs the following:
   * Save the mapping locally.
   * Successfully authenticated fingerprints and irises will be stored locally.
   * Fingerprints and irises with unsuccessful authentication will not be stored.
   * The status of the mapping is set to ‘Active’ or ‘Inactive’ as selected.
   * Mapping will be sent to the server during the next sync.
   * Biometrics will not be sent to the server.
4. If not successful: Triggers an error message.
5. Multiple users can be mapped to the machine by repeating the above flow. There is no limitation to the numbers of users mapped.

#### B. Registration client enables capturing an officer's biometrics during on-boarding in order to support login, local duplicate checks, and registration submission
1. When a Registration Officer or Supervisor enters his/her log in to registration client with their credentials, the system validates that the user is mapped to the same Registration Centre's client machine. System validates that the user is yet to be on-boarded to the client machine. System directs the user to the password entry page.
1. User enters password and submits. System sends OTP to the user and directs to the OTP entry page. Lock the user account for 30 minutes if an incorrect credential (password or OTP) is entered 5 times in succession.
1. User can request the system to resend OTP if not received earlier.
1. User enters OTP and submits. System directs the user to the dashboard page with all links disabled except for ‘User on-boarding’.
1. User navigates to the User on-boarding page.
1. User marks biometric exceptions if any (system do not mandate capture and authentication of those biometrics that are marked as exceptions).
1. User scans left slap, right slap and two thumbs. System displays the result of authentication of each finger.
1. The system validates that the device is registered in the Admin portal, associated to this Registration Centre ID, and the current date lies within the validity dates of the device model.
1. User scans both irises. System displays the result of authentication of each iris. User scans face and exception photo. System displays the result of authentication of face. Exception photo is not authenticated
1. User can choose to retry each biometric capture as required. There is no limit to the number of retries.
1. User submits then opts to submit the data. System validates that the total number of successful authentications is greater than or equal to the threshold value configured. System maps the user to the client machine and displays a pop-up confirmation message. System saves the successfully authenticated biometrics locally.
1. System validates that the total number of successful authentications is greater than or equal to the threshold value configured. For example, if 9 fingers + 2 irises + face are successfully authenticated, the total number of authentications is 9+2+1=12. Validate that 12 is greater than or equal to the threshold configured (say 10). Then save the user-machine mapping and the authenticated biometrics locally. Do not save the biometrics that are not authenticated.
1. The system displays the result of authentication of each biometric - 10 fingers, 2 irises and face - in a list.
1. User gets access to all links on the client according to their role.
User can update their biometrics at any time after successful on-boarding by choosing the ‘User on-boarding’ link from the menu. The biometrics provided during update will be authenticated with the server and saved locally if threshold for successful authentication is met. Updated biometrics will overwrite the biometrics stored locally earlier.

### 1.2 Login/Authentication [**[↑]**](#table-of-content)

#### A. Allows biometric login of the Registration Officer or Supervisor to the client application

MOSIP supports single factor and multi factor login including iris and face capture. An Admin config setting determines the mode of login. 

1. The Registration Officer or Supervisor opts to login to registration client application
   * System enables user to login by entering username, and submit iris and face photo.
2. The user enters their username.
3. The user scans any one iris through the iris capture device.
4. The user then captures face photo using the face photo capture-device.
5. On successful authentication, the system logs in the user.

#### B. Temporarily lock the user account after five unsuccessful login attempts.
1. The MOSIP system temporarily locks the user to login in case the user gives an invalid password for login five times continuously.
1. Upon the fifth unsuccessful attempt to login, displays an error message 
1. The temporarily lock lasts for 30 minutes (configured by an admin).
1. The same error message is displayed for any subsequent login attempt within 30 minutes.
1. After 30 minutes, the lock is released and the count of invalid login attempts is reset to zero.
1. The same is implemented if the fingerprint, iris, face, or multifactor login fails five times.
1. System captures and stores the transaction details for audit purpose (except PII data).

#### C. Authenticate online/offline login of the Supervisor to the client application [**[↑]**](#table-of-content)
If the Registration Client is offline, then system allows the supervisor to log in to the client machine only with a password-based login. Whereas, if the Registration Client is online, the supervisor can log in to the client machine with all various type of login such as Password-based login, OTP based login, etc.

When a supervisor opts to log in to the client machine the systems displays the appropriate options as per the mode of login.

* If the mode of login is username and password, displays the password-based login.
* If the mode of login is username and OTP, display the OTP based login 


**Password-based login**

The mode of login is configured by admin, if the login is configured as Password-based login, the supervisor can login to the client machine in both online and offline mode.

1. System allows the user to enter their username and password and submit.
1. System validates that the username belongs to an on boarded Registration Officer or Supervisor on that client.
1. System validates that the password matches the user’s password stored locally. The local password will be fetched from the server during sync.
1. System validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
1. System validates that the user has a role or Registration Officer or Supervisor. 

**OTP based login**

If the client machine is online and is mapped with the supervisor, then the system allows supervisor to login with the OTP-based login. The system allows supervisor to enter their username and authenticate himself or herself with OTP.

1. Allows the user to enter their username and submit.
1. Validates that the username belongs to an on-boarded Registration Officer or Supervisor on that client.
1. Generate and send an OTP by SMS to the user’s registered mobile number. Use the template defined in Admin for the OTP message. 
1. Allow the user to enter the OTP and submit.
   * Alternatively, allow the user to change entered username.
   * Alternatively, allow the user to request for resending the OTP.
5. Validates that the OTP submitted matches the one that was generated and is submitted within its validity period.
6. Validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
7. Validates that the user has a role of Registration Officer or Supervisor.
8. On successful validation of all conditions above, display the logged in screen to the user

#### D. Restrict access to each MOSIP feature to authorized users. [**[↑]**](#table-of-content)

In MOSIP system, a user can have multiple role. When a user is registered on admin portal, the system allows user to assign multiple roles.

When a logged in user tries to access a feature on the registration client the system determines if the requested feature is accessible to the role(s) mapped to the user.
1. If yes, permits the user to access the requested feature.
1. If no, displays an error message or hide the link to the feature as applicable. The UX design will drive whether to hide a link or display an error on click of the link.
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

### 1.3 Logout [**[↑]**](#table-of-content)
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
5. Upon logout, any unsaved data will be lost. Data will not be automatically saved in the database and will not be retained in memory.
1. The System also captures and stores the transaction details for audit purpose (except PII data).

## 2. Data Sync [**[↑]**](#table-of-content)
### 2.1 Master Data Sync [**[↑]**](#table-of-content)
### 2.2 Configuration Sync [**[↑]**](#table-of-content)
### 2.3 Packet ID Sync [**[↑]**](#table-of-content)
### 2.4 Packet Status Sync [**[↑]**](#table-of-content)
### 2.5 Pre-registration Data Download [**[↑]**](#table-of-content)
## 3. Health Check [**[↑]**](#table-of-content)
### 3.1 Peripherals Check [**[↑]**](#table-of-content)
### 3.2 Disk Space Check [**[↑]**](#table-of-content)
If disk space is insufficient, system displays an error message and data entered by registration officer will be not be save. Then Registration officer will clean up to make sufficient space on the client machine and tries the registration again.

Upon receiving a request from the UI to create an enrolment packet at the end of data capture and authentication steps, the system validates the disk space available on the client machine to store the enrolment packet as follows:
1. Calculates the size of the enrolment packet based on the data captured.
   * Data includes demographic, biometric, photographs, OSI authentication, enrolment metadata, audit data, and acknowledgement scan.
2. Calculates the disk space, which is available in the configured packet storage location.
1. Validates if the storage location is sufficient to store the enrolment packet.
1. In case of successful validation, responds with success message and proceed further. 
1. In case of unsuccessful validation, responds with an appropriate error message.
1. System captures and stores the transaction details for audit purpose (except PII data).

### 3.3 Virus Scan/Security Scan [**[↑]**](#table-of-content)

Upon receiving a request to perform a virus scan of the registration packets on the client machine, the system performs the following steps:
1. When the client application is open, the system scans the registration packets at a configured frequency.
1. Checks if viruses are available in the registration packets that are stored on the client machine.
   * All registration packets on the machine will be scanned.
3. At the end of the scan, displays an alert message (Security scan detected viruses in the following files [List of files]. Please take necessary action or contact the administrator) on screen if a virus is detected.
1. If the client application is not open at the configured time, the scan will be queued up and runs only when the client application is open.

## 4. Registration Data Services [**[↑]**](#table-of-content)
### 4.1 New Registration [**[↑]**](#table-of-content)

#### A. Capture consent from the individual for data storage and utilization				
1. For every registration, the system provides an option for the Registration Officer to mark an individual's consent as Yes or No
1. The Registration Officer marks consent after confirming with the individual offline.
1. Whether the consent is marked as Yes/No, it will not have any impact on issuance of UIN for that individual and the system will not execute any validations in this regard during packet processing.

#### B. Transliteration: Virtual keyboard

Refer to the section related to [**Transliteration and Virtual Keyboard**](#5103-transliteration-and-virtual-keyboard-).
#### C. Mark an individual's date of birth as 'Verified' (Not Specified for Morocco)
1. For new registration or UIN update, the system provides an option for the Registration Officer to mark an individual's date of birth as ‘Verified’.
1. For a new registration, the ‘Verified’ field is displayed as an option next to Date of Birth field. The default state is unchecked. When checked, it indicates that the Registration Officer has verified the date of birth of the individual.
1. For a UIN update, the ‘Verified’ field is applicable only when the Age/Date of Birth field is selected for update.
#### D. Register an individual who is less than 5 years old.
1. MOSIP system does not have an explicit ‘Category’ for registering children less than five years. However, the date of birth will automatically determine the category of the applicant, which can be setup by the country as required.
1. When a registration officer starts a new registration, the system intuitively determines if the registration is for a child using the date of birth.
1. If the date of birth indicates that the registration is for a child is less than 5 years on the date of registration, and if parent/guardian’s UIN exists. Then the system captures parent/guardian's details: UIN/Name/Biometrics/Proof of relationship. 
1. If the date of birth indicates that the registration is for a child is less than 5 years and if parent/guardian’s UIN does not exist then the system ensures parent/guardian is registered first and at least RID is available.
1. The system captures parent/guardian's details: Registration ID/Name/-Biometrics/PoR (Processor will pick up parent/guardian's registration first prior to child)
#### E. Mark an individual as Foreigner or Non-Foreigner
For every new registration, the system provides an option on the demographic details page for the Registration Officer to mark an individual as either a citizen of that country or a Foreigner. 

If the Registration Officer selects the desired option, indicates that the individual is a Foreigner. If option is not selected, indicates that the individual is a citizen of that country.
#### F. Enter the demographic details for registration

**The Registration Officer opts to initiate a new registration**
1. The system allows the registration officer to enter the individual’s demographic details such as Name, Gender, DOB, Residential Address, and other fields based on the [**ID Object Definition**](MOSIP-ID-Object-definition). 
1. The system validates the entered demographic fields.
1. If demographic fields validation fails, the system displays an error message.
1. On successful validation, the system proceeds to next step.

**The Registration Officer selects a pre-registration for registration**

1. Registration Officer enters the PRID provided by a pre-registered individual. 
1. The Registration Officer enters demographic details or edits pre-filled demographic details (details rendered from the provided PRID).
1. The Registration Client validates the entered demographic data as per the [**field definition document**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/Reg.%20Client/MOS-1220%20New%20Registration%20Field%20Definition.docx).
1. Displays error message(s) on screen in case of validation failure.
1. On successful validation, proceeds to next step.
#### G. Copy address from the previous registration
Upon receiving a request to copy address details from the previous registration to the current registration, the system performs the following steps:
1. Fetches the address details such as city, state or province, country and postal code of the previous registration from the cache.
   * If the cache does not contain any of those address details, responds as an error message. 
2. The address details will be pre-populated in the respective fields for the current registration and will be further editable. 
1. This feature is applicable to new registrations, pre-registered and non-pre-registered applicants but does not applies to registration correction such as UIN update, lost UIN and deactivation scenarios.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### H. Scan and upload of POI, POA and POR
1. The Registration Officer can input three types of documents- POA, POI and POR while registering an individual
   * POA refers to Proof of address, POI is proof of Identity and POR is proof of relationship
   * Document type is configurable by admin based on the country level.
2. The Registration officer collects these documents from individual and scans them
1. The scan and upload works in such a way that copy of documents is not saved in system or any external device.
1. The scanner scans the documents and upload them to the registration client machine
1. The following parameters will be met while uploading document
   * System lists various document categories as configured by admin
   * For each document category, system enables selection of the list of valid documents
   * The system validates if the document is pdf file format.
   * The System does not allow user to upload more than one document per category
   * The System performs size check after Document upload and revert the user to upload again if the Document Size is more than 1MB (Configurable)
   * The System displays the name of the document adjacent to the Document Category for which the document is uploaded 
6. The registration officer can delete files uploaded by mistake.
1. The System allows to view uploaded file(s)
1. The System allows to download the uploaded file(s)
#### I. Capture an individual's finger prints as per specification
When the registration officer uses finger print capture device to capture the individual left and right hand slap, the left thumb and the right thumb simultaneously, the system performs the following steps:
1. Displays the quality score and threshold score for each capture.
1. Allows the registration officer to re-try each capture up to a maximum no. of times (as configured) if threshold score is not met for one or more fingers.
1. Rejects further capture if the number of capture attempts are greater than the configured limits.
1. Determines and displays rank for each finger. The finger with the highest quality score is ranked 1 and so on till 10 (excluding exceptions)
1. Validates all available fingerprints that have been captured, the fingerprints, which are above threshold quality and the maximum retries attempted.
1. Retains only that capture which has the highest quality score.
1. Captures and stores the transaction details for audit purpose (except PII data).

##J. Enable capturing an individual's face photograph

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
8. System captures and stores the transaction (User id or system account; Machine Details; Event Name; Application Name, and Event data) details for audit purpose (except PII data). 
#### K. Capture an individual's face photograph and exception photograph.
1. When a registration officer opts to capture the face photograph or exception photograph of an individual during the registration process, the system validates that an on-boarded camera is connected to the machine.
   * If an on-boarded camera is not found, display an error message.
   * If more than one on-boarded camera is connected, proceed with the first camera that the system finds as it scans the ports of the machine.
2. Displays the face photo preview before capturing.
3. Allows the Registration Officer to initiate face capture.
4. Sends request to the camera for face photo capture.
5. Receives the face photo from the camera.
6. Display the face photo on screen.
7. Allows the Registration Officer to proceed to verify quality score.
8. Allows exception photo capture only if an exception has been marked.
   * Step 2 to 7 must be performed to capture the exception photo.

9. System captures and stores the transaction details for audit purpose (except PII data).
#### L. Retry capture of face photo as configured
While registering an individual, a registration officer captures the face photo of the individual. If the quality score of the photo captured is less than the threshold score, the system allows registration officer to retry face capture
1. The system displays the quality score and the threshold score for the capture.
1. The registration officer proceeds to the next step if the quality score >= threshold or if the maximum number of retry attempts as configured is reached.
1. The system validates that:
   * the photo has been captured, and
   * the photo quality score is above threshold quality (or) the maximum retries (as configured) have been attempted.
4. The system maintains a count of the number of retries of face photo for the current registration.
1. Every time a retry is captured, the earlier quality score and threshold score are replaced by the current quality score and threshold score on screen.
1. A retry is allowed only after at least x seconds since the previous capture. The value x is configured configurable (default value is 10 seconds)
1. The quality score is determined by the SDK and the threshold limits are configured by the admin.
1. The system does not allow further capture if the number of capture attempts are greater than the configured limits and Displays an alert message that the retry limit is reached and photo of sufficient quality is not obtained.
1. When the retry limit is reached and photo of sufficient quality is not obtained, the best quality photo is retained. The best photo will be displayed on screen along with its quality score.
1. All the above rules apply to exception photo capture as well.

#### M. Capture Iris as per defined specifications
When the Registration Officer scans the individual’s irises either individually or together, the system performs the following steps:
1. Displays the quality score and threshold for each iris captured.
1. Allows the registration officer to re-try each capture up to a maximum no. of times (as configured) if threshold score is not met for one or both irises.
1. The quality score is determined and the threshold limits are configured.
1. If the quality score meets threshold, a re-capture is not allowed.
1. Validates all available irises that have been captured, the irises, which are above threshold quality and the maximum retries attempted.
1. Retains only that capture which has the highest quality score.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### N. Restrict registration if the duration since the last export or upload is more than the configured limit
When the registration officer opts to start a new registration or UIN update. The system determines the time of the most recent export or upload (automatic uploads and manual uploads) of registration packets.
If the duration since the last export or upload is not more than the configured limit, then system displays the demographic details page or UIN update page. If exceeded the configured limit, then system displays an error message.

#### O. Register a non-pre-registered individual 
When the registration Officer opts to start a new registration, the system ensures that the demographic fields are set up and sequenced in the Admin portal. In addition, Master data and config settings must be synced from the server to client. Then the system identifies the fields to be displayed on the new registration form. 

#### P. Choose the 'Opt to Register' option. 

Upon receiving a request to start a new registration, the system performs the following steps:
1. Validates that the time since the last sync from server to client has not exceeded the maximum duration permitted (configured from Admin portal).
   * Sync includes Master data, Login credentials, Pre-registration data, Registration center config, Registration center setup, User role setup, Policies, Registration packet status.
2. Validates that the time since the last export of registration packets from client to server has not exceeded the maximum duration permitted, if applicable (configured from Admin portal).
1. Validates that the number of registration packets on the client yet to be exported to server has not exceeded the maximum limit, if applicable (configured from Admin portal).
1. Reads the config setting that determines if the geo-location of the machine needs to be captured before every registration or captured at beginning of day only.
1. If before every registration, captures geo-location of the machine. Validates that the captured location is within x meters of the Registration Centre location (Both x and the Centre location are configured from the Admin portal).
1. If captured at beginning of day only, validates that the beginning-of-day location is within x meters of the Registration Centre location.
1. On successful validation, sends a response and proceeds to the next step of choosing a pre-registered or non pre-registered applicant.
1. In case of failures validation, triggers appropriate error messages.
1. System sends a success response and allow it to proceed to the next step.
1. System captures and stores the transaction details for audit purpose (except PII data).
#### Q. Retrieve a lost UIN
When a Registration Officer navigates to the Lost UIN page then the Registration Officer performs the following steps to retrieve a lost UIN of an individual:
1. Enters demographic details such as name, age or date of birth, etc. of the individual who has lost their UIN. 
   * None of the demographic fields is mandatory.
2. Marks biometric exceptions and captures all fingerprints, irises, face photo and exception photo of the individual.
1. Views a preview of details captured of the individual.
1. Performs operator authentication by providing credentials in the configured mode.
1. Supervisor performs supervisor authentication for individuals with exceptions.
1. Views acknowledgement of Lost UIN request with a Registration ID assigned to it.
1. Prints acknowledgement of the UIN, then SMS and email notifications are sent if contact details of the individual are entered.
System captures and stores the transaction details for audit purpose (except PII data).

### 4.2 UIN Update [**[↑]**](#table-of-content)
### 4.3 Lost UIN [**[↑]**](#table-of-content)
### 4.4 Acknowledgement and Notifications [**[↑]**](#table-of-content)
### 4.5 Biometric Capture (SDK Integration, Extract and Match) [**[↑]**](#table-of-content)
### 4.6 Biometric Exceptions [**[↑]**](#table-of-content)
### 4.7 Operator and Supervisor Approval [**[↑]**](#table-of-content)
### 4.8 End of Day Process [**[↑]**](#table-of-content)
## 5. Geo-location [**[↑]**](#table-of-content)
## 6. Language Support [**[↑]**](#table-of-content)
### 6.1 Translation [**[↑]**](#table-of-content)
### 6.2 Transliteration [**[↑]**](#table-of-content)
## 7. Packet Upload [**[↑]**](#table-of-content)
### 7.1 Registration Packet Upload [**[↑]**](#table-of-content) 
### 7.2 Offline upload (Packet Exporter) [**[↑]**](#table-of-content)
## 8. Analytics and Audit Logs [**[↑]**](#table-of-content) 
## 9. Data Security [**[↑]**](#table-of-content)
### 9.1 Key Management [**[↑]**](#table-of-content)
## 10. Software Version Upgrade [**[↑]**](#table-of-content)
## 11. Clean up [**[↑]**](#table-of-content)
### 11.1 Data retention policies [**[↑]**](#table-of-content)
### 11.2 Machine Retirement [**[↑]**](#table-of-content)


