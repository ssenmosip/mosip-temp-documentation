## 1. MOSIP-INTRODUCTION
### 1.1	Scope
The scope of this document is to describe high level business objectives along with explicit functional requirements of MOSIP (Modular Open source Identity management platform) completely, accurately and unambiguously in Technology-independent manner.
### 1.2	Intended audience
#### 1.2.1	Internal audience
1. Business owners of the proposed system. They must be able to verify that their business requirements have been documented here completely, accurately and unambiguously.
1. Data Architects, Application Architects and Technical Architects would also find the information in this document useful when they need to design a solution that will address these business requirements.

#### 1.2.2	External Audience
1. SIs (System Integrator).
1. Since the requirements are documented here in Technology-independent manner, the end-users of the system should be able to comprehend the requirements fairly easily from this document.
## 2.	MOSIP -FOR IDENTITY MANAGEMENT
### 2.1	What-is an identity management system
### 2.2	Why-an identity management system is needed
### 2.3	Setting the stage for MOSIP. (How MOSIP as a product\platform wants to position itself)

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