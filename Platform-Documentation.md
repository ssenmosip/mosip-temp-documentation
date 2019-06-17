*WIP
## Table Of Content
- [DOCUMENT SCOPE](#document-scope-)
- [1. INTRODUCTION](#1-introduction-)
  * [1.1 Why-an Identity Management System is Needed](#11why-an-identity-management-system-is-needed-)
  * [1.2 Key Features of MOSIP Platform](#12key-features-of-mosip-platform-)
  * [1.3 Key Objectives of MOSIP Platform](#13-key-objectives-of-mosip-platform-)
- [2. FUNCTIONAL OVERVIEW](#2-functional-overview)
  * [2.1 Pre-Registration](#21-pre-registration-)
  * [2.2 Registration Services](#22-registration-services-)
  * [2.3 Registration Processor](#23-registration-processor-)
  * [2.4 ID Authentication](#24-id-authentication-)
  * [2.5 Kernel](#25-kernel-)
  * [2.6 Administrator Services (WIP)](#26-administrator-services-wip-)
  * [2.7 Resident Services (WIP)](#27-resident-services-wip-)
  * [2.8 Partner Management (WIP)](#28-partner-management-wip-)
  * [2.9 ID Repository](#29-id-repository-)
- [3. REQUIREMENT SPECIFICATIONS](#3-requirement-specifications)
  * [3.1 Functional Requirement Specifications](#31-functional-requirement-specifications-)
  * [3.2 Non-Functional Requirement Specifications](#32-non-functional-requirement-specifications-)
- [4. ARCHITECTURE OVERVIEW](#4-architecture-overview-)
  * [4.1 Principles](#41-principles-)
  * [4.2 Platform Features](#42-platform-features-)
    + [4.2.1 Configurability](#421-configurability-)
    + [4.2.2 Extensibility](#422-extensibility-)
    + [4.2.3 Modularity](#423-modularity-)
  * [4.3 Process View](#43-process-view-)
  * [4.4 Logical View](#44-logical-view-)
  * [4.5 Technology Stack](#45-technology-stack-)
  * [4.6 Data Architecture](#46-data-architecture-)
- [5. ARCHITECTURALLY SIGNIFICANT COMPONENTS](#5-architecturally-significant-components-)
  * [5.1 ID Object Definition](#51-id-object-definition-)
  * [5.2 Configurations](#52-configurations-)
  * [5.3 Registration Packet Structure](#53-registration-packet-structure-)
  * [5.4 ABIS Middleware](#54-abis-middleware-)
  * [5.5 Biometric Data Standards](#55-biometric-data-standards-)
  * [5.6 MOSIP Device Specification](#56-mosip-device-specification-)
  * [5.7 Core Data Management](#57-core-data-management-)
  * [5.8 Integration with External Systems](#58-integration-with-external-systems-)
- [6. TEST RIG](#6-test-rig-)
- [7. PERFORMANCE AND SIZING GUIDELINES](#7-performance-and-sizing-guidelines-)
- [8. PRIVACY AND SECURITY](#8-privacy-and-security-)
- [9. MOSIP APIs](#9-mosip-apis-)
  * [9.1 External APIs](#91external-apis-)
    + [9.1.1 ID Authentication APIs](#911-id-authentication-apis-)
    + [9.1.2 ABIS APIs](#912-abis-apis-)
    + [9.1.3 OTP Manager API](#913-otp-manager-api-)
    + [9.1.4 Pre-Registration APIs](#914-pre-registration-apis-)
    + [9.1.5 Registration Processor APIs](#915-registration-processor-apis-)
  * [9.2 Internal APIs](#92internal-apis-)
    + [9.2.1 Kernel](#921-kernel-)
    + [9.2.2 ID Repository](#922-id-repository-)
- [10. BUILDING AND DEPLOYING MOSIP (TBD)](#10-building-and-deploying-mosip-)
  * [10.1 Getting Started Guide](#101-getting-started-guide-)
  * [10.2 Developer Document](#102-developer-document-)
- [11. INFRASTRUCTURE RECOMMENDATIONS](#11--infrastructure-recommendations-)
  * [11.1 Customization (WIP)](#111-customization-wip-)
  * [11.2 Data Center Architecture (WIP)](#112-data-center-architecture-wip-)
- [12. GLOSSARY](#12--glossary-)
- [13. ABBREVIATIONS](#13-abbreviations-)
- [14. REFERENCES](#14-references-)

## DOCUMENT SCOPE [**[↑]**](#table-of-content)
The scope of this document is to describe high level business objectives along with explicit functional requirements of MOSIP (Modular Open source Identity management platform) completely, accurately and unambiguously. The document also gives an over view of the architecturally significant features, APIs, standards followed in MOSIP. Lastly, provides necessary information on implementation, customization and set up.

## 1. INTRODUCTION [**[↑]**](#table-of-content)

MOSIP acronym for Modular Open Source Identity Platform helps governments of countries to build a digital identity system. Using this, every Individual of a country can be given a Unique Identity Number (UIN). This helps in inclusivity and accessibility of all Individuals without disparity or discrimination.

### 1.1	Why-an Identity Management System is Needed [**[↑]**](#table-of-content)

![Indentity](_images/mosip_prd/Indentity.JPG)

A well-established identity management system can help countries to verify their people’s identity by issuing unique identity number which one can use to go into any institution and be readily accepted. The following are some key reasons why a country needs as Identity management system.
### 1.2	Key Features of MOSIP Platform [**[↑]**](#table-of-content)



![Basic features of MOSIP](_images/mosip_prd/mosip_basic_features.JPG)

                      Fig 1: Basic features of MOSIP

### 1.3 Key Objectives of MOSIP Platform [**[↑]**](#table-of-content)

![Key objectives of MOSIP](_images/mosip_prd/Key_objectives_of_the_platform.JPG)

## 2. FUNCTIONAL OVERVIEW
This section details out the design aspects of MOSIP, driven by the key functional modules as listed below. Navigate to wiki for further details on each module. 
### 2.1 Pre-Registration [**[↑]**](#table-of-content)

Pre-registration is the module which is the web channel of the MOSIP. This module enables a user to do the following: 
1. Book Registration Appointment 
1. Enter Demographic data & Upload supporting documents 
1. Appointment notification, rescheduling and cancellation 
1. Send resident data to registration center before appointment 

Please refer [**wiki**](FRS-Pre-Registration) for detailed functional specifications of pre-registration module.

### 2.2 Registration Services [**[↑]**](#table-of-content)
Registration Client application captures the Demographic and Biometric details of an Individual along with supporting information (proof documents & information about parent/guardian/introducer) and packages the information in a secure way. This module provides the following capabilities:
1. Provides a secure way of capturing an Individual's demographic and biometric data
1. Provides interfaces to biometric devices that comply to industry standards
1. Registration client works in online and offline mode to capture data
1. This module also provides option to transfer data to server when online and helps in uninterrupted registrations
1. Client has the ability to update itself for patch upgrades (bug fixes/enhancements) in a remote way. There could be hundreds of client instances running on laptops/desktops. Updates on all of them are controlled by the client and a central server.
1. Registration client is secured such that it cannot be tampered and misused

Please refer [**wiki**](FRS-Registration-Services) for detailed functional specifications of registration services.


### 2.3 Registration Processor [**[↑]**](#table-of-content)
Registration Processor processes the data (demographic and biometric) of an Individual for quality and uniqueness and then issues a Unique Identification Number (UIN). The source of data are primarily from:
1. MOSIP Registration Client
1. Existing ID system(s) of a country

This module has the following capabilities:
1. Provides guaranteed packet processing - Not lose the packet once received on the server
1. Handle server failure, recovery and re-submission of packets for processing automatically
1. It has the capability to add new processing step(s) without changing existing steps as different countries may have different processing requirements
1. Capability to integrate with multiple ABIS providers. Accommodate sending one or more biometric modality to one or more ABISs and calculate a composite fusion score and then take a decision on the processing
1. Each processing step is scalable independently based on the load

Please refer [**wiki**](FRS-Registration-Processor) for detailed functional requirement specifications of Registration Processor
### 2.4 ID Authentication [**[↑]**](#table-of-content)

ID Authentication in MOSIP provides services through APIs  that validates the authenticity of a resident based on one or more factors (demographic and biometric).  The authentication services are integrated with TSPs (Trusted Service Providers) for delivering eKYC services to citizens via user agencies.

This module provides the following capabilities:
1. Authenticate an Individual in a secure and trusted way
1. Captures of biometrics data as per the defined standards
1. Authenticates an Individual based on their basic identity data captured via MOSIP
1. In addition to demographic and biometric authentication, an Individual is also authenticated based on the following parameters:
   * TOTP based 
   * Static pin 
   * Challenge response
5. Authentication APIs
1. High Availability (HA) to ensure smooth service
1. Scalable to cater to the growing population of a country
1. Protects an Individual's identity from request-replay attacks
1. Audited for reporting and fraud management checks

Please refer [**wiki**](FRS-Authentication-Services) for detailed functional requirement specifications for authentication services.

### 2.5 Kernel [**[↑]**](#table-of-content)
Kernel is a platform to build higher-level services as well as a secure sandbox. Functionally it caters to the following services:
* UIN Generation
* Configuration Server
* Audit Manager
  * Log manager
* Authentication and Authorization
* Common Services
* Data Services
* Admin Services

Please refer wiki for detailed functional specification of the following services:
* [**UIN Generation**](UIN-Generation)
* [**Configuration Server**](Configuration-Server)
* [**Audit Manager**](Audit-Manager)
  * [**Log manager**](log-manager)
* [**Authentication and Authorization**](Authentication-and-Authorization)
* [**Common Services**](FRS-Common-Services)
* [**Data Services**](FRS-Data-Services)
* [**Admin Services**](FRS-Admin-Services)

### 2.6 Administrator Services (WIP) [**[↑]**](#table-of-content)
MOSIP Admin manages the functional and non-functional activities of MOSIP on Admin Portal through either the backend process or the UI screens. 

Admin will be able to:

 * Set up Platform Data, Process Flows, ID Definition, Configuration, and Security Policy (Through backend process).
 * Manage (Create, Update, View, Activate/Deactivate, Map/Un-map/Re-map/Decommission) the resources.
 * Map the resources (Users, Machines, and Devices) to a registration center.
 * Manage the master data (Create/Update/Activate/Deactivate).
 * Manage approval requests for creation and updation of resources and master data.
 * Manage personal account details (Reset Password, Forgot User Name, Change Password, Unlock Account, and Edit Personal 
   Details.
 * Activate/deactivate UIN
 * View status of packets

Please refer [**wiki**](FRS-Administrator-Services) for detailed functional specifications of administrator services module.
### 2.7 Resident Services (WIP) [**[↑]**](#table-of-content)

Resident Services module will provide a host of services for a user which he/she can utilize after generation of his/her UIN. The list of services a user can avail are outlined below:

1. Download e-UIN.
2. Retrieve lost UIN.
3. Initiate UIN Update.
4. Request re-print UIN.
5. Track status of UIN update.
6. View history of Authentication Requests.
7. Lock or Unlock UIN/VID for each ‘Auth’ type(s).

Additionally a user can also track status of his/her UIN generation after registration. 
These services include:

1. Retrieve Lost RID (registration ID).
2. Track Status of UIN Generation via RID.

Please refer [**wiki**](FRS-Resident-Services) for detailed functional specifications of resident services module.
### 2.8 Partner Management (WIP) [**[↑]**](#table-of-content)

Partner Management provides services for Partner and MISP (MOSIP Infrastructure Service Provider) Registration and Authentication. Registered Partners and MISP are only allowed to access MOSIP Authentication services. Partners and MISP are registered using Partner Management Services.  Authentication services of MOSIP will internally use the Partner Management Services to authenticate Partner and MISP and validate if only the registered entities are accessing the services.

Partner Management also involves policy management for Partners. Each partner can access Authentication services only based on a defined policy. Authentication services of MOSIP will internally use the Partner Management Services to authenticate a partner based on the policy.

Partners send authentication request and receive authentication responses in a secured setup. Public/Private keys are used for encryption/decryption/signing the request/response. A few of the key management activities are managed in the Partner Management Services.

Further Certificates are used by Partners for signing the authentication request.  Partner Management Services is used for a few of the signature related services.

Please refer [**wiki**](FRS-Partner-Management) for detailed functional specifications of Partner Management module.

### 2.9 ID Repository [**[↑]**](#table-of-content)
Please refer [**wiki**](FRS-ID-Repository) for detailed functional specifications of ID Repository.

## 3. REQUIREMENT SPECIFICATIONS
### 3.1 Functional Requirement Specifications [**[↑]**](#table-of-content)
This section provides a detailed functional requirement specification for each module in MOSIP
#### 3.1.1 [Pre-Registration](FRS-Pre-Registration)
#### 3.1.2 [Data Services](FRS-Data-Services)
#### 3.1.3 [Common Services](FRS-Common-Services)
#### 3.1.4 [Admin Services](FRS-Admin-Services)
#### 3.1.5 [UIN Generation](UIN-Generation)
#### 3.1.6 [Configuration Server](Configuration-Server)
#### 3.1.7 [Audit Manager](Audit-Manager)
#### 3.1.8 [Authentication and Authorization](Authentication-and-Authorization)
#### 3.1.9 [Registration Services](FRS-Registration-Services)
#### 3.1.10 [Registration Processor](FRS-Registration-Processor)
#### 3.1.11 [Authentication Services](FRS-Authentication-Services)
#### 3.1.12 [Resident Services](FRS-Resident-Services)
#### 3.1.13 [Administrator Services](FRS-Administrator-Services)
#### 3.1.14 [Partner Management](FRS-Partner-Management)
#### 3.1.15 [ID Repository](FRS-ID-Repository)
### 3.2 Non-Functional Requirement Specifications [**[↑]**](#table-of-content)
This section details out the non-functional requirements of MOSIP platform

Please refer [**wiki**](MOSIP-NON-Functional-Requirements) for the detailed functional spec.

## 4. ARCHITECTURE OVERVIEW [**[↑]**](#table-of-content)
MOSIP Architecture is defined in 5 separate sections which are detailed in GitHub wiki. Click on each specific header name to navigate to wiki for further details.

### 4.1 Principles [**[↑]**](#table-of-content)
This section consists of the foundational principles of MOSIP based on which the architecture is defined. The key principle considered includes: Open source and Vendor Neutral, Adaptability, Security, Multi party, Authorization, Authentication, Multi language support, Performance and Scalability, High Availability, and Auditability.

Please refer [**wiki**](Architecture-Principles-&-Platform-Goals) for more details.
### 4.2 Platform Features [**[↑]**](#table-of-content)
#### 4.2.1 Configurability [**[↑]**](#table-of-content)

MOSIP should be flexible for countries to configure the base platform according to their specific requirements. Some of the examples of configurability are
* Country should be able to choose the features required. For example, it must be possible for a country to turn off Finger Print capture
* Country should be able to configure the attributes of an ID Object
* Country should be able to define the length of the UIN number.
#### 4.2.2 Extensibility [**[↑]**](#table-of-content)

MOSIP should be flexible to extend functionality on top of the basic platform. Some of the examples of extensibility are
* A country should be able to introduce a new step in processing data
* Integrate MOSIP with other ID systems and include it as part of the MOSIP data processing flow
#### 4.2.3 Modularity [**[↑]**](#table-of-content)

All components in MOSIP should be modular and their features exposed via interfaces such that the implementation behind the interface can be changed without affecting other modules. Some examples of modularity are
* UIN generator algorithm provided by the platform can be replaced by a country with their own implementation
* The default demographic deduplication algorithm provided by MOSIP can be changed to a different one without impacting the process flow
### 4.3 Process View [**[↑]**](#table-of-content)
This section provides a functional overview of the processes like Pre-registration, Registration Client, Registration Processor, and ID Authentication.

Please refer [**wiki**](Process-view) for more details.

### 4.4 Logical View [**[↑]**](#table-of-content)
This section details the key design aspects considered for MOSIP. This includes Ecosystem approach, Configurability, Extensibility, Modularity, and Solution Principles. 

Please refer [**wiki**](Logical-Architecture) for more details.

### 4.5 Technology Stack [**[↑]**](#table-of-content)
This section lists all the technologies used in building MOSIP platform.

Please refer [**wiki**](Technology-Stack) for more details.

### 4.6 Data Architecture [**[↑]**](#table-of-content)
This section details the data architecture of MOSIP which includes Security, Multi-Language, High Availability, Auditability, and High Performance. It also details the data models and its naming standards. 

Please refer [**wiki**](MOSIP-Data-Architecture) for more details.

## 5. ARCHITECTURALLY SIGNIFICANT COMPONENTS [**[↑]**](#table-of-content)
### 5.1 ID Object Definition [**[↑]**](#table-of-content)
ID definition describes the attributes a Country or entity intends to capture from an Individual, which will formulate the definition of ID for a Country. This section elaborates on the mechanism MOSIP adopts, in order to provide the flexibility for each Country to define its preferred ID definition and ID object definition schema.

Please refer [**wiki**](MOSIP-ID-Object-definition) for more details.

### 5.2 Configurations [**[↑]**](#table-of-content)
MOSIP as a platform will have multiple applications running and each application will have a set of configurations.
This section details:
1. The key configuration files a system owner has to create before starting the platform – with a centralized Config Server.
1. Launcher component which will read the configuration files, validate and launch the platform.

Please refer [**wiki**](MOSIP-configuration-&-launcher) for more details.

### 5.3 Registration Packet Structure [**[↑]**](#table-of-content)
This section illustrates the packet creation flow along with the encryption process, as part of Registration Client.

Please refer [**wiki**](Registration-Packet) for more details.

### 5.4 ABIS Middleware [**[↑]**](#table-of-content)
This section provides details on the ability of MOSIP to support a single or multi-ABIS solution, specifics on the Components & APIs of ABIS Middleware, Strategies for Biometric data management in ABIS and Strategies for de-duplication in case of multiple ABIS systems.

Please refer [**wiki**](MOSIP-ABIS-Middleware) for more details.
### 5.5 Biometric Data Standards [**[↑]**](#table-of-content)
This section details out the specifications for Biometric data during data acquisition and verification. 

Please refer [**wiki**](MOSIP-Biometric-Data-Specifications) for more details.

### 5.6 MOSIP Device Specification [**[↑]**](#table-of-content)
This section illustrates the VDM technical specifications to be adhered by a vendor, who intends to adopt their devices to the MOSIP platform, so as to capture the biometric data and process the same. 

Please refer [**wiki**](MOSIP-VDM-Specifications) for more details.

### 5.7 Core Data Management [**[↑]**](#table-of-content)
ID Repository module contains the golden record of Identity for an Individual. Once new/update packets are processed by Registration Processor, the Identity details of an Individual are added/updated in ID Repository. The Identity information available in ID Repository is then used by ID Authentication to authenticate an Individual.

This module exposes few REST APIs which can be used to create/update/retrieve Identity of an Individual. Please refer [**wiki**](ID-Repository-API) for more details.

### 5.8 Integration with External Systems [**[↑]**](#table-of-content)
This section illustrates the integrational specifications of MOSIP with an external system.
Please refer to [**wiki**](/mosip/mosip/blob/0.12.0/docs/design/registration-processor/External_System_Integration_Guide.md) for more details.

## 6. TEST RIG [**[↑]**](#table-of-content)
Test Rig represents a one click automation to build, deploy and test a software module. Successful execution of test rig would ascertain complete setup of the MOSIP platform.

Please refer to [**wiki**](Test-Rig-Design) for more details about **Test Rig Design**.

Please refer to [**wiki**](Tester-Documentation) for more details about **Test Automation**.

## 7. PERFORMANCE AND SIZING GUIDELINES [**[↑]**](#table-of-content)
Please refer [**wiki**](Performance-and-Sizing-Guidelines) for more details.

## 8. PRIVACY AND SECURITY [**[↑]**](#table-of-content)
Multiple aspects of Security like Confidentiality, Privacy, and Integrity of data are key in ensuring an Individual's identity is not compromised. This section illuminates on the Security design principles MOSIP follows.

Please refer [**wiki**](Security) for more details.

## 9. MOSIP APIs [**[↑]**](#table-of-content)
APIs are the crux of MOSIP platform. This section explains about the internal and external APIs of MOSIP platform. Navigate to  wiki to know more about each API.
### 9.1	External APIs [**[↑]**](#table-of-content)
This sections details out the external APIs of MOSIP that interact with external entities.
#### 9.1.1 ID Authentication APIs [**[↑]**](#table-of-content)
Format: JSON

This section details the REST services exposed by ID Authentication. 

Please refer [**wiki**](ID-Authentication). 

This service details Auth Request to be used by TSPs to authenticate an Individual. Below are various authentication types supported by this service:
1. OTP based - Time-based OTP
2. Demo based - Personal Identity, Address
3. Bio based - Fingerprint, IRIS and Face

#### 9.1.2 ABIS APIs [**[↑]**](#table-of-content)
Format: JSON

An ABIS system that integrates with MOSIP should support the operations listed in this section.

Refer [**wiki**](ABIS-APIs). 

All ABIS operations are via a message queue & asynchronous and should adhere to the Common parameters as identified.
This service details the behavior of:
1. Insert Request
1. Identify Request
1. Delete Request
1. Ping Request
1. Pending Jobs Request
1. Reference Count Request
#### 9.1.3 OTP Manager API [**[↑]**](#table-of-content)
Format: JSON

OTP manager includes APIs for
1. OTP generation
1. OTP validation. 

Please refer [**wiki**](Kernel-APIs#otp-manager)
#### 9.1.4 Pre-Registration APIs [**[↑]**](#table-of-content)
Format: JSON

This [**wiki**](Pre-Registration-Services) details about the service APIs in the Pre-Registration modules
#### 9.1.5 Registration Processor APIs [**[↑]**](#table-of-content)
Format: JSON

This API will support the following features
1. APIs for receiving packets
1. APIs for packet registration status
1. APIs for Manual Verification. 

Refer [**wiki**](Registration-Processor-APIs) for more details
### 9.2	Internal APIs [**[↑]**](#table-of-content)
This section describes about APIs consumed by internal modules. Listed below are a few MOSIP internal APIs
#### 9.2.1 Kernel [**[↑]**](#table-of-content)
The Kernel APIs cover the following APIS
1. APIs for key management
1. APIs for master data management
1. APIs for configuration management
1. APIs for Audit and Log management

Please refer [**wiki**](Kernel-APIs) for more details.

#### 9.2.2 ID Repository [**[↑]**](#table-of-content)
This is a central API which all other modules of MOSIP will use to retrieve an ID record. This API will support the following features
1. Creation of a ID record
1. Lookup of an ID record based on the UIN
1. Updation of an ID record based on the UIN
1. Will not support search based on attributes of an ID

Please refer [**wiki**](ID-Repository-API) for more details

## 10. BUILDING AND DEPLOYING MOSIP [**[↑]**](#table-of-content)
### 10.1 Getting Started Guide [**[↑]**](#table-of-content)
Please refer [**wiki**](Getting-Started) for more details.
### 10.2 Developer Document [**[↑]**](#table-of-content)
Please refer [**wiki**](Developer-Documentation) for more details
## 11.  INFRASTRUCTURE RECOMMENDATIONS [**[↑]**](#table-of-content)
### 11.1 Customization (WIP) [**[↑]**](#table-of-content)
### 11.2 Data Center Architecture (WIP) [**[↑]**](#table-of-content)
## 12.  GLOSSARY [**[↑]**](#table-of-content)
## 13. ABBREVIATIONS [**[↑]**](#table-of-content)
## 14. REFERENCES [**[↑]**](#table-of-content)

