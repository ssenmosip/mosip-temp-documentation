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

#### A. Create Location Hierarchy in the Masterdata DB
Upon receiving a request to add Location hierarchy (e.g., Country - Region - Province - City- LAA) with the input parameters (code, name, hierarchy_level, hierarchy_level_name, parent_loc_code ,lang_code and is_active), the system store the Location hierarchy in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (128) - Mandatory
* hierarchy_level - smallint - Mandatory
* hierarchy_level_name - character (64) - Mandatory
* parent_loc_code - character (32) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Code and Language Code for the Location Hierarchy created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database

#### B. Check the existence of a Location in Master DB
Upon receiving a request to validate the Location Name with input parameters (Location Name), the system checks the Location Name in the Master DB
1. Validates if the request contains the following input parameters
* Location Name - Mandatory
2. If the mandatory input parameters are missing, throw the appropriate message
1. In case of Exceptions, system triggers relevant error messages
#### C. Fetch Location Hierarchy Levels based on a Language Code
Upon receiving a request to fetch the Location Hierarchy Levels with input parameters (Language Code), the system fetches the Location Hierarchy Levels
1. Validates if the request contains following input parameters (Language Code)
* Language Code - Mandatory
2. Validates if the response contains the Location Hierarchy Levels with the following attributes
* Hierarchy Level
* Hierarchy Name
* IsActive
3. In case of Exceptions, system triggers relevant error messages
#### D. Fetch the Location Hierarchy Data based on a Location Code and a Language Code
Upon receiving a  request to fetch all the Location Hierarchy Data with input parameters (Location Code and Language Code), the system fetches the Location Hierarchy Data
1. Validates if the request contains the following input parameters
* Location Code - Mandatory
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throw the appropriate message. 
1. Validates if the response contains the following location hierarchy data and the corresponding attributes against the Location Code and Language Code received in the input parameter

   **(i) List of Countries against the Location Code**
   * Country Code
   * Country Name
   * IsActive

   **(ii) List of Regions against the Location Code**
   * Region Code
   * Region Name
   * IsActive

   **(iii) List of Provinces against the Location Code**
   * Province Code
   * Province Name
   * IsActive

   **(iv) List of Cities against the Location Code**
   * City Code
   * City Name
   * IsActive

   **(v) List of Local Administrative authorities against the Location Code**
   * Local Administrative Authority Code
   * Local Administrative Authority Name
   * IsActive

   **(vi) List of Pincodes against the Location Code**
   * Pincode
   * IsActive
4. Respond to the source with all the Location Hierarchy Data based on the Location Code
1. In case of Exceptions, system triggers relevant error messages. 

#### E. Fetch the Location Hierarchy Data for the bottom next hierarchy based on a Location Code and a Language Code
Upon receiving a request to fetch all the Location Hierarchy Data with input parameters (Location Code and Language Code), the system fetches the Location Hierarchy Data for the next hierarchy level
1. Validates if the request contains the following input parameters
* Location Code - Mandatory
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Fetches the Location data of only the child hierarchy of location code received (For e.g., if the location code for a particular Province is received, responds with the data of all the Cities existing in that Province, similarly if location code of a City is received, responds all the data regarding the Local Administrative Authorities existing under that City)
1. Respond to the source with the data fetched
1. In case of Exceptions, system should triggers  error message. 



### 1.2 List of Holidays - Create/Read/Update/Delete
#### A. Create Holiday data in Masterdata DB
Upon receiving a request to add Holiday Data with the input parameters (location_code, holiday_date, holiday_name, holiday_desc, lang_code and is_active), the system store the Holiday in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* location_code - character (36) - Mandatory
* holiday_date - date - Mandatory
* holiday_name - character (64) - Mandatory
* holiday_desc - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. The component restricts the bulk creation of Master Data
1. Responds with the Location Code, Holiday Date, Holiday Name and Language Code for the Holiday created successfully
1. In case of Exceptions, system will trigger error messages as received from the Database

#### B. Fetch List of Holidays based on a Registration Center ID, a Year and a Language Code

On receiving a request to fetch the list of Holidays with the input parameters (Registration Center ID, Year and Language Code), the system fetches the list of Holidays  mapped to a Registration Center and for the year and Language Code received in input parameter
1. Validates if the received request contains the following input parameters
* Registration Center ID - Mandatory
* Year - Mandatory
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
1. Validates if the response contains the List of Holidays against the Registration Center ID and the year received and contains the following attributes for a Region
* Holiday ID
* Holiday Date
* Holiday Name
* IsActive
4. Respond to the source with the List of Holidays
1. In case of Exceptions, system triggers relevant error messages

#### C. Update and Delete a Location in Location Masterdata DB
##### (i) Update
On receiving a  request to update a Location with the input parameters (code, name, hierarchy_level, hierarchy_level_name, parent_loc_code, lang_code and is_active),  the system updates the Location in the Location DB for the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code character (36) - Mandatory
* name character (128) - Mandatory
* hierarchy_level smallint - Mandatory
* hierarchy_level_name character (64) - Mandatory
* parent_loc_code character (32) - Mandatory
* lang_code character (3) - Mandatory
* is_active boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Location database against the same code.
1. Deleted record are not be updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Code and Language Code for the Location Hierarchy updated successfully
1. In case of Exceptions, system triggers relevant error messages
##### (ii) Delete
On receiving a  request to delete a Location with the input parameters (code), the system updates the is_deleted flag to true in the Location DB against the code received
1. Validates if all required input parameters have been received as listed below for each specific request
1. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Code for the Location Hierarchy deleted successfully
* code - character (36) - Mandatory
7. In case of Exceptions, system triggers relevant error messages. 


