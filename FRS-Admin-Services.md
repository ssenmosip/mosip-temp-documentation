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
**A. Create a Rejection Reason in Reason List Master Data**

Upon receiving a request to add a Reason with the input parameters (code, name, descr, rsncat_code, lang_code and is_active) the system store the Reason in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* code - character (64) - Mandatory
* descr - character (256) - Mandatory
* rsncat_code - character (36) – Mandatory (The parameter rsncat_code refers to a Language stored in Language Masterdata)
* lang_code - character (3) – Mandatory (The parameter lang_code refers to a Language stored in Language Masterdata)
* is_active - boolean - Mandatory
2. Validate if the response contains the following attributes for a Reason Category Code added
* Code
* Language Code
* Rsncat_code (Reason Category Code)

Respond to the source with the appropriate message.

In case of Exceptions, system triggers relevant error messages as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Reason details|	KER-MSD-058|

**B. Fetch the requested list of reasons based on Reason Category Code and Language Code**
1. Upon receiving a request to Fetch the requested List of Reasons with the required input parameters (Reason 1. Category Code, Language Code) the system fetches the requested List of reasons stored against the Reason Category Code and Language Code received
1. Validates if the request contains the following input parameters
* Language Code - Mandatory
* Reason Category Code - Mandatory
3. If either of the mandatory input parameters are missing, responds with the appropriate message as define below in message sections
1. Validates if the response contains the:
(a) Requested list based on the requested Language Code and Reason Category Code
(b) List of Reasons with the corresponding attributes for the list
* Reason ID
* Reason Name (per Reason ID)
* Language Code
* Reason Category Code
* IsActive
5. Responds to the source with the relevant List of Reasons, as per the stated business rules
1. In case of Exceptions, system should trigger relevant error messages as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while fetching Reasons	|KER-MSD-035|
Reason not found	|KER-MSD-036|



### 1.10 List of Languages - Create/Read/Update/Delete

### 1.11 List of Titles - Create/Read/Update/Delete

### 1.12 Template File Format - Create/Read/Update/Delete

### 1.13 List of Template Types - Create/Read/Update/Delete
MOSIP system can create Template Type in the Masterdata DB.

Upon receiving a request to add Template Type (e.g, SMS Notification template - New Registration) with the input 
parameters (code, descr, lang_code and is_active) the system stores the Template Type in the DB

Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean – Mandatory

Respond with the Template Type Code and Language Code for the Template Type created successfully

This component also restrict the bulk creation of Master Data

In case of Exceptions, system triggers relevant error messages as listed below.
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Template Type details	|KER-MSD-072|

### 1.14 List of Templates - Create/Read/Update/Delete

### 1.15 List of Blacklisted Words - Create/Read/Update/Delete
**A. Create Blacklisted Words in Masterdata DB**

Upon receiving a request to add a Blacklisted Word with the input parameters (code, name, descr, lang_code and is_active) the system store the Blacklisted Word in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* word - character (128) - Mandatory
* descr - character (256) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Device ID and Language Code for the Device created successfully
1. The component  restricts the bulk creation of Master Data
1. In case of Exceptions, system will trigger error messages as received from the Database as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Device details	|KER-MSD-070|
**B. Update and Delete a Blacklisted Word in Blacklisted Word Masterdata DB**
**(i) Update**
1. Upon receiving request to update a Blacklisted Word with the input parameters (code, name, descr, lang_code and is_active) the system updates the Blacklisted Word in the Blacklisted Word DB for the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* word- character (128) - Mandatory
* descr - character (256) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
3. For the code received in the request, replaces all the data received in the request against the data existing in the Blacklisted Word database against the same code
4. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Word and Language Code for the Blacklisted word updated successfully
1. In case of Exceptions, system should trigger relevant error messages as listed below
**(ii) Delete**
1. Upon receiving a request to delete a Blacklisted Word with the input parameters (code) the system updates the is_deleted flag to true in the Blacklisted Word DB against the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* word- int - Mandatory
3. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Word for the Blacklisted word deleted successfully
1. In case of Exceptions, system should trigger relevant error messages as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while updating Blacklisted Word|	KER-MSD-105|
Error occurred while deleting Blacklisted Word	|KER-MSD-106|
Blacklisted Words not found	|KER-MSD-008|



