**# **MOSIP - Test Strategy (Work in progress copy)****
# 1 Introduction
## 1.1 Context
Test automation is the key to the success of comprehensive test coverage and test data. Here we will talk about utilities for test data generation, tools for test automation and test strategy in general.

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

# 6. Registration Client Approach

Framework followed is POM(Page Object Model)

Maintaining Locators

Each screen/object is maintained as Page; all the locators of a respective screen is saved under this Page. Any changes are to be updated/maintained at only one place at Page level.

Locators: Each object/element is to be located using unique ID locators. If cannot find any unique ID locators, request Dev team to provide the same instead of going ahead and implementing from qa side at target folder level.

Code for test cases/scripts:
Maintain test cases at Object/Page level. Test scripts to be built using re-usable library functions built as part of testing framework development.

## Input Test Data:

Test Data is kept outside the framework logic. All test inputs are provided wither by Data Util or Dev’s code on input file creation. We should get Demographic data as input jsons and using mappers to de-parameterize the fields under test.
To work with Data Util team on the agreed upon contract to be followed in naming/path to populate the inputs/how to call the utils etc for both Demographic and Biometric data.

## Folder Structure: 

We should follow unique folder structure for the packets, which are used for inputs and outputs as well; these packets will be in turn used as inputs by Reg-Proc client and hence can reuse them.

Health Checks
Need to come up with Health check tests for:
1.	All Interfaces (Integration Points)
2.	All Connectivity points

Exception Handling
Tests should be robust enough to handle error scenarios like
1.	Exception while capturing images
2.	Exception while processing data


# 7. RESTful API Automation – Rest Assured Approach

Api Automation will be done using Rest Assured IO DSL using Java. The tools/Libraries used are as below:

    IO Rest Assured DSL
    TestNG
    Java/J2EE
    Eclipse Editor

The framework consists majorly 3 Elements/parts as below:
	
      Test Case Configurator
      Test Data Util
      Test Execution and Assert
      Results

## Test Case Configurator

This is created on the fly while running the specific mofule’s api based on the combination of api specific attributes. Each api attribute is combined with valid and invalid data which forms specific test scenario. It is assumed that there is ONE valid scenario with all attributes of an api being valid and this forms smoke scenario. Error scenarios are formed by combination of invalid attributes of an api.
The configuration is formed with specific combination of api attributes and Data Util is called with this config file.

## Test Data Util

Test Data Util forms unique request and response jsons based on the config file received.

### Request:

Based on the valid/Invalid combination of api attributes, the templatized request.json is de-parameterized with randomized generation of input data and placed in folder named with test case name. 

### Resposne:

Based on the type of de-parameterized request, response is mapped with statically saved expected response.json files and saved under the same folder where request was been saved.

### Folder Structure:

Each test scenario/tes case/data combination is written to separate folder and named with test case name. Based on the api’s attribute combination from config file, the folders are populated.

### Test Execution and Assert

Execution:
IO Rest Assured methods (POST, GET, PUT, and DELETE) used to run the requests. These methods saved under Common Library so that same methods are re-used.

Assert:
All the foldeers under specific api is traversed through to run each request and compared the actual and expected response sent by Data Util.  Response files are converted to Json Object using Json Mappers and then Object to Object is compared.

### Results:

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



Doc_Version: 1.0

Point of Contact/Author: jyoti.kori@mindtree.com

Reviewed by:     	Avinash.Chandrashekar@mindtree.com

