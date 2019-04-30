## Table Of Content
- [Registration Processor](#registration-processor)
 - [1. ID Lifecycle Management](#1-id-lifecycle-management) 
   * [1.1 New ID Issuance](#11-new-id-issuance) _(RPR_FR_1.1)_
   * [1.2 Update Individual’s Information](#12-update-individuals-information) _(RPR_FR_1.2)_
   * [1.3 De-activate Individual’s ID](#13-de-activate-individuals-id) _(RPR_FR_1.3)_
   * [1.4 Re-activate Individual’s ID](#14-re-activate-individuals-id) _(RPR_FR_1.4)_
 - [2. Configurable Workflow](#2-configurable-workflow) 
   * [2.1 Orchestration](#21-orchestration) _(RPR_FR_2.1)_
   * [2.2 Retry Processing (In case of exceptions/failures)](#22-retry-processing-in-case-of-exceptionsfailures) _(RPR_FR_2.2)_
   * [2.3 Resume Workflow](#23-resume-workflow) _(RPR_FR_2.3)_
   * [2.4 Integration (System capability)](#24-integration-system-capability) _(RPR_FR_2.4)_
   * [2.5 Workflow Customization (Ability to plug-in/exclude stages)](#25-workflow-customization-ability-to-plug-inexclude-stages) _(RPR_FR_2.5)_
   * [2.6 Multiple Workflows (Specific to lifecycle – E.G.: New vs. Update, Activation vs. Deactivation, Applicant Type specific workflow)](#26-multiple-workflows-specific-to-lifecycle--eg-new-vs-update-activation-vs-deactivation-applicant-type-specific-workflow) _(RPR_FR_2.6)_
   * [2.7 Scalability and Throughput](#27-scalability-and-throughput) _(RPR_FR_2.7)_
 - [3. Types of Stages](#3-types-of-stages) 
   * [3.1 Pre-processing Validations](#31-pre-processing-validations) 
     * [3.1.1 Sanity Check](#311-sanity-check) _(RPR_FR_3.1)_
     * [3.1.2 Virus Scan](#312-virus-scan) _(RPR_FR_3.2)_
     * [3.1.3 Source Authentication](#313-source-authentication) _(RPR_FR_3.3)_
     * [3.1.4 Machine-User-Center-Device Checks](#314-machine-user-center-mapping-check) _(RPR_FR_3.4)_
     * [3.1.5 GPS Capture Check](#315-gps-capture-check) _(RPR_FR_3.5)_
     * [3.1.6 Operator & Supervisor Validation](#316-operator--supervisor-validation) _(RPR_FR_3.6)_
   * [3.2 Processing](#32-processing) 
     * [3.2.1 Individual Data Validations](#321-individual-data-validations) 
       * [3.2.1.1 Data Quality Check: Photo, Age, Gender Data Check](#3211-data-quality-check-photo-age-gender-data-check) _(RPR_FR_3.7)_
       * [3.2.1.2 Biometrics Quality Check](#3212-biometrics-quality-check) _(RPR_FR_3.8)_
       * [3.2.1.3 Doc. Validation - OCR](#3213-doc-validation---ocr) _(RPR_FR_3.9)_
     * [3.2.2 Functional Validations](#322-functional-validations) 
       * [3.2.2.1 File & Document Validation](#3221-file--document-validation) _(RPR_FR_3.10)_
       * [3.2.2.2 Introducer Validation](#3222-introducer-validation) _(RPR_FR_3.11)_
       * [3.2.2.3 Deduplication – Demographic, Biometrics](#3223-deduplication--demographic-biometrics) _(RPR_FR_3.12)_
     * [3.2.3 External System Integration: (Elaborate with examples)](#323-external-system-integration-elaborate-with-examples) 
       * [3.2.3.1 Data Verification (Pluggable by SI – Not part of MOSIP)](#3231-data-verification-pluggable-by-si--not-part-of-mosip) _(RPR_FR_3.13)_
       * [3.2.3.2 Data Enrichment (Incl. receipt of Update Packet from ext. system and process thereafter, in terms of MOSIP’s capability)](#3232-data-enrichment-incl-receipt-of-update-packet-from-ext-system-and-process-thereafter-in-terms-of-mosips-capability) _(RPR_FR_3.14)_
       * [3.2.3.3 Manual Verification for ext. system data update (Pluggable by SI)](#3233-manual-verification-for-ext-system-data-update-pluggable-by-si) _(RPR_FR_3.15)_
       * [3.2.3.4 Manual Adjudication (Pluggable by SI)](#3234-manual-adjudication-pluggable-by-si) _(RPR_FR_3.16)_
       * [3.2.3.5 ABIS Integration (Incl. ABIS Middleware)](#3235-abis-integration-incl-abis-middleware) _(RPR_FR_3.17)_
     * [3.2.4 ID Issuance](#324-id-issuance) 
       * [3.2.4.1 Identity Generation (Refer to UIN Generation service) – Incl. UIN Generation and UIN association](#3241-identity-generation-refer-to-uin-generation-service--incl-uin-generation-and-uin-association) _(RPR_FR_3.18)_
       * [3.2.4.2 Store/Update ID Repository (Refer to ID-Auth)](#3242-storeupdate-id-repository-refer-to-id-auth) _(RPR_FR_3.19)_
     * [3.2.5 Capture Audit Trails/Analytics Data](#325-capture-audit-trailsanalytics-data) _(RPR_FR_3.20)_
   * [3.3 Post-Processing](#33-post-processing) 
     * [3.3.1 Notification (Pluggable by SI)](#331-notification-pluggable-by-si) _(RPR_FR_3.21)_
     * [3.3.2 Print & Post (Pluggable by SI)](#332-print--post-pluggable-by-si) _(RPR_FR_3.22)_
     * [3.3.3 Data Seeding to External Functional ID System (Pluggable by SI)](#333-data-seeding-to-external-functional-id-system-pluggable-by-si) _(RPR_FR_3.23)_

# Registration Processor
# 1. ID Lifecycle Management

When an individual goes to the registration center, the registration officer or supervisor captures the Demographic and Biometric details of the Individual. Then Registration Client packages the information in a secure way (encrypted packets) and sends it to the Registration Processor. Registration Processor now processes the data of the Individual for quality and uniqueness and then issues new ID or updates the individual’s details. The packages received from the Registration Client must pass the sanity checks and validations to carry out the following processes:
* New ID Issuance
* Update individual’s information
* De-activate individual’s ID
* Re-activate individual’s ID

## 1.1 New ID Issuance
After the packets for new ID issuance are received from the Registration Client and has passed the sanity checks and validations, the system performs the demographic deduplication (using name, date of birth, and gender) and biometric deduplication (using [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface)) and then issues a new ID to the individual. After issuance of the ID, the system notifies the individual via the configured mode of notification (e-mail or SMS) and sends the ID card to the printing & postal service provider.
## 1.2 Update Individual’s Information
After the packets for update are received from the Registration Client or Residential Portal and have passed the sanity checks and validations, the system performs the demographic deduplication (using name, date of birth, and gender) and biometric deduplication (using [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface)) and then updates the individual’s information via two different ways:
1. Packets that are received through Registration Client updates the individual’s Biometric and demographic details.
1. Packets that are received through Residential Portal updates the individual’s address and contact information.

After the individual’s information is updated, the system notifies the individual via the configured mode of notification (e-mail or SMS) and sends the ID card to the printing & postal service provider.

## 1.3 De-activate individual’s ID
When the country chooses to de-activate individual’s ID due to any specific reason, the packets for UIN de-activate will go through the sanity checks and validations. Then the system checks if the status of the UIN is in activated state or not. If in activated state, the system de-activates the individual’s ID.
## 1.4 Re-activate individual’s ID
When the country chooses to re-activate individual’s ID due to any specific reason, the packets for UIN re-activate will go through the sanity checks and validations. Then the system checks if the status of the UIN is in de-activated state or not. If in de-activated state, the system re-activates the individual’s ID.
# 2. Configurable Workflow
## 2.1 Orchestration
## 2.2 Retry Processing (In case of exceptions/failures)
## 2.3 Resume Workflow
## 2.4 Integration (System capability)
## 2.5 Workflow Customization (Ability to plug-in/exclude stages)
## 2.6 Multiple Workflows (Specific to lifecycle – E.G.: New vs. Update, Activation vs. Deactivation, Applicant Type specific workflow)
## 2.7 Scalability and Throughput
# 3. Types of Stages
## 3.1 Pre-processing Validations
### 3.1.1 Sanity Check
After the packets received from the Registration Client, the system performs the sanity check as follows:
1. **Authentication** - Authenticates the packet whether it is received from the verified source.
2. **Virus Scan** - Performs a virus scan of that received packet and  move it to the DMZ file System. Refer below for the process:
   * The system sends the byte array of the encrypted packet to the virus scanner.
   * When virus scanning is successful, the system decrypts the packets in-memory and sends the byte array of the decrypted packet to the virus scanner.
   * If the virus scanner finds a virus, then the system rejects the packet.
   * If the virus scanner do not finds a virus, then the system moves the packet to DMZ file system. 
3. **Packet Integrity Check** - Calculates a hash sequence of the packet and compares with that of the hash sequence received from the registration client, to verify that the packet was not tempered during transit. Refer below for the process:
   * Fetches the hash sequence for the registration id from registration sync list table.
   * If registration id is not available then responds with an error code.
   * Calculates the hash sequence using the check sum utility.
   * Compares the hash sequences and if the hash sequences do not match, then responds with an error code. If the hash sequence matches then the system proceeds further to another step.
4. **Packet Size Check** - Calculates the size of the packet received and compares with that of the packet size received from the registration client, to verify that the packet was not tempered during transit.
   * Checks if the packet size is more than the configured size set in the configuration server. If the packet size is more than the configured size, then sends an error response to Registration Client.
5. **Packet Format Check** - Validates if the packet format is in the configured format i.e. “.zip” (configured by the admin).
   * Checks if the packet format is not as the configured format i.e. “.zip” set in the configuration server. If the packet format is not like the configured format, then sends an error response to Registration Client.
6. **Duplicate Check** – Validates if the packet is already available in the system
   * Checks if the packet is a duplicate request by validating the RID that is available in the Registration Table and the packet is not in RESEND status. If the Packet Request is a Duplicate Request, then send an error response to Registration Client.

### 3.1.2 Virus Scan
### 3.1.3 Source Authentication
### 3.1.4 Machine-User-Center Mapping Check
### 3.1.5 GPS Capture Check
### 3.1.6 Operator & Supervisor Validation
## 3.2 Processing
### 3.2.1 Individual Data Validations
#### 3.2.1.1 Data Quality Check: Photo, Age, Gender Data Check
#### 3.2.1.2 Biometrics Quality Check
#### 3.2.1.3 Doc. Validation - OCR 
### 3.2.2 Functional Validations
#### 3.2.2.1 File & Document Validation
#### 3.2.2.2 Introducer Validation
#### 3.2.2.3 Deduplication – Demographic, Biometrics
### 3.2.3 External System Integration: (Elaborate with examples)
#### 3.2.3.1 Data Verification (Pluggable by SI – Not part of MOSIP)
#### 3.2.3.2 Data Enrichment (Incl. receipt of Update Packet from ext. system and process thereafter, in terms of MOSIP’s capability)
#### 3.2.3.3 Manual Verification for ext. system data update (Pluggable by SI)
#### 3.2.3.4 Manual Adjudication (Pluggable by SI)
#### 3.2.3.5 ABIS Integration (Incl. ABIS Middleware)
### 3.2.4 ID Issuance 
#### 3.2.4.1 Identity Generation (Refer to UIN Generation service) – Incl. UIN Generation and UIN association
#### 3.2.4.2 Store/Update ID Repository (Refer to ID-Auth)
### 3.2.5 Capture Audit Trails/Analytics Data
## 3.3 Post-Processing
### 3.3.1 Notification (Pluggable by SI)
### 3.3.2 Print & Post (Pluggable by SI)
### 3.3.3 Data Seeding to External Functional ID System (Pluggable by SI)