### 1.3 Biometric Authentication Type - Create/Read/Update/Delete
#### A. Create Biometric Authentication Type in Masterdata DB
On receiving a request to add Biometric Authentication Type (e.g., Fingerprint, Iris) with the input parameters (code, name, descr, lang_code and is_active), the system store the Biometric Authentication Type in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (256) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Biometric Authentication Type Code and Language Code for the Biometric Authentication Type created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database.

#### B. Fetch the List of Biometric Authentication Type based on a Language Code
On receiving a request to fetch the List of Biometric Authentication Type with input parameters (Language Code), the system fetches the List of Biometric Authentication Type against the Language Code
1. Validates if the request to add Biometric Authentication Type contains the following parameters
* Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
1. Validates if the response contains the List of Biometric Authentication Type against the Language Code along with the IsActive Flag for each Biometric Authentication Type
1. Responds to the source with List of Biometric Authentication Type
1. In case of Exceptions, system should trigger relevant error messages


### 1.4 Biometric Attribute Type - Create/Read/Update/Delete

#### A. Create Biometric Attribute in Masterdata DB

On receiving a request to add Biometric Attribute (e.g., Right Thumb, Left Thumb) with the input parameters (code, name, descr, bmtyp_code, lang_code and is_active), the system stores the Biometric Attribute in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* bmtyp_code - character (36) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Biometric Attribute Code and Language Code for the Biometric Attribute created successfully
1. The component restricts the bulk creation of Master Data
1. Respond to the source with the appropriate message.
1. In case of Exceptions, system triggers error messages as received from the Database


#### B. Fetch the List of Biometric Attributes based on the Biometric Authentication Type and a Language Code

On receiving a request to fetch the List of Biometric Attributes with input parameters (Biometric Authentication Type and Language Code), the system fetches the List of Biometric Attributes against the Biometric Authentication Type and the Language Code Received
1. Validate if the request contains the following input parameters
* Biometric Authentication Type - Mandatory
* Language Code - Mandatory
2. If no data is present in the DB for the input parameter received, respond with appropriate message.
1. If both the input parameter is missing, respond with all the data.
1. If one of the input parameters is missing, throw the appropriate message. Refer "Messages" section.
1. Validate if the response contains the List of Biometric Attributes with all the attributes against Biometric Authentication Type and Language Code Received
* Biometric Attribute Code - Mandatory
* Biometric Attribute Name - Mandatory
* Biometric Attribute Description - Optional
* IsActive – Mandatory
6. Respond to the source with the Fetched Data
1. In case of Exceptions, system should trigger relevant error messages


### 1.5 Gender - Create/Read/Update/Delete
#### A. Create Gender Types in Masterdata DB

On receiving a request to add a Gender Type with the input parameters (code, name, lang_code and is_active), the system stores the Gender Type in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (16) - Mandatory
* name - character (64) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Gender Type Code and Language Code for the Gender Type created successfully
1. The component restricts the bulk creation of Master Data
1. Respond to the source with the appropriate message
1. In case of Exceptions, system will trigger error messages as received from the Database.
 

#### B. Update and Delete a Gender Type in Gender Type Masterdata DB

##### (i) Update

On receiving a request to update a Gender Type with the input parameters (code, name, lang_code and is_active), the system updates the Gender Type in the Gender Type DB for the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (16) - Mandatory
* name - character (64) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Gender Type database against the same code.
1. Deleted record are not be updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Gender Type Code and Language Code for the Gender Type updated successfully
1. In case of Exceptions, system should trigger relevant error messages.
##### (ii) Delete


On receiving a request to delete a Gender Type with the input parameters (code),  the system updates the is_deleted flag to true in the Gender Type DB against the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code - int - Mandatory
2. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Gender Type Code for the Gender Type deleted successfully
1. In case of Exceptions, system should trigger relevant error messages. 

#### C. Check the existence of a Gender in Master DB

On receiving a request to validate the Gender Name with input parameters (Gender Name), the system checks the Gender Name in the Master DB
1. Validates if the request contains the following input parameters
* Gender Name - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Respond to the source with the appropriate message
1. In case of Exceptions, system triggers relevant error messages

#### D. Fetch the List of Gender Types based on a Language Code

On receiving a request to fetch the List of Gender Types with the input parameters (Language Code), the system fetches the List of Gender Types against the Language Code received
1. Validates if the request contains the following input parameters
* Language Code - Mandatory
2. If the Language code is missing, responds with all the data.
1. Validates if the response contains the List of Gender Types with the following attributes
* Gender Code
* Gender Name
* isActive
4. Responds to the source with the List of Gender Types
5. In case of Exceptions, system triggers relevant error messages


### 1.6 Document Category - Create/Read/Update/Delete

#### A. Create Document Category in Master Data

On receiving a request to add Document Category with the input parameters (code, name, descr, lang_code and is_active), the system stores the Document Category in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Document Category added
* Code
* Language Code
3. Responds with the Document Category Code and Language Code for the Document Category created successfully
1. Respond to the source with the appropriate message.
1. In case of Exceptions, system should trigger relevant error messages


