## Table Of Content

- [Scope of Version 0.12.15](#scope-of-version-01215-)
- [Documentation](#documentation-)
- [Key Points](#key-points-)
- [Code](#code-)
- [Test Reports](#test-reports-)
  * [1. In Scope](#1-in-scope-)
  * [2. Out Of Scope – MOSIP V0.12.15 Platform](#2-out-of-scope--mosip-v01215-platform-)
  * [3. Executive Summary – Consolidated Quality Status](#3-executive-summary--consolidated-quality-status-)
  * [4. Types of Testing](#4-types-of-testing-)
  * [5. Manual Test Reports](#5-manual-test-reports-)
  * [6. Automation Test Reports](#6-automation-test-reports-)
- [Known Issues](#known-issues-)
- [Support Process (To Be Determined)](#support-process-to-be-determined-)
- [List Of Acronyms](#list-of-acronyms-)
## Scope of Version 0.12.15 [**[↑]**](#table-of-content)
This release is with **proxy biometrics**. This means that the implementation of Print system, SDK, MDM (Mosip Device Manager), ABIS and biometric devices has been stubbed. Also, this version is tested for functionality. Non-functional requirements (Performance, Scalability and  Security) are not yet tested and will be taken up in subsequent releases.

* Modules included – Pre-Registration, Registration Client, Registration Processor, ID Authentication, Reference GUI implementation of Pre-Registration and Registration Client. 
* Modules excluded – Administration, Partner Management, Resident Services
## Documentation [**[↑]**](#table-of-content)
### 1. Platform Documentation 
Includes Functional requirements, Process flows, Architecture and high level design, Getting started and Deployment guide, Developer documentation etc.  
   [**Link to Platform Documentation**](Platform-Documentation)
### 2. Detailed Documentation
[**Low Level design**](/mosip/mosip/tree/0.12.0/docs/design ), [**Test cases**](//mosipid.atlassian.net/issues/?jql=project%20%3D%20MOS%20AND%20issuetype%20%3D%20test%20order%20by%20%22Epic%20Link%22)

## Key Points [**[↑]**](#table-of-content)

|Key Points|	Details|
|----|----|
|Pre Registration - Browser(s) |	Chrome (Version - 74.0.3729)|
|Deployment Script Environment|	Microsoft Azure|
|Registration Client – OS version|	Windows 10 (English version)  with TPM 2.0|
|Camera|	Logitech / Default windows camera|
|Scanner|	Canon lide 120|
|GPS|	GlobalSat BU-353-S4|
|Biometrics standard for proxy|	CBEFF format (Version - 0.12.15)|
|SMS gateway|	MSG91, Infobip|
|Registration Client – face capture |	OpenImaj - This is licensed for demo purpose only|
|Keystore|	SoftHSM|
|Antivirus|	ClamAV|
|Maps	|OpenstreetMap|
|Supporting key based digital signatures, not using digital certificates||	
|Transliteration|	ICU4J (Library with French, Arabic languages)|

## Code [**[↑]**](#table-of-content)
The code and automation tests are available in [**GitHub**](/mosip/mosip/tree/0.12.15). The code needs to be build and deployed as per the [**Building And Deploying MOSIP**](Platform-Documentation#10-building-and-deploying-mosip). We would actively support the System Integrator during the first deployment process.

## Test Reports [**[↑]**](#table-of-content)
**Test Scope**
#### 1. In Scope [**[↑]**](#table-of-content)

The following have been the IN SCOPE entities for testing

|Title	|Description|
|------|------|
|Modules Tested|<li> Pre-registration (UI & Server) <li> Registration Client (UI & APIs) <li> Kernel (APIs) <li> Registration Processor (Server) <li> ID Authentication (APIs) <li> ID Repo (APIs)|
| Version Tag Tested|	0.12.15|
|Testing Methods| <li>  Manual <li>  Test Automation|
|Types of testing|<li>	 Smoke <li> Functional <li>  Integration <li> 	Regression|
|Testing Levels|![Image](_images/test_rig_automation/image1.jpg) |
|Configuration Parameters tested for| Refer to QA env properties file with suffix ‘qa’ in the filename, at [**Link**](/mosip/mosip-configuration/tree/master/config)|
|Browser Support|**Pre-Registration**    <li> Chrome – 74.0.3729.169|
|OS Support|**Registration Client**    <li> Windows 10|
|Language Support|French, Arabic, English|

#### 2. Out Of Scope – MOSIP V0.12.15 Platform [**[↑]**](#table-of-content)

|Title|	Description|
|------|------|
|NFR Testing| <li> Performance Testing <li> Security Testing|
|Global Configuration Testing|<li> Testing is done for one set of approved production configuration <li> Changing the configuration parameters for various values (boundary values) and testing the impact of each such value on the platform code will be taken up in subsequent releases.|

#### 3. Executive Summary – Consolidated Quality Status [**[↑]**](#table-of-content)

|Sl. No.|	Module / Activity|Testing Methodology|	Tested Entities|
|------|------|------|------|
|1|	Kernel	|<li> Test Automation	|<li> API|	
|2|	Pre-Registration|<li> Manual Testing <li> Test Automation|<li> UI <li> API <li> Workflows|<li> Certified critical functional workflows <li> Open Defects <li> Major – <li> Minor - |
|3|	Registration Client|<li> Manual Testing <li> Test Automation| <li> UI <li> API <li> Workflows||
|4|Registration Processor|<li> Manual Testing <li> Test Automation	|<li> API <li> Workflows| |
|5|	ID Authentication	|	Test Automation	|<li> API <li> Workflows|	|
|6|	ID Repo	|	Test Automation	|<li> API|	|	
|7|Pre-Registration to Registration Client integration testing|	Manual Testing|	Workflows|	|	
|8|	Registration Client to Registration Processor integration testing|	Manual Testing|	Workflows||	
|9|	Registration Processor to Pre-Registration integration testing|Manual Testing|Workflows|	|	
|10|	Registration Processor to Registration Client integration testing|	Manual Testing|	Workflows|	|
|11|	Registration Client to IDA integration testing|	Manual Testing|	Workflows|		|
|12|	Registration Processor to IDA integration testing|	Manual Testing|	Workflows	||
|13|	IDA to ID Repo|	Manual Testing|	Workflows	|	|
|14|Kernel API integration|	<li> Manual Testing <li> Test Automation|	
|15|	End to end testing|	Manual Testing|	Workflows	|	

#### 4. Types of Testing [**[↑]**](#table-of-content)

|Testing Type| Description|
|------|------|
|Smoke Testing|Test to ensure basic and critical domain workflows work fine|
|Functional Testing|Test to ensure functionality of each module and system at large work fine in accordance with the given requirements|
|Integration Testing|Test to ensure the inter module functionality works fine and in accordance with the integration requirements|
|Regression Testing|Test to ensure no new functionality or change breaks old functionality and all existing features work fine|
	
#### 5. Manual Test Reports [**[↑]**](#table-of-content)
To be done
#### 6. Automation Test Reports [**[↑]**](#table-of-content)
Consolidated report run on 0.12.15 on QA env, from merged automation code base
## Known Issues [**[↑]**](#table-of-content)

## Support Process (To Be Determined) [**[↑]**](#table-of-content)
Process to be followed for support required, escalation matrix, etc.

## List Of Acronyms [**[↑]**](#table-of-content)
[**Refer to List Of Acronyms**](Platform-Documentation#12-list-of-acronyms)




