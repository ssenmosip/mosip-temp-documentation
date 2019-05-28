## Table Of Content

- [1. Identity Service](#1-identity-service-)
  * [1.1 Store identity data and related documents in MOSIP database](#11-store-identity-data-and-related-documents-in-mosip-database-)
  * [1.2 Retrieve the stored identity details and the related documents](#12-retrieve-the-stored-identity-details-and-the-related-documents-)
  * [1.3 Retrieve identity data in ID-Repo by RID](#13-retrieve-identity-data-in-id-repo-by-rid-)
  * [1.4 Store identity data and related documents in MOSIP database](#14-store-identity-data-and-related-documents-in-mosip-database-)
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
1. Please refer Git for more details on the type of error messages.

### 1.2 Retrieve the stored identity details and the related documents [**[↑]**](#table-of-content)
### 1.3 Retrieve identity data in ID-Repo by RID [**[↑]**](#table-of-content)	
### 1.4 Store identity data and related documents in MOSIP database [**[↑]**](#table-of-content)
## 2. VID Service [**[↑]**](#table-of-content)
### 2.1 Create VID in the defined policy [**[↑]**](#table-of-content)
### 2.2 Maintain the appropriate status of a VID based on the attribute value of a VID [**[↑]**](#table-of-content)
### 2.3 Regenerate a specific type of VID [**[↑]**](#table-of-content)	
### 2.4 Revoke a VID based on the type [**[↑]**](#table-of-content)
### 2.5 Auto-restore a VID on revocation and with auto-restore policy [**[↑]**](#table-of-content)  
### 2.6 Retrieve the UIN corresponding to a VID [**[↑]**](#table-of-content)	