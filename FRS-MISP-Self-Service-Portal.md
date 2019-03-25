## Table Of Content
* [1. Partner Management - SSP](#1-partner-management---ssp) 
    * [1.1 Partners - Create/Read/Update/Delete](#11-partners---createreadupdatedelete) _(MSP_FR_1.1)_
    * [1.2 Policies - Create/Read/Update/Delete](#12-policies---createreadupdatedelete) _(MSP_FR_1.2)_
    * [1.3 Partner-Policy Mapping - Create/Read/Update/Delete](#13-partner-policy-mapping---createreadupdatedelete) _(MSP_FR_1.3)_
    * [1.4 MISP-Partner Mapping - Create/Read/Delete](#14-misp-partner-mapping---createreaddelete) _(MSP_FR_1.4)_
    * [1.5 Validate and Re-issue Digital Certificate to Partner](#15-validate-and-re-issue-digital-certificate-to-partner) _(MSP_FR_1.5)_
    * [1.6 Distribution of Public Keys to Partners](#16-distribution-of-public-keys-to-partners) _(MSP_FR_1.6)_


# 1. Partner Management - SSP
## 1.1 Partners - Create/Read/Update/Delete
### A. Create Partner
Upon receiving request to create a Partner with input parameters (Partner ID, Partner Organization Name, Partner Contact Number, Partner Email ID, Partner Address, IsActive), the system stores the data in the database

Throws an error message if mandatory parameters are missing
### B. Read Partner
Upon receiving request to fetch a Partner with input parameters (Partner ID and/or Partner Organization Name), the system fetches the data existing against the input parameter received.

1. If only Partner ID is received, fetches data against the Partner ID from the database
2. If Partner Organization Name is received, fetches data against the Partner Organization Name from the DB
3. If both Partner ID and Partner Organization Name is received, fetches data against the combination of both the input parameters
4. If the input parameter received is null or empty, fetches all the data
5. Fetches only active data from the database
6. If the data does not exist for input parameters received, throws the appropriate message. 
7. In case of exceptions, system should trigger relevant error messages. 
### C. Update Partner
Upon receiving a request to update a Partner with input parameters (Partner ID, Partner Organization Name, Partner Contact Number, Partner Email ID, Partner Address, IsActive) the system updates the data as per the below steps:

1. Partner ID serves as search criteria to update the record in the database
2. Updates the data received against the data already existing in the database against the Partner ID received
3. If the mandatory input parameters are missing, throws the appropriate message. 
4. In case of exceptions, system triggers relevant error messages. 
### D.  Delete Partner
Upon receiving a request to delete a Partner with input parameters (Partner ID), the system deletes the data as requested

1. Responds to the source with the required message
2. If the mandatory input parameters are missing, throw the appropriate message
3. In case of exceptions, system triggers relevant error messages

## 1.2 Policies - Create/Read/Update/Delete
## 1.3 Partner-Policy Mapping - Create/Read/Update/Delete
## 1.4 MISP-Partner Mapping - Create/Read/Delete
## 1.5 Validate and Re-issue Digital Certificate to Partner
## 1.6 Distribution of Public Keys to Partners