### 1.16 List of Reason Categories - Create/Read/Update/Delete

MOSIP system can create a Reason Category in Master Data

Upon receiving a request to add Reason Category with the input parameters (code, name, descr, lang_code and is_active) the system stores the Reason Category in the DB

Upon receiving a request to add Reason Category with the input parameters (code, name, descr, lang_code and is_active) the system stores the Reason Category in the DB

Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory

Validates if the response contains the following attributes for a Reason Category added
* Code
* Language Code
Responds with the Reason Category code and Language Code for the Reason Category created successfully

In case of Exceptions, system triggers relevant error messages as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Reason Category details|	KER-MSD-057|

### 1.17 List of Applications - Create/Read/Update/Delete
**A. Create a List of Applications in Master Data**

1. Upon receiving a request to add Application with the input parameters (code, name, descr, lang_code and is_active)the system stores the Application in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr- character (256) - Mandatory
* lang_code - character (3) – Mandatory (The parameter lang_code refers to a Language stored in Language Masterdata. Refer)
* is_active - boolean - Mandatory
3. Validates if the response contains the following attributes for a Application added
* Code
* Language Code
4. Responds with the Application ID and Language Code for the Application created successfully
1. In case of Exceptions, system should trigger relevant error messages as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Application details|	KER-MSD-056|

**B. Fetch List of Applications based on received input parameter**

**(i) Fetch the List of all Applications**

Upon receiving a request to Fetch List of Applications the system fetches all the List of Applications

1. Validates if the response contain the following attributes for each Application
* Application ID
* Application Detail
* IsActive

2. The response must contain the list of applications in all the languages present in the Database

1. Responds to the source with all the Application attributes.

**(ii) Fetch the Application detail based on a Language Code and Application ID**

Upon receiving a request to Fetch List of Applications with the required input parameters (Application ID, Language Code) the system fetches the Application Detail based on the Application ID and Language Code received

1. Validate if all required input parameters have been received as listed below for each specific request
* Application ID - Mandatory
* Language Code - Mandatory

2. Respond with the Application Data against the Application ID and Language Code Received

1. Validate if the response contain the following attributes for each Application
* Application ID
* Application Detail
* IsActive

4. Respond to the source with the Application Detail

1. If the mandatory input parameters are missing, responds with all the data.

1. In case of Exceptions, system should trigger relevant error messages as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while fetching Application|	KER-MSD-001|
Application not found	|KER-MSD-002|


### 1.18 List of ID Types - Create/Read/Update/Delete
**A. Create an ID type in Master Data**

1. Upon receiving a request to add an ID Type with the input parameters (code, name, descr, lang_code and is_active) the system stores the ID Type in the DB

1. Validates if all required input parameters have been received as listed below for each specific request

* code - character (36) - Mandatory
* code - character (64) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) – Mandatory(refers to a Language stored in Language Masterdata)
* is_active - boolean - Mandatory

3. Validates if the response contains the following attributes for an ID Type added

* Code
* Language Code

4. Responds with the ID Type Code and Language Code for the ID type created successfully

5. In case of Exceptions, system should trigger relevant error messages as listed below.

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting ID Type details	|KER-MSD-059|

**B. Fetch the List of ID Types based on Language Code**

1. Upon receiving a request to fetch the List of ID Types with input parameters (Language Code) the system fetches the List of ID Types against the Language Code Received

1. Validates if the request contains the following input parameters
* Language Code - Mandatory
3. If the mandatory input parameters are missing, throws the appropriate message. Refer "Messages" section below.

