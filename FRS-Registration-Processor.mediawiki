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