#### B. Update and Delete a Document Category in the Document Category Masterdata DB

##### (i) Update


On receiving a request to update a Document Category with the input parameters (code, name, descr, lang_code and is_active), the system update the Document Category in the Document Category DB for the Code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the code received in the request, replace all the data received in the request against the data existing in the Document Category database against the same code.
1. Deleted record should not be updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Document Category Code and Language Code for the Document Category updated successfully
1. In case of Exceptions, system triggers relevant error messages

##### (ii) Delete


On receiving a request to delete a Document Category with the input parameters (code), the system updates the is_deleted flag to true in the Document Category DB against the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Document Category Code for the Document Category deleted successfully
1. In case of Exceptions, system triggers relevant error messages

#### C. Fetch list of Document Categories based on a Language Code


On receiving a request to fetch Document Category Details with the input parameters (Language Code), the system fetches all the Document Categories for the Language Code Received

1. Validates if all required input parameters have been received as listed below for each specific request
* Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
1. Validates if the response contain the following attributes for the Document Category Code
* Document Category Code - Mandatory
* Document Category Name - Mandatory
* Document Category Description - Optional
* IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages


### 1.7 Document Type - Create/Read/Update/Delete


#### A. Create Document Type in Master Data


On receiving a request to add Document Type with the input parameters (code, name, descr, lang_code and is_active), the system stores the Document Type in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Document Type added
* Code
* Language Code
3. Responds with the Document Type Code and Language Code for the Document Type created successfully
1. In case of Exceptions, system triggers relevant error messages


#### B. Update and Delete a Document Type in the Document Type Masterdata DB

##### (i) Update


On receiving a request to update a Document Type with the input parameters (code, name, descr, lang_code and is_active), the system updates the Document Type in the Document Type DB for the Code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Document Type database against the same code
1. Deleted record are not be updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Document Category Code and Language Code for the Document Category updated successfully
1. In case of Exceptions, system should trigger relevant error messages


##### (ii) Delete

On receiving a request to delete a Document Type with the input parameters (code), the system updates the is_deleted flag to true in the Document Type DB against the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Document Category Code for the Document Category deleted successfully
1. In case of Exceptions, system should trigger relevant error messages


### 1.8 Document Category - Document Type Mapping - Create/Read/Update/Delete

#### A. Create a mapping of Document Type and Document Category in Masterdata DB

On receiving a request to add Document Type with the input parameters (code, name, descr, lang_code and is_active), the system stores the Document Type in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Document Type added
* Code
* Language Code
3. Responds with the Document Type Code and Language Code for the Document Type created successfully
1. In case of Exceptions, system triggers relevant error messages

#### B. Fetch List of Document Types based on Document Category and a Language Code


On receiving a request to fetch the List of Document Types with input parameters (Document Category Code and Language Code), the system fetches the List of Document Types against the Document Category Code and language Code Received
1. Validates if the request contains the following input parameters
* Document Category Code - Mandatory
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
1. Validates if the response contains the List of Document Types against the Document Category and Language Code Received and the corresponding attributes for each Document Type
* Document Type ID - Mandatory
* Document Type Name - Mandatory
* IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages

#### C. Delete a Document Category-Type mapping in the Document Category-Type mapping Masterdata DB


On receiving a request to delete a Document Category-Type mapping with the input parameters (doccat_code, doctyp_code), the system updates the is_deleted flag to true in the Document Category-Type mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* doccat_code - character (36) - Mandatory
* doctyp_code - character (36) - Mandatory
3. Responds with the doc_type Code and doccat_code for the Document Category-Type mapping deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 


#### D. Fetch applicant type based on Individual Type Code, Date of Birth, Gender Type Code and Biometric Exception Type


On receiving a request to get Applicant type with input parameters (Individual Type Code, Date of Birth, Gender Type Code and Biometric Exception Type), the system derives the Applicant Type from the input parameter
1. Validates if the request contains the following input parameters
* Individual Type Code - Mandatory
* Date of Birth - Mandatory
* Gender Type Code - Mandatory
* Biometric Exception Type - Optional
2. Derives the Age Group Type based on following logic
* Child if Age < 5
* Adult if Age >= 5
3. If the mandatory input parameters are missing, throws the appropriate message
1. Derives the applicant type as per the define logic
1. In case of Exceptions, system triggers relevant error messages


#### E. Check the mapping of Applicant Type-Document Category Name-Document Type Name


On receiving a request to check the mapping of Applicant Type-Document Category-Document Type mapping parameters (Applicant Type, Document Category Name and Document Type Name), the system checks the mapping

1. Validates if the request contains the following input parameters
* Applicant Type Code
* Document Category Name
* Document Type Name
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. If the mapping exists, respond with "Valid".
1. If the mapping does not exist, respond with "Invalid".
1. In case of Exceptions, system triggers relevant error messages


### 1.9 List of Rejection Reasons - Create/Read/Update/Delete
**A. Create a Rejection Reason in Reason List Master Data**

Upon receiving a request to add a Reason with the input parameters (code, name, descr, rsncat_code, lang_code and is_active), the system store the Reason in the DB

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

3. Respond to the source with the appropriate message.

