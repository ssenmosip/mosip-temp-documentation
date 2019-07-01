## Table Of Content

- [Scope of Version 1.0.0](#scope-of-version-100-)
- [Documentation](#documentation-)
- [Key Points](#key-points-)
- [Code](#code-)
- [Test Execution reports](#test-execution-reports-)
  * [Mindtree testing report](#mindtree-testing-report)
    * [1. In Scope](#1-in-scope-)
    * [2. Out Of Scope – MOSIP V1.0 Platform](#2-out-of-scope--mosip-v10-platform-)
    * [3. Executive Summary – Consolidated Quality Status](#3-executive-summary--consolidated-quality-status-)
    * [4. Types of testing - Definition](#4-types-of-testing-)
    * [5. Manual Test Execution Metrics & Graphs](#5-manual-test-execution-metrics--graphs-)
    * [6. Automation Test Reports](#6-automation-test-reports-)
- [Support Process (To Be Determined](#support-process-to-be-determined-)

## Scope of Version 1.0.0 [**[↑]**](#table-of-content)
This release is with **proxy biometrics**. This means that the implementation of Print system, SDK, MDM (Mosip Device Manager), ABIS and biometric devices has been stubbed. Also, this version is tested for functionality. Nonfunctional requirements (Performance, Security) are not tested.

* Modules included – Pre Registration, Registration Client, Registration Processor, ID Authentication
* Modules excluded – Administration, Partner Management, Resident Services
* Reference implementation of Pre-Registration and Registration Client UI
## Documentation [**[↑]**](#table-of-content)
### 1. Platform Documentation 
High Level documentation including Functional requirements, Process flows, Architecture and high level design documents, Deployment guide, Developer documentation etc.  
   [**Link to Platform Documentation**](Platform-Documentation)
### 2. Detailed Documentation
[**Low Level design**](/mosip/mosip/tree/0.12.0/docs/design ), Wireframes, [**Test cases**](//mosipid.atlassian.net/issues/?jql=project%20%3D%20MOS%20AND%20issuetype%20%3D%20test%20order%20by%20%22Epic%20Link%22)

## Key Points [**[↑]**](#table-of-content)

|Key Points|	Details|
|----|----|
|Pre Registration - Browser(s) |	Chrome (Version - 74.0.3729)|
|Deployment Script Environment|	Microsoft Azure|
|Registration Client – OS version|	Windows 10 (English version)  with TPM 2.0|
|Camera|	Logitech / Default windows camera|
|Scanner|	Canon lide 120|
|GPS|	GlobalSat BU-353-S4|
|Biometrics standard for proxy|	CBEFF format (Version - 1.0)|
|SMS gateway|	MSG91, Infobip|
|Registration Client – face capture |	OpenImaj - This is licensed for demo purpose only|
|Keystore|	SoftHSM|
|Antivirus|	ClamAV|
|Maps	|OpenstreetMap|
|Supporting key based digital signatures, not using digital certificates||	
|Transliteration|	ICU4J (Library with French, Arabic languages)|

## Code [**[↑]**](#table-of-content)
The code is available in open source repository. This includes automation test suite. The code needs to be downloaded and deployed as per the [**Deployment Guide**](Platform-Documentation#10-building-and-deploying-mosip). We would actively support the System Integrator during the first deployment process.

## Test Execution reports [**[↑]**](#table-of-content)
### Mindtree testing report

**Test Scope**

#### 1. In Scope [**[↑]**](#table-of-content)

The following have been the IN SCOPE entities for testing


|Title	|Description|
|------|------|
|Modules Tested|<li> Pre-registration (UI & Server) <li> Registration Client (UI) <li> Kernel (APIs) <li> Registration Processor (Server) <li> ID Authentication (APIs) <li> ID Repo (APIs)|
| Version Tag Tested|	0.12.15|
|Testing Methods| <li>  Manual <li>  Test Automation|
|Types of testing|<li>	 Smoke <li> Functional <li>  Integration <li> 	Regression|
|Testing Levels|![Image](_images/test_rig_automation/image1.jpg) |
|Configuration Parameters tested for| Refer to QA env properties file with suffix ‘qa’ in the filename, at [**Link**](/mosip/mosip-configuration/tree/master/config)|
|Browser Support|Pre-Registration Chrome – 74.0.3729.169|
|OS Support|Registration Client Windows 10|
|Language Support|French, Arabic, English|

#### 2. Out Of Scope – MOSIP V1.0 Platform [**[↑]**](#table-of-content)

|Title|	Description|
|------|------|
|NFR Testing| <li> Performance Testing <li> Security Testing|
|Global Configuration Testing|<li> Testing is done for one set of approved production configuration only <li> Changing the configuration parameters for various values (boundary values) and testing the impact of each such value on the platform code, is not tested for.|
|NFR Defect Fix Retesting|The outstanding NFR defects are not considered for fix or retesting in this release|
|Browser Support| <li>	IE <li>	Firefox <li> MAC|

#### 3. Executive Summary – Consolidated Quality Status [**[↑]**](#table-of-content)

|Sl. No.|	Module / Activity|	Jira Epic ID|	Testing Methodology|	Testing Complete For|
|------|------|------|------|------|
|1|	Kernel	|MOS-1|	Test Automation	|API|	
|2|	Pre-Registration|	MOS-2|<li> Manual Testing <li> Test Automation|<li> UI <li> API <li> Workflows|<li> Certified critical functional workflows <li> Open Defects <li> Major – <li> Minor - |
|3|	Registration Client|	MOS-14575| <li> Manual Testing <li> Test Automation| <li> UI <li> API <li> Workflows||
|4|Registration Processor|	MOS-4|<li> Manual Testing <li> Test Automation	|<li> API <li> Workflows| |
|5|	ID Authentication	|MOS-5|	Test Automation	|<li> API <li> Workflows|	|
|6|	ID Repo	|NA|	Test Automation	|<li> API|	|	
|7|Pre-Registration to Registration Client integration testing|	NA|	Manual Testing|	Workflows|	|	
|8|	Registration Client to Registration Processor integration testing|	NA|	Manual Testing|	Workflows||	
|9|	Registration Processor to Pre-Registration integration testing|	NA	|Manual Testing|Workflows|	|	
|10|	Registration Processor to Registration Client integration testing|	NA|	Manual Testing|	Workflows|	|
|11|	Registration Client to IDA integration testing|	NA|	Manual Testing|	Workflows|		|
|12|	Registration Processor to IDA integration testing|	NA|	Manual Testing|	Workflows	||
|13|	IDA to ID Repo|	NA|	Manual Testing|	Workflows	|	|
|14|Kernel API integration|	NA|	<li> Manual Testing <li> Test Automation|	
|15|	End to end testing|	NA|	Manual Testing|	Workflows	|	

#### 4. Types of testing [**[↑]**](#table-of-content)

|Testing Type| Description|
|------|------|
|Smoke Testing|Test to ensure basic and critical domain workflows work fine|
|Functional Testing|Test to ensure functionality of each module and system at large work fine in accordance with the given requirements|
|Integration Testing|Test to ensure the inter module functionality works fine and in accordance with the integration requirements|
|Regression Testing|Test to ensure no new functionality or change breaks old functionality and all existing features work fine|
	
#### 5. Manual Test Execution Metrics & Graphs [**[↑]**](#table-of-content)
to be done
#### 6. Automation Test Reports [**[↑]**](#table-of-content)
consolidated report run on 0.12.15 on QA env, from merged automation code base


## Support Process (To Be Determined) [**[↑]**](#table-of-content)
Process to be followed for support required, escalation matrix [**need link to update**]








