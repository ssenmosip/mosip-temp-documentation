## Table Of Content

- [Registration Client](#registration-client)
- [Registration Services](#registration-services)
- [1. Master Data Sync](#1-master-data-sync) 
  * [1.1 Master Data, Configuration](#11-master-data-configuration-) _(REG_FR_1.1)_
  * [1.2 End of Day Process](#12-end-of-day-process-) _(REG_FR_1.2)_
- [2. Booking Data Sync](#2-booking-data-sync) 
  * [2.1 Appointments (PRIDs)](#21-appointments-prids-) _(REG_FR_2.1)_
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
```diff
- 5.2 API Client _(REG_FR_5.3)_
```
  * [5.3 Biometric Device Manager](#53-biometric-device-manager-)
    * [5.3.1 Vendor Device Manager Integration and Support](#531-vendor-device-manager-integration-and-support-) _(REG_FR_5.4)_

```diff

- 5.4 Local Storage 

```

    
   * [5.4.1 Database](#541-database-) _(REG_FR_5.5)_
   
   * [5.4.2 File system](#542-file-system-) _(REG_FR_5.6)_

```diff
- 5.5 Data Security
```
  * [5.5.1 Trust Environment](#551-trust-environment-) _(REG_FR_5.7)_
    * [5.5.2 Encryption and Decryption](#552-encryption-and-decryption-) _(REG_FR_5.8)_
    * [5.5.3 Storage Policies](#553-storage-policies-) _(REG_FR_5.9)_
    * [5.5.4 Key Management](#554-key-management-) _(REG_FR_5.10)_

```diff
- 5.6 Business Validations _(REG_FR_5.11)_


- 5.7 Data Sync 
```

   * [5.7.1 Master Data](#571-master-data-) _(REG_FR_5.12)_
   * [5.7.2 Pre-registration Data](#572-pre-registration-data-) _(REG_FR_5.13)_
   * [5.7.3 Registration Data](#573-registration-data-) _(REG_FR_5.14)_
   * [5.7.4 Analytics and Audit Logs](#574-analytics-and-audit-logs-) _(REG_FR_5.15)_
  * [5.8 Peripherals Management (Scanner, Camera,...)](#58-peripherals-management-scanner-camera-) _(REG_FR_5.16)_
 
```diff
- 5.9 Software Version Upgrade _(REG_FR_5.17)_
```
```diff
- 5.10 Cleanup
```
   * [5.10.1 Data retention policies](#5101-data-retention-policies-) _(REG_FR_5.18)_
   * [5.10.2 Device moving to new center](#5102-device-moving-to-new-center-) _(REG_FR_5.19)_
   * [5.10.3 Device retirement](#5103-device-retirement-) _(REG_FR_5.20)_

```diff
- 5.11 Language Support
```

 
   * [5.11.1 Language Selection](#5111-language-selection-)  _(REG_FR_5.21)_
   * [5.11.2 Internationalization](#5112-internationalization-) _(REG_FR_5.22)_
   * [5.11.3 Transliteration](#5113-transliteration-) _(REG_FR_5.23)_
   * [5.11.4 Virtual Keyboards](#5114-virtual-keyboards-) _(REG_FR_5.24)_
   * [5.11.5 Translation??](#5115-translation-) _(REG_FR_5.25)_
```diff
- 5.12 Health Check 
```

   * [5.12.1 Disk Space Check](#5121-disk-space-check-) _(REG_FR_5.26)_
   * [5.12.2 Peripherals Check](#5122-peripherals-check-) _(REG_FR_5.27)_
   * [5.12.3 Virus Scan/Security Scan](#5123-virus-scansecurity-scan-) _(REG_FR_5.28)_
   * [5.12.4 Reports (WIP)](#5124-reports-wip-) _(REG_FR_5.29)_
- [6. Registration Client UI](#6-registration-client-ui-) _(REG_FR_6)_


# Registration Client
# Registration Services

# 1. Master Data Sync
## 1.1 Master Data, Configuration [**[↑]**](#table-of-content)
#### A. Turn ON or OFF face capture 
1. A country may opt to turn ON or OFF the face capture process. It can be done by the admin. 
1. A Registration Officer logs in to the Registration Client and commences a new registration, enters the demographic data and uploads documents.
1. If face capture is turned ON, user captures the individual’s face photo.
1. Alternatively, if face capture is turned OFF, system does not show any provision for face capture and proceeds to the next step.
1. User captures the other applicable biometrics, authenticates, and completes the registration.

#### B. Turn ON or OFF iris capture 
1. A country may opt to turn ON or OFF the iris capture process .It can be done by the admin. 
1. A Registration Officer logs in to the Registration Client and commences a new registration, enters the demographic data and uploads documents
1. If iris capture is turned ON, user captures the individual’s iris scan
1. Alternatively, if iris capture is turned OFF, system does not show any provision for iris capture and proceeds to the next step.
1. User captures the other applicable biometrics, authenticates, and completes the registration.


#### C. Turn ON or OFF UIN Updates [**[↑]**](#table-of-content)
1. A country may opt to turn ON or OFF the UIN update process. It can be done by the admin. 
1. An individual approaches the Registration Officer for UIN Update.
1. If UIN Update is turned ON, the registration officer proceeds to capture the individual’s updated details.
1. Alternatively, if UIN Update is turned OFF, the link for UIN Update will not be available. 
1. The registration officer will not be able to carry out the UIN Update process.

#### D. Update to UIN data only for configured fields

An admin can configure the fields that will be available for update through the registration client. The configuration applies at a country level.

The Admin can set the following fields to be update-able at a country level 
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

#### E. Turn geo-location capture ON or OFF
1. A country may opt to turn ON or OFF the geo-location capture process .It can be done by the admin. 
1. The Registration Officer commences a new registration.
1. If Geo location capture is turned ON, the system captures the location of the machine to be stored in the registration packet. System validates that the location is within configured limits of the master data.
1. Alternatively, if Geo location capture is turned OFF, the system does not capture the location of the machine. System does not validate the location.
1. User proceeds to the next step (demographic data capture).

#### F. Turn ON or OFF Supervisor authentication for biometric exceptions [**[↑]**](#table-of-content)

The 'Supervisor authentication for exceptions' process can be set to ON or OFF at the country level through by admin.
 
1. The Registration Officer completes operator authentication at the end of registering an individual with exceptions.
1. If supervisor authentication is turned ON, a Supervisor is required to enter their credentials.
1. Alternatively, if supervisor authentication is turned OFF, system does not show the supervisor authentication option. User proceeds to the next step (acknowledgement).
 
#### G. Sync Registration Centre Setup data with data store servers
1. Each machine is mapped to a registration center. Server sends only the Registration Centre data for the specific center to the data store server
1. Registration Centre data includes the following attributes: Registration Centre ID, Registration Centre Name, Latitude, Longitude, Is Active, Centre Type, Address with Postal Code, Working Hours, Contact Number.
1. The system determines if a restart is required in order to apply the updates. If restart is required, notify the registration officer as a part of the sync success message: “Sync successful. Please restart the application to finish updating.”
#### H. Sync data from client to server [**[↑]**](#table-of-content)
1. The registration client receives a request to sync data (through manual trigger or scheduled job) from client to server.
2. Client in turn sends request with the applicable data to server.
   * User on-boarding data is synced.
   * Only the additions, deletions, and modifications made since the last sync are sent.
3. Client receives response from server as a success or failure message.
4. Client displays a success or failure message on the UI
5. The following data elements will be synced:

User on-boarding data: User ID, USB device ID, Computer ID

6. Alternatively, if the client machine is not online
   * Display san error message and does not sync when a user tries to initiate a manual sync.
   * Does not sync when an automatic sync is triggered.


#### I. Sync master data with data store servers
1. The registration client receives a request (through manual trigger or scheduled job) to sync master data from server to client.
1. Client in turn requests server for master data sync.
1. Client receives response from server with incremental changes to master data.
1. Client saves the data in the local machine making the incremental changes as received.
1. Client displays a success or failure message on the UI
1. Alternatively if the client machine is not online
   * Displays an error message and does not sync when a user tries to initiate a manual sync
   * Does not sync when an automatic sync is triggered


#### J. Sync Config details with data store servers [**[↑]**](#table-of-content)
1. The registration client receives a request (through manual trigger or scheduled job) to sync config data from server to client.
1. Client in turn requests server for config data sync.
1. Client receives response from server with incremental changes to config data.
1. Client saves the data in the local machine overwriting previous values of the config settings received.
1. Client displays a success or failure message on the UI.
1. Alternatively if the client machine is not online
1. If the client is not online
   * Displays an error message and does not sync when a user tries to initiate a manual sync.
   * Does not sync when an automatic sync is triggered.


#### K. Requirement for document categories and document types to be shown based on the configuration per applicant type.
1. The Registration Officer commences a new registration, enter demographic details The system then allows a registration officer to upload documents
1. User views the applicable document categories based on the demographic data entered. For each category, the applicable document types are displayed in the UI. In case of new registration or UIN update, the Document Categories and their respective Document Types will be configured by MOSIP admin.
1. User selects Document Types, scans and upload the documents and proceeds with registration.
1. The categories PoI and PoA are mandatory. The registration officer should select a Document Type under each Category and upload a document.
1. PoR is optional.


## 1.2 End of Day Process [**[↑]**](#table-of-content)

#### A. Approval of registrations through an end of day process.

Supervisor can log in to the registration client application and view a list of registration ID that are awaiting approval

The supervisor may opt to see the details of one or many registration ID. The system should show the display the acknowledgement slip of the registration\s

The supervisor then choses to either approve, reject or keep the registration on hold.

The supervisor must provide a reason in case of reject. Some of the values of Reason for hold are: Gender-photo mismatch, Age-photo mismatch, Name correction required, Address correction required, Date of birth correction required

The supervisor then authenticates the registration by providing any one biometric - fingerprint, iris, or face.
The system then shows a confirmation of successful approval.

1. In case of authentication failure, the supervisor can try again by providing the same or different biometric.
1. The packet status should change only when supervisor completes authentication. Else the packet status should revert to its original status.
1. The packets, which are approved or rejected followed by successful authentication are removed from the ‘Pending Approval’ list.
1. The packets, which are placed on hold followed by successful authentication, are moved from the ‘Pending Approval’ list to the ‘Pending Action’ list.
1. The approved and rejected packets are placed in the upload location on the client and should be sent to server during the next upload.
1. If a registration is on hold for more than x days, it is auto-approved by the system. No Supervisor authentication is required for this. The parameter x is configurable
1. ‘Authenticated' registrations report: Allow the supervisor to view a report of approved registrations for the past 15 days.


#### B. Registration client allows supervisor to view packets that are in pending approval state [**[↑]**](#table-of-content)
1. The system allows Supervisor to view packets in “Pending approval” status
1. The system displays the packets with the fields as shown here ”Registration ID, Registration Type, Resident Name, Operator ID, Operator Name”
1. The system displays error messages in case of any errors

#### C. Registration client enables a supervisor to approve data packets.
1. The system allows a Supervisor to view packets in “Pending approval” status or “On hold”
1. The supervisor can view the following fields: “(Packet ID, New Status = Approved, Approver ID)”
1. The supervisor can then change the packet status to “Approve”, “Reject” or “On hold”
1. The system displays error messages in case of any errors
1. The system ensures that the rejected packets and the packets that have been put on hold should not appear in the approval list again

#### D. Supervisor can inform individuals to 'Re-register'

1. A supervisor can view the packets whose status has been received from the processor as ‘Re-register’.
1. The system displays the list of registration IDs that have been flagged as ‘re-register’ during packet status sync from the processor.
1. The supervisor can see the registration details (the acknowledgement slip) for registration ID\s
1. Supervisor informs the individual by phone, email, physical mail, or physical visit to re-register. This is an offline process.
1. Supervisor also records it in the system that he has ‘Informed’ the individual
   * If unable to contact the individual, Supervisor records it as ‘Can’t inform'.
6. The supervisor then ‘Authenticates by providing biometric data -fingerprint, Iris, or face. Further, select the specific finger or iris being provided.
1. Scan the selected biometric.
1. Authenticate with locally stored biometric and display the result.
   * On successful authentication, the actioned packets are removed from the ‘-Re-register’ list.
   * On unsuccessful authentication, the user can retry his authentication with the same or a different biometric


# 2. Booking Data Sync
## 2.1 Appointments (PRIDs) [**[↑]**](#table-of-content)

#### A. Register a pre-registered individual by searching & fetching pre-registration data associated to a pre-registration ID from local system or server

When a registration officer starts a new registration by entering a pre-registration id of an individual, the system checks if an exact match for the ID exists in local database.
1. If yes, checks if an updated pre-registration packet for that ID is available on the server.
   * If yes, downloads the pre-registration packet from the server and pre-populate on screen.
   * If update is not available on server, display data from local database.
   * If client if offline, displays data from the local database.
2. If data is not available in local database, checks if data for that ID is available on the server.
   * If yes, downloads the pre-registration packet from the server and pre-populate on screen.
   * If data not available on server, displays data from local database.
3. Based on the availability of data, the system populates the demographic details of the resident and pre-populates the registration form.
1. The demographic details can still be edited at this stage
1. The registration officer can then view the documents uploaded during pre-registration
1. If no matching PRID exists in local system and server, the system displays an error message.

#### B. Scanning a Pre-registration QR code [**[↑]**](#table-of-content)
1. While starting a new registration, the registration client allows scanning a QR code to populate the pre-registration ID on screen.
1. A bar code scanner must be connected to the client machine in order to read the pre-registration QR code and pass on the pre-registration ID to the client.
1. System then populates the rest of the pre-registration data from the locally stored pre-registration details and checking for updates on the server
1. User proceeds with registration
#### C. Registration client allows downloading of pre-registration data in real time or manually for a specific PRID
**Real time downloads of Pre-registration data**

1. When a registration officer starts a new registration by entering a pre-registration ID and opts to fetch pre-registration data, the system checks if the pre-registration ID entered has a match in the local system
1. The system then fetches the demographic details of the resident and pre populate the registration form if there is exactly one match for pre-registration ID in the local system

**Manual downloads of Pre-registration data**

A registration officer can download the pre-registration data while being online. It is possible to download the demographic data of a resident only and the system does not allow to download the documents uploaded by the applicant. 

The system also enables a user to view the progress of download.

The pre-registration data can be downloaded only for that particular registration center, where the pre-registration data download is initiated

It is possible to download the pre-registration data from current date plus 1 to current date plus 7. This date range should be configurable

The downloaded pre-registration data overwrites the previously downloaded data for the same pre-registration ID

The downloaded pre-registration data is stored in its stipulated path as defined



# 3. Registration Data Services
## 3.1 List of Registrations [**[↑]**](#table-of-content)
## 3.2 Registration Packet Upload [**[↑]**](#table-of-content)

#### A. Views the packets first, selects which ones to upload, and then initiates the packet to upload
1. Once the Registration Officer selects the “Upload Packets” option, a list of packets are displayed.
1. Each packet has a check box for selection and also has an option to “Select All” and “Deselect All” the packets. 
1. After the Registration Officer selects the packet, he/she can upload the selected packet to server.

   NOTE: If any packets are selected, the ‘Export’ option gets disable because the selection of packets is applicable only for ‘Upload’ and not for the ‘Export’ feature.

#### B. Pushes those packets that are marked 'Resend' to the server

1. When the Registration Officer or Supervisor navigates to the ‘Upload Packets’ page, the list of RIDs that are pending packets to upload will be displayed.
   * Pending packets are those packets, which are not sent to the server and have been marked for resending.
2. When the Registration Officer or Supervisor selects the ‘Upload’ option, the pending packets will be uploaded to the server.
3. The result of each packet uploaded will be displayed as ‘Success’ or ‘Failure’.
   * Packets that are successfully sent or resent will not be sent again unless the server requests for them.
   * Packets for which upload fails will continue to be in pending state.
4. System captures and stores the transaction details for audit purpose.

#### C. Pushes a registration packet via FTP mode to the server [**[↑]**](#table-of-content)

1. The Registration Officer or Supervisor enters their FTP username and password.
1. When the user chooses the packets to push it to server, the list of packet RIDs that have been synced to server and exported to the local folder but not yet pushed to server will be displayed.
1. If applicable, the user can select a different source folder and a destination folder.
1. When the user selects the packets to push, the system checks that the selected EIDs have been synced to the server prior to pushing.
1. Then the user copies from the local folder to server and updates the status of the packets to ‘Pushed to Server’.
1. System captures and stores the transaction details for audit purpose.

#### D. Enables a real time packet upload when system is online upon registration submission

**When EoD process is turned ON**

1. Registration Client checks if the system is online as soon as the assigned approver (such as Supervisor) approves or rejects a new registration or UIN update.
1. If client is online, the registration client sends registration id to server and then the packets are marked as “Ready to upload” and auto uploaded to server.
1. If client is offline or on low bandwidth, then when the client next comes online, the registration id’s are sent to server through scheduled or manual sync and the packets are then marked as “ready to upload”.
1. Once the packets are ready for upload, packets are uploaded in two ways:
   * The registration officer can initiate upload to server using upload function.
   * Export to external storage device for subsequent upload as required.
5. System captures and stores the transaction details for audit purpose.

**When EoD process is turned OFF**

1. Registration Client checks if system is online as soon as the Registration Officer submits a new registration or UIN update.
1. If client is online, the registration client sends registration id to server and then the packets are marked as “Ready to upload” and auto uploaded to server.
1. If client is offline or on low bandwidth, then when the client next comes online, the registration id’s are sent to server through scheduled or manual sync and the packets are then marked as “ready to upload”.
1. Once the packets are ready for upload, packets are uploaded in two ways:
   * The registration officer can initiate upload to server using client’s upload function.
   * Export to external storage device for subsequent upload as required.
5. System captures and stores the transaction details for audit purpose.

## 3.3 Online / Offline Behavior(Offline data upload is covered under this) (Packet Exporter) [**[↑]**](#table-of-content)

System exports registration packet data from client machine to an external device as follows:
1. Allows the Registration Officer to select a destination folder.
   * The destination folder includes the laptop/desktop, an external hard drive or a remote location.
   * External storage devices are not necessary to be MOSIP-registered devices.
2. When the destination folder is selected, user initiates export of packets.
1. System exports the packets to the selected folder and performs the following steps:
   * Identifies the packets in ‘Ready to Upload’ state.
   * If EoD process is turned ON, packets which have been Approved or Rejected and packet ID sync is completed are considered ‘Ready to Upload’.
   * If EoD process is turned OFF, packets are considered ‘Ready to Upload’ as soon as the registration is submitted and packet ID sync is completed.
   * Places the packets in the destination folder.
4. Once the server acknowledges that the packets have been received, the packets in the client will be marked as ‘Uploaded’.
   * Packets that remain in ‘Ready to Upload’ status will be exported again when the next export is executed.
   * Packets in ‘Uploaded’ or any other status will not be exported again.
5. All the Registration Officers and Supervisors on-boarded to the USB client dongle is able to export all packets.
1. Supports the partial export. If the system is able to export some packets to the folder and not other files due to lack of storage space or unavailability of the folder, the successfully exported packets should remain on the destination folder.
1. For partial or full failure, the system displays error message.
1. System captures and stores the transaction details for audit purpose.


## 3.4 New Registration [**[↑]**](#table-of-content)
## 3.5 UIN Updates [**[↑]**](#table-of-content)

#### A. UIN Updates Turn ON or OFF

The UIN update feature is configurable by a country. Admin can either turn ON or OFF the UIN update feature.

When an individual approaches the Registration Officer for UIN update, the following scenarios may arise:

1. If UIN update is turned ON by a country, the registration officer can proceeds to capture the individual’s updated details.
1. Alternatively, if UIN Update is turned OFF by a country the RO will not be able to carry out the UIN Update process.

#### B. Registration client allows update to UIN data only for configured fields
1. An admin can configure the fields that are available for update through the registration client. The configuration applies at a country level.
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
1. The Registration Officer selects the fields to update for an individual seeking modification of UIN data. Select one or more of the following fields to update the corresponding data: Name, Age or Date of Birth, Gender, Foreigner/National, Address, Email ID, Phone Number, CNIE/PIN/Residence Card Number, Parent/Guardian Details, Biometrics.
1. Registration Officer captures the mandatory demographic attributes and other demographic fields selected for update. In case of update of Parent/Guardian details, the applicable fields that are updated should be ‘Parent/Guardian Name’ and ‘Parent/Guardian UIN’. The system at this stage also validates that the Parent/Guardian’s UIN is different from the individual’s UIN .If they are same, displays an error message 

1. Registration Officer then uploads documents. The applicable documents are determined by the system based on configuration
1. If biometrics were selected for update, Registration Officer marks exceptions and scans all biometrics. Else scans any one biometric.
1. Registration Officer captures face photo and exception photo.
1. After capturing all the biometric and demographic details the Registration Officer can see a preview of the data captured and performs operator authentication.
1. If biometric exceptions were marked, supervisor performs authentication.
1. A unique RID (registration ID is generated) on successful completion of registration process. Please refer to [**Wiki**](FRS-Data-Services#4-id-generator-and-validator) for more details.
1. Registration Officer Views and prints acknowledgement. 
1. SMS and/or email notifications are sent if the contact details are entered during the update process.

## 3.6 Acknowledgement and Notifications [**[↑]**](#table-of-content)
#### A. Printing the registration receipt.
1. Upon completion of a registration the system generates a unique RID 
1. The system the enables the user to generate the registration receipt.
1. The registration receipt contains details in a print-friendly format.
   * Receipt includes labels and data in two languages - the default language and the secondary language as configured. 
   * All labels and fields are in the default language. Only name and address labels and fields are shown in the secondary language
   * Receipt displays the 2D bar code.
4. This print friendly receipt can then be printed using a printer

#### B. Acknowledgement receipt sent by email on completion of registration process [**[↑]**](#table-of-content)
1. When a registration is completed, that is, a Registration ID has been generated and assigned the system, sends an acknowledgement email to the resident
2. The email template is defined by the admin at country level.
3. Email is sent to the email address entered during registration.
4. The subject and the body of the acknowledgement email are configured by admin.
5. No email is sent under the following scenario
   * If mode of confirmation is not set to ‘email’ or ‘email and SMS’
   * If an email address is not provided during registration
   * If the client is not online during registration completion
#### C. Acknowledgement receipt sent by SMS on completion of registration process
1. When a registration is completed, that is, a Registration ID has been generated and assigned the system sends an acknowledgement email to the resident
2. The template of the SMS is defined by the admin at the country level.
3. The “from” id of the SMS will be set up by the system integrator.
4. The system triggers the SMS to the mobile number provided during registration.
5. The SMS contains the registration number.
6. An SMS  is triggered regardless of the applicant being an adult or child as determined by the date of birth.
7. The system will not be able to send SMS, if the client is not online at the time of registration completion.

**Proposed template**

SMS content: “Dear [Individual full name], Thank you for registering with Digital Identity platform. Your registration id is [Registration ID]. If there are any corrections to be made in your details, please contact the Registration center within the next 4 days.

#### D. Sending email and SMS acknowledgements to additional recipients
This feature enables registration client to send SMS and email acknowledgements to additional recipient\s (other than the resident’s primary email id and mobile number)


## 3.7 Biometric Exceptions [**[↑]**](#table-of-content)

#### A. Low quality biometrics marked as reason for exceptions

1. During a registration process while capturing biometrics, if the configured threshold is not met for fingerprints and/or irises in spite of the x attempts(configurable) to capture the biometrics, then system mandates capture of exception photo 
1. Also, system automatically flags the reason for exception as ‘Low Quality of biometrics’. 
1. If the individual has missing biometrics and low quality of biometrics, both the reasons are auto-associated. Here also the system mandates capture of exception photo.

#### B. Mark fingerprint and iris exceptions for an individual

1. During a registration process after the demographic details and documents have been captured the system allow a registration officer to mark biometric exceptions for missing finger(s) and missing iris(es) if the resident has any such exceptions.

2. If ‘Biometric Exception’ is ‘Yes’, at least one missing biometric must be mandatorily marked.
3. The registration officer can mark the missing finger(s) and missing iris(es).

## 3.8 Supervisor Approval [**[↑]**](#table-of-content)

**Supervisor authentication for biometric exceptions**

1. The 'Supervisor authentication for exceptions' process is configurable and can be switched ON or OFF at a country level by the Admin 
1. A Registration Officer completes operator authentication at the end of registering an individual with exceptions.
1. If a country has opted to turned on supervisor authentication, a supervisor is required to enter their credentials
1. The mode of supervisor authentication is a configurable at the country level. It can be set to password, OTP, fingerprint, or multifactor.
1. In case of OTP authentication, the client first sends a request to server to generate the OTP, then allows the Supervisor to enter OTP and requests the server to match the input value with the generated OTP.
1. In case of multifactor authentication, the client prompts the Supervisor to enter credentials in the order configured and authenticates each input before proceeding to the entry of the next credential.
1. In case of multifactor authentication, the client prompts the Supervisor to enter credentials in the order configured and authenticates each input before proceeding to the entry of the next credential.
1. On successful validation the system proceeds to the next step of Registration ID generation and displays of registration acknowledgement.
1. If the validation fails, the system displays an error message and allows user to try again. Unlimited retries are be allowed.
1. Based on country-specific requirements, it is also possible for the Registration Officer and Supervisor to be the same person. In this case the user will be required to provide biometrics twice in succession, once as part of the Officer authentication and once for Supervisor authentication of exceptions.
1. Alternatively, if supervisor authentication is turned OFF, system does not show the supervisor authentication option at all and a registration officer may proceed to the next step (acknowledgement)

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

#### B. Updating the mapping of registration officers and supervisors to a client machine [**[↑]**](#table-of-content)
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

#### A. Login with iris and face to registration client
#### B. A Supervisor, can unlock a user's account on the Registration Client

A Supervisor or Admin can unlock a user’s account that has been locked due to five consecutive unsuccessful login attempts.

A Supervisor or Admin can log in to the Registration Client and views a list of users whose accounts are locked at a given point of time.

#### C. Allows biometric login of the Registration Officer or Supervisor to the client application

MOSIP supports single factor and multi factor login including iris and face capture. An Admin config setting determines the mode of login. 

1. The Registration Officer or Supervisor opts to login to registration client application
   * System enables user to login by entering username, and submit iris and face photo.
2. The user enters their username.
3. The user scans any one iris through the iris capture device.
4. The user then captures face photo using the face photo capture-device.
5. On successful authentication, the system logs in the user.

#### D. Enforce multi factor login for Admin users. [**[↑]**](#table-of-content)

When an Admin user opens the registration client by entering his/her username the system recognizes the username as that of an Admin and enforces multi-factor authentication in the configured order

The System enforces multi-factor authentication for Admin users as configured, regardless of the mode of authentication for Registration Officers and Supervisors.

Note: multifactor authentication is the type of authentication where an admin user is authenticated by more than one mode. Some examples could be OTP and Iris, and Finger print and OTP, etc.
#### E. Temporarily lock the user account after five unsuccessful login attempts.
1. The MOSIP system temporarily locks the user to login in case the user gives an invalid password for login five times continuously.
1. Upon the fifth unsuccessful attempt to login, displays an error message 
1. The temporarily lock lasts for 30 minutes.
1. The same error message is displayed for any subsequent login attempt within 30 minutes.
1. After 30 minutes, the lock is released and the count of invalid login attempts should be reset to zero.
1. The same is implemented if the fingerprint, iris, face, or multifactor login fails five times.
1. System captures and stores the transaction details for audit purpose.

#### F. Authenticate online/offline login of the Supervisor to the client application [**[↑]**](#table-of-content)

When a supervisor opts to log in to the client machine the systems displays the appropriate options as per the mode of login.

* If the mode of login is username and password, displays the password-based login.
* If the mode of login is username and OTP, display the OTP based login 


**Password-based login**
1. Allows the user to enter their username and password and submit.
1. Validates that the username belongs to an on boarded Registration Officer or Supervisor on that client.
1. Validates that the password matches the user’s password stored locally. The local password will be fetched from the server during sync.
1. Validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
1. Validates that the user has a role or Registration Officer or Supervisor. 

**OTP based login**

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

#### G. Restrict access to each MOSIP feature to authorized users. [**[↑]**](#table-of-content)

In MOSIP system, a user can have a single role only For example, a user can be either a Registration Officer or Supervisor. User to role mapping is done by the admin

When a logged in user tries to access a feature on the registration client the system determines if the requested feature is accessible to the role(s) mapped to the user.
1. If yes, permits the user to access the requested feature.
2. If no, displays an error message or hide the link to the feature as applicable. The UX design will drive whether to hide a link or display an error on click of the link.
3. Both registration officers and supervisors can access the following features. The role to rights mapping is configurable at a country level. The list given below corresponds to the default configuration.
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


#### A. Authenticate online/offline login of the Supervisor to the client application by Password and OTP based login

When a Registration Officer or Supervisor opts to the login to the registration client application, the system displays the appropriate login option based on admin config.

1. In case of the user opts to log in using the username and password, the system enables them to do so by providing appropriate options

1. The system validates that the username belongs to an on boarded Registration Officer or Supervisor on that client
1. Validates that the password matches the user’s password stored locally
1. Validates that the user is not blacklisted
1. Validates that the user has a role of Registration Officer or Supervisor.

1. Alternatively, if the user wants to log in using OTP, the system allows the user to enter their username and submits. System sends an OTP to the user’s registered mobile number.

1. Validates that the username belongs to an on-boarded Registration Officer or Supervisor on that client.
1. Generates and send an OTP by SMS to the user’s registered mobile number
1. Allows the user to enter the OTP and submit.
   * Alternatively, allows the user to change entered username.
   * Alternatively, allows the user to request for resending the OTP.
10. Validates that the OTP submitted matches the one that was generated and is submitted within its validity period.
11. Validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
12. Validates that the user has a role of Registration Officer or Supervisor.
On successful validation of all conditions above, display the logged in home page.

#### B. MOSIP supports single factor and multi factor login including iris and face capture. The mode of login is determined by Admin configuration setting

1. The Registration Officer or Supervisor opts to log in to the registration client.
1. System enables the Registration Officer or Supervisor to login by entering username, submit iris and face photo.
1. The Registration Officer or Supervisor enters their username.
1. The Registration Officer or Supervisor scans any one iris through the iris capture device.
   * If an on-boarded iris capture device is not found, display an error message.
   * If more than one on-boarded iris capture device is connected, proceed with the first iris capture device that the system finds as it scans the ports of the machine
5. The Registration Officer or Supervisor capture face photo using the face photo capture device.
6. Upon submission the system validates the following
   * System matches the username entered with the usernames of on-boarded users on that machine and identifies a match.
   * If a username match is not found, displays an error.
   * System compares the captured iris with each locally stored iris of the user until a match is identified.
   * Match score must be equal to or greater than the config setting ‘Authentication quality threshold for irises.
   * If an iris match is not found, displays an error.
   * Allows the user to retry by providing the same or different iris.
   * After five consecutive login failures for a valid username, temporarily locks the user’s account.
   * Validates that the user is not blacklisted. The blacklisted user details will be fetched from the server during sync.
7. On successful validation, display the logged-in home page.

#### C. Enforce multi factor login for Admin users [**[↑]**](#table-of-content)

The mode of authentication (single of multifactor) for a user is based on the admin configurations. For admin user its always multifactor authentication

When an admin user opts to log in to the registration client application by entering the user name and password the System recognizes the username as that of an Admin and enforces multi-factor authentication in the configured order to enter biometric data.

#### D. Registration Officer authenticates each registration with password/biometrics/multi factor elements

The registration officer authenticates each registration by providing credentials--biometrics and/or OTP and/or password as configured by the admin

1. In case registration officer’s credentials do not match the locally saved credentials or the OTP, the system allows registration officer to retry unlimited number of times.
1. If the system is configured for multi factor authentication, the registration officer should provide the credentials (biometric) in the configured order (as defined by the country)
1. The system allows the registration officer to proceed to the next step only upon successful authentication of all configured credentials
1. The system validates that the input (registration officer’s credentials) matches with the locally saved credentials for that registration officer.
   * The system accepts the biometrics match only if the match score is greater than the configured threshold value
   * In case of OTP, the system matches the input with the OTP on the server.
   * In case of password, the system does full match.
5. In case of multi-factor authentication, all inputs provided must match as per the rules defined for each individual parameter

### 5.1.2 Biometric SDK Integration (Extract and Match) [**[↑]**](#table-of-content)


Registration Client performs a local duplicate check for irises and face of an individual against the mapped registration officers' biometrics (Stubbed-WIP)
1. The Registration Officer captures the irises of the resident and clicks and opts to proceed further in the registration process
1. The system performs a local duplicate check of the resident’s irises with the irises of all the users on-boarded to the client.
1. In case of forced capture the system uses only the best capture for local duplicate check
1. The iris images of the individual are compared with the irises of the users mapped to the Client.
1. Each iris is matched individually.
1. The two captured irises are also compared against each other to identify a potential duplicate.
1. The SDK determines the match score, and this is compared with the threshold match score. If match score >= threshold then it is a match.
1. If at least one iris match is found, display an alert, set retry count to zero, and require recapture of both irises.
1. If a match is not found, allows the user to proceed to the face capture step
1. The Registration Officer captures the face photo and opts to proceed further in the registration process
1. On force capture/successful capture of face performs a local duplicate check of face of the individual against faces of all users on-boarded to the client.
1. In case of forced capture uses only the best capture for local duplicate check

1. The system performs a local duplicate check of the resident’s face with the faces of all the users on-boarded to the client.
1. If a match is found, display an error message and require individual to provide the face scan again.
1. When no match is found, system proceeds to the next step (Registration Preview).
1. The number of recapture attempts due to local duplicate check failures is not capped.

## 5.2 API Client [**[↑]**](#table-of-content)

Please refer [**wiki**](ID-Authentication-APIs) for more details on the APIs for ID authentication.


## 5.3 Biometric Device Manager [**[↑]**](#table-of-content)
### 5.3.1 Vendor Device Manager Integration and Support [**[↑]**](#table-of-content)

#### A. On-boarding fingerprint, iris, camera, GPS, printer, scanner, and barcode devices to a registration machine.

1. In MOSIP any Registration Officer or Supervisor can on-board a device.
2. Every model has a start date and end date associated to it by the admin. Devices of a certain model can only be used for registrations within this configured date range.
3. A device-machine mapping cannot be created if the end date of the model validity has passed. However it can be created ahead of the validity start date.
4. The admin user first sets up models in the admin portal, then registers devices by entering their serial number, model number and manufacturer.
5. While mapping a fingerprint or ‘IRIS’ or 'Camera' or 'Printer' or 'Scanner' or 'GPS' device to the client machine.
   * The system should enable a Supervisor or Registration Officer to select Device Type = ‘Fingerprint’ or ‘Iris’ or ‘Camera’ or ‘Printer’ or ‘Scanner’ or ‘GPS’ or ‘Barcode reader’.
   * Upon section of a device type, the system shows a list of devices that are registered. Device registration is done through by the Admin. 
   * The available devices list should show only those devices whose model’s validity end date is not a past date.

      (i) For example, say the validity of xyz model of fingerprint scanner is set from 1 Jan 2018 to 30 Jun 2018. If current date is 15 Oct 2018, system should not show this device under available devices.

      (ii) During usage of a device, the client will again check if the device is within its validity dates. This validation is covered in other user stories.

   * User can select one or more device\s, and mark them as ‘mapped’ and submit.
   * The user should also be able to unmap devices by moving from the ‘mapped’ list to the ‘available’ one.
   * The devices must be plugged in at the time of on-boarding.
   * The machine need not have internet connectivity at the time of on-boarding.
6. When the mapping is saved locally, the mapping is sent to the server during the next device mapping sync.
7. There is  no limitation to the numbers of devices mapped to the machine.

#### B. Virtual device manager [**[↑]**](#table-of-content)
Please refer [**wiki**](MOSIP-VDM-Specifications) for more details on Virtual device manager implementation

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

#### A. Registration Officer or Supervisor can download and unzip the client application set up kit

When a Registration Officer or Supervisor opts to download setup kit and selects the OS-specific setup kit to download, the system allows the user to download the setup kit to the storage location chosen by the user

1. User then unzips the setup kit.
2. Extract the files and folders from the zip file to a chosen location.
3. Allows user to verify that the files and folder structure are as described in the design document.
4. System captures and stores the download transaction details for audit purposes. 

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

## 5.10 Cleanup [**[↑]**](#table-of-content)
### 5.10.1 Data retention policies [**[↑]**](#table-of-content)
### 5.10.2 Device moving to new center [**[↑]**](#table-of-content)
### 5.10.3 Device retirement [**[↑]**](#table-of-content)
## 5.11 Language Support [**[↑]**](#table-of-content)
### 5.11.1 Language Selection [**[↑]**](#table-of-content)
### 5.11.2 Internationalization [**[↑]**](#table-of-content)
### 5.11.3 Transliteration [**[↑]**](#table-of-content)

**Registration client enables viewing transliterated data other than French and Arabic**

The registration client application will support two type of languages: Primary (the language in which the registration officer enters data) and secondary language (transliteration language). The secondary language is country specific and is set by the administrator

When a Registration Officer starts a new registration, update or lost UIN process and enters data in the primary language for Full Name, Address Line 1, Address Line 2, Address Line 3, and Parent/Guardian Name.

System transliterates the data and displays in the corresponding secondary language fields.

The following data are transliterated into the secondary language in addition to being shown in the primary language.
1. Demographic details page: Data for Full Name, Address Line 1, Address Line 2, Address Line 3 and Parent/Guardian Name.
1. Registration preview page: Data for Full Name, Address Line 1, Address Line 2, Address Line 3 and Parent/Guardian Name.
1. Registration confirmation page: Data for Full Name, Address Line 1, Address Line 2, Address Line 3 and Parent/Guardian Name.

Registration Officer can invoke the virtual keyboard to edit transliterated data and proceeds with registration. The flowing rules are followed during transliteration.
1. Editing a transliterated fields does not change the data entered in the primary language field
1. The system also validates the maximum character length in the transliterated field and ensures that it is same as the limits defined for the primary language field.
1. If no secondary language is set, system does not do any transliteration and will display empty space instead.
1. Numeric fields are not transliterated. The same numerals are displayed in the in the secondary language section of the page and are not editable.

Master data selections are not transliterated. Instead, the translated master data values are displayed in the secondary language section of the page and are not editable 

The Registration Officer can then view the preview page

The system then enables a Registration Officer to view the registration confirmation page. The fields as transliterated and edited earlier are also shown in the secondary language.

### 5.11.4 Virtual Keyboards [**[↑]**](#table-of-content)
### 5.11.5 Translation?? [**[↑]**](#table-of-content)

**A registration officer can view static data translated to secondary language**
1. In MOSIP, the primary and secondary languages are configured by the admin 
1. All static data (headers, labels, action buttons, and alert messages) is set up by the admin in both languages so that the registration officer can view all pages in the client application in both the default (primary) language and translated (secondary) language. 
1. If configured translation language is same as default language, the system displays text in default language only.

## 5.12 Health Check [**[↑]**](#table-of-content)
### 5.12.1 Disk Space Check [**[↑]**](#table-of-content)

Upon receiving a request from the UI to create an enrolment packet at the end of data capture and authentication steps, the system validates the disk space available on the client machine to store the enrolment packet as follows:
1. Calculates the size of the enrolment packet based on the data captured.
   * Data includes demographic, biometric, photographs, OSI authentication, enrolment metadata, audit data, and acknowledgement scan.
2. Calculates the disk space, which is available in the configured packet storage location.
1. Validates if the storage location is sufficient to store the enrolment packet.
1. In case of successful validation, responses with success message and proceed further. 
1. In case of unsuccessful validation, responses with an appropriate error message.
1. System captures and stores the transaction details for audit purpose.

### 5.12.2 Peripherals Check [**[↑]**](#table-of-content)
### 5.12.3 Virus Scan/Security Scan [**[↑]**](#table-of-content)

Upon receiving a request to perform a virus scan of the registration packets on the client machine, the system performs the following steps:
1. When the client application is open, the system scans the registration packets at a configured frequency.
1. Checks if viruses are available in the registration packets that are stored on the client machine.
   * All registration packets on the machine will be scanned.
3. At the end of the scan, displays an alert message (Security scan detected viruses in the following files [List of files]. Please take necessary action or contact the administrator) on screen if a virus is detected.
1. If the client application is not open at the configured time, the scan will be queued up and runs only when the client application is open.

### 5.12.4 Reports (WIP) [**[↑]**](#table-of-content)

1. Allows the supervisor to generate reports as detailed in the [**field definition document**](/mosip/mosip/blob/master/docs/requirements/MOSIP_Reporting_Requirements_18Dec18.xlsx).
2. All data will be specific to the computer or USB client dongle, which is being accessed.
3. Data reported will not be specific to a certain supervisor. All data across supervisor on the client will be reported.
4. Allows the supervisor to sort the report data by clicking on the column headers.
5. Data reported will not be clickable / not support drill down to view individual transactions.
6. Display '0' for fields whose data is not available on the USB client dongle.
7. Export the report in csv format.
8. System captures and stores the transaction details for audit purpose.


# 6. Registration Client UI [**[↑]**](#table-of-content)