4. In case of Exceptions, system triggers relevant error messages as listed below

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Reason details|	KER-MSD-058|

**B. Fetch the requested list of reasons based on Reason Category Code and Language Code**


Upon receiving a request to Fetch the requested List of Reasons with the required input parameters (Reason 1. Category Code, Language Code), the system fetches the requested List of reasons stored against the Reason Category Code and Language Code received
1. Validates if the request contains the following input parameters
* Language Code - Mandatory
* Reason Category Code - Mandatory
2. If either of the mandatory input parameters is missing, responds with the appropriate message as define below in message sections
1. Validates if the response contains the:
(a) Requested list based on the requested Language Code and Reason Category Code
(b) List of Reasons with the corresponding attributes for the list
* Reason ID
* Reason Name (per Reason ID)
* Language Code
* Reason Category Code
* IsActive
4. Responds to the source with the relevant List of Reasons, as per the stated business rules
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


#### A. Create List of Languages in Master Data


After receiving a request to add Language Details with the input parameters (code, name, family, native_name and is_active), the system stores the Language Details in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (3) - Mandatory
* name - character (64) - Mandatory
* family - character (64) - Optional
* native_name - character (64) - Optional
* is_active - boolean - Mandatory
2. Responds with the Language Code for the language successfully created
1. In case of Exceptions, system triggers relevant error messages

#### B. Fetch the List of Languages


After receiving a request to fetch the List of Languages the system fetches the List of Languages

1. Validates if the response contains the List of all Languages with the following attributes
* Language Code - Mandatory
* Language Name - Mandatory
* IsActive – Mandatory
2. Respond to the source with the List of Languages
1. In case of Exceptions, system triggers relevant error messages

#### C. Update and Delete a Language in the List of Languages Masterdata DB

##### (i) Update


After receiving a request to update a Language with the input parameters (code, name, family, native_name and is_active), the system updates the Language Details in the List of languages DB for the Code received in request
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (3) - Mandatory
* name - character (64) - Mandatory
* family - character (64) - Optional
* native_name - character (64) - Optional
* is_active - boolean - Mandatory
2. For the Code received in the request, replaces all the data received in the request against the data existing in the List of languages database against the same code.
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Language Code for the language successfully updated
1. In case of Exceptions, system triggers relevant error messages


##### (ii) Delete


After receiving a request to delete a Language with the input parameters (code), the system updates the is_deleted flag to true in the List of languages DB against the code received in request

1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (3) - Mandatory
2. Deleted record should not deleted again
1. Responds with data not found error  if deleted record is received in the request
1. Responds with the Language Code for the language successfully deleted
1. In case of Exceptions, system triggers relevant error messages. 


### 1.11 List of Titles - Create/Read/Update/Delete

#### A.	Create a Title in Masterdata DB

On receiving a request to add a Title (e.g., MR., Mrs.) with the input parameters (code, name, descr, lang_code and is_active), the system stores the Title in the DB


1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (16) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Title Code and Language Code for the Title created successfully
1. In case of Exceptions, system triggers error messages as received from the Database. 

#### B.	Update and Delete a Title in Title Masterdata DB

##### (i) Update


On receiving a request to update a Title with the input parameters (code, name, descr, lang_code and is_active), the system updates the Title in the Title DB for the code received

1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (16) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Title database against the same code.
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Title Code and Language Code for the Title created successfully
1. In case of Exceptions, system triggers relevant error messages.

##### (i) Delete

On receiving a request to delete a Title with the input parameters (code), the system updates the is_deleted flag to true in the Title DB against the code received

1. Validates if all required input parameters have been received as listed below for each specific request
* code - int - Mandatory
2. Delete all records for the code received
1. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Title Code for the Title created successfully
1. In case of Exceptions, system triggers relevant error messages. 


#### C. Fetch the List of Titles based on a Language Code

On receiving a request to fetch Title Details with the input parameters (Language Code), the system fetches all the Titles with all the attributes for the Language Code Received


1. Validates if all required input parameters have been received as listed below for each specific request
* Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
1. Validates if the response contain List of Titles against the received Language Code along with the following attributes for the Title Code
* Title Code - Mandatory
* Title Name - Mandatory
* Title Description - Optional
* IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages


### 1.12 Template File Format - Create/Read/Update/Delete

#### A. Create Template File Format in Master Data


On receiving a request to add Template File Format with the input parameters (code, descr, lang_code and is_active), the system stores the Template File Format in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Template File Format added
* Code
* Language Code
3. Responds with the Template File Format Code and Language Code for the Template File Format created successfully
1. In case of Exceptions, system triggers relevant error messages. 


### 1.13 List of Template Types - Create/Read/Update/Delete
MOSIP system can create Template Type in the Masterdata DB.

Upon receiving a request to add Template Type (e.g., SMS Notification template - New Registration) with the input 
parameters (code, descr, lang_code and is_active), the system stores the Template Type in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean – Mandatory

2. Respond with the Template Type Code and Language Code for the Template Type created successfully

3. This component also restrict the bulk creation of Master Data

4. In case of Exceptions, system triggers relevant error messages as listed below.
### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting Template Type details	|KER-MSD-072|

### 1.14 List of Templates - Create/Read/Update/Delete

#### A. create Template in the Masterdata DB


