- [Registration Client](#registration-client)
- [Registration Services](#registration-services)
- [1. Master Data Sync](#1-master-data-sync) _(REG_FR_1)_
  * [1.1 Master Data, Configuration](#11-master-data-configuration) _(REG_FR_1.1)_
  * [1.2 End of Day Process](#12-end-of-day-process) _(REG_FR_1.2)_
- [2. Booking Data Sync](#2-booking-data-sync) _(REG_FR_2)_
  * [2.1 Appointments (PRIDs)](#21-appointments-prids) _(REG_FR_2.1)_
  * [2.2 PR Packets](#22-pr-packets) _(REG_FR_2.2)_
- [3. Registration Data Services](#3-registration-data-services) _(REG_FR_3)_
  * [3.1 List of Registrations](#31-list-of-registrations) _(REG_FR_3.1)_
  * [3.2 Registration Packet Upload](#32-registration-packet-upload) _(REG_FR_3.2)_
  * [3.3 Online / Offline Behavior(Offline data upload is covered under this) (Packet Exporter)](#33-online--offline-behavioroffline-data-upload-is-covered-under-this-packet-exporter) _(REG_FR_3.3)_
  * [3.4 New Registration](#34-new-registration) _(REG_FR_3.4)_
  * [3.5 UIN Updates](#35-uin-updates) _(REG_FR_3.5)_
  * [3.6 Acknowledgement and Notifications](#36-acknowledgement-and-notifications) _(REG_FR_3.6)_
  * [3.7 Biometric Exceptions](#37-biometric-exceptions) _(REG_FR_3.7)_
  * [3.8 Supervisor Approval](#38-supervisor-approval) _(REG_FR_3.8)_
- [4. User Services](#4-user-services) _(REG_FR_4)_
  * [4.1 User on-boarding](#41-user-on-boarding) _(REG_FR_4.1)_
  * [4.2 Login/Authentication](#42-loginauthentication) _(REG_FR_4.2)_
  * [4.3 Logout](#43-logout) _(REG_FR_4.3)_
- [5. Registration Client Library](#5-registration-client-library) _(REG_FR_5)_
  * [5.1 Local Authentication](#51-local-authentication) _(REG_FR_5.1)_
    * [5.1.1 Offline Authentication using Biometrics](#511-offline-authentication-using-biometrics)
    * [5.1.2 Biometric SDK Integration (Extract and Match)](#512-biometric-sdk-integration-extract-and-match)
  * [5.2 API Client](#52-api-client) _(REG_FR_5.2)_
  * [5.3 Biometric Device Manager](#53-biometric-device-manager) _(REG_FR_5.3)_
    * [5.3.1 Vendor Device Manager Integration and Suuport](#531-vendor-device-manager-integration-and-suuport)
  * [5.4 Local Storage](#54-local-storage) _(REG_FR_5.4)_
    * [5.4.1 Database](#541-database)
    * [5.4.2 File system](#542-file-system)
  * [5.5 Data Security (Take Architects Help)](#55-data-security-take-architects-help) _(REG_FR_5.5)_
    * [5.5.1 Trust Environment](#551-trust-environment)
    * [5.5.2 Encryption and Decryption](#552-encryption-and-decryption)
    * [5.5.3 Storage Policies](#553-storage-policies)
    * [5.5.4 Key Management](#554-key-management)
  * [5.6 Business Validations](#56-business-validations) _(REG_FR_5.6)_
  * [5.7 Data Sync](#57-data-sync) _(REG_FR_5.7)_
    * [5.7.1 Master Data](#571-master-data)
    * [5.7.2 Pre-registration Data](#572-pre-registration-data)
    * [5.7.3 Registration Data](#573-registration-data)
    * [5.7.4 Analytics and Audit Logs](#574-analytics-and-audit-logs)
  * [5.8 Peripherals Management (Scanner, Camera,...)](#58-peripherals-management-scanner-camera) _(REG_FR_5.8)_
  * [5.9 Software Version Upgrade](#59-software-version-upgrade) _(REG_FR_5.9)_
  * [5.10 Cleanup](#510-cleanup) _(REG_FR_5.10)_
    * [5.10.1 Data retention policies](#5101-data-retention-policies)
    * [5.10.2 Device moving to new center](#5102-device-moving-to-new-center)
    * [5.10.3 Device retirement](#5103-device-retirement)
  * [5.11 Language Support](#511-language-support) _(REG_FR_5.11)_
    * [5.11.1 Language Selection](#5111-language-selection) 
    * [5.11.2 Internationalization](#5112-internationalization)
    * [5.11.3 Transliteration](#5113-transliteration)
    * [5.11.4 Virtual Keyboards](#5114-virtual-keyboards)
    * [5.11.5 Translation??](#5115-translation)
  * [5.12 Health Check](#512-health-check) _(REG_FR_5.12)_
    * [5.12.1 Disk Space Check](#5121-disk-space-check)
    * [5.12.2 Peripherals Check](#5122-peripherals-check)
    * [5.12.3 Virus Scan/Security Scan](#5123-virus-scansecurity-scan)
    * [5.12.4 Reports](#5124-reports)
- [6. Registration Client UI](#6-registration-client-ui) _(REG_FR_6)_


# Registration Client
# Registration Services

# 1. Master Data Sync
## 1.1 Master Data, Configuration
## 1.2 End of Day Process

# 2. Booking Data Sync
## 2.1 Appointments (PRIDs)
## 2.2 PR Packets


# 3. Registration Data Services
## 3.1 List of Registrations
## 3.2 Registration Packet Upload
## 3.3 Online / Offline Behavior(Offline data upload is covered under this) (Packet Exporter)
## 3.4 New Registration
## 3.5 UIN Updates
## 3.6 Acknowledgement and Notifications
## 3.7 Biometric Exceptions
## 3.8 Supervisor Approval

# 4. User Services
## 4.1 User on-boarding
## 4.2 Login/Authentication
## 4.3 Logout

# 5. Registration Client Library
## 5.1 Local Authentication
### 5.1.1 Offline Authentication using Biometrics
### 5.1.2 Biometric SDK Integration (Extract and Match)
## 5.2 API Client
## 5.3 Biometric Device Manager
### 5.3.1 Vendor Device Manager Integration and Suuport
## 5.4 Local Storage
### 5.4.1 Database
### 5.4.2 File system
## 5.5 Data Security (Take Architects Help)
### 5.5.1 Trust Environment
### 5.5.2 Encryption and Decryption
### 5.5.3 Storage Policies
### 5.5.4 Key Management
## 5.6 Business Validations
## 5.7 Data Sync
### 5.7.1 Master Data
### 5.7.2 Pre-registration Data
### 5.7.3 Registration Data
### 5.7.4 Analytics and Audit Logs
## 5.8 Peripherals Management (Scanner, Camera,...)
## 5.9 Software Version Upgrade
## 5.10 Cleanup
### 5.10.1 Data retention policies
### 5.10.2 Device moving to new center
### 5.10.3 Device retirement
## 5.11 Language Support
### 5.11.1 Language Selection
### 5.11.2 Internationalization
### 5.11.3 Transliteration
### 5.11.4 Virtual Keyboards
### 5.11.5 Translation??
## 5.12 Health Check
### 5.12.1 Disk Space Check
### 5.12.2 Peripherals Check
### 5.12.3 Virus Scan/Security Scan
### 5.12.4 Reports

# 6. Registration Client UI