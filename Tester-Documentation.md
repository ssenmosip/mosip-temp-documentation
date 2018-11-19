**# **MOSIP - SOAPUI testing best practices****
# 1 Introduction
## 1.1 Context
MOSIP SOAPUI tests are developed as an open source framework project. The tests developed using soapui with the following best practices.

## 1.2 Purpose of this document
This document gives various RESTful soapui api data driven automation testing standards which have to be followed during the MOSIP testing.
## 1.3 Scope of this document
This document covers the automation testing standards, for the RESTful webservice testers.

# 2 Structuring Tests
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




																																																						Operations
										
## 2.6 Exceptional behavior checking	
This type of testing is performed to check if apis fail gracefully with proper error code and error messages. Need to simulate error scenarios and validate the 4xx and 5xx series of status codes.	
Sending incorrect or invalid parameters to the API triggers a negative outcome, which is commonly an error message or other indication of a problem

## 2.7 Database Validation
The data created/Updated/Deleted should be validated against DB entry with JDBC step using the tool.

# 3 Input Data Handling
## 3.1 Parsing/generating input data 
Input data should be handled as master json file and then it is parsed across the soapui project to refer input elements.
Groovy scripting is used to generate data dynamically (Ex: email address).

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




Point of Contact

Name of doc	Date	Version	Created by	Reviewed by
Soapui_testing_bestPractices	15/11/2018	1.0	Jyoti.kori@mindtree.com	Avinash.Chandrashekar@mindtree.com