On receiving a request to add a Template with the input parameters (id, name, descr, file_format_code, model, file_txt, module_id, module_name, template_typ_code, lang_code and is_active), the system stores the Template in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* id- character (36) - Mandatory
* name - character (128) - Mandatory
* descr - character (256) - Optional
* file_format_code - character (36) – Mandatory (refers to a Template File Format stored in Template File Format Masterdata)
* model - character (128) - Optional
* file_txt - character (4086) - Optional
* module_id - character (36) - Optional
* module_name - character (128) - Optional
* template_typ_code - character (36) – Mandatory (refers to a Template Type stored in Template Type Masterdata)
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Responds with the Template Id and Language Code for the Template created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers relevant error messages. 

#### B. Fetch Template based on a Template Type and a Language Code


On receiving a request to fetch a Template with the input parameters (Template Type Code and List of Language Code), the system fetches the Template for the Template Type Code and all Language Codes received


1. Validates if all required input parameters have been received as listed below for each specific request
* Template Type Code - Mandatory
* List of Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. Refer "Messages" section.
1. Response must contain templates for all the language codes received in the input parameter
1. Validates if the response contains the Template along with the following attributes
* Template Type Code - Mandatory
* Template - Mandatory
* IsActive
5. In case of Exceptions, system triggers relevant error messages


#### C. Update and Delete a Template in Template Masterdata DB

##### (i) Update

On receiving a request to update a Template with the input parameters (id, name, descr, file_format_code, model, file_txt, module_id, module_name, template_typ_code, lang_code and is_active), the system updates the Template in the Template DB for the id received

1. Validates if all required input parameters have been received as listed below for each specific request
* id - character (36) - Mandatory
* name - character (128) - Mandatory
* descr - character (256) - Optional
* file_format_code - character (36) - Mandatory
* model - character (128) - Optional
* file_txt - character (4086) - Optional
* module_id - character (36) - Optional
* module_name - character (128) - Optional
* template_typ_code - character (36) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the id received in the request, replaces all the data received in the request against the data existing in the Template database against the same id
1. Deleted record are not updated
1. Responds with data not found error (Refer Acceptance criteria) if deleted record is received in the request
1. Responds with the Template Id and Language Code for the Template updated successfully
1. In case of Exceptions, system triggers relevant error messages.


##### (ii) Delete

On receiving a request to delete a Template with the input parameters (id), the system Updates the is_deleted flag to true in the Template DB against the id received

1. Validates if all required input parameters have been received as listed below for each specific request
* id- character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record should are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Template Id for the Template deleted successfully
1. In case of Exceptions, system triggers relevant error messages


### 1.15 List of Blacklisted Words - Create/Read/Update/Delete
**A. Create Blacklisted Words in Masterdata DB**

Upon receiving a request to add a Blacklisted Word with the input parameters (code, name, descr, lang_code and is_active), the system store the Blacklisted Word in the DB

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

Upon receiving request to update a Blacklisted Word with the input parameters (code, name, descr, lang_code and is_active), the system updates the Blacklisted Word in the Blacklisted Word DB for the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* word- character (128) - Mandatory
* descr - character (256) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Blacklisted Word database against the same code
3. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Word and Language Code for the Blacklisted word updated successfully
1. In case of Exceptions, system should trigger relevant error messages as listed below
**(ii) Delete**

Upon receiving a request to delete a Blacklisted Word with the input parameters (code), the system updates the is_deleted flag to true in the Blacklisted Word DB against the code received
1. Validates if all required input parameters have been received as listed below for each specific request
* word- int - Mandatory
2. Deleted record are not deleted again
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


Upon receiving a request to add Reason Category with the input parameters (code, name, descr, lang_code and is_active), the system stores the Reason Category in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory

2. Validates if the response contains the following attributes for a Reason Category added
* Code
* Language Code
3. Responds with the Reason Category code and Language Code for the Reason Category created successfully

4. In case of Exceptions, system triggers relevant error messages as listed below
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

Upon receiving a request to add Application with the input parameters (code, name, descr, lang_code and is_active), the system stores the Application in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr- character (256) - Mandatory
* lang_code - character (3) – Mandatory (The parameter lang_code refers to a Language stored in Language Masterdata. Refer)
* is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for an Application added
* Code
* Language Code
3. Responds with the Application ID and Language Code for the Application created successfully
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

Upon receiving a request to Fetch List of Applications, the system fetches all the List of Applications

1. Validates if the response contain the following attributes for each Application
* Application ID
* Application Detail
* IsActive

2. The response must contain the list of applications in all the languages present in the Database

1. Responds to the source with all the Application attributes.

**(ii) Fetch the Application detail based on a Language Code and Application ID**

Upon receiving a request to Fetch List of Applications with the required input parameters (Application ID, Language Code), the system fetches the Application Detail based on the Application ID and Language Code received

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

Upon receiving a request to add an ID Type with the input parameters (code, name, descr, lang_code and is_active), the system stores the ID Type in the DB

1. Validates if all required input parameters have been received as listed below for each specific request

* code - character (36) - Mandatory
* code - character (64) - Mandatory
* descr - character (256) - Mandatory
* lang_code - character (3) – Mandatory (refers to a Language stored in Language Masterdata)
* is_active - boolean - Mandatory

2. Validates if the response contains the following attributes for an ID Type added

