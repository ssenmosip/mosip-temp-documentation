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
   * [2.4 Integration (System Integrator can integrate their system with MOSIP)](#24-integration-system-integrator-can-integrate-their-system-with-mosip) _(RPR_FR_2.4)_
   * [2.5 Multiple Workflows](#25-multiple-workflows) (RPR_FR_2.6)_
   * [2.6 Scalability and Throughput](#26-scalability-and-throughput) _(RPR_FR_2.7)_
 - [3. Types of Stages](#3-types-of-stages) 
   * [3.1 Pre-processing Validations](#31-pre-processing-validations) 
     * [3.1.1 Sanity Check](#311-sanity-check) _(RPR_FR_3.1)_
     * [3.1.2 Virus Scan](#312-virus-scan) _(RPR_FR_3.2)_
     * [3.1.3 Machine-User-Center-Device Checks](#314-machine-user-center-mapping-check) _(RPR_FR_3.4)_
     * [3.1.4 Officer & Supervisor Validation](#316-officer--supervisor-validation) _(RPR_FR_3.6)_
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
       * [3.2.3.2 Data Enrichment](#3232-data-enrichment) _(RPR_FR_3.14)_
       * [3.2.3.3 Manual Verification for ext. system data update (Pluggable by SI)](#3233-manual-verification-for-ext-system-data-update-pluggable-by-si) _(RPR_FR_3.15)_
       * [3.2.3.4 Manual Adjudication (Pluggable by SI)](#3234-manual-adjudication-pluggable-by-si) _(RPR_FR_3.16)_
       * [3.2.3.5 ABIS Integration (Incl. ABIS Middleware)](#3235-abis-integration-incl-abis-middleware) _(RPR_FR_3.17)_
     * [3.2.4 ID Issuance](#324-id-issuance) 
       * [3.2.4.1 Identity Generation (Refer to UIN Generation service) – Incl. UIN Generation and UIN association](#3241-identity-generation-refer-to-uin-generation-service--incl-uin-generation-and-uin-association) _(RPR_FR_3.18)_
       * [3.2.4.2 Store/Update ID Repository (Refer to ID-Auth)](#3242-storeupdate-id-repository-refer-to-id-auth) _(RPR_FR_3.19)_
       * [3.2.4.3 Data Extractor for ID Authentication](#3243-data-extractor-for-id-authentication)
     * [3.2.5 Capture Audit Trails/Analytics Data](#325-capture-audit-trailsanalytics-data) _(RPR_FR_3.20)_
   * [3.3 Post-Processing](#33-post-processing) 
     * [3.3.1 Notification (Pluggable by SI)](#331-notification-pluggable-by-si) _(RPR_FR_3.21)_
     * [3.3.2 Print & Post (Pluggable by SI)](#332-print--post-pluggable-by-si) _(RPR_FR_3.22)_
     * [3.3.3 Data Seeding to External Functional ID System (Pluggable by SI)](#333-data-seeding-to-external-functional-id-system-pluggable-by-si) _(RPR_FR_3.23)_

# Registration Processor
# 1. ID Lifecycle Management
When an individual visits a registration center to get a UIN or update his/her UIN information, a registration officer or supervisor captures the individual’s demographic (name, date of birth, gender, etc.) and biometric (face, iris, finger print image, etc.) details. These information are packaged in a secure way (using encrypted packets) by Registration Client and sent to Registration Processor. The various life cycle events that can be processed by Registration Processor are:

The packet received from the Registration Client must pass the [**sanity checks**](#311-sanity-check) and validations to carry out the following processes:
* New ID Issuance
* Update individual’s information
* De-activate individual’s ID
* Re-activate individual’s ID

## 1.1 New ID Issuance

When the Registration Processor receives a packet for registering an individual in the system, it performs various [**sanity checks**](#311-sanity-check) & validations, and identifies demographic duplicates (using demographic data like name, date of birth and gender) and biometric duplicates (using [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface)). After all the validations are successful, the system allocates a UIN for the individual. 

## 1.2 Update Individual’s Information
An individual can update his/her information via two different ways:
1. **Visiting a Registration Center** – The individual can update their biometric and demographic information.
1. **Using the Resident Portal** – The individual can update their address and contact information.

When the request is made by the individual, a packet is received by registration processor which goes through various [**sanity checks**](#311-sanity-check) and validations and then updates the individual’s information.

## 1.3 De-activate individual’s ID
If a country wants to deactivate an individual’s ID due to any specific reason, the system provides a feature to do so after certain validations are performed. As a result of de-activation of UIN, the individual can not authenticate themselves by using UIN or VID. 
## 1.4 Re-activate individual’s ID
If a country wants to re-activate a deactivated individual’s ID, the system provides a feature to do so after certain validations are performed.
# 2. Configurable Workflow
## 2.1 Orchestration

Orchestration is the process of configuring various services which will be coordinated and managed to achieve a business goal. 

In Registration Processor, there are various independent components which are connected in a workflow to perform various Identity Lifecycle events. 

For more details about Orchestration, refer to the below link.

Link to [**design**](/mosip/mosip/blob/master/docs/design/registration-processor/Approach_for_external_system_integration.md)

Link to [**design**](/mosip/mosip/blob/master/docs/design/registration-processor/Approach_for_http_integration.md)

## 2.2 Retry Processing (In case of exceptions/failures)
Registration Processor interacts with multiple external and internal systems, hence, there might be a chance that there is a communication failure between the systems for some time.

To handle such issues, the system has the capability to retry communicating with the external/internal systems multiple times (as configured). 

## 2.3 Resume Workflow
Registration Processor, even after retrying multiple time fails to communicate or there is a system error, the system stops processing the packets. 

These packets are later picked up by a module in Registration Processor called the Re-Processor based on a configurable logic which resumes the workflow.
## 2.4 Integration (System Integrator can integrate their system with MOSIP)
System Integrator can integrate their system with MOSIP. Which in turn  allows them to
* Customize their workflow   
* Plug-in stages
* Exclude stages 
 
Please refer to the design links below to understand how system integrator can integrate their system\s with MOSIP 

Link to [**design**](/mosip/mosip/blob/master/docs/design/registration-processor/Approach_for_external_system_integration.md)

Link to [**design**](/mosip/mosip/blob/master/docs/design/registration-processor/Approach_for_http_integration.md)

## 2.5 Multiple Workflows 

MOSIP provides different workflows for different life cycle events. For example
* New ID Issuance
* Update individual’s information
* De-activate individual’s ID
* Re-activate individual’s ID

These workflows use a common set of components (micro services)

Multiple workflows increase reusability, readability and maintainability of different components (micro services).
## 2.6 Scalability and Throughput
MOSIP is scalable so that it can handle any kind of processing load or request in the future without disturbing the base architecture. MOSIP infrastructure can handle additional processing request based on the requirement of a country. The architecture is designed in such a way that it is flexible to support scalability and holds the request until the end goal is achieved.

Link to [**design**](/mosip/mosip/blob/0.9.0_MOS-15017/docs/design/registration-processor/Approach_for_Back_Pressure_Handling.md)

# 3. Types of Stages
## 3.1 Pre-processing Validations
### 3.1.1 Sanity Check
When Registration Processor receives a packet, the system performs various sanity checks, such as:
1. **Authentication** - The system authenticates if the requestor is an verified user.
1. **Virus Scan** - The system performs in-memory virus scan of the packet received.
1. **Packet Integrity Check** - The system validates if the packet received was not tampered during transit by performing check sum validation.
1. **Packet Size Check** - The system validates if the packet received was not tampered during transit by validating the size of the packet.
1. **Packet Format Check** - The system validates if the packet format is per the configured format.
1. **Duplicate Check** – The system validates if the request received is not a duplicate request.

### 3.1.2 Virus Scan
Virus Scanning is an important process which helps to remove virus infected files from the system. 

In Registration Processor, virus scanning is performed twice, which are listed below:
1. When a packet is received by Registration Processor.
2. When Registration Processor stores the packet in its internal secure file system.

### 3.1.3 Machine-User-Center Mapping Check
The system validates a registration machine, registration officer, registration center details, and devices, which are used for packet creation. This validation is to ensure that the packet received by the Registration Processor was created in a authenticated device by a authentic Officer or superviser. 

### 3.1.4 Officer & Supervisor Validation

When a packet is created in registration client, the officer or supervisor IDs and mode of authentication is captured in the packet. The information captured can be used to perform the same validation in Registration Processor. 

The modalities used for authenticating an officer or supervisor are:
1. Biometric Authentication (Biometrics such as Iris, Face or Finger Prints)
1. Password Authentication 
1. OTP Based Authentication
## 3.2 Processing
### 3.2.1 Individual Data Validations
#### 3.2.1.1 Data Quality Check: Photo, Age, Gender Data Check
The system checks if the photo, age and gender captured by the registration officer while registering an individual using registration client are in sync. 
#### 3.2.1.2 Biometrics Quality Check
The system checks the quality of biometrics (Face Photo, Finger Print Image, and Iris Image) captured by the registration officer while registering an individual using registration client. 

The system also checks the liveliness of the Finger Print Image captured of an individual and validates the photo captured as per ICAO (International Civil Aviation Organization) standards.

#### 3.2.1.3 Doc. Validation - OCR 
The system checks if some data captured while registering an individual using registration client is available in the document, which is uploaded using OCR (Optical Character Recognition).
### 3.2.2 Functional Validations
#### 3.2.2.1 File & Document Validation

When the Registration Packets are received from Registration Client, the system checks if all the files listed in the packet are available. If available, the system verifies if the documents required for an individual are present in the packet as per the data captured. In order to perform this validation, the mapping of the data captured and mandatory document required can be configured by the country. 
For Example:
1. If name is captured, the country can add a validation for Proof of Identity.
2. If address is captured, the country can add a validation for Proof of Address.

#### 3.2.2.2 Introducer Validation

When a Minor needs to be registered, the system mandates the capture of the UIN or RID and biometrics of an Introducer (Parent or Guardian). In Registration Processor, this data is used to Authenticate the Introducer.

#### 3.2.2.3 Deduplication – Demographic, Biometrics
Deduplication is the process to find a duplicate by comparing the individual’s details (biometric and demographic data) with the data stored in the system for which UIN has been generated or yet to be generated.
#### A. Demographic deduplication

1. The system compares the demographic details (name, gender, and date of birth) of the individual with the data available in the system to find a potential match.
2. If a potential match is found, then the system sends the packet to [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface) to perform 1:1 biometric match (it is an additional check to confirm that it is a duplicate).
3. If a potential match is not found in [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface) or Demographic deduplication, then system sends the packet to perform biometric deduplication.
#### B. Biometric deduplication
1. The system performs Biometric deduplication (1:N, where N indicates the whole set of biometric available in the system) by sending the data to [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface).
2. [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface) compares the biometric data received with the whole set of the data to find a potential match based on a configured threshold.
3. If a potential match is found in [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface), then the system sends the packet for manual verification.
4. If a manual verifier (experts who know more about biometrics) finds a duplicate, then the system rejects the packet.
5. If the manual verifier or [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface) does not find the duplicate, then the system sends the packet for UIN generation.

### 3.2.3 External System Integration: (Elaborate with examples)
#### 3.2.3.1 Data Verification (Pluggable by SI – Not part of MOSIP)

The System Integrator can plug-in a stage in the workflow, where the stage can communicate with any other external system and receive some data. 

Data verification is a process in which the system verifies the data captured during a registration with the data received from the external system to ensure accuracy and consistency. It helps to determine whether data was accurately translated, is complete and supports the interoperability standards.

#### 3.2.3.2 Data Enrichment 

Data enrichment is a value adding process, where external data from multiple sources is added to the existing data sets in MOSIP to enhance the quality and richness of the data.
MOSIP receives some data from the external system in the form of Packet (as per MOSIP Standards). The System has the capability to receive this updated packet from external sources and process it with the packet received from Registration Client.

#### 3.2.3.3 Manual Verification for ext. system data update (Pluggable by SI)

When there are any discrepancies between the data received from external system vs.the data captured during registration, a country may opt to manually verify the data. 
The System Integrator in such case may build a Manual Verification Module for External System data mismatch. MOSIP will enable the system integrator to integrate the manual verification system with MOSIP platform

#### 3.2.3.4 Manual Adjudication (Pluggable by SI)
When Biometric Deduplicates are found in [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface), the System Integrator can plug-in the Manual Adjudication Stage, which would send the biometric and demographic data of the duplicates to a Manual Adjudicator. The Manual Adjudicator now can perform various validations on the duplicate data and inform the MOSIP system if the two records are duplicates or not.
#### 3.2.3.5 ABIS Integration (Incl. ABIS Middleware)
The MOSIP System, in-order to perform Biometric Deduplication (validate if there are no biometric duplicates in system), integrates with one or multiple ABISs ([**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface)). 

ABIS Middleware, which is designed by MOSIP and MOSIP Middleware, designed by [**Automated Biometric Identification System**](Automated-Biometric-Identification-System-(ABIS)-Interface) is used to communicate between MOSIP system and ABIS.

### 3.2.4 ID Issuance 
#### 3.2.4.1 Identity Generation (Refer to UIN Generation service) – Incl. UIN Generation and UIN association
After all the business validations are completed, the system gets a Unique Identification Number (UIN) from the [**UIN Generation**](UIN-Generation) API and allocates the UIN by sending the new UIN number and the individual's information to [**ID repository**](ID-Repository-API).
#### 3.2.4.2 Store/Update ID Repository (Refer to ID-Auth)
After all the business validations are performed for a new ID issuance or updating an individual’s information, this information is sent to [**ID repository**](ID-Repository-API) for storing or updating the information respectively.  
#### 3.2.4.3 Data Extractor for ID Authentication
The system that extracts the latest copy of an individual’s data after the Individual has registered in MOSIP or has updated their data in MOSIP and sends it to ID Authentication. Now, ID Authentication can use the latest copy of the Individual’s data for Authentication.         

### 3.2.5 Capture Audit Trails/Analytics Data
When any transaction is performed in MOSIP system or the packet fails any validations or any system level exception happens, then the same is captured as part of MOSIP Audit Trails, which can be further used for Reporting/Analytics as required.
## 3.3 Post-Processing
### 3.3.1 Notification (Pluggable by SI)
Notification (SMS/Email as configured), which is received by an individual is the final step of all the life cycle processes. System sends a notification to the individual for various life cycle scenarios such as, successful or un-successful issuance of UIN, update of UIN data, activate or deactivate UIN, finding a lost UIN, etc. using kernel [**Template Merger**](FRS-Common-Services#45-template-merger-) and [**Notification Manager**](FRS-Common-Services#4-notification-).
### 3.3.2 Print & Post (Pluggable by SI)
After a UIN is generated or UIN data is updated, the system creates a UIN card using kernel [**Template Merger**](FRS-Common-Services#45-template-merger-) and sends it to Printing and Postal Service Provider.
### 3.3.3 Data Seeding to External Functional ID System (Pluggable by SI)
If a country wants to Integrate with any External Functional ID Systems, MOSIP provides the capability to integrate with any External System.
