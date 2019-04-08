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
   * If the one-time process has not yet run, the user will still be able to login and perform sync, end of day approval, re-register updates, export, and upload. The user cannot perform pre-registration download and user on boarding.
5. As part of sync M1 receives the list of RC2 users. RC2 can users proceed to on-board themselves.

## 3.7 Biometric Exceptions [**[↑]**](#table-of-content)
## 3.8 Supervisor Approval [**[↑]**](#table-of-content)

# 4. User Services
## 4.1 User on-boarding [**[↑]**](#table-of-content)
## 4.2 Login/Authentication [**[↑]**](#table-of-content)
## 4.3 Logout [**[↑]**](#table-of-content)

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