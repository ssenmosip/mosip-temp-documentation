# 1. ID Repository Overview

ID Repository contains the record of identity for an individual, and provides API based mechanism to store and retrieve identity details by any other MOSIP modules.

When new/update packets are processed by Registration Processor, the identity details of an individual are added or updated in ID Repository. The identity information available in ID Repository is then used by ID Authentication to authenticate an individual.

# 2. ID Services Which Access the Repository 
## 2.1 Target Users

* Registration Processor can use Identity Repo services to create and update Identity information associated with a UIN
* ID Authentication can use Identity Repo services to validate an input UIN and read identity details associated with a UIN
* Resident Services can use Update ID API when an Individual requests for updating ID details like address

## 2.2 Key Features

* Store identity information for a given UIN
* Update Identity information partially or status of UIN
* Read Identity Information associated with a valid UIN
* Read Identity Information for a given RID
* Check status of UIN for validating a UIN

[**Please refer wiki for more details on the key functional and non-Functional requirements of ID rep.**](/mosip/mosip/blob/6c097369722ddff4ec513c15db03b09a6e6ebdc3/docs/design/idrepository/identity-service.md)

# 3. ID Repository services
## 3.1 Store Identity Data and Documents in Database
## 3.2 Retrieve the Stored Identity Details by UIN
## 3.3 Retrieve the Stored Identity Details by RID
## 3.4 Update Identity Data and Documents in Database

 

[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/idrepository/identity-service.md)


### ID Repository API
[**Refer to Wiki for more details on ID Repository API**](ID-Repository-API).

### Process View
[**Link to Process View of ID Repository**](Process-view#5-id-repository-)
