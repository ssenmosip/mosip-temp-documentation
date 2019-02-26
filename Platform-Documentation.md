*WIP
## Table Of Content
* [1. MOSIP-INTRODUCTION](#1-mosip-introduction)
  * [1.1 Scope](#11scope)
  * [1.2 Intended Audience](#12intended-audience)
* [2. MOSIP -FOR IDENTITY MANAGEMENT](#2mosip--for-identity-management)
  * [2.1 What-is an Identity Management System](#21what-is-an-identity-management-system)
  * [2.2 Why-an Identity Management System is needed](#22why-an-identity-management-system-is-needed)
  * [2.3 Key Objectives of MOSIP Platform](#23key-objectives-of-MOSIP-platform)
* [3. MOSIP FUNCTIONAL OVERVIEW](#3mosip-functional-overview)
  * [3.1 Pre-Registration](#31-pre-registration)
  * [3.2 Registration Client](#32-registration-client)
  * [3.3 Registration Processor](#33-registration-Processor)
  * [3.4 ID Authentication](#34-id-authentication)
  * [3.5 Kernel](#35-kernel)
  * [3.6 Administration](#36-administration)
  * [3.7 Resident Services](#37-resident-services)
 * [4. MOSIP SCOPE](#4mosip-scope)
* [5. MOSIP REQUIREMENT SPECIFICATIONS](#5-mosip-requirement-specifications)
  * [5.1 Functional Requirement Specifications](#51-functional-requirement-specifications)
  * [5.2 Non-Functional Requirement Specifications](#52-non--functional-requirement-specifications)
* [6. PRODUCT DEMO (VDs)](#6-product-demo-vds)
* [7. MOSIP ARCHITECTURE OVERVIEW](#7mosip-architecture-overview)
  * [7.1 Principles](#71-principles)
  * [7.2 Platform Features](#72-platform-features)
    * [7.2.1 Configurability](#721-configurability)
    * [7.2.2 Extensibility](#722-extensibility)
    * [7.2.3 Modularity](#723-modularity)
  * [7.3 Process View](#73-process-view)
  * [7.4 Logical View](#74-logical-view)
  * [7.5 Technology Stack](#75-technology-stack)
  * [7.6 Data Architecture](#76-data-architecture)
* [8. ARCHITECTURALLY SIGNIFICANT COMPONENTS OF MOSIP](#8architecturally-significant-components-of-mosip)
  * [8.1 ID Object Definition](#81-id-object-definition)
  * [8.2 Configurations](#82-configurations)
  * [8.3 Registration Packet Structure](#83-registration-packet-structure)
  * [8.4 ABIS middleware](#84-abis-middleware)
  * [8.5 MOSIP Biometric Data Standards](#85-mosip-biometric-data-standards)
  * [8.6 Vendor Device Specifications](#86-vendor-device-specifications)
  * [8.7 Security](#87-security)
  * [8.8 Core Data Management](#88-core-data-management)
  * [8.9 Test Rig Design](#89-test-rig-design)
  * [8.10 Integration with External System](#810-integration-with-external-systems)
* [9. MOSIP APIs](#9-mosip-apis)
  * [9.1 External APIs](#91external-apis)
    * [9.1.1 ID Authentication APIs](#911-id-authentication-apis)
    * [9.1.2 ABIS APIs](#912abis-apis)
    * [9.1.3 OTP Manager API](#913otp-manager-api)
    * [9.1.4 Pre-Registration APIs](#914pre-registration-apis)
    * [9.1.5 Registration Processor APIs](#915registration-processor-apis)
  * [9.2 Internal APIs](#92internal-apis)
    * [9.2.1 Kernel](#921kernel)
    * [9.2.2 ID Repository](#922id-repository)
* [10. HOW TO GUIDE](#10-how-to-guide-tbd)
  * [10.1 Getting Started Guide](https://github.com/mosip/mosip/wiki/Getting-Started)
  * [10.2 Developer Document](#102developer-document)
* [11. INFRASTRUCTURE RECOMMENDATIONS](#11--inrfastructure-recommendations)
* [12. GLOSSARY](#12--glossary)
* [13. ABBREVIATIONS](#13-abbreviations)
* [14. REFERENCES](#14-references)

## 1. MOSIP-INTRODUCTION
### 1.1	Scope
The scope of this document is to describe high level business objectives along with explicit functional requirements of MOSIP (Modular Open source Identity management platform) completely, accurately and unambiguously in Technology-independent manner. The document also gives an over view of the architecturally significant features, APIs, standards followed in MOSIP. Lastly provides necessary information on implementation, customization and set up.
### 1.2	Intended Audience
* Business owners of the proposed system. They must be able to verify that their business requirements have been documented here completely, accurately and unambiguously.
* Data Architects, Application Architects and Technical Architects would also find the information in this document useful when they need to design a solution that will address these business requirements.
* SIs (System Integrator).
* Since the requirements are documented here in Technology-independent manner, the end-users of the system should be able to comprehend the requirements fairly easily from this document.
## 2.	MOSIP -FOR IDENTITY MANAGEMENT
### 2.1	What-is an Identity Management System
To better understand and serve citizens, countries are placing increasing attention on establishing national identification systems .The ability to formally identify oneself has increasingly become integral to many aspects of civic participation and inclusion. Proponents argue that formalized identity management systems have the potential to establish strategic partnerships between the state and citizen’s .Failure to register populations and provide identity documents is believed to have detrimental effects for both the individual and the state.

The complexity of government administration in “the modern world” is a major problem in developing countries. Often, individual government programs have their own database of beneficiaries that are not digitized and therefore cannot be easily merged. Delivering public services efficiently and providing financial inclusion to the poor in partnership with the private sector depends on accurate identification and authentication of citizens and residents. Hence Government programs must have the capacity to cross-reference databases and information.
### 2.2	Why-an Identity Management System is Needed

![Indentity](_images/mosip_prd/Indentity.JPG)

A well-established identity management system can help countries to verify their people’s identity by issuing unique identity number which one can use to go into any institution and be readily accepted. The following are some key reasons why a country needs as Identity management system.

### 2.3	Key Objectives of MOSIP platform
MOSIP (Modular Open Source Identity Platform) helps government countries to build a digital identity system. Using this, every Individual of a country can be given a Unique Identity Number (UIN). This helps in inclusivity and accessibility of all Individuals without disparity or discrimination.



![Basic features of MOSIP](_images/mosip_prd/mosip_basic_features.JPG)

                      Fig: 1 Basic features of MOSIP

![Key objectives of MOSIP](_images/mosip_prd/Key_objectives_of_the_platform.JPG)



## 3.	MOSIP FUNCTIONAL OVERVIEW
This section details out the design aspects of MOSIP, driven by the key functional modules as listed below. Navigate to wiki for further details on each module. 
### 3.1 Pre-Registration
Pre-registration  is the web channel of MOSIP. 

This section elaborates on the functional requirement specifications for Pre-registration

Please refer [wiki](https://github.com/mosip/mosip/wiki/FRS-Pre-Registration) for more details.

### 3.2 Registration Client
Registration Client application captures the Demographic and Biometric details of an Individual along with supporting information (proof documents & information about a parent/guardian/introducer) and packages the information in a secure way. 

This section elaborates on the following aspects of Registration Client 

**A.** Provides details on the architecturally significant use cases of Registration Client, which include the ability to be adhered to industry standards, facilitate secure data transmission, Process View and Logical View, to name a few.

Please refer [wiki](https://github.com/mosip/mosip/wiki/Registration-Client) for more details.

B.Detailed functional requirement specifications for Registration Client

Please refer [wiki](https://https://github.com/mosip/mosip/wiki/FRS-Registration-Services) for more details.


### 3.3 Registration Processor
Registration Processor processes the data (Demographic and Biometric) of an Individual for quality and uniqueness and then issues a Unique Identification Number (UIN). 

This section elucidates the following aspects of Registration Processor

**A.**Architecturally significant use cases of Registration Processor, which include ability to be scalable, facilitate integration, look-up of the Process View and Logical View, to name a few.

Please refer [wiki](https://github.com/mosip/mosip/wiki/Registration-Processor) for more details.

B.Detailed functional requirement specifications for Registration Processor

Please refer [wiki](https://github.com/mosip/mosip/wiki/FRS-Registration-Processor) for more details
### 3.4 ID Authentication

ID Authentication provides an API based authentication mechanism for entities to validate Individuals. 

This section elaborates the following aspects of ID authentication services

**A**. Provides details on the architecturally significant use cases of ID-Authentication, which include specifics on API standards, the Process View and Logical View, to list a few.

Please refer [wiki](https://github.com/mosip/mosip/wiki/ID-Authentication) for more details.

**B.** Detailed functional requirement specifications for authentication services

Please refer [wiki](https://github.com/mosip/mosip/wiki/FRS-Authentication-Services) for more details.

### 3.5 Kernel
Kernel is a platform to build higher-level services as well as a secure sandbox. Functionally it caters to the following services
* Sub-Systems
* Common Services
* Data Services
* Admin Services

This section elaborates the following aspects of Kernel

A.Provides details on the active framework of MOSIP, its structure & rules within which the higher-level services operate, the architecturally significant use cases and Logical View, to name a few.

Please refer [wiki](https://github.com/mosip/mosip/wiki/Kernel) for more details.

B. Detailed functional requirement specifications
 
Please refer wiki for detailed functional specification of the following services
* [Sub-Systems](https://github.com/mosip/mosip/wiki/FRS-MOSIP-Sub-Systems)
* [Common Services](https://github.com/mosip/mosip/wiki/FRS-Common-Services)
* [Data Services](https://github.com/mosip/mosip/wiki/FRS-Data-Services)
* [Admin Services](https://github.com/mosip/mosip/wiki/FRS-Admin-Services)

### 3.6 Administration
### 3.7 Resident Services
## 4.	MOSIP SCOPE
## 5. MOSIP REQUIREMENT SPECIFICATIONS
### 5.1 Functional Requirement Specifications
This Section provides a detailed functional requirement specification for each module in MOSIP
#### 5.1.1 [FRS Pre-Registration](https://github.com/mosip/mosip/wiki/FRS-Pre-Registration)
#### 5.1.2 [FRS Data Services](https://github.com/mosip/mosip/wiki/FRS-Data-Services)
#### 5.1.3 [FRS Common Services](https://github.com/mosip/mosip/wiki/FRS-Common-Services)
#### 5.1.4 [FRS Admin Services](https://github.com/mosip/mosip/wiki/FRS-Admin-Services)
#### 5.1.5 [FRS MOSIP Sub Systems](https://github.com/mosip/mosip/wiki/FRS-MOSIP-Sub-Systems)
#### 5.1.6 [FRS Registration Services](https://github.com/mosip/mosip/wiki/Registration-Services)
#### 5.1.7 [FRS Registration Processor](https://github.com/mosip/mosip/wiki/FRS-Registration-Processor)
#### 5.1.8 [FRS Authentication Services](https://github.com/mosip/mosip/wiki/Authentication-Services)
#### 5.1.9 [FRS Resident Services](https://github.com/mosip/mosip/wiki/FRS-Resident-Services)
### 5.2 Non- Functional Requirement Specifications
This Section details out the non-functional requirements of MOSIP platform
Please refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-NON-Functional-Requirements) for the detailed functional spec.
## 6. PRODUCT DEMO (VDs)
## 7.	MOSIP ARCHITECTURE OVERVIEW
MOSIP Architecture is defined in 5 separate sections which are detailed in GitHub wiki. Click on each specific header name to navigate to wiki for further details.

### 7.1 Principles
This section consists of the foundational principles of MOSIP based on which the architecture is defined. The key principle considered includes: Open source and Vendor Neutral, Adaptability, Security, Multi party, Authorization, Authentication, Multi language support, Performance and Scalability, High Availability, and Auditability.

Please Refer [wiki](https://github.com/mosip/mosip/wiki/Architecture-Principles-&-Platform-Goals) for more details.
### 7.2 Platform Features
#### 7.2.1 Configurability
#### 7.2.2 Extensibility
#### 7.2.3 Modularity
### 7.3 Process View
This section provides a functional overview of the processes like Pre-registration, Registration Client, Registration Processor, and ID Authentication.
Please Refer [wiki](https://github.com/mosip/mosip/wiki/Process-view) for more details.

### 7.4 Logical View
This section details the key design aspects considered for MOSIP. This includes Ecosystem approach, Configurability, Extensibility, Modularity, and Solution Principles. 

Please Refer [wiki](https://github.com/mosip/mosip/wiki/Logical-Architecture) for more details.

### 7.5 Technology Stack
This section lists all the technologies used in building MOSIP platform.

Please Refer [wiki](https://github.com/mosip/mosip/wiki/Technology-Stack) for more details.





### 7.6 Data Architecture
This section details the data architecture of MOSIP which includes Security, Multi-Language, High Availability, Auditability, and High Performance. It also details the data models and its naming standards. 

Please Refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-Data-Architecture) for more details.

## 8.	ARCHITECTURALLY SIGNIFICANT COMPONENTS OF MOSIP
### 8.1 ID Object Definition
ID definition describes the attributes a Country or entity intends to capture from an Individual, which will formulate the definition of ID for a Country. This section elaborates on the mechanism MOSIP adopts, in order to provide the flexibility for each Country to define its preferred ID definition and ID object definition schema.

Please Refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-ID-Object-definition) for more details.

### 8.2 Configurations
MOSIP as a platform will have multiple applications running and each application will have a set of configurations.
This section details:
1. The key configuration files a system owner has to create before starting the platform – with a centralized Config Server.
1. Launcher component which will read the configuration files, validate and launch the platform.
Please Refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-configuration-&-launcher) for more details.

### 8.3 Registration Packet Structure
This section illustrates the packet creation flow along with the encryption process, as part of Registration Client.

Please Refer [wiki](https://github.com/mosip/mosip/wiki/Registration-Packet) for more details.

### 8.4 ABIS Middleware
This section provides details on the ability of MOSIP to support a single or multi-ABIS solution, specifics on the Components & APIs of ABIS Middleware, Strategies for Biometric data management in ABIS and Strategies for de-duplication in case of multiple ABIS systems.

Please Refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-ABIS-Middleware) for more details.
### 8.5 MOSIP Biometric Data Standards
This section details out the specifications for Biometric data during data acquisition and verification. 

Please Refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-Biometric-Data-Specifications) for more details.

### 8.6 Vendor Device Specifications
This section illustrates the VDM technical specifications to be adhered by a vendor, who intends to adopt their devices to the MOSIP platform, so as to capture the biometric data and process the same. 

Please Refer [wiki](https://github.com/mosip/mosip/wiki/MOSIP-VDM-Specifications) for more details.




### 8.7 Security 
Multiple aspects of Security like Confidentiality, Privacy, and Integrity of data are key in ensuring an Individual's identity is not compromised. This section illuminates on the Security design principles MOSIP follows.

Please Refer [wiki](https://github.com/mosip/mosip/wiki/Security) for more details.
### 8.8 Core Data Management
### 8.9 Test Rig Design
Test Rig represents a one click automation to build, deploy and test a software module. Successful execution of test rig would ascertain complete setup of the MOSIP platform.
Navigate to wiki for further details.
### 8.10 Integration with External Systems
This section illustrates the integrational specifications of MOSIP with an external system – WIP.





## 9. MOSIP APIs
APIs are the crux of MOSIP platform. This section explains about the internal and external APIs of MOSIP platform. Navigate to  wiki to know more about each API.
### 9.1	External APIs
This sections details out the external APIs of MOSIP that interact with external entities.
#### 9.1.1 ID Authentication APIs
Format: JSON
This section details the REST services exposed by ID Authentication. 
Please refer [wiki](https://github.com/mosip/mosip/wiki/ID-Authentication). This service details Auth Request to be used by TSPs to authenticate an Individual. Below are various authentication types supported by this service:
1. OTP based - TOTP
1. Pin based - Static Pin
1. Demo based - PersonalIdentity, Address, FullAddress
1. Bio based - Fingerprint, IRIS and Face
#### 9.1.2	ABIS APIs
Format: JSON
An ABIS system that integrates with MOSIP should support the operations listed in this section.

Refer [wiki](https://github.com/mosip/mosip/wiki/ABIS-APIs). All ABIS operations are via a message queue & asynchronous and should adhere to the Common parameters as identified.
This service details the behavior of:
1. Insert Request
1. Identify Request
1. Delete Request
1. Ping Request
1. Pending Jobs Request
1. Reference Count Request
#### 9.1.3	OTP Manager API
Format: JSON
OTP manager includes APIs for
1. OTP generation
1. OTP validation. 
Please refer [wiki](https://github.com/mosip/mosip/wiki/OTP-Manager)
#### 9.1.4	Pre-Registration APIs
Format: JSON
This section [wiki](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs) details about the service APIs in the Pre-Registration modules
#### 9.1.5	Registration Processor APIs
Format: JSON
This API will support the following features
1. APIs for receiving packets
1. APIs for packet registration status
1. APIs for Manual Verification. Refer [wiki](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs) for more details
### 9.2	Internal APIs
This section describes about APIs consumed by internal modules. Listed below are a few MOSIP internal APIs
#### 9.2.1	Kernel
The Kernel APIs cover the following APIS
1. APIs for key management
1. APIs for master data management
1. APIs for configuration management
1. APIs for Audit and Log management

Please refer [wiki](https://github.com/mosip/mosip/wiki/Kernel-APIs) for more details.

#### 9.2.2	ID Repository
This is a central API which all other modules of MOSIP will use to retrieve an ID record. This API will support the following features
1. Creation of a ID record
1. Lookup of an ID record based on the UIN
1. Updation of an ID record based on the UIN
1. Will not support search based on attributes of an ID

Please refer [wiki](https://github.com/mosip/mosip/wiki/ID-Repository-API) for more details

### 10. HOW TO GUIDE (TBD)
#### 10.1 Getting Started Guide
Please refer [wiki](https://github.com/mosip/mosip/wiki/Getting-Started) for more details
#### 10.2 Developer Document
## 11.  INFRASTRUCTURE RECOMMENDATIONS
## 12.  GLOSSARY
## 13. ABBREVIATIONS
## 14. REFERENCES