1. Validates if the response contains the List of ID Types with the following attributes
* ID Type Name
* ID Type Code
* IsActive
5. In case of Exceptions, system should trigger relevant error messages as listed below.

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while fetching ID Types|	KER-MSD-021|
ID Type not found	|KER-MSD-022|









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
#### A. Create a mapping record of Machine and Center in Machine-Center Mapping Masterdata DB
Upon receiving a request to add a mapping of Machine and Center with the input parameters (regcntr_id, machine_id, and is_active) the system stores the Mapping of Machine and Center in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (10) – Mandatory (refers to a Registration Center stored in Registration Center)
* machine_id - character (10) – Mandatory(refers to a Machine stored in Machine Masterdata)
* is_active - boolean - Mandatory
2. Responds with the Machine Id and Center ID for the mapping of Machine and Center created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting a mapping of Machine and Center|	KER-MSD-074

#### B. Delete a Center-Machine mapping in the Center-Machine mapping Masterdata DB

1. Upon receiving a request to delete a Center-Machine mapping with the input parameters (regcntr_id, machine_id) the system updates the is_deleted flag to true in the Center-Machine mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) - Mandatory
* machine_id - character (36) - Mandatory
3. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request.
1. Responds with the Machine Id and Center ID for the mapping of Machine and Center deleted successfully
1. In case of Exceptions, system should trigger relevant error messages as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while deleting a mapping of Machine and Center|	KER-MSD-106|
Mapping for Machine and Center not found|	KER-MSD-114|

### 2.11 Mappings of Registration Center and Device - Create/Read/Update/Delete
#### A. Create a mapping record of Device and Center in Device-Center Mapping Masterdata DB
1. Upon receiving a request to add a mapping of Device and Center with the input parameters (regcntr_id, device_id, and is_active) the system stores the Mapping of Device and Center in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (10) – Mandatory(refers to a Registration Center stored in Registration Center)
* device_id - character (36) – Mandatory(refers to a Device stored in Device Masterdata)
* is_active - boolean - Mandatory
3. Responds with the Device Id and Center ID for the mapping of Device and Center created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting a mapping of Device and Center|	KER-MSD-075|

#### B. Delete a Center-Device mapping in the Center-Device mapping Masterdata DB
1. Upon receiving a request to delete a Center-Device mapping with the input parameters (regcntr_id, device_id) the system updates the is_deleted flag to true in the Center-Device mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) - Mandatory
* device_id - character (36) - Mandatory
3. Deleted record should not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device Id and Center ID for the mapping of Device and Center deleted successfully
1. In case of Exceptions, system should trigger relevant error messages as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while deleting a mapping of Device and Center|	KER-MSD-105|
Mapping for Device and Center not found	|KER-MSD-115|




### 2.12 Mappings of Registration Center, Machine, and Device - Create/Read/Update/Delete


### A. Create a mapping record of Center, Machine and Device in Center-Machine-Device Mapping Masterdata DB

1. Upon receiving a request to add a mapping of Center, Machine and Device with the input parameters (regcntr_id, machine_id, device_id, and is_active) the system store the Mapping of Center, Machine and Device in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) – Mandatory(refers to a Registration Center stored in Registration Center Masterdata)
* machine_id - character (36) – Mandatory(refers to a Registration Center stored in Registration Center Masterdata)
* device_id - character (36) – Mandatory(refers to a Device stored in Device Masterdata)
* is_active - boolean - Mandatory
3. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting a mapping of Center, Machine and Device|	KER-MSD-076|

#### B. Delete a Center-Machine-Device mapping in the Center-Machine-Device mapping Masterdata DB
1. Upon receiving a request to delete a Center-Machine-Device mapping with the input parameters (regcntr_id, machine_id, device_id) the system updates the is_deleted flag to true in the Center-Machine-Device mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) - Mandatory
* machine_id - character (36) - Mandatory
* device_id - character (36) - Mandatory
3. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device deleted successfully
1. In case of Exceptions, system triggers relevant error messages as listed below
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while deleting a mapping of Center, Machine and Device|	KER-MSD-107|
Mapping for Center, Machine and Device not found	|KER-MSD-116|

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




