
***
**# **MOSIP - Test Strategy (Work in progress copy)****
# 1 Introduction
## 1.1 Context
The MOSIP architecture mainly consists of the following functional blocks/modules
* Pre-Registration - Web application that will be independently tested
* Registration Client - A thick desktop client application that will be connected to scanner devices (finger print, iris), camera and printer
* Registration Processor - A backend server application that processes the client packets and generates UIN based on de-dup information from ABIS (Automated Biometrics Identification System)
* IDA (ID Authentication) - A backend authentication server that authenticates the resident based on biometric and demographic information

Test automation is the key to the success of comprehensive test coverage and test data. However in the context of MOSIP testing, where there are external devices and integration with third party software, test automation cannot be exhaustive and comprehensive test coverage can be achieved by testing driven by manual intervention, along with test automation.

In this document we will also talk about utilities for test data generation, tools for test automation and test strategy in general.

<!---MOSIP SOAPUI tests are developed as an open source framework project. The tests developed using soapui with the following best practices.--->

## 1.2 Scope
1. Test Coverage
* a. Test Automation - tools, approach, test code configuration management process, regular usage
* b. Device integration
* c. End to end or System testing
2. Data Coverage
a. Data utility tools - approach, usage
3. Test Management Tools
4. Defect Management & Lifecycle

# 2 Test Approach
A progressively evolving test approach will be adopted i.e. a bottom up approach starting from individual API verification --> module level testing --> integration across modules --> End to end workflow testing

## 2.1 API Testing
API testing will be carried out in 2 stages, both via Test Automation.
1. Soap UI automation - This approach is mainly to catch up with the backlog and disclose bugs soon, however this approach has disadvantages when the APIs undergo changes
2. Restassured API test framework development and test automation - This will be a more generic framework, that is both modular and comes with less cost of maintenance

### 2.1.1 Restassured API Test Framework 
In this approach the request and response APIs will be templatized. The input request API template will be parameterised via a data utility, which also prepares the expected response JSON file. The request is then posted to get the actual response. The actual and expected response JSONs are compared to verify the result. 
Data utility also handles the transliteration of input values.

Api Automation will be done using Rest Assured IO DSL using Java. The tools/Libraries used are as below:

*     IO Rest Assured DSL
*     TestNG
*     Java/J2EE
*     Eclipse Editor

The framework consists majorly 3 Elements/parts as below:
	
      Test Case Configurator
      Test Data Util
      Test Execution and Assert
      Results

#### 2.1.1.1 Test Case Configurator

This is created on the fly while running the specific mofule’s api based on the combination of api specific attributes. Each api attribute is combined with valid and invalid data which forms specific test scenario. It is assumed that there is ONE valid scenario with all attributes of an api being valid and this forms smoke scenario. Error scenarios are formed by combination of invalid attributes of an api.
The configuration is formed with specific combination of api attributes and Data Util is called with this config file.

#### 2.1.1.2 Test Data Util

Test Data Util forms unique request and response jsons based on the config file received.

### Request:

Based on the valid/Invalid combination of api attributes, the templatized request.json is de-parameterized with randomized generation of input data and placed in folder named with test case name. 

### Response:

Based on the type of de-parameterized request, response is mapped with statically saved expected response.json files and saved under the same folder where request was been saved.

### Folder Structure:

Each test scenario/tes case/data combination is written to separate folder and named with test case name. Based on the api’s attribute combination from config file, the folders are populated.

#### 2.1.1.3 Test Execution and Assert

Execution:
IO Rest Assured methods (POST, GET, PUT, and DELETE) used to run the requests. These methods saved under Common Library so that same methods are re-used.

Assert:
All the foldeers under specific api is traversed through to run each request and compared the actual and expected response sent by Data Util.  Response files are converted to Json Object using Json Mappers and then Object to Object is compared.

#### 2.1.1.4 Results:

Result is captured in output.json file where each test case is mapped with unique JIRA ID. This info intern is used to write to Zephyr. After each automation run, Test Cycle will be created and can see detailed report in Zephyr.

## Contract to be followed with Test Data Util:

1.	Based on the templatized request, the api attributes have to be parameterized. If any of the attribute is not tokenized (data is already provided) then retain original value else de-parameterize using randomly generated input data(based on valid/invalid config parameters). This is to avoid parameterization of static data.

2.	Folder Naming Convention

If all attributes in the config file is valid then folder name to be followed as “testcase_smoke” (There will be only one valid scenario for each api)

