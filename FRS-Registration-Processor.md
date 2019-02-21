## Table Of Content
- [Registration Processor](#registration-processor)
 - [1. ID Lifecycle Management](#1-id-lifecycle-management)
   * [1.1 New UIN Issuance](#11-new-uin-issuance)
   * [1.2 UIN Update](#12-uin-update)
   * [1.3 De-activate UIN – Manual/Automated](#13-de-activate-uin--manualautomated)
   * [1.4 Re-activate UIN](#14-re-activate-uin)
 - [2. Configurable Workflow](#2-configurable-workflow)
   * [2.1 Orchestration](#21-orchestration)
   * [2.2 Retry Processing (In case of exceptions/failures)](#22-retry-processing-in-case-of-exceptionsfailures)
   * [2.3 Resume Workflow](#23-resume-workflow)
   * [2.4 Integration (System capability)](#24-integration--system-capability-)
   * [2.5 Workflow Customization (Ability to plug-in/exclude stages)](#25-workflow-customization--ability-to-plug-in-exclude-stages-)
   * [2.6 Multiple Workflows (Specific to lifecycle – E.G.: New vs. Update, Activation vs. Deactivation, Applicant Type specific workflow)](#26-multiple-workflows--specific-to-lifecycle---eg--new-vs-update--activation-vs-deactivation--applicant-type-specific-workflow-)
   * [2.7 Scalability and Throughput](#27-scalability-and-throughput)
 - [3. Types of Stages](#3-types-of-stages)
   * [3.1 Pre-processing Validations](#31-pre-processing-validations)
     * [3.1.1 Sanity Check](#311-sanity-check)
     * [3.1.2 Virus Scan](#312-virus-scan)
     * [3.1.3 Source Authentication](#313-source-authentication)
     * [3.1.4 Machine-User-Center Mapping Check](#314-machine-user-center-mapping-check)
     * [3.1.5 GPS Capture Check](#315-gps-capture-check)
     * [3.1.6 Operator & Supervisor Validation](#316-operator---supervisor-validation)
   * [3.2 Processing](#32-processing)
     * [3.2.1 Individual Data Validations](#321-individual-data-validations)
       * [3.2.1.1 Data Quality Check: Photo, Age, Gender Data Check](#3211-data-quality-check--photo--age--gender-data-check)
       * [3.2.1.2 Biometrics Quality Check](#3212-biometrics-quality-check)
       * [3.2.1.3 Doc. Validation - OCR](#3213-doc-validation---ocr)
     * [3.2.2 Functional Validations](#322-functional-validations)
       * [3.2.2.1 File & Document Validation](#3221-file---document-validation)
       * [3.2.2.2 Introducer Validation](#3222-introducer-validation)
       * [3.2.2.3 Deduplication – Demographic, Biometrics](#3223-deduplication---demographic--biometrics)
     * [3.2.3 External System Integration: (Elaborate with examples)](#323-external-system-integration---elaborate-with-examples-)
       * [3.2.3.1 Data Verification (Pluggable by SI – Not part of MOSIP)](#3231-data-verification--pluggable-by-si---not-part-of-mosip-)
       * [3.2.3.2 Data Enrichment (Incl. receipt of Update Packet from ext. system and process thereafter, in terms of MOSIP’s capability)](#3232-data-enrichment--incl-receipt-of-update-packet-from-ext-system-and-process-thereafter--in-terms-of-mosip-s-capability-)
       * [3.2.3.3 Manual Verification for ext. system data update (Pluggable by SI)](#3233-manual-verification-for-ext-system-data-update--pluggable-by-si-)
       * [3.2.3.4 Manual Adjudication (Pluggable by SI)](#3234-manual-adjudication--pluggable-by-si-)
       * [3.2.3.5 ABIS Integration (Incl. ABIS Middleware)](#3235-abis-integration--incl-abis-middleware-)
     * [3.2.4 ID Issuance](#324-id-issuance)
       * [3.2.4.1 Identity Generation (Refer to UIN Generation service) – Incl. UIN Generation and UIN association](#3241-identity-generation--refer-to-uin-generation-service----incl-uin-generation-and-uin-association)
       * [3.2.4.2 Store/Update ID Repository (Refer to ID-Auth)](#3242-store-update-id-repository--refer-to-id-auth-)
     * [3.2.5 Capture Audit Trails/Analytics Data](#325-capture-audit-trails-analytics-data)
   * [3.3 Post-Processing](#33-post-processing)
     * [3.3.1 Notification (Pluggable by SI)](#331-notification--pluggable-by-si-)
     * [3.3.2 Print & Post (Pluggable by SI)](#332-print---post--pluggable-by-si-)
     * [3.3.3 Data Seeding to External Functional ID System (Pluggable by SI)](#333-data-seeding-to-external-functional-id-system--pluggable-by-si-)

# Registration Processor
# 1. ID Lifecycle Management
## 1.1 New UIN Issuance
## 1.2 UIN Update
## 1.3 De-activate UIN – Manual/Automated
## 1.4 Re-activate UIN
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
