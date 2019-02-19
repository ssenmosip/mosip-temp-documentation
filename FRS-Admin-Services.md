## Table Of Content

  * [1. Master Data Management](#1-master-data-management)
    * [1.1 Location Hierarchy - Create/Read/Update/Delete](#11-location-hierarchy---createreadupdatedelete)
    * [1.2 List of Holidays - Create/Read/Update/Delete](#12-list-of-holidays---createreadupdatedelete)
    * [1.3 Biometric Authentication Type - Create/Read/Update/Delete](#13-biometric-authentication-type---createreadupdatedelete)
    * [1.4 Biometric Attribute Type - Create/Read/Update/Delete](#14-biometric-attribute-type---createreadupdatedelete)
    * [1.5 Gender - Create/Read/Update/Delete](#15-gender---createreadupdatedelete)
    * [1.6 Document Category - Create/Read/Update/Delete](#16-document-category---createreadupdatedelete)
    * [1.7 Document Type - Create/Read/Update/Delete](#17-document-type---createreadupdatedelete)
    * [1.8 Document Category - Document Type Mapping - Create/Read/Update/Delete](#18-document-category---document-type-mapping---createreadupdatedelete)
    * [1.9 List of Rejection Reasons - Create/Read/Update/Delete](#19-list-of-rejection-reasons---createreadupdatedelete)
    * [1.10 List of Languages - Create/Read/Update/Delete](#110-list-of-languages---createreadupdatedelete)
    * [1.11 List of Titles - Create/Read/Update/Delete](#111-list-of-titles---createreadupdatedelete)
    * [1.12 Template File Format - Create/Read/Update/Delete](#112-template-file-format---createreadupdatedelete)
    * [1.13 List of Template Types - Create/Read/Update/Delete](#113-list-of-template-types---createreadupdatedelete)
    * [1.14 List of Templates - Create/Read/Update/Delete](#114-list-of-templates---createreadupdatedelete)
    * [1.15 List of Blacklisted Words - Create/Read/Update/Delete](#115-list-of-blacklisted-words---createreadupdatedelete)
    * [1.16 List of Reason Categories - Create/Read/Update/Delete](#116-list-of-reason-categories---createreadupdatedelete)
    * [1.17 List of Applications - Create/Read/Update/Delete](#117-list-of-applications---createreadupdatedelete)
    * [1.18 List of ID Types - Create/Read/Update/Delete](#118-list-of-id-types---createreadupdatedelete)
  * [2. Registration Management](#2-registration-management)
    * [2.1 Registration Center Type - Create/Read/Update/Delete](#21-registration-center-type---createreadupdatedelete)
    * [2.2 Registration Center - Create/Read/Update/Delete](#22-registration-center---createreadupdatedelete)
    * [2.3 List of Machine Types - Create/Read/Update/Delete](#23-list-of-machine-types---createreadupdatedelete)
    * [2.4 List of Machine Specifications - Create/Read/Update/Delete](#24-list-of-machine-specifications---createreadupdatedelete)
    * [2.5 List of Machines - Create/Read/Update/Delete](#25-list-of-machines---createreadupdatedelete)
    * [2.6 Mappings of Registration Center, Machine and User Mappings - Create/Read/Update/Delete](#26-mappings-of-registration-center-machine-and-user-mappings---createreadupdatedelete)
    * [2.7 List of Devices - Create/Read/Update/Delete](#27-list-of-devices---createreadupdatedelete)
    * [2.8 List of Device Specifications - Create/Read/Update/Delete](#28-list-of-device-specifications---createreadupdatedelete)
    * [2.9 List of Device Types - Create/Read/Update/Delete](#29-list-of-device-types---createreadupdatedelete)
    * [2.10 Mappings of Registration Center and Machine - Create/Read/Update/Delete](#210-mappings-of-registration-center-and-machine---createreadupdatedelete)
    * [2.11 Mappings of Registration Center and Device - Create/Read/Update/Delete](#211-mappings-of-registration-center-and-device---createreadupdatedelete)
    * [2.12 Mappings of Registration Center, Machine and Device - Create/Read/Update/Delete](#212-mappings-of-registration-center-machine-and-device---createreadupdatedelete)
  * [3. Partner Management](#3-partner-management)
    * [3.1 License Key Manager](#31-license-key-manager)
# Admin Services
## 1. Master Data Management
### 1.1 Location Hierarchy - Create/Read/Update/Delete

### 1.2 List of Holidays - Create/Read/Update/Delete

### 1.3 Biometric Authentication Type - Create/Read/Update/Delete

### 1.4 Biometric Attribute Type - Create/Read/Update/Delete

### 1.5 Gender - Create/Read/Update/Delete

### 1.6 Document Category - Create/Read/Update/Delete

### 1.7 Document Type - Create/Read/Update/Delete

### 1.8 Document Category - Document Type Mapping - Create/Read/Update/Delete

### 1.9 List of Rejection Reasons - Create/Read/Update/Delete

### 1.10 List of Languages - Create/Read/Update/Delete

### 1.11 List of Titles - Create/Read/Update/Delete

### 1.12 Template File Format - Create/Read/Update/Delete

### 1.13 List of Template Types - Create/Read/Update/Delete

### 1.14 List of Templates - Create/Read/Update/Delete

### 1.15 List of Blacklisted Words - Create/Read/Update/Delete

### 1.16 List of Reason Categories - Create/Read/Update/Delete

### 1.17 List of Applications - Create/Read/Update/Delete

### 1.18 List of ID Types - Create/Read/Update/Delete

## 2. Registration Management
### 2.1 Registration Center Type - Create/Read/Update/Delete

### 2.2 Registration Center - Create/Read/Update/Delete

### 2.3 List of Machine Types - Create/Read/Update/Delete

MOSIP system can create Machine Type in Masterdata DB

Upon receiving a request to add Machine Type (e.g, Dongle) with the input parameters (code, name, descr, lang_code and is_active), the system store the Machine Type in the DB

Validates if all required input parameters have been received as listed below for each specific request

* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory

Respond with the Machine Type Code and Language Code for the Machine Type created successfully

This feature also restrict the bulk creation of Master Data

Respond to the source with the appropriate message

In case of Exceptions, system triggers error messages as received from the Database as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
|Error occurred while inserting Machine Type details	|KER-MSD-061|

### 2.4 List of Machine Specifications - Create/Read/Update/Delete

### 2.5 List of Machines - Create/Read/Update/Delete

### 2.6 Mappings of Registration Center, Machine and User Mappings - Create/Read/Update/Delete

### 2.7 List of Devices - Create/Read/Update/Delete	

### 2.8 List of Device Specifications - Create/Read/Update/Delete

### 2.9 List of Device Types - Create/Read/Update/Delete
### 2.10 Mappings of Registration Center and Machine - Create/Read/Update/Delete

### 2.11 Mappings of Registration Center and Device - Create/Read/Update/Delete

### 2.12 Mappings of Registration Center, Machine and Device - Create/Read/Update/Delete

## 3. Partner Management 
### 3.1 License Key Manager
MOSIP system can generate and validate a license Key
#### 1. Generate License Key
(a) Upon receiving a request to generate License Key with input parameters (TSP ID, Expiry Time)

(b) Fetch the length from the configurations

(c) Validate if the request contains the following input parameters

* TSP ID - Mandatory
* Expiry Time - Mandatory
* If the mandatory input parameters are missing, throw the appropriate message. Refer "Messages" section.
* License Key generated must be of length configured by ADMIN

(d) Generate the License key

(e) Map the License key to the TSP ID and Expiry time

(f) Respond to the source with the License Key (String)

(g) In case of Exceptions, system should trigger relevant error messages as specified below.

#### 2. Mapping Permissions to License Key
(a) Upon receiving a request to map permissions to the License Key with input parameters (TSP ID, License Key, List of Permissions) the system maps the received permissions to the License Key

(b) Validates if the request contains the following input parameters
* TSP ID - Mandatory
* License Key - Mandatory
* List of Permissions - Mandatory

(c) If the mandatory input parameters are missing, throw the appropriate message

(d) Respond to the source with appropriate message

(e) In case of Exceptions, system triggers relevant error messages

#### 3. Fetch Permissions for a License Key


(a) Upon receiving a request to fetch permissions for a License Key with input parameters (TSP ID, License Key) the system validate if the License Key is Valid

(b) Validates if the request contains the following input parameters
* TSP ID - mandatory
* License key - Mandatory

(c) If the mandatory input parameters are missing, throws the appropriate message.

(d) Validate the License key based on following logic

* License key received should be mapped to the TSP ID received in the request
* License key should not be expired as per the expiry time mapped to the License Key

(e) If the License key is invalid, throws error message

(f) In case of Exceptions, system triggers relevant error messages

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
When license key is mapped with the permissions|	Mapped License with the permissions|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
|-	|TSP entered is null or empty	|KER-LKM-001
|-	|The length of license key generated was not of the specified length.|	KER-LKM-002
|-	|Permission value entered is not accepted.	|KER-LKM-003
|-	|LicenseKey Not Found.	|KER-LKM-004
|-	|LicenseKey Expired.|	KER-LKM-005
|-	|License Key entered is null or empty.|	KER-LKM-006
|-	|Permission entered is an empty string.|	KER-LKM-007
|HttpMessageNotReadableException|	<Dynamic Message as received>	|KER-LKM-008
|RunTimeException	|<Dynamic Message as received>|	KER-LKM-009