If any of the attribute is invalid then folder name to be followed as “Invalid_+”name of the invalid attribute”. It is assumed, each time only one attribute will be invalid, if found more than one attribute as invalid then can suffix that name with prior one (Ex: “Invalid_+”name of the invalid attribute1 + name of the invalid attribute2”)

3.	As part of Integration scenario, have to generate request json consuming specific parameters from output of another api.

4.	Few of the input data has to be dynamically generated at the time of de-parameterizing  request.json files 
Examples: 

Datetimestamp lesser/greater than 20 min than current time (requirement from IDA, Kernel modules) 
Adding logic to encode/encrypt specific demographic/biometric data

5.	Handling Biometric Data

Util to generate packets is been shared by Reg client, by using this util input request is to be generated as part of Reg-Proc apis requirement.

## 2.2 Api Testing Strategy

Api Testign is broadly classified as Component and integration(Scenario) testing.

### Component Tests
Component tests are like unit tests for the API - It checks individual methods available in the API in isolation. We create these tests by making a test step for each method or resource that is available in the service contract. 

The easiest way to create component tests is to consume the service contract and let it create the clients. We will then data-drive each individual test case with positive and negative data to validate that the responses that come back have the following characteristics:

* 	 The request json payload is well-formed (schema validation)
* 	The response json payload is well-formed (schema validation)
* 	The response status is as expected (200 OK, SQL result set returned)
* 	The response error payloads contain the correct error messages and error codes
* 	Assertion - the individual elements in the response match our expectations (presence of specific element, datatype 
        of element etc).
* 	The service responds within an expected time frame 
* 	Validate how the system behaves when some request headers are missing, e.g., Content-Type, Authorization, etc.
*	Checking what happens if provide query parameters for a method that should accept only form parameters in a body
* 	verifying whether a protected resource is not available over HTTP when it should be only on HTTPS
* 	Business logic testing. Say while Fetching application (PreId) presence of valid Preregistration ID is mandatory      
       in the request.
* 	Positive and Negative testing. Making sure that if you make a bad request, it responds as expected.

These individual API tests are the most important tests that we build because they will be leveraged in all of the subsequent testing techniques.  These tests simplify the process of approaching API testing.

### Scenario Tests
Under this type of testing, we assemble the individual component tests into a sequence, much like the example described as below.
Ex: Create Application, Upload Document, Book appointment and Fetch Application data.
There are two great techniques for obtaining the sequence:
1.	Review the user story to identify the individual API calls that are being made.
2.	Exercise the UI and capture the traffic being made to the underlying APIs.

Scenario tests allow us to understand if defects might be introduced by combining different data points together.


## 2.3 Module level testing
MOSIP module level testing cannot be completely automated due to the use of scanner devices and others that involve manual intervention. Therefore the following approach will be adopted for creating a controlled end to end regression test suite that considers no devices, but simulators. This also includes the simulation of ABIS responses via a ABIS Simulator.

# Registration Client Approach

Please ensure the following prerequisites is available in the machine from where we are going to launch and test the application:
1. Updated derby DB 
2. Registration-UI jar
3. Java version (build 1.8.0_181-b13)

First in order to launch the application, we must configure our machine to the center and it can be achieved by inserting a query in Derby DB where user will insert / update the MAC address of the particular machine from where user launches the application.

# Login Functionality:
To create a packet, the user must have a valid user name and password and more importantly on-boarded to the machine. The User can create one using insert query in "User details" table in Derby DB.Once logged in to the application, the user will be routed to "Home screen" where the user has option to start a New Registration, UIN Update and Lost UIN. If the credentials are not valid or the user is not on-boarded then the application will display appropriate error message and restricts the user to proceed further

# Packet Creation:

## a. Pre-Registration Sync:
The resident's are allowed to provide their Demographic and basic proof documents via online. Upon completion of those information, they will be provided with a PRID. Post that the resident are supposed to make an appointment to the registration center and complete the registration. Once the PRID is generated, the pre-registration team will provide a service through which they will put all PRID available for the registration client and in turn RC team will get those in to their DB by Pre-Registration sync.

## b. Demo Data Capture:
Using New Registration tab on home screen, the user can either enter the resident's detail manually or the user can fetch the details using PRID(Pre-registration ID). When user fetches the details using PRID, the RC will check whether the information is available in DB and if not it will check online and based on availability it will display the details. If in case, the details are available in both places, then it will fetch it from online considering the online is the recent and updated one. All mandatory fields needs to be captured and the configured secondary language will display the same on the right hand side of the application. If user wants to transliterate the information, then using virtual keyboard the user can enter the data.

## c. Document Upload
Once demographic information are captured, the user has to upload the necessary documents through document upload screen and the document category will come from Master data. The user will not be allowed to upload more than one document type for a single category. The RC should not have an option to store or export it to external devices but must have access to view and delete it.