* Code
* Language Code

3. Responds with the ID Type Code and Language Code for the ID type created successfully

4. In case of Exceptions, system should trigger relevant error messages as listed below.

### <p align="left">**1. Type : Success – Info Message**
|Scenario|Message|Message Code|
|:------:|:------:|:------:|
NA|	NA|	NA

### <p align="left">**2. Type : Error/Failure – Info Message**
|Message|Message Code|
|:------:|:------:|
Error occurred while inserting ID Type details	|KER-MSD-059|

**B. Fetch the List of ID Types based on Language Code**

Upon receiving a request to fetch the List of ID Types with input parameters (Language Code), the system fetches the List of ID Types against the Language Code Received

1. Validates if the request contains the following input parameters
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. Refer "Messages" section below.

1. Validates if the response contains the List of ID Types with the following attributes
* ID Type Name
* ID Type Code
* IsActive
4. In case of Exceptions, system should trigger relevant error messages as listed below.

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

#### A. Create Registration Center Type in Master Data

On receiving a request to add Registration Center Type with the input parameters (code, name, descr, lang_code and is_active), the system store the Registration Center Type in the DB


1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Registration Center Type added
* Code
* Language Code
3. Responds with the Registration Center Type code and Language Code for the Registration Center Type successfully created
1. In case of Exceptions, system triggers relevant error messages. 

	
#### B. Update and Delete a Registration Center Type in the Registration Center Type Masterdata DB

##### (i) Update

On receiving a request to update a Registration Center Type with the input parameters (code, name, descr, lang_code and is_active), the system Updates the Registration Center Type Details in the Registration Center Type DB for the Code received


1. Validates if all required input parameters have been received as listed below for each specific request
1. code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory
2. For the Code received in the request, replaces all the data received in the request against the data existing in the Registration Center Type database against the same code.
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Registration Center Type code and Language Code for the Registration Center Type successfully updated
1. In case of Exceptions, system triggers relevant error messages

##### (ii) Delete

On receiving a request to delete a Registration Center Type with the input parameters (code), the system updates the is_deleted flag to true in the Registration Center Type DB against the code received


1. Validates if all required input parameters have been received as listed below for each specific request
* code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Registration Center Type code for the Registration Center Type successfully deleted
1. In case of Exceptions, system triggers relevant error messages. 


### 2.2 Registration Center - Create/Read/Update/Delete


#### A. Create a Registration Center record in Masterdata DB


Upon receiving a request to add Registration Center with the input parameters (center_id, name, cntrtyp_code, addr_line1, addr_line2, addr_line3, latitude, longitude, location_code, contact_phone, contact_person, number_of_kiosks, working_hours
per_kiosk_process_time, start_time, end_time, lunch_start_time. lunch_end_time, holiday_loc_code, timezone, lang_code and is_active), the system Stores the Registration Center in the DB


1. The system validates if all required input parameters have been received as listed below for each specific request
* center_id - character (36) - mandatory
* name - character (128) - mandatory
* cntrtyp_code - character (36) - optional
* addr_line1 - character (256) - optional
* addr_line2 - character (256) - optional
* addr_line3 - character (256) - optional
* latitude - character (32) - optional
* longitude - character (32) - optional
* location_code - character (36) - mandatory
* contact_phone - character (16) - optional
* contact_person - character (256) - optional
* number_of_kiosks - smallint - optional
* working_hours - character (32) - optional
* per_kiosk_process_time - time - optional
* center_start_time - time - optional
* center_end_time - time - optional
* lunch_start_time - time - optional
* lunch_end_time - time - optional
* holiday_loc_code - character (36) - optional
* timezone - string (128) - optional
* lang_code - character (3) - mandatory
* is_active - boolean - mandatory
2. Responds with the Registration Center Code and Language Code for the Registration Center created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database. 

#### B. Update and Delete a Registration Center in the List of Registration Center Masterdata DB
##### (i) Update


On receiving a request to update a Registration Center with the input parameters (center_id, name, cntrtyp_code, addr_line1, addr_line2, addr_line3, latitude, longitude, location_code, contact_phone, contact_person, number_of_kiosks, working_hours, per_kiosk_process_time, start_time, end_time, lunch_start_time. lunch_end_time, holiday_loc_code, timezone, lang_code and is_active), the system updates the Registration Center Details in the List of Registration Center DB for the center_id received

1. The system validates if all required input parameters have been received as listed below for each specific request
* center_id - character (36) - mandatory
* name - character (128) - mandatory
* cntrtyp_code - character (36) - optional
* addr_line1 - character (256) - optional
* addr_line2 - character (256) - optional
* addr_line3 - character (256) - optional
* latitude - character (32) - optional
* longitude - character (32) - optional
* location_code - character (36) - mandatory
* contact_phone - character (16) - optional
* contact_person - character (256) - optional
* number_of_kiosks - smallint - optional
* working_hours - character (32) - optional
* per_kiosk_process_time - time - optional
* center_start_time - time - optional
* center_end_time - time - optional
* lunch_start_time - time - optional
* lunch_end_time - time - optional
* holiday_loc_code - character (36) - optional
* timezone - character (64) - optional
* lang_code - character (3) - mandatory
* is_active - boolean - mandatory
2. For the center_id received in the request, replaces all the data received in the request against the data existing in the List of Registration Center database against the same center_id.
1. Responds with the Registration Center Code and Language Code for the Registration Center updated successfully
1. In case of Exceptions, system triggers relevant error messages

