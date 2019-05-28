## Table Of Content

- [1. Identity Service](#1-identity-service-)
  * [1.1 Store identity data and related documents in MOSIP database](#11-store-identity-data-and-related-documents-in-mosip-database-)
  * [1.2 Retrieve the stored identity details and the related documents](#12-retrieve-the-stored-identity-details-and-the-related-documents-)
  * [1.3 Retrieve identity data in ID-Repo by RID](#13-retrieve-identity-data-in-id-repo-by-rid-)
  * [1.4 Update identity data and related documents in MOSIP database](#14-update-identity-data-and-related-documents-in-mosip-database-)
- [2. VID Service](#2-vid-service-)
  * [2.1 Create VID in the defined policy](#21-create-vid-in-the-defined-policy-)
  * [2.2 Maintain the appropriate status of a VID based on the attribute value of a VID](#22-maintain-the-appropriate-status-of-a-vid-based-on-the-attribute-value-of-a-vid-)
  * [2.3 Regenerate a specific type of VID](#23-regenerate-a-specific-type-of-vid-)
  * [2.4 Revoke a VID based on the type](#24-revoke-a-vid-based-on-the-type-)
  * [2.5 Auto-restore a VID on revocation and with auto-restore policy](#25-auto-restore-a-vid-on-revocation-and-with-auto-restore-policy-)
  * [2.6 Retrieve the UIN corresponding to a VID](#26-retrieve-the-uin-corresponding-to-a-vid-)

## 1. Identity Service [**[↑]**](#table-of-content)
### 1.1 Store identity data and related documents in MOSIP database [**[↑]**](#table-of-content)

Upon receiving a request (from Registration Processor) with the following parameters: UIN, id, ver, timestamp, registration-id. The system performs the following steps to store identity data and related documents in MOSIP database:
1. Validates if the request contains “individualBiometrics” or the “parentOrGuardianBiometrics” CBEFF files in the request.
1. The system interacts with biometric SDK to convert the FIR (Fingerprint Image Record) in the CBEFF file to FMR.
1. Appends the FMR (Fingerprint Minutiae Record) to the CBEFF file by using the kernel CBEFF utility service.
1. Stores the files in the distributed file system (DFS).
1. Stores the references to the file in DFS in the database.
1. Validates if the request contains files corresponding to proofOfAddress, or proofOfIdentity, or proofOfRelationship, or proofOfDateOfBirth attributes.
1. Stores the files in the distributed file system.
1. Stores the references to the file in DFS in the database.
1. The system validates if the request contains fullName, dateOfBirth, age, gender, addressLine1, addressLine2, addressLine3, region, province, city, postalCode, phone, email, CNIENumber, localAdministrativeAuthority, parentOrGuardianRIDOrUIN and parentOrGuardianNam in the request.
1. Stores the available identity details of the individual in the database securely.
1. Validate if at least one identity element is present in the request.
1. Validate if a document is present in the input the corresponding category is present in the identity element.
1. The system sends the response with the following parameters id, version, timestamp, status, and the entity element.
1. The default status is ‘ACTIVATED’. The status is configurable.
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

### 1.2 Retrieve the stored identity details and the related documents [**[↑]**](#table-of-content)

Upon receiving a request to retrieve the UIN details with type as an optional parameter, the system performs the following steps to retrieve the stored identity details and the related documents:
1. Retrieves the identity details of the individual corresponding to the UIN in the request.
1. Validates if the type attribute in the request is “demo”.
   * The system references the link for the demo docs from the database and retrieves the demographic documents from the DFS and appends in the response.
1. Validates if the type attribute in the request is “bio”.
   * The system references the link for the bio docs from the database and retrieves the bio documents from the DFS and appends in the response.
1. Validates if the type attribute in the request is “all”.
   * The system references the links for the bio and demo docs from the database and retrieves the documents from the DFS and appends in the response.
1. Sends the response with the following parameters id, version, timestamp, status, and the response element with the appended elements.
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

### 1.3 Retrieve identity data in ID-Repo by RID [**[↑]**](#table-of-content)	

Upon receiving a request to retrieve the UIN details with type as an optional parameter, the system performs the following steps to retrieve identity data in ID-Repo by RID:
1. Retrieves the identity details of the individual corresponding to the RID in the request.
1. Validates if the type attribute in the request is “demo”.
   * The system references the link for the demo docs from the database and retrieves the demographic documents from the DFS and appends in the response.
1. Validates if the type attribute in the request is “bio”.
   * The system references the link for the bio docs from the database and retrieves the bio documents from the DFS and appends in the response.
1. Validates if the type attribute in the request is “all”.
   * The system references the links for the bio and demo docs from the database and retrieves the documents from the DFS and appends in the response.
1. Sends the response with the following parameters id, version, timestamp, status, and the response element with the appended elements.
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).

### 1.4 Update identity data and related documents in MOSIP database [**[↑]**](#table-of-content)

Upon receiving a request to update the UIN details with the following parameters: id, UIN, version, timestamp, registration id, status and identity attributes and documents, the system performs the following steps to update identity data and related documents in MOSIP database:
1. Updates only the identity attributes corresponding to the UIN in the request. 
   * E.g., if e-mail is available in the input, only then the e-mail of the UIN in the database will be updated/replaced.
1. Validates if the demo “documents” are available in the input.
   * The system updates the demographic documents corresponding to the UIN in the DFS.
1. Validates if the biometric “documents” are available in the input.
   * The system updates the biometric documents corresponding to the UIN in the DFS.
1. Validates if both the demo and biometric documents are available in the input.
   * The system updates the biometric and demographic documents corresponding to the UIN in the DFS.
1. The status of the UIN can also be updated to ‘deactivated’ or ‘blocked’.
1. Sends the response with the following parameters id, version, timestamp, status, and the response entity.
1. Please refer Git for more details on the type of [**error messages**](/mosip/mosip/blob/master/docs/requirements/Requirements%20Detailing%20References/ID-Authentication/Sprint%2010/Consolidated%20error%20messages%20V2.2.xlsx).


[Refer to Wiki for more details on **Identity Services**](ID-Repository-API#identity-services-private).

## 2. VID Service [**[↑]**](#table-of-content)
### 2.1 Create VID in the defined policy [**[↑]**](#table-of-content)
### 2.2 Maintain the appropriate status of a VID based on the attribute value of a VID [**[↑]**](#table-of-content)
### 2.3 Regenerate a specific type of VID [**[↑]**](#table-of-content)	
### 2.4 Revoke a VID based on the type [**[↑]**](#table-of-content)
### 2.5 Auto-restore a VID on revocation and with auto-restore policy [**[↑]**](#table-of-content)  
### 2.6 Retrieve the UIN corresponding to a VID [**[↑]**](#table-of-content)	