## d. Biometric capture:
Since due to non-availability of external devices, biometric details are stubbed while creating a packet. Biometric details like Fingerprint (4+4+2), IRIS (1+1) and Face photo. Except applicant photo, all other details are stubbed.Also the biometric details are placed as CBEFF file format in the packets.

## e. Preview
After user has captured all the information, the application will display the preview screen where the user and resident will re-verify for correctness of information. If something needs to be changed, using Edit option the user will change the value and complete the registration capture process

## f. Registration Authentication
The final step to create a packet is by authenticating it with RO credentials. The packets which have biometric exception information will need supervisor credentials for authenticating it. Upon successful authentication, the packet will get created and stored in the default configured path. 

# EOD Process:
In EOD process, the user can either approve a packet or reject with reasons. The list of reason to reject will come from master data and this can be achieved by sync job. Only supervisor will have access to EOD process. Once supervisor logged in and start to approve the packet. Before approving, all pending approval packets are available in "Pending approval" queue. Select a packet / group of packets and user can approve / reject based on necessity. 

# Upload Packets:
Click the upload button and all the internal approved packets will get uploaded and moved to the server. The UI will display the uploaded status whether it is uploaded successfully or not. 

# Packet Validation:
## a.	Basic Checks:
1. Packet store folder and packet availability
2. Acknowledgement
3. Packet is encrypted or not

## b.	Advanced checks: 
1. Decrypt the packet using the utility and verify the packet structure like availability of Demo, Bio, HMAC, Documents uploaded, Exception info, Supervisor and RO info 


**<GITA - context setting and high level approach continues here>**

Reg Client Automation Approach

Registration Client is thick Desktop application built using JavaFX accessible in Windows and Linux machines. The Enrollment Client expects inputs from user in the form of Demographic and Biometric and generates Registration ID by exposing several Java and Restful apis. 

Tools/Technology Used: TestFX, Java, Maven, Junit 5, Eclipse, derby db