##### (ii) Delete


Upon receiving a request to delete a Registration Center with the input parameters (center_id), the system updates the is_deleted flag to true in the List of Registration Center DB against the center_id received


1. The system validates if all required input parameters have been received as listed below for each specific request
* center_id - character (36) - Mandatory
2. Responds with the Registration Center Code and Language Code for the Registration Center deleted successfully
1. In case of Exceptions, system trigger relevant error messages


#### C. Fetch Registration Center details based on a Registration Center ID and Language Code.


On receiving a request to fetch Registration Center Details with the input parameters (Registration Center ID and Language Code), the system fetches all the Registration Center attributes for the Registration Center ID and Language Code received
1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
* Registration Center ID - Mandatory
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. System also validates if the response contain the following attributes for the Registration Center ID along with values as applicable
* Registration Center ID
* Registration Center Name
* Longitude
* Latitude
* IsActive
* Center Type Code
* Address
* Working Hours
* Contact Number
* No. of kiosk
* Per kiosk Processing time
* Starting time
* End time
* IsActive

4. In case of Exceptions, system triggers relevant error messages. 

#### D. Fetch Registration Center record based on a Registration center ID, Date and Language Code from the Registration Center Updation/Creation History table


On receiving a request to fetch Registration Center Creation/Updation History Detail with the input parameters (Registration Center ID, Date and Language Code), the system fetches all the attributes of Registration Center from the history table for the Registration Center ID, Date and Language Code received


1. While fetching registration center records the system validates if all required input parameters have been received as listed below for each specific request
* Registration Center ID - Mandatory
* Date - Mandatory
* Language Code - Mandatory
2. The record fetched are  the latest record existing on or before the date received in the input parameter
1. If the mandatory input parameters are missing, system throws the appropriate message. 
1. Validates if the response contain the following attributes for the Registration Center ID along with values as applicable
* Registration Center ID
* Registration Center Name
* Longitude
* Latitude
* IsActive
* Center Type Code
* Address
* Working Hours
* Contact Number
* No. of kiosk
* Per koisk Processing time
* Starting time
* End time
* IsActive
5. In case of Exceptions, system triggers relevant error messages.

#### E. Fetch the List of Holidays based on a Holiday ID and/or Language Code


On receiving a request to fetch the list of Holidays with the input parameters (Holiday ID and/or Language Code), the system fetches the required data as per the input parameter received. 


1. System Fetches all the records of Holiday List if the request does not contain any input parameters
1. If the input parameter is Holiday ID, system will fetch the List of Holidays against the Holiday ID Received for all the languages
1. If the input parameter is Holiday ID and Language Code, fetches the List of Holidays against the Holiday ID and the Language Code Received
1. The system also validates if the response contains all the below attributes for each Holiday Fetched
* Holiday ID
* Holiday Date
* Holiday Name
* IsActive
5. In case of Exceptions, system triggers relevant error messages. Refer “Messages” section

#### F. Fetch Registration Center details based on a Location Code and a Language Code

Upon receiving a  request to fetch the List of Registration Centers with the input parameter (Location Code and Language Code), the system fetches the list of all the Registration Centers against the Location Code and Language Code received with all the attributes for each Registration Center

1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
* Location Code
* Language Code
2. If the mandatory input parameters are missing, throws the appropriate message
1. Validates if the response contains all the Registration Center against the Location Code received with the following attributes for the Registration Centers
* Registration Center ID
* Registration Center Name
* Longitude
* Latitude
* IsActive
* Center Type
* Address
* Working Hours
* Contact Number
* No. of kiosk
* Per koisk Processing time
* Starting time
* End time
* IsActive
4. In case of Exceptions, system triggers relevant error messages

#### G. Fetch Registration Center details based on a Longitude and a Latitude, Proximity Distance and Language Code


On receiving a request  to fetch the List of Registration Centers with the input parameter (Longitude and Latitude, Proximity distance and Language Code), the system fetches the  List of Registration Centers against the input parameters received.

1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
* Longitude
* Latitude
* Proximity Distance
* Language Code
2. If the mandatory input parameters are missing, throw the appropriate message
1. The responses contains the list of all the Registration Centers in the radius of Proximity distance radius of the Longitude and the Latitude received with all the attributes for each Registration Center
1. System fetches the record against the Language Code Received
1. Validates if the response contains all the Registration Center against the Longitude and the Latitude and the Language Code received with the following attributes for the Registration Centers
* Registration Center ID
* Registration Center Name
* Longitude
* Latitude
* IsActive
* Center Type
* Address
* Working Hours
* Contact Number
* No. of kiosk
* Per koisk Processing time
* Starting time
* End time
* IsActive
6. In case of Exceptions, system triggers relevant error messages

#### H. Fetch the List of Registration Centers based on Location Hierarchy Level, text input and a Language Code


Upon receiving a request to fetch the List of Registration centers with input parameters (Location Hierarchy Level, Text Input and a Language Code), the system fetches the List of Registration centers


