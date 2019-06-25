## Table Of Content
- [1. ID Repository Overview](#1-id-repository-overview-)
- [2. ID Services Which Access the Repository](#2-id-services-which-access-the-repository-)
  * [2.1 Target Users](#21-target-users-)
  * [2.2 Key Features](#22-key-features-)
- [3. ID Repository services](#3-id-repository-services-)
  * [3.1 Store Identity Data and Documents in Repository](#31-store-identity-data-and-documents-in-repository-)
  * [3.2 Retrieve the Stored Identity Details by UIN](#32-retrieve-the-stored-identity-details-by-uin-)
  * [3.3 Retrieve the Stored Identity Details by RID](#33-retrieve-the-stored-identity-details-by-rid-)
  * [3.4 Update Identity Data and Documents in Repository](#34-update-identity-data-and-documents-in-repository-)
- [ID Repository API](#id-repository-api-)
- [Process View](#process-view-)

## 1. ID Repository Overview [**[↑]**](#table-of-content)

ID Repository contains the record of identity for an individual, and provides API based mechanism to store, retrieve and update identity details by other MOSIP modules.

## 2. ID Services Which Access the Repository [**[↑]**](#table-of-content)
### 2.1 Target Users [**[↑]**](#table-of-content)

* Registration Processor can use Identity Repository services to create and update identity information associated with a UIN
* ID Authentication can use Identity Repository services to validate an input UIN and read identity details associated with a UIN
* Resident Services can use Update ID API when an individual requests for updating ID details like address

### 2.2 Key Features [**[↑]**](#table-of-content)

* Store identity information for a given UIN
* Update identity information partially or status of UIN
* Read identity Information associated with a valid UIN
* Read identity Information for a given RID
* Check status of UIN for validating a UIN

Please refer to section related to [**ID Repository services**](#3-id-repository-services-).

The identity data stored inside the ID repository is encrypted. The Identity Repository is the most critical storage repository and is configured keeping the following non-functional aspects in mind:
* Scalability 
* Performance
* High Availability

[**Please refer wiki for more details on the key non-Functional requirements of ID Repository.**](/mosip/mosip/blob/6c097369722ddff4ec513c15db03b09a6e6ebdc3/docs/design/idrepository/identity-service.md)

## 3. ID Repository services [**[↑]**](#table-of-content)
### 3.1 Store Identity Data and Documents in Repository [**[↑]**](#table-of-content)

Upon receiving the request to store identity details of individual in ID Repository, the system validates input ID attributes in the request against MOSIP ID defined for the country
1. Stores ID JSON of an individual generated during registration
1. Receives and stores individual biometric documents generated during registration
1. Receives and stores documents of proofs provided by individual at the time of registration
1. On successful storage of identity for an individual, status of UIN of the individual is marked as 'ACTIVATED'
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

### 3.2 Retrieve the Stored Identity Details by UIN [**[↑]**](#table-of-content)

Upon receiving a request to retrieve identity details of an individual based on input UIN and type as an optional parameter, the system performs the following steps to retrieve the stored identity details and related documents:
1. Validates if input UIN is 'ACTIVATED'
1. Retrieves latest ID of individual
1. The system retrieves and sends a response based on the type of request as follows:
   * If demographic details are requested, system retrieves demographic documents in the response
   * If biometric details are requested, system retrieves biometric documents in the response
   * If both biometric and demographic details are requested, system retrieves both biometric and demographic documents in the response
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

### 3.3 Retrieve the Stored Identity Details by RID [**[↑]**](#table-of-content)

Upon receiving a request to retrieve identity details of an individual based on input RID and type as an optional parameter, the system performs the following steps to retrieve the stored identity details and related documents:
1. Retrieves UIN mapped to input RID
1. Validates if mapped UIN is 'ACTIVATED'
1. Retrieves latest ID of individual
1. The system retrieves and sends a response based on the type of request as follows:
   * If demographic details are requested, system retrieves demographic documents in the response
   * If biometric details are requested, system retrieves biometric documents in the response
   * If both biometric and demographic details are requested, system retrieves both biometric and demographic documents in the response
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

### 3.4 Update Identity Data and Documents in Repository [**[↑]**](#table-of-content)

Upon receiving a request to update identity details of an individual, the system performs the following steps:
1. Validate if input UIN is 'ACTIVATED'
1. Updates input ID attributes of individual
1. If request contains demographic documents, the system updates with the latest documents received
1. If request contains biometric document of individual, the system updates with the latest documents received
1. If request updates status of UIN as 'DEACTIVATED' or 'BLOCKED', the system updates the same
1. Sends the response with updated ID details of individual
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).


[**Link to design**](/mosip/mosip/blob/0.12.0/docs/design/idrepository/identity-service.md)


#### ID Repository API [**[↑]**](#table-of-content)
[**Refer to Wiki for more details on ID Repository API**](ID-Repository-API).

#### Process View [**[↑]**](#table-of-content)
[**Link to Process View of ID Repository**](Process-view#5-id-repository-)
