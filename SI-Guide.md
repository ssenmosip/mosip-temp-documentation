* [1. MOSIP-INTRODUCTION](#1-mosip-introduction)
  * [1.1 Scope](#11scope)
  * [1.2 Intended audience](#12intended-audience)
    * [1.2.1 Internal audience](#121internal-audience)
    * [1.2.2 External Audience](#122external-audience)
* [3. MOSIP FUNCTIONAL OVERVIEW](#3mosip-functional-overview)
  * [3.1 Pre-Registration](#31-pre-registration)
  * [3.2 Registration Client](#32-registration-client)
  * [3.3 Registration Processor](#33-registration-Processor)
  * [3.4 ID Authentication](#34-id-authentication)
  * [3.5 Kernel](#35-kernel)
  * [3.6 ADMINISTRATION](#36-administration)
  * [3.7 MOSIP RESIDENT SERVICES](#37-mosip-resident-services)
  * [3.8 Reports](#38-reports)
* [4. MOSIP ARCHITECTURE OVERVIEW](#4mosip-architecture-overview)
  * [4.1 Patterns and Principles](#41-patterns-and-principles)
  * [4.2 Logical View](#42-logical-view)
  * [4.3 Technology Stack](#43-technology-stack)
  * [4.4 Process View](#44-process-view)
  * [4.5 Data Architecture](#45-data-architecture)
* [5. ARCHITECTURALLY SIGNIFICANT COMPONENTS OF MOSIP](#5architecturally-significant-components-of-mosip)
  * [5.1 MOSIP ID Object Definition](#51-mosip-id-object-definition)
  * [5.2 MOSIP Configuration and Launcher](#52-mosip-configuration-and-launcher)
  * [5.3 Registration Packet Structure](#53-registration-packet-structure)
  * [5.4 MOSIP-ABIS middleware](#54-mosip-abis-middleware)
  * [5.5 Know more about ABIS interface Spec](#55-know-more-about-abis-interface-spec)
  * [5.6 MOSIP Biometric Data Standards](#56-mosip-biometric-data-standards)
  * [5.7 Vendor Device Specifications](#57-vendor-device-specifications)
  * [5.8 Security](#58-security)

## 1. MOSIP-INTRODUCTION
### 1.1	Scope
The scope of this document is to describe high level business objectives along with explicit functional requirements of MOSIP (Modular Open source Identity management platform) completely, accurately and unambiguously in Technology-independent manner.
### 1.2	Intended Audience
#### 1.2.1	Internal audience
1. Business owners of the proposed system. They must be able to verify that their business requirements have been documented here completely, accurately and unambiguously.
1. Data Architects, Application Architects and Technical Architects would also find the information in this document useful when they need to design a solution that will address these business requirements.

#### 1.2.2	External Audience
1. SIs (System Integrator).
1. Since the requirements are documented here in Technology-independent manner, the end-users of the system should be able to comprehend the requirements fairly easily from this document.
## 2.	MOSIP -FOR IDENTITY MANAGEMENT
### 2.1	What-is an identity management system
To better understand and serve citizens, countries are placing increasing attention on establishing national identification systems .The ability to formally identify oneself has increasingly become integral to many aspects of civic participation and inclusion. Proponents argue that formalized identity management systems have the potential to establish strategic partnerships between the state and citizen’s .Failure to register populations and provide identity documents is believed to have detrimental effects for both the individual and the state.

The complexity of government administration in “the modern world” is a major problem in developing countries. Often, individual government programs have their own database of beneficiaries that are not digitized and therefore cannot be easily merged. Delivering public services efficiently and providing financial inclusion to the poor in partnership with the private sector depends on accurate identification and authentication of citizens and residents. Hence Government programs must have the capacity to cross-reference databases and information.
### 2.2	Why-an identity management system is needed

A well-established identity management system can help countries to verify their people’s identity by issuing unique identity number which one can use to go into any institution and be readily accepted. The following are some key reasons why a country needs as Identity management system.

### 2.3	Setting the stage for MOSIP. (How MOSIP as a product\platform wants to position itself)

MOSIP (Modular Open Source Identity Platform) helps government countries to build a digital identity system. Using this, every Individual of a country can be given a Unique Identity Number (UIN). This helps in inclusivity and accessibility of all Individuals without disparity or discrimination.



## 3.	MOSIP FUNCTIONAL OVERVIEW
This section details out the design aspects of MOSIP, driven by the key functional modules as listed below. 
### 3.1 Pre-Registration
Pre-registration is the module which is the web channel of MOSIP. This section elaborates on the key design considerations for Pre-registration which include micro-service based architecture, Data validation as executed in UI, key design patterns like aggregate service pattern and proxy design pattern. It also elaborates on the architecturally significant use cases by providing a Process View and Conceptual View.

### 3.2 Registration Client
Registration Client application captures the Demographic and Biometric details of an Individual along with supporting information (proof documents & information about a parent/guardian/introducer) and packages the information in a secure way. This section provides details on the architecturally significant use cases of Registration Client, which include the ability to be adhered to industry standards, facilitate secure data transmission, Process View and Logical View, to name a few.


### 3.3 Registration Processor
Registration Processor processes the data (Demographic and Biometric) of an Individual for quality and uniqueness and then issues a Unique Identification Number (UIN). This section elucidates the architecturally significant use cases of Registration Processor, which include ability to be scalable, facilitate integration, look-up of the Process View and Logical View, to name a few.


### 3.4 ID Authentication

MOSIP ID Authentication provides an API based authentication mechanism for entities to validate Individuals. This section provides details on the architecturally significant use cases of ID-Authentication, which include specifics on API standards, the Process View and Logical View, to list a few.

### 3.5 Kernel
Kernel is a platform to build higher-level services as well as a secure sandbox. This section provides details on the active framework of MOSIP, its structure & rules within which the higher-level services operate, the architecturally significant use cases and Logical View, to name a few.


### 3.6 ADMINISTRATION
### 3.7 MOSIP RESIDENT SERVICES
### 3.8 Reports
## 4.	MOSIP ARCHITECTURE OVERVIEW
MOSIP Architecture is defined in 5 separate sections as stated below.
### 4.1 Patterns and Principles
This section consists of the foundational principles of MOSIP based on which the architecture is defined. The key principle considered includes: Open source and Vendor Neutral, Adaptability, Security, Multi party, Authorization, Authentication, Multi language support, Performance and Scalability, High Availability, and Auditability.

### 4.2 Logical View
This section details the key design aspects considered for MOSIP. This includes Ecosystem approach, Configurability, Extensibility, Modularity, and Solution Principles. 
### 4.3 Technology Stack
This section lists all the technologies used in building MOSIP platform.

### 4.4 Process View
This section provides a functional overview of the processes like Pre-registration, Registration Client, Registration Processor, and ID Authentication.

### 4.5 Data Architecture
This section details the data architecture of MOSIP which includes Security, Multi-Language, High Availability, Auditability, and High Performance. It also details the data models and its naming standards. 
## 5.	ARCHITECTURALLY SIGNIFICANT COMPONENTS OF MOSIP
### 5.1 MOSIP ID Object Definition
ID definition describes the attributes a Country or entity intends to capture from an Individual, which will formulate the definition of ID for a Country. This section elaborates on the mechanism MOSIP adopts, in order to provide the flexibility for each Country to define its preferred ID definition and ID object definition schema.

### 5.2 MOSIP Configuration and Launcher
MOSIP as a platform will have multiple applications running and each application will have a set of configurations.
This section details:
1. The key configuration files a system owner has to create before starting the platform – with a centralized Config Server.
1. Launcher component which will read the configuration files, validate and launch the platform.

### 5.3 Registration Packet Structure
This section illustrates the packet creation flow along with the encryption process, as part of Registration Client.

### 5.4 MOSIP-ABIS middleware
This section provides details on the ability of MOSIP to support a single or multi-ABIS solution, specifics on the Components & APIs of ABIS Middleware, Strategies for Biometric data management in ABIS and Strategies for de-duplication in case of multiple ABIS systems.

### 5.5 Know more about ABIS interface Spec
This section provides the specifications that an ABIS provider must implement to meet MOSIP's requirements.


### 5.6 MOSIP Biometric Data Standards
This section details out the specifications for Biometric data during data acquisition and verification. 
### 5.7 Vendor Device Specifications
This section illustrates the VDM technical specifications to be adhered by a vendor, who intends to adopt their devices to the MOSIP platform, so as to capture the biometric data and process the same. 
### 5.8 Security 
Multiple aspects of Security like Confidentiality, Privacy, and Integrity of data are key in ensuring an Individual's identity is not compromised. This section illuminates on the Security design principles MOSIP follows.
## 6. MOSIP REQUIREMENT SPECIFICATIONS
### 6.1 FUNCTIONAL REQUIREMENT SPECIFICATIONS
This Section provides a detailed functional requirement specification for each module in MOSIP
Please refer wiki for the detailed functional spec.
###  6.2 NON-FUNCTIONAL REQUIREMENT SPECIFICATIONS
This Section details out the non-functional requirements of MOSIP platform
Please refer wiki for the detailed functional spec.

## 7. MOSIP APIs
APIs are the crux of MOSIP platform. This section explains about the internal and external APIs of MOSIP platform. Navigate to  wiki to know more about each API.
### 7.1	External APIs
This sections details out the external APIs of MOSIP that interact with external entities.
#### 7.1.1	ID Authentication APIs
Format: JSON
This section details the REST services exposed by ID Authentication. Please refer wiki This service details Auth Request to be used by TSPs to authenticate an Individual. Below are various authentication types supported by this service:
1. OTP based - TOTP
1. Pin based - Static Pin
1. Demo based - PersonalIdentity, Address, FullAddress
1. Bio based - Fingerprint, IRIS and Face
#### 7.1.2	ABIS APIs
Format: JSON
An ABIS system that integrates with MOSIP should support the operations listed in this section Refer wiki. All ABIS operations are via a message queue & asynchronous and should adhere to the Common parameters as identified.
This service details the behavior of:
1. Insert Request
1. Identify Request
1. Delete Request
1. Ping Request
1. Pending Jobs Request
1. Reference Count Request
#### 7.1.3	OTP Manager API
Format: JSON
OTP manager includes APIs for
1. OTP generation
1. OTP validation Please refer wiki
#### 7.1.4	Pre-Registration APIs
Format: JSON
This section Refer wiki details about the service APIs in the Pre-Registration modules
#### 7.1.5	Registration Processor APIs
Format: JSON
This API will support the following features
1. APIs for receiving packets
1. APIs for packet registration status
1. APIs for Manual Verification Refer wiki for more details
### 7.2	Internal APIs
This section describes about APIs consumed by internal modules. Listed below are a few MOSIP internal APIs
#### 7.2.1	Kernel
The Kernel APIs cover the following APIS
1. APIs for key management
1. APIs for master data management
1. APIs for configuration management
1. APIs for Audit and Log management

#### 7.2.2	ID Repository
This is a central API which all other modules of MOSIP will use to retrieve an ID record. This API will support the following features
1. Creation of a ID record
1. Lookup of an ID record based on the UIN
1. Updation of an ID record based on the UIN
1. Will not support search based on attributes of an ID

## 8. MOSIP TOOL KIT
The MOSIP tool kit provides a comprehensive guide to install and deploy MOSIP platform. It also provide infrastructure recommendations. The visual designs provides an over view of the application features and functionalities.
### 8.1	DEPLOYMENT GUIDE
(Guide on deployment (Used by SI/ Device manufacturers)
### 8.2	SET UP GUIDE
#### 8.2.1. Backend Setup (ID Definition Schema, Configs, others)
#### 8.2.2. Setup Manual: Guide to Setup and initiate platform
#### 8.2.3. Setup Manual: Guide to Pre-registration 
#### 8.2.4. Setup Manual: Guide to Registration Client Application
#### 8.2.5. Admin portal (Data, Device, User Setup)
### 8.3	Infrastructure Recommendations (Used by SI/ Device manufacturers)
### 8.4	PRODUCT DEMO (VDs)
## 9.  SUMMARY (WIP)
## 10. APPENDICES
## 11. REFERENCES