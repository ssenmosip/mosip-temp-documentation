## Table Of Content
- [Data services](#data-services)
  * [1. Data mapper](#1-data-mapper)
  * [2. Data Access Manager](#2-data-access-manager)
  * [3. Sync Handler](#3-sync-handler)
  * [4. ID Generator and Validator](#4-id-generator-and-validator)
    * [4.1 ID Validator](#41-id-validator)
      * [4.1.1 Static Pin Validator](#411-static-pin-validator)
      * [4.1.2  UIN Validator](#412--uin-validator)
      * [4.1.3 PRID Validator](#413-prid-validator)
      * [4.1.4 VID Validator](#414-vid-validator)
      * [4.1.5 RID Validator](#415-rid-validator)
      * [4.1.6 TSP ID Validator](#416-tsp-id-validator)
    * [4.2 ID Generator](#42-id-generator)
      * [4.2.1 RID Generator](#421-rid-generator)
      * [4.2.2 Machine ID Generator](#422-machine-id-generator)
      * [4.2.3 Registration Center ID Generator](#423-registration-center-id-generator)
      * [4.2.4 TSP ID Generator](#424-tsp-id-generator)
      * [4.2.5 PRID Generator](#425-prid-generator)
      * [4.2.6 VID Generator](#426-vid-generator)
      * [4.2.7 Token ID Generator](#427-token-id-generator)
# Data services
## 1. Data mapper
## 2. Data Access Manager
## 3. Sync Handler
## 4. ID Generator and Validator
### 4.1 ID Validator
#### 4.1.1 Static Pin Validator
MOSIP system can perform Static PIN validation against a defined Static PIN logic.

Upon receiving a request to perform data validation on Static PIN with input parameters (Static PIN), the system validate Static PIN as per the Static PIN generation logic and responds with the required result (Valid/Invalid).

1. Validate if the request has the following input parameters.
* Static PIN
2. Validate if the Static PIN is of configured length. (Current configured length = 6)
1. Validate if the Static PIN is only numerical.

In case of Exceptions, system should trigger relevant error messages. Refer “Messages” section
### <p align="left"> **1. Type: Success – Info Message**

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|Static PIN is Valid|True|NA|

### <p align="left"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|Static PIN in Invalid|Static PIN length Must be <Length configured>|KER-IDV-501|
|Static PIN in not numeric|	Static PIN length must be numeric>|	KER-IDV-502|
|Static PIN input parameter is missing	|Input parameter is missing	|KER-IDV-503|





#### 4.1.2  UIN Validator
#### 4.1.3 PRID Validator
#### 4.1.4 VID Validator
MOSIP system can perform VID validation against a defined VID policy

Upon receiving a request to validate the VID with input parameters (UIN), the system validates the VID against the defined VID policy
1. Validates if the VID is of configured length.
1. If no length is configured, validate if VID length is of 16 digits
1. Validates the VID by verifying the checksum
1. Validates if the VID received follows the VID generation logic listed in User Story

Respond to the source with appropriate message and Raise an alert in case of listed exceptions 

### <p align="left"> **1. Type: Success – Info Message**

<center>

|**Scenario**|**Message**|**Message Code**|
|:------:|:------:|:------:|
|VID is Valid|"Valid"|NA|
|VID is Invalid|"Invalid"|NA|



### <p align="CENTER"> **2. Type: Error/Failure – Info Message**
|**Scenario**|**Message**|**Message Code**|
|:------:|------|:------:|
|MosipInvalidIDException|Entered VID should not be empty or null.|KER-IDV-VID-001|
|MosipInvalidIDException|Entered VID should not contain any sequential and repeated block of number for 2 or more than two digits|KER-IDV-VID-002
|MosipInvalidIDException|Entered VID length should be 16 digit|	KER-IDV-VID-003|
|MosipInvalidIDException|Entered VID should not contain any alphanumeric characters|KER-IDV-VID-004|
|MosipInvalidIDException|Entered VID should match checksum|KER-IDV-VID-005|
|MosipInvalidIDException|Entered VID should not contain Zero or One as first Digit|KER-IDV-VID-006|






#### 4.1.5 RID Validator
#### 4.1.6 TSP ID Validator
### 4.2 ID Generator
#### 4.2.1 RID Generator
#### 4.2.2 Machine ID Generator
#### 4.2.3 Registration Center ID Generator
#### 4.2.4 TSP ID Generator
#### 4.2.5 PRID Generator
#### 4.2.6 VID Generator
#### 4.2.7 Token ID Generator



FORMAT: 1A

# Tables API 
Note: Tables can be handcrafted or generated at <http://www.tablesgenerator.com/markdown_tables>.

## Table 1
**Discussion option 1**

| Tables   |      Are      |  Cool |
|----------|:-------------:|------:|
| col 1 is |  left-aligned | $1600 |
| col 2 is |    centered   |   $12 |
| col 3 is | right-aligned |    $1 |

# Message [/pages]
## Create a Message [POST]

### Table 2
**Discussion option 2**

| Tables   |      Are      |  Cool |
|----------|:-------------:|------:|
| col 1 is |  left-aligned | $1600 |
| col 2 is |    centered   |   $12 |
| col 3 is | right-aligned |    $1 |

+ Request (application/json)

    ## Table 3
    **Discussion option 3**

    | Tables   |      Are      |  Cool |
    |----------|:-------------:|------:|
    | col 1 is |  left-aligned | $1600 |
    | col 2 is |    centered   |   $12 |
    | col 3 is | right-aligned |    $1 |

    + Headers

            Authorization:Bearer tokenString