1. While fetching the list of registration centers the system validates if the request contains the following input parameters
* Location Hierarchy Level - Mandatory
* Text Input - Mandatory
* Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
1. The list of registration center is fetched based on the combination of Location Hierarchy level and Text received.
1. System also fetches the list based on the language code received.
1. The response contain below mentioned attributes for each registration center
* Registration Center ID
* Registration Center Name
* Longitude
* Latitude
* IsActive
* Center Type Code
* Address
* Working Hours
* Contact Number
* No. of kiosk
* Per kiosk Processing time
* Starting time
* End time
* IsActive
6. In case of Exceptions, system triggers relevant error messages. 

#### I. Validate whether a Registration Center is under working hours based on a timestamp received


On receiving a request to fetch Registration Center Details with the input parameters (Registration Center ID and Date-Timestamp), the system determines the status of the Registration center as per the logic defined. 


1. While determining the status of registration center the system validates if all required input parameters have been received as listed below for each specific request
* Registration Center ID - Mandatory
* Date-Timestamp - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message. 
1. Responds with "Accept" message if both the following conditions are met:
* The Registration Center corresponding to the Registration Center ID received must be not on a holiday on the date received in the input parameter.
* The Timestamp received in the input parameter must be greater the Registration Center Opening time and Less than or equal to Closing time + 1 Hour.
4. Responds with the reject scenario if the above two conditions together are not met.
1. E.g., If the Registration center in not on a holiday and its opening and closing time is (9:00 AM to 5:00 PM). Find the sample response below for different timestamp received.
* Timestamp - 4:00 PM - Accepted
* Timestamp - 5:00 PM - Accepted
* Timestamp - 6:00 PM - Accepted
* Timestamp - 6:01 PM - Rejected
6. In case of Exceptions, system trigger relevant error messages



### 2.3 List of Machine Types - Create/Read/Update/Delete

MOSIP system can create Machine Type in Masterdata DB

Upon receiving a request to add Machine Type (e.g., Dongle) with the input parameters (code, name, descr, lang_code and is_active), the system store the Machine Type in the DB

1. Validates if all required input parameters have been received as listed below for each specific request

* code - character (36) - Mandatory
* name - character (64) - Mandatory
* descr - character (128) - Optional
* lang_code - character (3) - Mandatory
* is_active - boolean - Mandatory

2. Respond with the Machine Type Code and Language Code for the Machine Type created successfully

3. This feature also restrict the bulk creation of Master Data

4. Respond to the source with the appropriate message

5. In case of Exceptions, system triggers error messages as received from the Database as listed below
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
Upon receiving a request to add a mapping of Machine and Center with the input parameters (regcntr_id, machine_id, and is_active), the system stores the Mapping of Machine and Center in the DB

1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (10) – Mandatory (refers to a Registration Center stored in Registration Center)
* machine_id - character (10) – Mandatory (refers to a Machine stored in Machine Masterdata)
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

Upon receiving a request to delete a Center-Machine mapping with the input parameters (regcntr_id, machine_id), the system updates the is_deleted flag to true in the Center-Machine mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) - Mandatory
* machine_id - character (36) - Mandatory
2. Deleted record are not be deleted again
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
Upon receiving a request to add a mapping of Device and Center with the input parameters (regcntr_id, device_id, and is_active), the system stores the Mapping of Device and Center in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (10) – Mandatory (refers to a Registration Center stored in Registration Center)
* device_id - character (36) – Mandatory (refers to a Device stored in Device Masterdata)
* is_active - boolean - Mandatory
2. Responds with the Device Id and Center ID for the mapping of Device and Center created successfully
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
Upon receiving a request to delete a Center-Device mapping with the input parameters (regcntr_id, device_id), the system updates the is_deleted flag to true in the Center-Device mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) - Mandatory
* device_id - character (36) - Mandatory
2. Deleted record should not be deleted again
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

Upon receiving a request to add a mapping of Center, Machine and Device with the input parameters (regcntr_id, machine_id, device_id, and is_active), the system store the Mapping of Center, Machine and Device in the DB
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) – Mandatory (refers to a Registration Center stored in Registration Center Masterdata)
* machine_id - character (36) – Mandatory (refers to a Registration Center stored in Registration Center Masterdata)
* device_id - character (36) – Mandatory (refers to a Device stored in Device Masterdata)
* is_active - boolean - Mandatory
2. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device created successfully
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
Upon receiving a request to delete a Center-Machine-Device mapping with the input parameters (regcntr_id, machine_id, device_id), the system updates the is_deleted flag to true in the Center-Machine-Device mapping DB against the input received
1. Validates if all required input parameters have been received as listed below for each specific request
* regcntr_id - character (36) - Mandatory
* machine_id - character (36) - Mandatory
* device_id - character (36) - Mandatory
2. Deleted record are not be deleted again
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
(a) Upon receiving a request to map permissions to the License Key with input parameters (TSP ID, License Key, List of Permissions), the system maps the received permissions to the License Key

(b) Validates if the request contains the following input parameters
   * TSP ID - Mandatory
   * License Key - Mandatory
   * List of Permissions - Mandatory

(c) If the mandatory input parameters are missing, throw the appropriate message

(d) Respond to the source with appropriate message

(e) In case of Exceptions, system triggers relevant error messages

#### 3. Fetch Permissions for a License Key


(a) Upon receiving a request to fetch permissions for a License Key with input parameters (TSP ID, License Key), the system validate if the License Key is Valid

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




