## Table Of Content

  * [1. Master Data Management](#1-master-data-management) 
    * [1.1 Location Hierarchy - Create/Read/Update/Delete](#11-location-hierarchy---createreadupdatedelete) _(ADM_FR_1.1)_
    * [1.2 List of Holidays - Create/Read/Update/Delete](#12-list-of-holidays---createreadupdatedelete) _(ADM_FR_1.2)_
    * [1.3 Biometric Authentication Type - Create/Read](#13-biometric-authentication-type---createread) _(ADM_FR_1.3)_
    * [1.4 Biometric Attribute Type - Create/Read](#14-biometric-attribute-type---createread) _(ADM_FR_1.4)_
    * [1.5 Gender - Create/Read/Update/Delete](#15-gender---createreadupdatedelete) _(ADM_FR_1.5)_
    * [1.6 Document Category - Create/Read/Update/Delete](#16-document-category---createreadupdatedelete) _(ADM_FR_1.6)_
    * [1.7 Document Type - Create/Update/Delete](#17-document-type---createupdatedelete) _(ADM_FR_1.7)_
    * [1.8 Applicant Type - Document Category - Document Type Mapping - Read](#18-applicant-type---document-category---document-type-mapping---read) _(ADM_FR_1.8)_
    * [1.9 List of Rejection Reasons - Create/Read](#19-list-of-rejection-reasons---createread) _(ADM_FR_1.9)_
    * [1.10 List of Languages - Create/Read/Update/Delete](#110-list-of-languages---createreadupdatedelete) _(ADM_FR_1.10)_
    * [1.11 List of Titles - Create/Read/Update/Delete](#111-list-of-titles---createreadupdatedelete) _(ADM_FR_1.11)_
    * [1.12 Template File Format - Create/Update/Delete](#112-template-file-format---createupdatedelete) _(ADM_FR_1.12)_
    * [1.13 List of Template Types - Create](#113-list-of-template-types---create) _(ADM_FR_1.13)_
    * [1.14 List of Templates - Create/Read/Update/Delete](#114-list-of-templates---createreadupdatedelete) _(ADM_FR_1.14)_
    * [1.15 List of Blacklisted Words - Create/Read/Update/Delete](#115-list-of-blacklisted-words---createreadupdatedelete) _(ADM_FR_1.15)_
    * [1.16 List of Reason Categories - Create](#116-list-of-reason-categories---create) _(ADM_FR_1.16)_
    * [1.17 List of Applications - Create/Read](#117-list-of-applications---createread) _(ADM_FR_1.17)_
    * [1.18 List of ID Types - Create/Read](#118-list-of-id-types---createread) _(ADM_FR_1.18)_
  * [2. Registration Management](#2-registration-management) 
    * [2.1 Registration Center Type - Create/Update/Delete](#21-registration-center-type---createupdatedelete) _(ADM_FR_2.1)_
    * [2.2 Registration Center - Create/Read/Update/Delete](#22-registration-center---createreadupdatedelete) _(ADM_FR_2.2)_
    * [2.3 List of Machine Types - Create](#23-list-of-machine-types---create) _(ADM_FR_2.3)_
    * [2.4 List of Machine Specifications - Create/Update/Delete](#24-list-of-machine-specifications---createupdatedelete) _(ADM_FR_2.4)_
    * [2.5 List of Machines - Create/Read/Update/Delete](#25-list-of-machines---createreadupdatedelete) _(ADM_FR_2.5)_
    * [2.6 Mappings of Registration Center, Machine and User Mappings - Create/Read/Delete](#26-mappings-of-registration-center-machine-and-user-mappings---createreaddelete) _(ADM_FR_2.6)_
    * [2.7 List of Devices - Create/Read/Update/Delete](#27-list-of-devices---createreadupdatedelete) _(ADM_FR_2.7)_
    * [2.8 List of Device Specifications - Create/Read/Update/Delete](#28-list-of-device-specifications---createreadupdatedelete) _(ADM_FR_2.8)_
    * [2.9 List of Device Types - Create](#29-list-of-device-types---create) _(ADM_FR_2.9)_
    * [2.10 Mappings of Registration Center and Machine - Create/Delete](#210-mappings-of-registration-center-and-machine---createdelete) _(ADM_FR_2.10)_
    * [2.11 Mappings of Registration Center and Device - Create/Read/Delete](#211-mappings-of-registration-center-and-device---createreaddelete) _(ADM_FR_2.11)_
    * [2.12 Mappings of Registration Center, Machine and Device - Create/Delete](#212-mappings-of-registration-center-machine-and-device---createdelete) _(ADM_FR_2.12)_
  * [3. MISP Management](#3-MISP-management) 
    * [3.1 MISP - Create/Read/Update/Delete](#33-misps) _(ADM_FR_3.1)_
      * [3.1.1 License Key Allocation- Create/Read/Update/Delete](#33-misps) _(ADM_FR_3.2)_ 
  
# Admin Services
## 1. Master Data Management
### 1.1 Location Hierarchy - Create/Read/Update/Delete

#### A. Create Location Hierarchy in the Masterdata Database
Upon receiving a request to add Location hierarchy (e.g., Country - Region - Province - City- LAA) with the input parameters (code, name, hierarchy_level, hierarchy_level_name, parent_loc_code ,lang_code and is_active), the system stores the Location hierarchy in the Database

While storing the location hierarchy in the database, the system performs the following steps:
1.  Validates if all required input parameters have been received as listed below for each specific request
    * code - character (36) - Mandatory
    * name - character (128) - Mandatory
    * hierarchy_level - smallint - Mandatory
    * hierarchy_level_name - character (64) - Mandatory
    * parent_loc_code - character (32) - Optional
    * lang_code - character (3) - Mandatory
    * is_active - boolean - Mandatory
2. Responds with the Location Hierarchy created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database

#### B. Check the existence of a Location in Master Database
Upon receiving a request to validate the Location Name with input parameters (Location Name), the system checks the Location Name in the Master Database

While checking the location in the Database, the system performs the following steps:

1. Validates if the request contains the following input parameters
   * Location Name - Mandatory
2. If the mandatory input parameters are missing, throw the appropriate message
1. In case of Exceptions, system triggers relevant error messages
#### C. Fetch Location Hierarchy Levels based on a Language Code
Upon receiving a request to fetch the Location Hierarchy Levels with input parameters (Language Code), the system fetches the Location Hierarchy Levels in the requested language. The following steps are performed by the system: 

1. Validates if the request contains following input parameters (Language Code)
   * Language Code - Mandatory
2. Validates if the response contains the Location Hierarchy Levels with the following attributes
   * Hierarchy Level
   * Hierarchy Name
   * IsActive
3. In case of Exceptions, system triggers relevant error messages
#### D. Fetch the Location Hierarchy Data based on a Location Code and a Language Code

Upon receiving a  request to fetch all the Location Hierarchy Data with input parameters (Location Code and Language Code), the system fetches the Location Hierarchy Data based on requested Location code and language code. The following steps are performed by the system:

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
4. Responds to the source with all the Location Hierarchy Data based on the Location Code
1. In case of Exceptions, system triggers relevant error messages. 

#### E. Fetch the Location Hierarchy Data for the bottom next hierarchy based on a Location Code and a Language Code
Upon receiving a request to fetch all the Location Hierarchy Data with input parameters (Location Code and Language Code), the system fetches the Location Hierarchy Data for the next hierarchy level. The following steps are performed by the system:
1. Validates if the request contains the following input parameters
   * Location Code - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Fetches the Location data of only the child hierarchy of location code received (For e.g., if the location code for a particular Province is received, responds with the data of all the Cities existing in that Province, similarly if location code of a City is received, responds all the data regarding the Local Administrative Authorities existing under that City)
1. Responds to the source with the data fetched
1. In case of Exceptions, system should trigger an error message. 

#### F. Update and Delete a Location in Location Masterdata Database
#### (i) Update
On receiving a  request to update a Location with the input parameters (code, name, hierarchy_level, hierarchy_level_name, parent_loc_code, lang_code and is_active), the system updates the Location in the Location Database
for the code received.

The system performs the following steps to update the location in the Masterdata Database:
 
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
#### (ii) Delete
On receiving a  request to delete a Location with the input parameters (code), the system updates the is_deleted flag to true in the Location Database against the code received. 

The system performs the following steps in order to delete the loaction\s received in the code:
1. Validates if all required input parameters have been received as listed below for each specific request
1. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Code for the Location Hierarchy deleted successfully
   * code - character (36) - Mandatory
7. In case of Exceptions, system triggers relevant error messages. 


### 1.2 List of Holidays - Create/Read/Update/Delete
#### A. Create Holiday data in Masterdata Database

Upon receiving a request to add Holiday Data with the input parameters (location_code, holiday_date, holiday_name, holiday_desc, lang_code and is_active), the system stores the Holiday in the Database. The following steps are performed by the system:
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

On receiving a request to fetch the list of Holidays with the input parameters (Registration Center ID, Year and Language Code), the system fetches the list of Holidays  mapped to a Registration Center and for the year and Language Code received in input parameter as per the below steps:

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
4. Responds to the source with the List of Holidays
1. In case of Exceptions, system triggers relevant error messages

#### C. Update and Delete List of Holiday in  Masterdata Database
#### (i) Update

On receiving a  request to update a Holiday list with the input parameters (id, location_code, holiday_date, holiday_name, holiday_desc, lang_code and is_active), the system updates the Holiday List in the Holiday Database for the code received as per the below steps:

1. Validate if all required input parameters have been received as listed below for each specific request
   * id - integer
   * location_code - character (36) - Mandatory
   * holiday_date - date - Mandatory
   * holiday_name - character (64) - Mandatory
   * holiday_desc - character (128) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
   * New Holiday Date - date - Optional
   * New Holiday Name - character (64) - Optional
   * New Holiday Description - character (128) - Optional
2. For the code received in the request, replaces all the data received in the request against the data existing in the List of Holidays database against the same id.
1. Deleted record are  updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Location Code, Holiday Date, Holiday Name and Language Code for the Holiday updated successfully
1. In case of Exceptions, system triggers relevant error messages.
 
#### (ii) Delete

On receiving a  request to delete a Holiday List with the input parameters (code), the system updates the is_deleted flag to true in the Holiday Database against the code received  as per the below steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * location_code - character (36) - Mandatory
   * holiday_date - date - Mandatory
   * holiday_name - character (64) - Mandatory
2. Delete all records for the code received
1. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Location Code, Holiday Date and Holiday Name for the Holiday deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

### 1.3 Biometric Authentication Type - Create/Read
#### A. Create Biometric Authentication Type in Masterdata Database
On receiving a request to add Biometric Authentication Type (e.g., Fingerprint, Iris) with the input parameters (code, name, descr, lang_code and is_active), the system stores the Biometric Authentication Type in the Database as per the below steps:
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
On receiving a request to fetch the List of Biometric Authentication Type with input parameters (Language Code), the system fetches the List of Biometric Authentication Type against the Language Code as per the below steps:
1. Validates if the request to add Biometric Authentication Type contains the following parameters
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
1. Validates if the response contains the List of Biometric Authentication Type against the Language Code along with the IsActive Flag for each Biometric Authentication Type
1. Responds to the source with List of Biometric Authentication Type
1. In case of Exceptions, system triggers relevant error messages

### 1.4 Biometric Attribute Type - Create/Read

#### A. Create Biometric Attribute in Masterdata Database

On receiving a request to add Biometric Attribute (e.g., Right Thumb, Left Thumb) with the input parameters (code, name, descr, bmtyp_code, lang_code and is_active), the system stores the Biometric Attribute in the Database as per the below steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
   * name - character (64) - Mandatory
   * descr - character (128) - Optional
   * bmtyp_code - character (36) - Mandatory
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Biometric Attribute Code and Language Code for the Biometric Attribute created successfully
1. The component restricts the bulk creation of Master Data
1. Responds to the source with the appropriate message.
1. In case of Exceptions, system triggers error messages as received from the Database

#### B. Fetch the List of Biometric Attributes based on the Biometric Authentication Type and a Language Code

On receiving a request to fetch the List of Biometric Attributes with input parameters (Biometric Authentication Type and Language Code), the system fetches the List of Biometric Attributes against the Biometric Authentication Type and the Language Code Received as per the below steps:
1. Validates if the request contains the following input parameters
   * Biometric Authentication Type - Mandatory
   * Language Code - Mandatory
2. If no data is present in the Database for the input parameter received, responds with an appropriate message.
1. If both the input parameter is missing, responds with all the data.
1. If one of the input parameters is missing, throw the appropriate message. Refer "Messages" section.
1. Validates if the response contains the List of Biometric Attributes with all the attributes against Biometric Authentication Type and Language Code Received
   * Biometric Attribute Code - Mandatory
   * Biometric Attribute Name - Mandatory
   * Biometric Attribute Description - Optional
   * IsActive – Mandatory
6. Responds to the source with the Fetched Data
1. In case of Exceptions, system triggers relevant error messages

### 1.5 Gender - Create/Read/Update/Delete
#### A. Create Gender Types in Masterdata Database

On receiving a request to add a Gender Type with the input parameters (code, name, lang_code and is_active), the system stores the Gender Type in the Database as per the below steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (16) - Mandatory
   * name - character (64) - Mandatory
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Gender Type Code and Language Code for the Gender Type created successfully
1. The component restricts the bulk creation of Master Data
1. Responds to the source with the appropriate message
1. In case of Exceptions, system will trigger error messages as received from the Database.
 
#### B. Update and Delete a Gender Type in Gender Type Masterdata Database

#### (i) Update

On receiving a request to update a Gender Type with the input parameters (code, name, lang_code and is_active), the system updates the Gender Type in the Gender Type Database for the code received as per the below steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (16) - Mandatory
   * name - character (64) - Mandatory
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Gender Type database against the same code.
1. Deleted record are not be updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Gender Type Code and Language Code for the Gender Type updated successfully
1. In case of Exceptions, system triggers relevant error messages.
#### (ii) Delete

On receiving a request to delete a Gender Type with the input parameters (code),  the system updates the is_deleted flag to true in the Gender Type Database against the code received as per the below steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - int - Mandatory
2. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Gender Type Code for the Gender Type deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### C. Check the existence of a Gender in Master Database

On receiving a request to validate the Gender Name with input parameters (Gender Name), the system checks the Gender Name in the Master Database as per the below listed steps:
1. Validates if the request contains the following input parameters
   * Gender Name - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Responds to the source with the appropriate message
1. In case of Exceptions, system triggers relevant error messages

#### D. Fetch the List of Gender Types based on a Language Code

On receiving a request to fetch the List of Gender Types with the input parameters (Language Code), the system fetches the List of Gender Types against the Language Code received as per the below listed steps:
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

On receiving a request to add Document Category with the input parameters (code, name, descr, lang_code and is_active), the system stores the Document Category in the Database as per the below listed steps:
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
1. Responds to the source with the appropriate message.
1. In case of Exceptions, system triggers relevant error messages

#### B. Update and Delete a Document Category in the Document Category Masterdata Database

#### (i) Update

On receiving a request to update a Document Category with the input parameters (code, name, descr, lang_code and is_active), the system update the Document Category in the Document Category Database for the Code received as per the below listed steps:
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

#### (ii) Delete

On receiving a request to delete a Document Category with the input parameters (code), the system updates the is_deleted flag to true in the Document Category Database against the code received as per the below listed steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Document Category Code for the Document Category deleted successfully
1. In case of Exceptions, system triggers relevant error messages

#### C. Fetch list of Document Categories based on a Language Code

On receiving a request to fetch Document Category Details with the input parameters (Language Code), the system fetches all the Document Categories for the Language Code Received as per the below listed steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
1. Validates if the response contains the following attributes for the Document Category Code
   * Document Category Code - Mandatory
   * Document Category Name - Mandatory
   * Document Category Description - Optional
   * IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages

### 1.7 Document Type - Create/Update/Delete

#### A. Create Document Type in Master Data

On receiving a request to add Document Type with the input parameters (code, name, descr, lang_code and is_active), the system stores the Document Type in the Database

Refer below for the process:
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

#### B. Update and Delete a Document Type in the Document Type Masterdata Database

#### (i) Update

On receiving a request to update a Document Type with the input parameters (code, name, descr, lang_code and is_active), the system updates the Document Type in the Document Type Database for the Code received

Refer below for the process:
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
1. In case of Exceptions, system triggers relevant error messages

#### (ii) Delete

On receiving a request to delete a Document Type with the input parameters (code), the system updates the is_deleted flag to true in the Document Type Database against the code received

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Document Category Code for the Document Category deleted successfully
1. In case of Exceptions, system triggers relevant error messages

### 1.8 Applicant Type - Document Category - Document Type Mapping - Read

#### A. Fetch list of Document Categories based on Applicant Type from Masterdata Database

Upon receiving a request  to fetch List of Document Categories with the input parameters (Applicant Type Code), the system fetches all the Document Categories for the Applicant Type Code Received

While fetching the list of documents, the system performs the following steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * Applicant Type Code - Mandatory
2. If the mandatory input parameter is missing, responds with the appropriate error message
1. Validates if the response contains the following attributes for each Document Category Code
   * Document Category Code
   * Name
   * Description
   * Language Code
   * Is Active
4. In case of Exceptions, system triggers relevant error messages


#### B. Fetch List of Document Category-Document Type mappings based on Applicant Type and a List of Language Codes

Upon receiving a request to fetch List of Document Category-Document Type mappings with input parameters (Applicant Type and List of Language Codes), the system fetches the required data

While fetching the data, the system performs the following steps:
1. Validates if the request contains the following input parameters
   * Applicant Type - Mandatory
   * List of Language Codes - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Fetches the Document Category-Document Type mapping for all language codes received in response
1. The response contains the List of Mappings of Document Category and Document Type against each Document Category
1. Each Document Category contains the below attributes
   * Document Category Code
   * Name
   * Description
   * Language Code
   * Is Active
6. Each Document Type contains the below attributes
   * Document Type Code
   * Name
   * Description
   * Language Code
   * Is Active
7. In case of Exceptions, system triggers relevant error messages


#### C. Delete a Document Category-Type mapping in the Document Category-Type mapping Masterdata Database

On receiving a request to delete a Document Category-Type mapping with the input parameters (doccat_code, doctyp_code), the system updates the is_deleted flag to true in the Document Category-Type mapping Database against the input received

The system performs the following steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * doccat_code - character (36) - Mandatory
   * doctyp_code - character (36) - Mandatory
3. Responds with the doc_type Code and doccat_code for the Document Category-Type mapping deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### D. Fetch applicant type based on Individual Type Code, Date of Birth, Gender Type Code and Biometric Exception Type

On receiving a request to get Applicant type with input parameters (Individual Type Code, Date of Birth, Gender Type Code and Biometric Exception Type), the system derives the Applicant Type from the input parameter and performs the following steps:

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

On receiving a request to check the mapping of Applicant Type-Document Category-Document Type mapping parameters (Applicant Type, Document Category Name and Document Type Name), the system checks the mapping and performs the following steps:

1. Validates if the request contains the following input parameters
   * Applicant Type Code
   * Document Category Name
   * Document Type Name
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. If the mapping exists, responds with "Valid".
1. If the mapping does not exist, responds with "Invalid".
1. In case of Exceptions, system triggers relevant error messages

### 1.9 List of Rejection Reasons - Create/Read
#### A. Create a Rejection Reason in Reason List Master Data

Upon receiving a request to add a Reason with the input parameters (code, name, descr, rsncat_code, lang_code and is_active), the system stores the Reason in the Database

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
   * code - character (64) - Mandatory
   * descr - character (256) - Mandatory
   * rsncat_code - character (36) – Mandatory (The parameter rsncat_code refers to a Language stored in Language Masterdata)
   * lang_code - character (3) – Mandatory (The parameter lang_code refers to a Language stored in Language Masterdata)
   * is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Reason Category Code added
   * Code
   * Language Code
   * Rsncat_code (Reason Category Code)

3. Responds to the source with the appropriate message.
4. In case of Exceptions, system triggers relevant error messages. 

#### B. Fetch the requested list of reasons based on Reason Category Code and Language Code

Upon receiving a request to Fetch the requested List of Reasons with the required input parameters (Reason 1. Category Code, Language Code), the system fetches the requested List of reasons stored against the Reason Category Code and Language Code received

The system performs the following steps:
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
1. In case of Exceptions, system triggers relevant error messages as listed below


### 1.10 List of Languages - Create/Read/Update/Delete

#### A. Create List of Languages in Master Data

After receiving a request to add Language Details with the input parameters (code, name, family, native_name and is_active), the system stores the Language Details in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (3) - Mandatory
   * name - character (64) - Mandatory
   * family - character (64) - Optional
   * native_name - character (64) - Optional
   * is_active - boolean - Mandatory
2. Responds with the Language Code for the language successfully created
1. In case of Exceptions, system triggers relevant error messages

#### B. Fetch the List of Languages

After receiving a request to fetch the List of Languages, the system fetches the List of Languages and performs the following steps:

1. Validates if the response contains the List of all Languages with the following attributes
   * Language Code - Mandatory
   * Language Name - Mandatory
   * IsActive – Mandatory
2. Responds to the source with the List of Languages
1. In case of Exceptions, system triggers relevant error messages

#### C. Update and Delete a Language in the List of Languages Masterdata Database

#### (i) Update

After receiving a request to update a Language with the input parameters (code, name, family, native_name and is_active), the system updates the Language Details in the List of languages Database for the Code received in request

The system performs the following steps:


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

#### (ii) Delete

After receiving a request to delete a Language with the input parameters (code), the system updates the is_deleted flag to true in the List of languages Database against the code received in request

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (3) - Mandatory
2. Deleted record should not be deleted again
1. Responds with data not found error  if deleted record is received in the request
1. Responds with the Language Code for the language successfully deleted
1. In case of Exceptions, system triggers relevant error messages. 

### 1.11 List of Titles - Create/Read/Update/Delete

#### A.	Create a Title in Masterdata Database

On receiving a request to add a Title (e.g., MR., Mrs.) with the input parameters (code, name, descr, lang_code and is_active), the system stores the Title in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (16) - Mandatory
   * name - character (64) - Mandatory
   * descr - character (128) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Title Code and Language Code for the Title created successfully
1. In case of Exceptions, system triggers error messages as received from the Database. 

#### B.	Update and Delete a Title in Title Masterdata Database

#### (i) Update

On receiving a request to update a Title with the input parameters (code, name, descr, lang_code and is_active), the system updates the Title in the Title Database for the code received and performs the following steps:

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

#### (i) Delete

On receiving a request to delete a Title with the input parameters (code), the system updates the is_deleted flag to true in the Title Database against the code received

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - int - Mandatory
2. Delete all records for the code received
1. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Title Code for the Title created successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### C. Fetch the List of Titles based on a Language Code

On receiving a request to fetch Title Details with the input parameters (Language Code), the system fetches all the Titles with all the attributes for the Language Code Received

The system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, responds with all the data.
1. Validates if the response contains List of Titles against the received Language Code along with the following attributes for the Title Code
   * Title Code - Mandatory
   * Title Name - Mandatory
   * Title Description - Optional
   * IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages

### 1.12 Template File Format - Create/Update/Delete

#### A. Create Template File Format in Master Data

On receiving a request to add Template File Format with the input parameters (code, descr, lang_code and is_active), the system stores the Template File Format in the Database and performs the following steps:
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

#### B. Create Template File Format in Master Data

Update and Delete a Template File Format in Template File Format Masterdata Database

#### (i) Update

On receiving  a request to update a Template File Format with the input parameters (code, descr, lang_code and is_active), the system updates the Template File Format in the Template File Format Database for the Code received

While updating the Template File Format, the system performs the following steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
   * descr - character (256) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Template File Format database against the same code.
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Template File Format Code and Language Code for the Template File Format updated successfully
1. In case of Exceptions, system triggers relevant error messages

#### (ii) Delete

On receiving  a request to delete a Template File Format with the input parameters (code), the system updates the is_deleted flag to true in the Template File Format Database against the code received

While deleting the Template File Format, the system performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error (Refer Acceptance criteria) if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Template File Format Code for the Template File Format deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

### 1.13 List of Template Types - Create
MOSIP system can create Template Type in the Masterdata Database.

Upon receiving a request to add Template Type (e.g., SMS Notification template - New Registration) with the input 
parameters (code, descr, lang_code and is_active), the system stores the Template Type in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
   * descr - character (256) - Mandatory
   * lang_code - character (3) - Mandatory
   * is_active - boolean – Mandatory

2. Responds with the Template Type Code and Language Code for the Template Type created successfully
3. This component also restricts the bulk creation of Master Data
4. In case of Exceptions, system triggers relevant error messages as listed below.


### 1.14 List of Templates - Create/Read/Update/Delete

#### A. Create Template in the Masterdata Database

On receiving a request to add a Template with the input parameters (id, name, descr, file_format_code, model, file_txt, module_id, module_name, template_typ_code, lang_code and is_active), the system stores the Template in the Database and performs the following steps:

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

Refer below for the process:

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

#### C. Update and Delete a Template in Template Masterdata Database

#### (i) Update

On receiving a request to update a Template with the input parameters (id, name, descr, file_format_code, model, file_txt, module_id, module_name, template_typ_code, lang_code and is_active), the system updates the Template in the Template Database for the id received and performs the following steps:

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

#### (ii) Delete

On receiving a request to delete a Template with the input parameters (id), the system Updates the is_deleted flag to true in the Template Database against the id received and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * id- character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record should be not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Template Id for the Template deleted successfully
1. In case of Exceptions, system triggers relevant error messages

### 1.15 List of Blacklisted Words - Create/Read/Update/Delete

#### A. Create Blacklisted Words in Masterdata Database

Upon receiving a request to add a Blacklisted Word with the input parameters (code, name, descr, lang_code and is_active), the system stores the Blacklisted Word in the Database and performs the following steps:

1. Validates if all required input parameters have been received as listed below for each specific request
   * word - character (128) - Mandatory
   * descr - character (256) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Device ID and Language Code for the Device created successfully
1. The component  restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database. 


#### B. Update and Delete a Blacklisted Word in Blacklisted Word Masterdata Database


#### (i) Update

Upon receiving request to update a Blacklisted Word with the input parameters (code, name, descr, lang_code and is_active), the system updates the Blacklisted Word in the Blacklisted Word Database for the code received and performs the following steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * word- character (128) - Mandatory
   * descr - character (256) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. For the code received in the request, replaces all the data received in the request against the data existing in the Blacklisted Word database against the same code
3. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Word and Language Code for the Blacklisted word updated successfully
1. In case of Exceptions, system triggers relevant error messages as listed below


#### (ii) Delete

Upon receiving a request to delete a Blacklisted Word with the input parameters (code), the system updates the is_deleted flag to true in the Blacklisted Word Database against the code received and performs the following steps:
1. Validates if all required input parameters have been received as listed below for each specific request
   * word- int - Mandatory
2. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Word for the Blacklisted word deleted successfully
1. In case of Exceptions, system triggers relevant error messages as listed below


#### C. Fetch List of Blacklisted words based on a Language Code

Upon receiving a  request to Fetch the List of Blacklisted words with input parameters (Language Code), the system fetches the List of Blacklisted words against the Language Code received

While fetching the black listed words, the system performs the following steps:

1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Validates if the response contains the List of Blacklisted words against Language Code and the corresponding attributes for the Blacklisted word
   * Blacklisted Word
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 

### 1.16 List of Reason Categories - Create

MOSIP system can create a Reason Category in Master Data


Upon receiving a request to add Reason Category with the input parameters (code, name, descr, lang_code and is_active), the system stores the Reason Category in the Database and performs the following steps:

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


### 1.17 List of Applications - Create/Read
#### A. Create a List of Applications in Master Data

Upon receiving a request to add Application with the input parameters (code, name, descr, lang_code and is_active), the system stores the Application in the Database

Refer below for the process:
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
1. In case of Exceptions, system triggers relevant error messages as listed below


#### B. Fetch List of Applications based on received input parameter

#### (i) Fetch the List of all Applications

Upon receiving a request to Fetch List of Applications, the system fetches all the List of Applications and performs the following steps:

1. Validates if the response contains the following attributes for each Application
   * Application ID
   * Application Detail
   * IsActive

2. The response must contain the list of applications in all the languages present in the Database

1. Responds to the source with all the Application attributes.

#### (ii) Fetch the Application detail based on a Language Code and Application ID

Upon receiving a request to Fetch List of Applications with the required input parameters (Application ID, Language Code), the system fetches the Application Detail based on the Application ID and Language Code received

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * Application ID - Mandatory
   * Language Code - Mandatory

2. Responds with the Application Data against the Application ID and Language Code Received

1. Validates if the response contains the following attributes for each Application
   * Application ID
   * Application Detail
   * IsActive

4. Responds to the source with the Application Detail

1. If the mandatory input parameters are missing, responds with all the data.

1. In case of Exceptions, system triggers relevant error messages as listed below


### 1.18 List of ID Types - Create/Read
#### A. Create an ID type in Master Data

Upon receiving a request to add an ID Type with the input parameters (code, name, descr, lang_code and is_active), the system stores the ID Type in the Database

Refer below for the process:

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

4. In case of Exceptions, system triggers relevant error messages as listed below.


#### B. Fetch the List of ID Types based on Language Code

Upon receiving a request to fetch the List of ID Types with input parameters (Language Code), the system fetches the List of ID Types against the Language Code Received

Refer below for the process:

1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. Refer "Messages" section below.

1. Validates if the response contains the List of ID Types with the following attributes
   * ID Type Name
   * ID Type Code
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 


## 2. Registration Management
### 2.1 Registration Center Type - Create/Update/Delete

#### A. Create Registration Center Type in Master Data

On receiving a request to add Registration Center Type with the input parameters (code, name, descr, lang_code and is_active), the system stores the Registration Center Type in the Database

Refer below for the process:

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

	
#### B. Update and Delete a Registration Center Type in the Registration Center Type Masterdata Database

#### (i) Update

On receiving a request to update a Registration Center Type with the input parameters (code, name, descr, lang_code and is_active), the system Updates the Registration Center Type Details in the Registration Center Type Database for the Code received

Refer below for the process:


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

#### (ii) Delete

On receiving a request to delete a Registration Center Type with the input parameters (code), the system updates the is_deleted flag to true in the Registration Center Type Database against the code received

Refer below for the process:


1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
2. Delete all records for the code received
1. Deleted record are deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Registration Center Type code for the Registration Center Type successfully deleted
1. In case of Exceptions, system triggers relevant error messages. 

### 2.2 Registration Center - Create/Read/Update/Delete


#### A. Create a Registration Center record in Masterdata Database

Upon receiving a request to add Registration Center with the input parameters (center_id, name, cntrtyp_code, addr_line1, addr_line2, addr_line3, latitude, longitude, location_code, contact_phone, contact_person, number_of_kiosks, working_hours
per_kiosk_process_time, start_time, end_time, lunch_start_time. lunch_end_time, holiday_loc_code, timezone, lang_code and is_active), the system Stores the Registration Center in the Database

Refer below for the process:

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

#### B. Update and Delete a Registration Center in the List of Registration Center Masterdata Database
#### (i) Update


On receiving a request to update a Registration Center with the input parameters (center_id, name, cntrtyp_code, addr_line1, addr_line2, addr_line3, latitude, longitude, location_code, contact_phone, contact_person, number_of_kiosks, working_hours, per_kiosk_process_time, start_time, end_time, lunch_start_time. lunch_end_time, holiday_loc_code, timezone, lang_code and is_active), the system updates the Registration Center Details in the List of Registration Center Database for the center_id received

Refer below for the process:

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

#### (ii) Delete


Upon receiving a request to delete a Registration Center with the input parameters (center_id), the system updates the is_deleted flag to true in the List of Registration Center Database against the center_id received

Refer below for the process:


1. The system validates if all required input parameters have been received as listed below for each specific request
   * center_id - character (36) - Mandatory 
2. Responds with the Registration Center Code and Language Code for the Registration Center deleted successfully
1. In case of Exceptions, system triggers relevant error messages


#### C. Fetch Registration Center details based on a Registration Center ID and Language Code.


On receiving a request to fetch Registration Center Details with the input parameters (Registration Center ID and Language Code), the system fetches all the Registration Center attributes for the Registration Center ID and Language Code received

Refer below for the process:
1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. System also validates if the response contains the following attributes for the Registration Center ID along with values as applicable
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

Refer below for the process:


1. While fetching registration center records the system validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Date - Mandatory
   * Language Code - Mandatory
2. The record fetched is the latest record existing on or before the date received in the input parameter
1. If the mandatory input parameters are missing, system throws the appropriate message. 
1. Validates if the response contains the following attributes for the Registration Center ID along with values as applicable
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

#### E. Fetch Registration Center details based on a Location Code and a Language Code

Upon receiving a  request to fetch the List of Registration Centers with the input parameter (Location Code and Language Code), the system fetches the list of all the Registration Centers against the Location Code and Language Code received with all the attributes for each Registration Center

Refer below for the process:

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

#### F. Fetch Registration Center details based on a Longitude and a Latitude, Proximity Distance and Language Code


On receiving a request  to fetch the List of Registration Centers with the input parameter (Longitude and Latitude, Proximity distance and Language Code), the system fetches the  List of Registration Centers against the input parameters received.

Refer below for the process:

1. While fetching the registration center details the system validates if all required input parameters have been received as listed below for each specific request
   * Longitude
   * Latitude
   * Proximity Distance
   * Language Code
2. If the mandatory input parameters are missing, throw the appropriate message
1. The responses contain the list of all the Registration Centers in the radius of Proximity distance radius of the Longitude and the Latitude received with all the attributes for each Registration Center
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

#### G. Fetch the List of Registration Centers based on Location Hierarchy Level, text input and a Language Code


Upon receiving a request to fetch the List of Registration centers with input parameters (Location Hierarchy Level, Text Input and a Language Code), the system fetches the List of Registration centers

Refer below for the process:


1. While fetching the list of registration centers the system validates if the request contains the following input parameters
   * Location Hierarchy Level - Mandatory
   * Text Input - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
1. The list of registration center is fetched based on the combination of Location Hierarchy level and Text received.
1. System also fetches the list based on the language code received.
1. The response contains below mentioned attributes for each registration center
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

#### H. Validates whether a Registration Center is under working hours based on a timestamp received


On receiving a request to fetch Registration Center Details with the input parameters (Registration Center ID and Date-Timestamp), the system determines the status of the Registration center as per the logic defined. 

Refer below for the process:


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
6. In case of Exceptions, system triggers relevant error messages


### 2.3 List of Machine Types - Create

Upon receiving a request to add Machine Type (e.g., Dongle) with the input parameters (code, name, descr, lang_code and is_active), the system stores the Machine Type in the Database

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
   * name - character (64) - Mandatory
   * descr - character (128) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Machine Type Code and Language Code for the Machine Type created successfully

3. This feature also restricts the bulk creation of Master Data

4. Responds to the source with the appropriate message

5. In case of Exceptions, system triggers error messages as received from the Database.

### 2.4 List of Machine Specifications - Create/Update/Delete


#### A. Create Machine Specifications in the Masterdata Database


On receiving a request to add Machine Specifications with the input parameters (name, brand, model, mtyp_code, min_driver_ver, descr, lang_code and is_active), the system stores the Machine Specifications in the Database 

Refer below for the process:

1. While creating machine specification in Database the system validates if all required input parameters have been received as listed below for each specific request
   * Id - character (36) - Mandatory
   * name - character (64)- Mandatory
   * brand - character (32)- Mandatory
   * model - character (16)- Mandatory
   * mtyp_code - character (36)- Mandatory
   * min_driver_ver - character (16)- Mandatory
   * descr - character (256)- Optional
   * lang_code - character (3)- Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Machine Specification ID and Language Code for the Machine Specification created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database

#### B. Update and Delete a Machine Specification in the Machine Specification Masterdata Database

#### (i) Update


On receiving a request to update a Machine Specification with the input parameters (id, name, brand, model, mtyp_code, min_driver_ver, descr, lang_code and is_active), the system updates the Machine Specification Details in the Machine Specification Database for the id received


While updating the Machine Specification the system validates the following


1. Validates if all required input parameters have been received as listed below for each specific request
   * id - character (36) - Mandatory
   * name - character (64)- Mandatory
   * brand - character (32)- Mandatory
   * model - character (16)- Mandatory
   * mtyp_code - character (36)- Mandatory
   * min_driver_ver - character (16)- Mandatory
   * descr - character (256)- Optional
   * lang_code - character (3)- Mandatory
   * is_active - boolean - Mandatory
2. For the id received in the request, replaces all the data received in the request against the data existing in the Machine Specification database against the same id.
1. Deleted record are not updated
1. Responds with data not found error, if deleted record is received in the request
1. Responds with the Machine Specification ID and Language Code for the Machine Specification updated successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### (ii) Delete


On receiving a request to delete a Machine Specification with the input parameters (id), the system Updates the is_deleted flag to true in the Machine Specification Database against the id received

Refer below for the process:


1. While deleting the machine specifications the system validates if all required input parameters have been received as listed below for each specific request
   * id - character (36) - Mandatory
2. Delete all records for the id received
1. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Machine Specification ID for the Machine Specification deleted successfully
1. In case of Exceptions, system triggers relevant error messages


### 2.5 List of Machines - Create/Read/Update/Delete

#### A. Create a Machine in Masterdata Database

On receiving a request to add Machine with the input parameters (machine_id, name, mac_address, serial_num, ip_address, validity_end_dtimes, mspec_id, lang_code and is_active), the system Stores the Machine Details in the Database

Refer below for the process:

1. While creating the machine IDs the system validates if all required input parameters have been received as listed below for each specific request
   * machine_id - character (36) - mandatory
   * name - character (64) - mandatory
   * mac_address - character (64) - mandatory
   * serial_num - character (64) - mandatory
   * ip_address- character (17) - optional
   * validity_end_dtimes - timestamp
   * mspec_id - character (36) - mandatory
   * lang_code - character (3) - mandatory
   * is_active - boolean - mandatory


2. Responds with the Machine ID and Language Code for the Machine created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database. 


#### B. Update and Delete a Machine in the List of Machines Masterdata Database

#### (i) Update


On receiving a request to update a Machine with the input parameters (machine_id, name, mac_address, serial_num, ip_address, validity_end_dtimes, mspec_id, lang_code and is_active), the system Updates the Machine Details in the List of Machines Database for the machine_id received

Refer below for the process:


1. While updating the machine ID the system Validates if all required input parameters have been received as listed below for each specific request
   * machine_id - character (36) - mandatory
   * name - character (64) - mandatory
   * mac_address - character (64) - mandatory
   * serial_num - character (64) - mandatory
   * ip_address- character (17) - optional
   * validity_end_dtimes - timestamp
   * mspec_id - character (36) - mandatory
   * lang_code - character (3) - mandatory
   * is_active - boolean - mandatory
2. For the machine_id received in the request, replaces all the data received in the request against the data existing in the List of Machines database against the same machine_id.
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Machine ID and Language Code for the Machine updated successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### (ii) Delete

On receiving a request to delete a Machine with the input parameters (machine_id), the system Updates the is_deleted flag to true in the List of Machines Database against the machine_id received

Refer below for the process:


1. While deleting the machine IDs the system Validates if all required input parameters have been received as listed below for each specific request
   * machine_id - character (36) - Mandatory
2. Delete all records for the id received
1. Deleted record are not deleted again
1. Responds with data not found error  if deleted record is received in the request
1. Responds with the Machine ID for the Machine deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 


#### C. Fetch Machine Registration/Updation History detail based on a Machine ID and Language Code


Upon receiving a request to fetch Machine History Registration/Updation Detail with the input parameters (Machine ID, Date and Language Code), the system Fetches all the attributes of Machine from the history table for the Machine ID, Date and Language Code received

The record fetched is the latest record existing on or before the date received in the input parameter

Refer below for the process:


1. While fetching the machine registration and updation history the system Validates if all required input parameters have been received as listed below for each specific request
   * Machine ID - Mandatory
   * Date - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message
1. Validates if the response contains the following attributes for the Machine ID and Language Code Received
   * Machine ID
   * Machine Name
   * Mac Address
   * IP Address
   * Serial Number
   * Machine Spec ID
   * IsActive
4. In case of Exceptions, system triggers relevant error messages

#### D. Fetch Machine Details based on a Machine ID and a Language Code


On receiving a request to Fetch Machine Details with the input parameters (Machine ID and Language Code), the system Fetches all the Machine attributes for the Machine ID and the Language Code Received

Refer below for the process:

1. While fetching the machine IDs the system Validates if all required input parameters have been received as listed below for each specific request
   * Machine ID - Mandatory
   * Language Code
2. If the request has come for fetching all the machine details, responds with all the list of machines
1. If the mandatory input parameters are missing, throws the appropriate message. 
1. Validates if the response contains the following attributes for the Machine ID
   * Machine ID
   * Machine Name
   * Mac Address
   * IP Address
   * Serial Number
   * Machine Spec ID
   * IsActive
5. In case of Exceptions, system triggers relevant error messages. 


### 2.6 Mappings of Registration Center, Machine and User Mappings - Create/Read/Delete


#### A. Create a mapping record of Center, User and Machine in Center-User-Machine Mapping Masterdata Database

On receiving a request to add a mapping of Center, User and Machine with the input parameters (regcntr_id, usr_id, machine_id and is_active), the system Stores the Mapping of Center, User and Machine in the Database

Refer below for the process:


1. While mapping the system Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (10) - Mandatory
   * usr_id- character (36) - Mandatory
   * machine_id - character (10) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Center ID, Machine ID ad User ID for the Center, User and Machine mapping created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database.


#### B. Delete a Center-Machine-User mapping in the Center-Machine-User mapping Masterdata Database

On receiving a request to delete a Center-Machine-User mapping with the input parameters (regcntr_id, machine_id, usr_id), the system Updates the is_deleted flag to true in the Center-Machine-User mapping Database against the input received

Refer below for the process:


1. While deleting the system Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (36) - Mandatory
   * machine_id - character (36) - Mandatory
   * usr_id - character (36) - Mandatory
2. Responds with the Center ID, Machine ID ad User ID for the Center, User and Machine mapping deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### C. Fetch Mapping History of Registration Center, Machine and User based on Registration Centre ID, Machine ID, User ID and Date

On receiving a request to fetch Mapping History of Registration, Machine and User with input parameters (Registration Centre ID, Machine ID, User ID and Date), the system  Fetches all the attributes of Registration, Machine and User Mapping from the history table for the Machine ID and Date received

The record fetched is the latest record existing on or before the date received in the input parameter

Refer below for the process:


1. While fetching the mappings the system Validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Machine ID - Mandatory
   * User ID - Mandatory
   * Date - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message.
1. Validates if the response contains following attributes
   * Registration Center ID
   * Machine ID
   * User ID
   * IsActive
4. In case of Exceptions, system triggers relevant error messages. 


### 2.7 List of Devices - Create/Read/Update/Delete

#### A. Create a Device in Masterdata Database

On receiving request to add a device with the input parameters (name, mac_address, serial_num, ip_address, dspec_id, validity_end_date, lang_code and is_active), the system Stores the device in the Database

Refer below for the process:

1. While creating a device the system Validates if all required input parameters have been received as listed below for each specific request
   * name - character (64) - Mandatory
   * mac_address - character (64) - Mandatory
   * serial_num - character (64) - Mandatory
   * ip_address - character (17) - Optional
   * dspec_id - character (36) - Mandatory
   * validity_end_date - date - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Responds with the Device ID and Language Code for the Device created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database.

 
#### B. Fetch all the List of Devices based on Device Type and Language Code


On receiving request to Fetch list of all Device with the requirement input parameter (Language Code and/or Device Type), the system Fetches all the Devices against the Language Code and/or Device Type as requested

Refer below for the process:


1. While fetching the device types the system Validates if the request contains the following input parameters
   * Device Type - Optional
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message. 
1. If the input parameters contain only Language Code:
   * The response contains all the list of devices for all device types against the Languages code received
4. If the input parameters contain both Device Type and Language Code:
   * The response  contains the list of devices against the Languages code for that Device Type only
5. After validation, the above listed parameters system responds with an appropriate message if data does not exist against the Language code/Device Type received. 
1. Validates if the response contains the following attributes for each Device ID, if the input parameters contain only Language Code:
   * Device ID - Mandatory
   * Machine Name - Mandatory
   * Mac Address - Mandatory
   * IP address - Optional
   * Serial Number - Mandatory
   * Device Spec ID - Mandatory
   * IsActive - Mandatory
7. Validates if the response contains the following attributes for each Device ID, if the input parameters contain Device Type and Language Code:
   * Device Type-Mandatory
   * Device ID - Mandatory
   * Machine Name - Mandatory
   * Mac Address - Mandatory
   * IP address - Optional
   * Serial Number - Mandatory
   * Device Spec ID - Mandatory
   * IsActive - Mandatory
8. In case of Exceptions, system triggers relevant error messages. 


#### C. Fetch Device Registration/Update History detail based on a Device ID and Language Code

On receiving request to fetch Device History Registration/Update Detail with the input parameters (Device ID, Date and Language Code), the system fetches all the attributes of Device from the history table for the Device ID, Date and Language Code received


The record fetched is the latest record existing on or before the date received in the input parameter

Refer below for the process:


1. While fetching the device registration and update history the system validates if all required input parameters have been received as listed below for each specific request
   * Device ID - Mandatory
   * Date - Mandatory
   * Language Code - Mandatory
2. If the mandatory input parameters are missing, system throws the appropriate message
1. Validates if the response contains the following attributes for the Device ID and Language Code Received
   * Device ID - Mandatory
   * Device Name - Mandatory
   * Mac Address - Mandatory
   * IP address - Optional
   * Serial Number - Mandatory
   * Device Spec ID - Mandatory
   * Validity Time - Optional
   * Language Code - Mandatory
   * IsActive - Mandatory
4. In case of Exceptions, system triggers relevant error messages. 

#### D. Update and Delete a Device in the List of Devices Masterdata Database

#### (i) Update

Upon receiving a request update a Device with the input parameters (id, name, mac_address, serial_num, ip_address, dspec_id, validity_end_date, lang_code and is_active), the system Updates the Device Details in the List of Devices Database for the id received

Refer below for the process:

1. While updating the device in device type list the system Validates if all required input parameters have been received as listed below for each specific request
   * id - character (36) - Mandatory
   * name - character (64) - Mandatory
   * mac_address - character (64) - Mandatory
   * serial_num - character (64) - Mandatory
   * ip_address - character (17) - Optional
   * dspec_id - character (36) - Mandatory
   * validity_end_date - date - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. For the id received in the request, replaces all the data received in the request against the data existing in the List of Devices database against the same id.
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device ID and Language Code for the Device updated successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### (ii) Delete

Upon receiving a request to delete a Device with the input parameters (id) and Update the is_deleted flag to true in the List of Devices Database against the id received

Refer below for the process:


1. While deleting the device in the device list the system validates if all required input parameters have been received as listed below for each specific request
   * id - character (36) - Mandatory
2. Delete all records for the id received
1. Deleted record are not  deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device ID for the Device deleted successfully
1. In case of Exceptions, system triggers relevant error messages
	

### 2.8 List of Device Specifications - Create/Read/Update/Delete

#### A. Create Device Specifications in Master Data


On receiving request to add Device Specifications with the input parameters (name, brand, model, dtype_code, min_driver_ver, descr, lang_code and is_active), the system Stores the Device Specifications in the Database

Refer below for the process:


1. While storing the device specifications the system Validates if all required input parameters have been received as listed below for each specific request
   * name - character (64) - Mandatory
   * brand - character (32) - Mandatory
   * model - character (16) - Mandatory
   * dtyp_code - character (36) - Mandatory
   * min_driver_ver - character (16) - Mandatory
   * descr - character (256) - Mandatory
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Device Specification added
   * Device Specification ID
3. Responds with the Device Specification ID and Language Code for the Device Specification created successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### B. Fetch List of Device Specifications based on a Language Code

On receiving request to fetch the List of Device Specifications with input parameters (Language Code and/or Device Type) the system fetches the List of Device Specifications against the Language Code and/or Device Type

While fetching the List of Device Specifications against the Language Code and/or Device Type the system performs the following steps
1. Validates if the request contains the following input parameters
   * Language Code - Mandatory
   * Device Type - Optional
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. If the input parameters contain only Language Code:
   * The response contains all the list of device specs against all the devices for the requested Language Code
4. If the input parameters contain Device Type and Language Code:
   * The response contains only the list of device specs against the requested device type for the requested Language Code
5. Validates if the response contains the List of Device Specifications with the following attributes, if the input parameters contain only Language Code
   * Device Specification ID
   * Device Name
   * Device Brand
   * Device Model
   * Device Type
   * Minimum Driver Version
   * IsActive
6. Validates if the response contains the List of Device Specifications with the following attributes, if the input parameters contain Device Type and Language Code
   * Device Type
   * Device Specification ID
   * Device Name
   * Device Brand
   * Device Model
   * Device Type
   * Minimum Driver Version
   * IsActive
7. In case of Exceptions, system triggers relevant error messages


#### C. Update and Delete a Device Specification in the Device Specification Masterdata Database

#### (i) Update

On receiving a request to update a Device Specification with the input parameters (id, name, brand, model, dtype_code, min_driver_ver, descr, lang_code and is_active) the system updates the Device Specification Details in the Device Specification Database for the id received


While updating the device specifications the system performs the following steps
1. Validates if all required input parameters have been received as listed below for each specific request
   * id - character (36) - Mandatory
   * name - character (64) - Mandatory
   * brand - character (64) - Mandatory
   * model - character (16) - Mandatory
   * dtyp_code - character (36) - Mandatory
   * min_driver_ver - character (16) - Mandatory
   * descr - character (256) - Mandatory
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. For the id received in the request, replaces all the data received in the request against the data existing in the Device Specification database against the same id
1. Deleted record are not updated
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device Specification ID and Language Code for the Device Specification updated successfully
1. In case of Exceptions, system triggers relevant error messages. 

#### (ii) Delete


On receiving a request to delete a Device Specification with the input parameters (id) the system updates the is_deleted flag to true in the Device Specification Database against the id received

While deleting the device specifications the system performs the following steps
1. Validates if all required input parameters have been received as listed below for each specific request
   * id - character (36) - Mandatory
2. Delete all records for the id received
1. Deleted record are not deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with dependency found error if a record to be deleted is used as foreign key in the dependent table
1. Responds with the Device Specification ID for the Device Specification deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

### 2.9 List of Device Types - Create
#### A. Create Device Type in Master Data


Upon receiving a request to add Device Type with the input parameters (code, name, descr, lang_code and is_active), the system Stores the Device Type in the Database

Refer below for the process:


1. While creating device type the system validates if all required input parameters have been received as listed below for each specific request
   * code - character (36) - Mandatory
   * name - character (64) - Mandatory
   * descr - character (128) - Optional
   * lang_code - character (3) - Mandatory
   * is_active - boolean - Mandatory
2. Validates if the response contains the following attributes for a Device Type added
   * Code
   * Language Code
3. Responds with the Device Type Code and Language Code for the Device Type created successfully
1. In case of Exceptions, system triggers relevant error messages

### 2.10 Mappings of Registration Center and Machine - Create/Delete
#### A. Create a mapping record of Machine and Center in Machine-Center Mapping Masterdata Database
Upon receiving a request to add a mapping of Machine and Center with the input parameters (regcntr_id, machine_id, and is_active), the system stores the Mapping of Machine and Center in the Database

Refer below for the process:

1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (10) – Mandatory (refers to a Registration Center stored in Registration Center)
   * machine_id - character (10) – Mandatory (refers to a Machine stored in Machine Masterdata)
   * is_active - boolean - Mandatory
2. Responds with the Machine Id and Center ID for the mapping of Machine and Center created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database. 


#### B. Delete a Center-Machine mapping in the Center-Machine mapping Masterdata Database

Upon receiving a request to delete a Center-Machine mapping with the input parameters (regcntr_id, machine_id), the system updates the is_deleted flag to true in the Center-Machine mapping Database against the input received

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (36) - Mandatory
   * machine_id - character (36) - Mandatory
2. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request.
1. Responds with the Machine Id and Center ID for the mapping of Machine and Center deleted successfully
1. In case of Exceptions, system triggers relevant error messages .


### 2.11 Mappings of Registration Center and Device - Create/Read/Delete
#### A. Create a mapping record of Device and Center in Device-Center Mapping Masterdata Database
Upon receiving a request to add a mapping of Device and Center with the input parameters (regcntr_id, device_id, and is_active), the system stores the Mapping of Device and Center in the Database

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (10) – Mandatory (refers to a Registration Center stored in Registration Center)
   * device_id - character (36) – Mandatory (refers to a Device stored in Device Masterdata)
   * is_active - boolean - Mandatory
2. Responds with the Device Id and Center ID for the mapping of Device and Center created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database. 


#### B. Delete a Center-Device mapping in the Center-Device mapping Masterdata Database
Upon receiving a request to delete a Center-Device mapping with the input parameters (regcntr_id, device_id), the system updates the is_deleted flag to true in the Center-Device mapping Database against the input received

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (36) - Mandatory
   * device_id - character (36) - Mandatory
2. Deleted record should not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device Id and Center ID for the mapping of Device and Center deleted successfully
1. In case of Exceptions, system triggers relevant error messages.


#### C. Fetch Device-Center History record based on the timestamp received

On receiving a request to fetch Mapping History of Center and Device with input parameters (Registration Center ID, Device ID and Date Timestamp) the system fetches all the attributes of Center and Device Mapping from the history table for the Registration Center ID, Device ID and Date received


The record fetched is the latest record existing on or before the date received in the input parameter


While fetching the attributes of Center and Device Mapping from the history table the system performs the following steps
1. Validates if all required input parameters have been received as listed below for each specific request
   * Registration Center ID - Mandatory
   * Device ID - Mandatory
   * Date Timestamp - Mandatory
2. If the mandatory input parameters are missing, throws the appropriate message. 
1. Validates if the response contains following attributes
   * Registration Center ID
   * Device ID
   * IsActive
   * Effective date
4. In case of Exceptions, system triggers relevant error messages

### 2.12 Mappings of Registration Center, Machine, and Device - Create/Delete

### A. Create a mapping record of Center, Machine and Device in Center-Machine-Device Mapping Masterdata Database

Upon receiving a request to add a mapping of Center, Machine and Device with the input parameters (regcntr_id, machine_id, device_id, and is_active), the system stores the Mapping of Center, Machine and Device in the Database

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (36) – Mandatory (refers to a Registration Center stored in Registration Center Masterdata)
   * machine_id - character (36) – Mandatory (refers to a Registration Center stored in Registration Center Masterdata)
   * device_id - character (36) – Mandatory (refers to a Device stored in Device Masterdata)
   * is_active - boolean - Mandatory
2. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device created successfully
1. The component restricts the bulk creation of Master Data
1. In case of Exceptions, system triggers error messages as received from the Database. 


#### B. Delete a Center-Machine-Device mapping in the Center-Machine-Device mapping Masterdata Database
Upon receiving a request to delete a Center-Machine-Device mapping with the input parameters (regcntr_id, machine_id, device_id), the system updates the is_deleted flag to true in the Center-Machine-Device mapping Database against the input received

Refer below for the process:
1. Validates if all required input parameters have been received as listed below for each specific request
   * regcntr_id - character (36) - Mandatory
   * machine_id - character (36) - Mandatory
   * device_id - character (36) - Mandatory
2. Deleted record are not be deleted again
1. Responds with data not found error if deleted record is received in the request
1. Responds with the Device Id, Machine ID and Center ID for the mapping of Center, Machine and Device deleted successfully
1. In case of Exceptions, system triggers relevant error messages. 

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-masterdata.md)


## 3. MISP Management 
### 3.1 MISP - Create/Read/Update/Delete
### 3.1.1 License Key Allocation


[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-licensekeymanager.md)