Page Object Model
The framework customized is Page Object Model (POM), each screen/Object view is treated as an individual page. Input Data, Page locators and test logic are segregated from each other. They are loosely connected to accommodate the future changes with lesser maintenance effort.
The below diagram depicts the high level view.
[[https://github.com/mosip/mosip/blob/fd53c0f8343d3d23fb01630b7655a28421e57a39/testing/automation/RegClientAutoFrmwrk.JPG]]

* Core framework – which holds common code for functions, Input Data, the controller script and generic services like logging, exception handling
* Page Object – These are the pages, which hold info about the pages/object view relative to their locators, values and respective page assertions

Following is the description of each package/module under the framework
1. Input Data Handling
DataUtil is the provider of Demographic and Biometric input provider. It generates multiple samples of simulated Biometric data for fingerprints, Iris and photo. The util in turn uses sample simulators to generate unique set of data dynamically at runtime.

2. Base Package
It holds the entire configuration to initialize and trigger the Runner class to start the execution. It instantiates stage robot elements of TestFX.

3. Page Handling
Each screen of JavaFX represents a Page and it is implemented using Enum classes of Java. Constants under the enum class (separate enum for each screen/page) holds locator, values and behavior/method to interact with the screen. It also encapsulates the assertion messages specifically for any behavior.
Ex: Login Page, Registration Page etc

4. Test Scripts
Test Scripts are implemented using TestFX and Java code. TestFX provides Robot api with rich collection of keyword mouse movement/interaction libraries. It also provides Hamcrest matchers to assert tests.
Every script starts calling Datautil for input data based on the scenario. Relevant page/enum values are used to customize the behavior. Test is asserted for its result referring static data mainted under pages.

5. Exception Handling
Every behavior is associated with success and parallel failure scenario. All the failures are caught with systematic error handling using try/catch block and user will be prompted with meaningful messages on the action to be taken further. 
Exceptions might also arrive at the integration (say SDK devices while capturing images), they are also handled based on the scope (Device or Enrollment Client). Device connectivity is checked at the code.

6. Reporting and Screenshot
All execution are captured in a report along with attached screenshot of failed test cases in case of failure. Report listener is added at test script level to get detailed logging and report on execution status. 

**Test Scripts Types:**
**Health Checks**
Need to come up with Health check tests for:
1.	All Interfaces (Integration Points)
2.	All Connectivity points

**Exception Handling**
Tests should be robust enough to handle error scenarios like
1.	Exception while capturing images
2.	Exception while processing data

**Functional Validation**
Tests to validate the functionality of each screen either with Successful or Error scenario coverage

**Sample directory structure from the current framework**

[[https://github.com/mosip/mosip/blob/add180c7590ac0d97ae941008a22fc01e0a01de3/testing/automation/RegClientAutoFrmwrk-DirStr.JPG]]

# Data Coverage
The approach includes creating data generation utilities for specific purposes in testing 
There are 5 data generation utilities with the following purposes 
1. for testing Pre-Reg and Reg Client UIs
2. for testing Pre-Reg APIs
3. for testing Kernal APIs
4. for testing Reg-Proc APIs
5. for testing IDA APIs

The utilities are flexible and easy to use
* Manual test team uses the utility for testing UI and Rest API testing
Manual Testing team can run the test data util jar in local machine and generate test data any time.

* Automation test team uses them for test automation of API and E2E scenario 
The test data util is integrated with the automation code to generate data at run time and carry out the automation tests.

Design: 
The utility is designed to take input data from a configuration file generates varied combinations of data dynamically and it is different for each run of the utility there by generating random but specific combinations that can be used.

Test Data Util uses 2 files as input:
Config property file - where user can configure below things:
 - number of test data output jsons need to be generated
 - fields for which the test data is required
 - output json file name to be generated
 - valid/invalid data to be generated for each field

Master yml file - is basically a dictionary that contains all valid and invalid data for each field as separate tags.
Test data util when run picks the random data from respective tags in master yml file based on the configuration provided by the user in config property file.

<!---This document covers the automation testing standards, for the RESTful webservice testers.--->

# 2 Structuring Tests for API testing
## 2.1 Naming Convention

Project Name as Mosip
Every module as Test Suite
Test Suites are as below:
    Pre-Registration 
    Reg-Proc
    IDA
    Kernel

Note: As Registration module doe not have any Restful apis, not considered for automation.

**Test Case**

Naming convention followed as:

ModuleName SprintCycle_Type of Test_Fetaure_JIRA ID_Description

**ModuleName:**

   Pre-Registration - 1
   Reg-Proc -2
   IDA -3
   Kernel -4

Sprint Cycle: 1 , 2 ,3 etc

Type of Test as below
   1 – Sanity
   2 – Progression
   3- Regression
   4- Progression and Regression both

JIRA ID – Relevant story under test

Description: Test Scenario explanation

Ex: 14_3_OTP_MOS-27_Verify OTP triggered successfully

The above test case is interpreted as this test case belongs to Pre-Registration module of  4th sprint, regression test case, testing OTP feature addressed using JIRA no as MOS-27 for test scenario “verify otp is triggered successfully”.

## 2.2 Header
Every test is to be preceded with Header script addressing below elements

Name: Name of the tests
Module: Module going to test
Author: Individual who is writing tests
Date: Date of development of tests

## 2.3 Functional testing of individual methods or operations

This testing ensures whether a method or operation performs the task correctly, which it is intended to do actually.
Example: Say if a POST method/operation ‘register’ used to create a user then a new user creation is completed with an entry into database.

## 2.4 Syntax checking of individual methods/operations
This type of testing is done to validate if it accepts only valid inputs and all invalid inputs are rejected with proper error code/messages.

## 2.5 Construct test scenarios
By clubbing, multiple methods/operations create End-to-End regression scenarios.

Example: Simulate Input Data -> Trigger OTP -> Generate OTP -> Get OTP -> Authenticate OTP
										
## 2.6 Exceptional behavior checking
	
This type of testing is performed to check if apis fail gracefully with proper error code and error messages. Need to simulate error scenarios and validate the 4xx and 5xx series of status codes.	

Sending incorrect or invalid parameters to the API triggers a negative outcome, which is commonly an error message or other indication of a problem

## 2.7 Database Validation
The data created/Updated/Deleted should be validated against DB entry with JDBC step using the tool.

# 3 Input Data Handling

## 3.1 Parsing/generating input data 

Input data should be handled as master json file and then it is parsed across the soapui project to refer input elements.
Groovy scripting is used to generate data dynamically (Ex: email address).

All input json files are saved in git and accessed accordingly.

## 3.2 Use realistic data 

Make it a priority to understand the rationale behind the API, along with the information being sent to it, both in design and in practice.

## 3.3 Mock Services

As part of End-to-End testing if feature is not available (out of scope for feature under test and not yet implemented), create Mock services using SOAP UI tool. Also, can create stubs using Groovy scripting.

## 3.4 Capturing Logs

As part of proof of validation, save logs of execution; which can then be transferred to git repository as a reference point.

# 4 Assertions

## 4.1 Add as many as assertions
	
Cultivate habit of adding assertions as many as possible which would uniquely validates whether a test is pass or fail. Use tool assertions, which would be quicker and reuse script assertions wherever required.

## 4.2 Dynamic assertions

Tightly couple assertions with dynamic data, which is generated as part of test execution. This will ensure the expected result exactly matches the requirement along with changing data.

Example: txn_id in the response should match with txn_id in request, which is dynamically generated each time test is run. Add Json path assertion to check txn_id in response is same as txn_id in the request.

# 5 Scope of apis

Get the clarity of feature under scope of testing. Testing the features which are not under current scope and 3rd party operations should be avoided.  3rd party apis are tested only to check if it is prompting expected element/status. This strategy helps us to arrive with quality tests. 

# 6 Test Strategy
## 6.1 Registration Processor
Registration Processor is the core part of MOSIP where the Identity and Validation of resident’s enrolled data happens, and on a successful verification UIN will be generated and delivered to the residents. Functional verification and security aspects plays a critical role in evaluation of Registration Processor. Unlike the regular black box testing, this will be more of a Grey box testing that involves verification of the stages for the Registration Processor Module of the MOSIP Software.
## 6.2 Module Level Testing
This testing ensures Registration Processor Module level operation performed correctly (intended) without any issues. Example: Registration Processor starts with uploading packets leading to virus scan, then to Packet store and finally creating the UIN. 
## 6.3 Reg Processor Workflow 
Following are the high level positive and negative scenarios covering the below shown workflow diagram of the reg proc module

Number | Test Scenarios | Category| 
-----  | -----------------|-------------|
1 | Verify Packet is Unique/Duplicate | 	Functionality | 
2 | Verify Packet sync for which packet generated from Registration client | 	Functionality |
3 | Verify whether Virus scan is success/Failure for RID Packet | 	Functionality |
4 | Verify Packet Archival location | 	Functionality |
5 | Verify Packet Decryption with the valid key store | 	Functionality |
6 | Verify Packet Decryption with the invalid key store | 	Functionality |
7 | Verify Packet Integrity with valid check sum value | 	Functionality |
8 | Verify Packet Integrity with invalid check sum value | 	Functionality |
9 | Verify structural validation with valid packet structure | 	Functionality |
10 | Verify structural validation with invalid packet structure | 	Functionality |
11 | Verify  Demographic Dedupe for valid Packet | 	Functionality |
12 | Verify  Demographic Dedupe for Packet having exception in Demographic info | 	Functionality |
13 | Verify   Biometric Dedupe for valid Packet | 	Functionality |
14 | Verify  Biometric Dedupe for Packet having exception in biometric info | 	Functionality |
15 | Verify Manual adjudication when demo dedup is Failure | 	Functionality |
16 | Verify Email Notification | 	Functionality |
17 | Verify UIN generation  | 	Functionality |
18 | Verify Invalid Packet naming convention  | 	Functionality |
19 | Verify Packet name exceeding less than 29 digits  | 	Functionality |
20 | Verify Packet name exceeding more than 29 digits | 	Functionality |
21 | Verify Invalid Fotrmat  | 	Functionality |
22 | Verify SMS Notification  | 	Functionality |
23 | Verify RegistrationProcessorIdentity json file   | 	Configuration |
24 | Verify Camel route XML  | 	Configuration |
25 | Verify bio-dedupe-service max result  | 	Configuration |
26 | Verify packet-receiver max file size in mb | 	Configuration |
26 | Verify bio-dedupe-service threshold  | 	Configuration |
27 | verify packet-manager virus scan location when empty  | 	Configuration |
28 | verify packet-manager packet extension when empty | 	Configuration |
29 | verify packet-manager encrypted packet location empty  | 	Configuration |

[[https://github.com/mosip/mosip-test/blob/master/Registration-Processor-Workflow1.JPG]]

## 6.4 Pre-requisite for Reg Proc testing
1.	Create resident test packet from reg client
2.	Ensure Reg Proc and all its associated job are up and running

 | Jobs | 
 | -----------------| 
 | packet-receiver-stage-1.0.0-SNAPSHOT.jar |
 | virus-scanner-stage-1.0.0-SNAPSHOT.jar |
 | packet-uploader-stage-1.0.0-SNAPSHOT.jar |
 | osi-validator-stage-1.0.0-SNAPSHOT.jar |
 | demo-dedupe-stage-1.0.0-SNAPSHOT.jar |
 | packet-bio-dedupe-api-1.0.0-SNAPSHOT.jar |
 | registration-processor-abis-1.0.0-SNAPSHOT.jar |
 | bio-dedupe-stage-1.0.0-SNAPSHOT.jar|
 | ui-generator-stage-1.0.0-SNAPSHOT.jar |
 | manual-verification-stage-1.0.0-SNAPSHOT.jar |
 | packet-validator-stage-1.0.0-SNAPSHOT.jar |


3.	Ensure DB is up and running fine. 
4.	Ensure the required DB scripts (Master Data / Schema) are executed.
5.	Required Privileges to DB for Testdata updates to create positive / negative flow.
6.	Ensure all the depended services are deployed.

## 6.5 Test Step
Registration packets created by the registration clients will be periodically uploaded to the server for processing. The packets will be stored in Virus scan initially and status will be updated in registration status table. Check the Enrollment status table for the packets for which are present in Virus Scan Folder. Scan the Virus Scan Folder for the list of Packets and Perform Virus Scan on the Packets using services from Core Kernel. In case of successful Virus Scan, moves packets to DFS.In case of Virus Scan failure, moves packets to Retry Folder. Updates the status of these packets in the Enrollment Status Table.
Packets that successfully uploaded to file system and ready for decryption. Decrypt the encrypted zip file and receives a Zip file. Unpack the Zip file. Store the unpacked files in file system. Using  RSA PKI Algorithm we create Public keys/private Keys through which will do packet decryption. After Packet decryption, Packet will go and check Packet integrity HMAC Algorithm used to validate the (Check sum value) and structure.
After successful packet structure validation, the packet Meta info is stored in DB. The user, machine and center information will be further validated at Master Data in DB to check if authorized person creates the packet.
After successful Bio dedupe, the UIN Generator will be called to allocate an unique identification number to the applicant by using 'kernel-idgenerator-uin' Rest API to generate UIN. It will return the unique id which will be allotted to the applicant.it will call kernel-idrepo-service create API to add a new applicant to id repository. After successful response from the idrepo-service, store the uin information in registration processor db. Update individual_demo_dedupe table with uin information against the registration id.

### 6.5.1 OSI Validation
Testing an OSI validation we populate the MASTER DB with User,machine,center details in a combination set with valid / Invalid Details. We create packets using Utils by passing valid/Invalid details of User/Machine/Center Details .The validation of OSI stage DB record for each condition will be verified.
### 6.5.2 Demo Dedupe:
Demo dedupe records matching GENDER,NAME and DOB  .Perform demo dedupe on all potential 'demo dedupe records' with 'applicant demographic information' using levenshtein distance algorithm. However for Testing we modify the DB with UIN with pre populated data . We use the same of set data while creating the packet to validate the condition.
### 6.5.3 Configuration:
Camel route xml is implemented in the private network where the stages are running on loosely coupled.By Modifying the route in-out of the vertx end point we validate the stages behaviors . 
### 6.5.4 Bio-Dedupe:
We create packet with dummy tag as unique / duplicate in CBEF which passed on Mock ABIS service to validate the Bio-Dedupe. Based on the tag ABIS decide the uniqueness of the packet .  


## 6.6 Test Data
Registration processor takes input as packet , the validation of stages involves data carried inside the packet. To validate positive and negative conditions we need to create the different combination of packet as mentioned below.

 | Packet with different Conditions | 
 | -----------------| 
| Registration Packet size < 5 MB  |
| Registration Packet size >5 MB (Max size Config) |
| Half info Packet / Missing info |
| Existing RID in DB |
| packet name with Valid Centre ID |
| packet name with valid Machine ID |
| packet name with valid Centre ID and valid Machine ID |
| packet name with  Invalid Centre ID |
| packet name with Invalid Machine ID |
| packet name with Ivalid Centre ID and invalid Machine ID |
| packet name with invalid Centre ID and invalid Machine ID |
| packet name with invalid Centre ID and valid Machine ID |
| packet name with Invalid Packet naming convention - Date |
| packet name with Invalid Packet naming convention - Month |
| packet name with Invalid Packet naming convention - Year |
| packet name with Invalid Packet naming convention - Time (H) |
| packet name with Invalid Packet naming convention - Time (M) |
| Invalid Packet naming convention - Time (S) |
| Valid Packet naming convention - Date |
| Valid Packet naming convention - Month |
| Valid Packet naming convention - Year |
| Valid Packet naming convention - Time (H) |
| Valid Packet naming convention - Time (M) |
| Valid Packet naming convention - Time (S) |
| Packet name combination - Text + Symbol |
| Packet name combination - Text + Number |
| Packet name combination - Symbol + Number |
| Packet name combination - Invalid Date + Invalid Month |
| Packet name combination - Invalid Date + Invalid Year |
| Packet name combination - Invalid Date + Invalid Time (H) |
| Packet name combination - Invalid Date + Invalid Time (M) |
| Packet name combination - Invalid Date + Invalid Time (S) |
| Packet name combination - Invalid Year + Invalid Month |
| Packet name combination - Invalid Time (H)+ Invalid Month |
| Packet name combination - Invalid Time (M)+ Invalid Month |
| Packet name combination - Invalid Time (S)+ Invalid Month |
| Packet name combination - Invalid Year + Invalid Time (H) |
| Packet name combination - Invalid Year + Invalid Time (M) |
| Packet name combination - Invalid Year + Invalid Time (S) |
| Packet name exceeding less than 28 digits |
| Packet name exceeding more than 28 digits |
| Virus scan success |
| Corrupted file - Virus scan failure |
| Invalid Applicant - BothThumbs |
| Invalid Applicant - Left Finger |
| Invalid Applicant - Right Finger |
| Invalid Applicant - Both Left and Right Eye |
| Invalid Applicant - Left Eye |
| Invalid Applicant - Right Eye |
| Valid Applicant - BothThumbs |
| Valid Applicant - Left Finger |
| Valid Applicant - Right Finger |
| Valid Applicant - Both Left and Right Eye |
| Valid Applicant - Left Eye |
| Valid Applicant - Right Eye |
| Invalid Introducer - BothThumbs |
| Invalid Introducer - Left Finger |
| Invalid Introducer - Right Finger |
| Invalid Introducer - Both Left and Right Eye |
| Invalid Introducer - Left Eye |
| Invalid Introducer - Right Eye |
| Valid Introducer - BothThumbs |
| Valid Introducer - Left Finger |
| Valid Introducer - Right Finger |
| Valid Introducer - Both Left and Right Eye |
| Valid Introducer - Left Eye |
| Valid Introducer - Right Eye |
| Demographic  - Invalid ApplicantPhoto |
| Demographic  - Invalid ExceptionPhoto |
| Demographic  - Invalid ProofOfAddress |
| Demographic  - Invalid ProofOfIdentity |
| Demographic  - Invalid RegistrationAcknowledgement |
| Demographic  - Valid ApplicantPhoto |
| Demographic  - Valid ExceptionPhoto |
| Demographic  - Valid ProofOfAddress |
| Demographic  - Valid ProofOfIdentity |
| Demographic  - Valid RegistrationAcknowledgement |
| Valid DemographicInfo JSON file |
| Invalid DemographicInfo JSON file |
| Valid audit JSON file |
| Invalid audit JSON file |
| Valid PacketMetaInfo JSON file |
| Invalid PacketMetaInfo  JSON file |
| Valid EnrollmentOfficerBioImage  |
| Invalid EnrollmentOfficerBioImage  |
| Valid EnrollmentSupervisorBioImage |
| Invalid EnrollmentSupervisorBioImage |
| Valid HMACFile |
| Invalid HMACFile |
| Invalid EnrollmentOfficerBioImage and EnrollmentSupervisorBioImage  |
| Invalid EnrollmentOfficerBioImage and HMACFile  |
| Invalid EnrollmentOfficerBioImage and PacketMetaInfo JSON file |
| Invalid EnrollmentOfficerBioImage and DemographicInfo JSON file |
| Invalid EnrollmentSupervisorBioImage and HMACFile  |
| Invalid EnrollmentSupervisorBioImage and PacketMetaInfo JSON file |
| Invalid EnrollmentSupervisorBioImage and audit JSON file |
| Invalid EnrollmentSupervisorBioImage and DemographicInfo JSON file |
| Invalid HMACFile and PacketMetaInfo JSON file |
| Invalid HMACFile and audit JSON file |
| Invalid HMACFile and DemographicInfo JSON file |
| Invalid PacketMetaInfo JSON file and audit JSON file |
| Invalid PacketMetaInfo JSON file and DemographicInfo JSON file |
| Invalid audit JSON file and EnrollmentOfficerBioImage  |
| Invalid audit JSON file and DemographicInfo JSON file |
| Unique Packet |
| Duplicate Packet |
| Duplicate request - Packet is up for retry- success |
| Duplicate request - Packet is up for retry- Failure |
| Packet integrity validation - successful |
| Packet integrity validation - Failure |
| Virus scan - successful |
| Virus scan - Failure |
| Decrypt packets - successful |
| Decrypt packets - Failure |
| Unpack packets - Success |
| Unpack packets - Failure |
| Metadata validation - success |
| Metadata validation - failure |
| File validation - Successful |
| File validation - failure |
| Insert packet data in DB - successful |
| Insert packet data in DB - successful |
| Data validation - success |
| Data validation - failure |
| Active officer Authentication Success Using finger |
| Active officer Authentication Failure Using finger |
| Active officer Authentication Success Using Iris |
| Active officer Authentication Failure Using Iris |
| Active officer Authentication Success Using pin |
| Active officer Authentication Failure Using pin |
| Active officer Authentication Success Using Password |
| Active officer Authentication Failure Using Password |
| supervisor Authentication Success Using finger |
| supervisor Authentication Failure Using finger |
| supervisor Authentication Success Using Iris |
| supervisor Authentication Failure Using Iris |
| supervisor Authentication Success Using pin |
| supervisor Authentication Failure Using pin |
| supervisor Authentication Success Using Password |
| supervisor Authentication Failure Using Password |
| Packet on hold by supervisor -> Yes |
| Packet on hold by supervisor -> No |
| On hold for manual Adjudication- Yes |
| On hold for manual Adjudication- No |
| Notify the Resident that Registration is under processing - Yes |
| Notify the Resident that Registration is under processing - No |
| Create a packet with unknown Operator ID  |
| Create a packet with unknown supervisor ID not available |
| Create a packet with unknown Machine |
| Create a packet with unknown Center ID |
| Create a packet for which operator-center-machine-mapping-not available |
| Create a packet for which supervisor-center-machine-mapping-not available |
| Create a packet with Geo data not Available |
| Create a packet with Office supervisor is missing  |
| Create a packet  with unknown Geo data in master DB |

## 6.7 Output verification
1.	Packet Handler request and response for JSON format/ structure/contents validation and verification according to the API specs.
2.	Status and error code verification according to the API spec.
3.	Biometric accuracy for Biometric dedupe
4.	Audit log verification
5.	DB status check for the packet processing across various stages in Registration Processor.
6.	Application log - ensure no errors logged .

## 6.8 Test Execution Process:
QA Analyst is responsible for the sanity testing.  QA Analyst will be executing the sanity testing of the Registration Processor as specified below.  Test cases will be executed & Defects are logged in JIRA.  
### 6.8.1 Entrance Criteria:
1. Unit testing and Integration Testing are completed.
2. Sanity test cases are identified.
3. QA environment is available.
### 6.8.2 Exit Criteria:
1. All Sanity test cases are executed and results documented.
2. Defects are documented and severity is designated. 

## 6.9 Test Setup
Below is the Block diagram / network diagram depicting all the connections and hardware devices.
[[https://github.com/mosip/mosip-test/blob/master/rptopo.png]]

## 6.10 Hardware – Server configuration

Item | Setup | 
-----  | -----------------|
Microsoft Azure | Azure Virtual Machine Application server | 
Microsoft Azure | Azure DB Instance | 	

## 6.11 Hardware – Registration Client Machine
Item | Configuration | 
-----  | -----------------|
Intel | Core i5 | 

## 6.12 Software – Server 
Item | Configuration | 
-----  | -----------------|
Microsoft Azure| apache-maven-3.5.4 maven | 
Microsoft Azure | jdk1.8.0_181-amd64 | 	

## 6.13 Software – Client 
Item | Configuration | 
-----  | -----------------|
Microsoft| Windows 10 | 

## 6.14 Test Tools (software)
This section should contain a table that documents the testing tools that will be needed to plan, script, and perform functional testing. Tools are required for test scripting, test defect tracking, test results logging, performance testing, automated testing and test management. 

Item | Area | 
-----  | -----------------|
Jira | Defect Tracking | 
PostgreSQL | DB | 	
Swager UI | API Manual Testing | 

## 6.15 Integration Testing 
The purpose of System Integration testing is to test a set of logically related components in a business like scenario. Integrating the Registration Processor with other modules in MOSIP for example Kernel for Cryptography , Registration packet from Registration client etc. To ensure Registration Processor able to work as intended.

## 6.16 End to End Testing 
The process of this to Test the MOSIP as a system like by considering the real deployment, we create test scenarios  which starts by Pre-registration demo data will consumed by Registration client and then create a packet to upload in registration processor. Registration Processor will do Virus Scan,Integrity check,structural validation,OSI Validation,Demo Dedupe and finally do bio Dedupe post successful of the before stages the UIN will be created . Our Test Scenarios will be cover with positive and negative on the end to end flow .			





Doc_Version: 1.0

Point of Contact/Author: jyoti.kori@mindtree.com, gita.phutane@mindtree.com

Reviewed by:     	Avinash.Chandrashekar@mindtree.com, gita.phutane@mindtree.com


***
