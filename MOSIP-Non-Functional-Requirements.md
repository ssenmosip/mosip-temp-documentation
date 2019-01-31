## 1. Audit Manager
### 1.1 Audit Manager
1. Ability to store the audit logs
1. Ability to store the audit logs locally (in case of offline)
1. Ability to archive audit data based on defined archival policy
## 2. Exception Manager (MOSIP-Exception)
### 2.1 Exception Handler 
1. Ability to provide base exception framework
1. Framework to include base exception parameters (message, throwable, cause)
## 3. Log Manager (MOSIP-Logging)
### 3.1 Logging
Provide the following logging utility
1. Generate logs for implementation events across the application
1. Stores the generated logs in configured location
1. Each log can be generated as a file/console
1. Raise an alert in case of listed exceptions (file not found, no such file exists, to be identified)
1. Links various logs associated to one applicant
## 4. MOSIP-Utils
### 4.1 Util
MOSIP provides the following utilities
1. String utility
1. Calendar utility
1. Math utility
1. File utility
1. Hash utility
## 5. Data Access Manager
### 5.1 Data Access-Hibernate
Provides an implementation for DAM (Data Access Manager) interface 
## 6. OTP Manager
### 6.1 OTP Generator
Generates OTP for unique key, the length and expiry of the OTP is configurable
### 6.2 OTP Validator
Validates the OTP against a unique key
## 7. Key Management
### 7.1 Key Generator
1. Generates key pair for encryption and decryption 
1. Store key pairs in DB 
1. Update validity status of the key-pair
1. Audit with common attributes
### 7.2 Certificate Generator
1. Generate a certificate for new machines, devices and users through a batch job using a defined algorithm
1. Stores certificate in a password protected Key Store
1. Update validity status of the Key-pair
1. Audit with common attributes
### 7.3 Key Services
Track usage and validity of key-pair/certificate
## 8. Security
### 8.1 File Encryptor
Encrypts the data packets to secure the data
### 8.2 File Decryptor
Decrypts the data packets for further processing
### 8.3 Authentication
Authenticates the internal and external communications across the platform
### 8.4 Authorization
Authorizes the user as per the privileges
## 9. Data Mapper (MOSIP-Beanmapper)
### 9.1 Data Mapper
Facilitate data mapping between DTO (Data Transfer Object) and entity
## 10. Data Validator 
### 10.1 Mobile Validator
Performs the pattern validation on the mobile number based on the configured length
### 10.2 Email Validator
Performs the pattern validation on email ID based on the configured parameters
### 10.3 Blacklisted Words Validator
Performs word to word validation against a configured list of blacklisted words
## 11. Master Data Manager
### 11.1 Master Data
Performs CRUD (Create, Read, Update, Delete) operations on the master data
## 12. UIN Generator
### 12.1 UIN Generator
Generates and validates UIN as per defined logic
## 13. ID Manager
### 13.1 RID Generator
Generates and validates RID (Registration ID) as per defined logic
### 13.2 PRID Generator
Generates and validates PRID (Pre-Registration ID) as per defined logic
### 13.3 VID Generator
Generates and validates VID (Virtual ID) as per defined logic
### 13.4 Token ID Generator
Generates and validates token ID as per defined logic for TSPs (Third party Service Provider)
### 13.5 Static PIN Generator
Generates and validates static PIN for user authentication
### 13.6 Registration Center ID Generator
Generates a registration center ID
### 13.7 Machine ID Generator
Generates a machine ID of the client machine
### 13.8 TSP ID Generator
Generates and validates a TSP ID
## 14. Virus Scanner
### 14.1 ClamAV Virus Scanner
Performs virus scan on registration and pre-registration packet
## 15. Template Merger
### 15.1 Template Merger
Merges a pre-configured template with dynamic values
## 16. PDF Generator
### 16.1 PDF Generator
This utility enables PDF file creation of received content (e.g., acknowledge and notification templates)
## 17. Notification Manager
### 17.1 Notification-SMS
Provides an interface to send an SMS notification
### 17.2 Notification-Email
Provides an interface to send an email notification
## 18. Sync Handler
### 18.1 Master data
Syncs master data between the MOSIP master data server and the client local database
### 18.2 Public Keys
Syncs public keys between the MOSIP DB and client DB
### 18.3 Configuration Changes
Syncs the configurations stored in MOSIP configuration server with the locally stored configuration of client
### 18.4 List of Roles and users
Syncs user role data between the MOSIP server and the client local database
## 19. Multi-Language Manager
### 19.1 Translation
Provides multi language support through translation for an admin configured primary and secondary languages for a country
### 19.2 Transliteration
Provides multi language support through transliteration for an admin configured primary and secondary languages for a country
## 20. QR Code Generator
### 20.1 QR Code Generator
This utility enable QR code generation for pre-registration, registration and UIN acknowledgment
## 21. FTP\Packet Uploader
### 21.1 FTP - Upload Packet
Provides an upload portal for registration client to upload packets for sending it to registration processor
## 22. Demand Capacity and Performance
The solution should have capacities to cater to the following workload while meeting the performance levels indicated below:

### <p align="center"> **Table 1: _Demand Capacity and Performance Requirements_**


|**S. No.**| **Item**| **Description**|
|:------:|-----|---|
|1.|Biometric Gallery size| Scalable to peak capacity 40 million records|
|2.|Biometric Gallery size (Phase-I)| At peak capacity nearly 8.00 million|
|3.|Biometric Gallery size (Phase-II)| At peak capacity nearly 32.00 million|
|4.|Peak Enrolment per day (Phase-I)| At peak capacity 30,000 enrolments per day|
|5.|Peak Enrolment per day (Phase-II) |At peak capacity 50,000 enrolments per day |
|6.|Peak Enrolment packet to be uploaded per day (incl. backlog) | At peak capacity 60,000 enrolments per day|
|7.|Authentication Request (Phase-I)| At peak capacity 0.5 Million requests per day (12 hours)|
|8.|e-KYC Request (Phase-I)| At peak capacity 0.5 Million requests per day (12 hours)|
|9.|Authentication Request (Phase-II)| At peak capacity 1.8 Million requests per day (12 hours)|
|10.|e-KYC Request (Phase-II)|At peak capacity 1.8 Million requests per day (12 hours) |

The solution shall cater to at least the following indicative performance level: 

### <p align="center"> **Table 2: _Demand Capacity and Performance Requirements_**


|**S. No.**| **Item**| **Description**|
|:------:|-----|---|
|**A.**| **Response time**||
|1.|Enrolment Request (at ABIS Level)| No daily backlog i.e. maximum of 24 hours at peak load|
|2.|Enrolment Request (at MOSIP Level)| No daily backlog i.e. maximum of 24 hours at peak load|
|3.|Authentication Request (SDK)| <= 0.5 seconds|
|4.|Authentication Request (Overall)|>= 3 seconds |
|**B.**|**Accuracy** | |
|1.|De-duplication| FPIR <= 0.1% and FNIR <=1% |
|2.|Authentication Services| FMR <= 0.001% and FNMR <= 0.05% |
|**C.**|**Uptime and Availability**| |
|1.|De-duplication|99.5 % uptime evaluated on monthly basis on 24*7 service window |
|2.|Authentication Services| 99.99% uptime evaluated on monthly basis on 24*7 service window|

## 23. Estimated Enrolment Volumes

A tabular representation of the estimated volumes in the overall project implementation is given below:

### <p align="center"> **Table 3: _Enrolment Volume Estimates_**


|**S. No.**| **Item**| **Volumes (in million)**|
|:------:|-----|:------:|
|**A.**| **Phase-I [Social Sector Beneficiaries in RAMED, DAAM and TAYSSIR]**|**8.00**|
|1.|Stage-I (Rabat Prefecture)| 0.04|
|2.|Stage-II (Kenitra Province)| 0.12|
|3.|Stage-III (Nationwide)| 7.84|
|**B.**|**Phase-II [Other Beneficiaries and Targeted Population]** |**26.49** |
|1.|Enrolment of 85% of Targeted Population [November 2021 to July 2023]| 22.86 |
|2.|Additional enrolment of 10% of Targeted Population [August 2023 onward]| 3.63 |
|**C.**|**Continuous Enrolment (New Born) and Updates (Demo. and Bio.)**|**8.90** |
|1.|New Born Enrolment (From 2021 to 2023)|1.28 |
|2.|Demographic Updates (From 2020 to 2023)| 4.24|
|3.|Biometric Updates (From 2020 to 2023)| 3.38|

The table given above is an estimated of the enrolment and updated volumes under this program. The detailed explanation of the line items is provided below:
1. The total population of Morocco as per the census data of 2014, stands at 33.77 million. The population at the end of year 2021 is estimated to be 36.31 million which is estimated to reach 39.33 million at the end of year 2030.
1. In the first phase, the beneficiaries under RAMED, DAAM and TAYSSIR are planned to be covered. The approximate number of beneficiaries under these programs is 8 million. 
1. For the purpose of enrolment of all the citizens and foreign Residents of Morocco, a figure of 95% of the total population is considered. It is estimated that 85% of the population will be enrolled in Phase-I and Phase-II of implementation. Considering this, the total enrolment volumes in Phase-II come out to be 22.86 million till July 2023. Thereafter, an additional 10% of the population i.e. nearly 3.63 million will be covered August 2023 onward. 
1. In addition to the enrolment volumes as mentioned above, the continuous enrolment of the annual increment in the population (new born children) will be carried out. Moreover, the updates in demographic information such as mobile number, address, email address, etc. will also be carried out. Similarly, the update in biometric information will be carried out at the age of 5 years, 15 years and on demand basis for other registered individuals.

## 24. Estimated Authentication Volumes

The estimated volume of authentication services are provided in this section. 

In the Phase-I (between Aug 2019 to Oct 2021), there is expected to be a one-time usage of e-KYC for all the social sector beneficiaries i.e. 8 million. During this phase, nearly 100 million authentication transactions are estimated per annum. Thus, considering an average of 250 working days in a year, nearly 0.43 million authentication transactions are estimated per day. The authentication transactions are expected to originate from below mentioned schemes:

1. In TAYSSIR, a total of 0.74 million beneficiaries are registered. The beneficiaries are school going children, and it is estimated that these children would authenticate and mark their attendance in school twice each week. These transactions are estimated to be over a period of 250 working days of a year. Thus, nearly 77 million authentication transactions are estimated annually under this program.
1. RAMED is a health insurance scheme where government provides financial support to vulnerable people. It is estimated that the beneficiaries under the scheme will undertake at least three visits in the hospitals and their transactions would need to be authenticated. Thus, the total estimated authenticated transactions is 22.8 million per annum. 
1. In the DAAM program, a total of nearly 0.077 million beneficiaries are registered. It is estimated that a beneficiary will undertake at least four authentication transactions in a year. Thus, the total estimated authentication transaction works out to 0.31 million per annum.

The above information is summarized in the table given below:

### <p align="center"> **Table 4: _Authentication and e-KYC volume estimates during Phase-I_**
|**S. No.**| **Parameter**| **Description**| **Sizing Estimations**
|:------:|-----|---|:-----:|
|**A.**|**Authentication**|
|1.|Authentication Example 1| TAYSSIR Authentications in schools on a daily basis|77 million per annum [estimated as 0.74 million (per day) x 250 working days]|
|2.|Authentication Example 2|RAMED Authentications at hospitals | 22.8 million per annum [estimated as 7.6 million x 3 authentications per beneficiary per year] |
|3.|Authentication Example 3| DAAM Authentications|0.31 million per annum [estimated as 0.077 million beneficiaries x 4 times per year]|
|**B.**|**KYC**| **One-Time**|
|1.|Authentication Example 1| TAYSSIR Authentications in schools on a daily basis | 0.74 million|
|2.|Authentication Example 2| RAMED Authentications at hospitals | 7.60 million|
|3.|Authentication Example 3| DAAM Authentications | 0.077 million |

After the end of Phase-I of the implementation, the authentication services and the corresponding authentication volumes would start growing. During peak usage under the Phase-II, it is estimated that 10% of the total population of Morocco would use authentication services on a daily basis. In other words, it is estimated that authentication transactions during Phase-II would be in the range of 3.6 million per day. Thus, the total volumes are estimated to be 650 Million transactions per annum during Phase-II. 

## 25. Transaction Volumes
### <p align="center"> **Table 5: _Indicative Transaction Volumes_**
|**S. No.**| **Parameters**| **Indicative Units**|
|:------:|-----|:---:|
|**A.**|**Enrolments**| |
|1.|Total number of enrolments till October 2021| 8.00 million|
|2.|Total number of enrolments till July 2023| 30.48 Million|
|3.|Size of Enrolment Packet| 3 MB|
|4.|Peak enrolment per day (Phase-I)|30,000 |
|5.|Peak enrolment per day (Phase-II)|50,000 |
|6.|Peak Enrolment packet to be uploaded per day (incl. backlog)|60,000 |
|7.|Peak Enrolment batch process per hour (Phase-I)| 1500|
|8.|Peak Enrolment batch process per hour (Phase-II)| 2500|
|9.|Pre-enrolment during peak hour (Phase-I):|2,600 Users |
||(a) 8 million enrolments in 2 years
||(b) Peak hour will see double of average requests
||(c) 90% of registration happens in 8 hour window 
|10.|Pre-enrolment during peak hour (Phase-II):| 6,750 Users|
|| (a) 22.5 million enrolments in 2 years
|| (b) Peak hour will see double of average requests
|| (c) 90% of registration happens in 8 hour window
|**B.**|**Authentication and E-KYC**| |
|1.|Number of authentication requests (At peak load during Phase-I)| 0.50 million per day|
|2.|Number of e-KYC requests (At peak load during Phase-I)|0.10 million per day |
|3.|Number of authentication requests (At peak load during Phase-II)| 1.80 million per day|
|4.|Number of e-KYC requests (At peak load during Phase-II)|1.80 million per day |
|**C.**|**Internet Usage**
|1.|Web page size|130Kb, 0.13Mb|
|2.|Total number of web users in Morocco|22.5 Million|
|3.|Concurrency percentage per hour|2.5%|
|4.|Number of Concurrent internet users|5,62,500|
|5.|Average no. of hits by same users during the same login on web page|2|
|6.|Web users during peak hour|100,969|
|7.|Web users during peak hour| (a) 2.5% users/day| 
||| (b) Peak hour will see double of average requests|
|**D.**|**Miscellaneous**
|1.|Number of sessions during peak load |36 million per annum|
|2.|Assumed CPU and memory Utilization for Non-ABIS Application|60%|
|3.|Bandwidth at each center|2 MBPS|
### 25.1. Assumptions for Server Sizing
1. All production and non-production servers will be hosted at common Data Centre
1. Baring certain citizen facing applications, DC-DR will be in active passive configuration
1. All servers will be based on x86 architecture
1. Used for hosting high compute requirements with SAN
1. Optimized Data Centre space utilization
1. More compute and memory power per server 
1. High compute and memory consuming workloads should use Blades 
### 25.2. Usage Factors for Storage and Tape Library
1. Host mount points for blade servers
1. Provides support for storage array based replication to meet DR requirements 
1. Host IO intensive workloads like database, data analytics and data warehouse 
1. Provide a front-end, fast cache to a tape library infrastructure
1. Shorten the backup window period 
1. Enables faster data restoration 
1. Provides data retention for longer duration
1. Provides cost effective way of retaining data for longer duration
1. Enables department to meet data compliance requirements
### 25.3. Data Size
This section provides the details of the data size required to be handled in the RNP information system

### <p align="center"> **Table 6: _Data Size_**
|**Parameter**|**Description**|**Sizing Estimations**|
|----|----|:----:|
Size of Enrolment Packet|Demographic, Photograph, 2 Iris and Documents |3 MB Raw Packet |
Authentication Packet|Demographic, OTP, Iris or Facial|3-5 KB|
e-KYC Packet|OTP, Iris or Facial|30 KB
## 26. Estimation of Users 
### <p align="center"> **Table 7: _Estimation of Users_**
|**S. No.**|**Parameter**|**Description**|**Sizing Estimations**|
|:----:|----|----|----|
|1.|Total User|Total Number of Users|150 Users|
|2.|Kit Operators| Field Operators|2000 
||| Working Hours|8 hours x 22 working days per month
|3.|Verification| CNIE Verification|10 per shift
|||Working Hours|8 hours per shift x 2 Shift
|4.|Adjudicators| Manual Adjudication|10 per shift |
|||Working Hours|8 hours per shift x 2 Shift|
|5.|Contact Centre| Helpdesk Personnel|10 x 2 Shift 
||| Number of Supervisors|1 (First Shift) + 1 (Second Shift) 
||| Contact Centre Seats|11 (minimum) 
||| Waiting time|2 Minutes (maximum) 
||| Working Hours|8 hours per shift x 2 Shift 
|6.| IT Helpdesk| Helpdesk Personnel|5 (First Shift) + 5 (Second Shift) + 2 (Third Shift)|
||| Number of Supervisors|1 (First Shift) + 1 (Second Shift) 
|7.|Network Operations Centre| Number of Users| 3 (First Shift) + 3 (Second Shift) + 1 (Third Shift) 
||| Working Hours| 8 hours per shift x 3 Shifts
|8.|Security Operations Centre|Number of Users|4 (First Shift) + 4 (Second Shift) + 2 (Third Shift) 
|||Number of Supervisors|1 (First Shift) + 1 (Second Shift) 
|||Working Hours|8 hours per shift x 3 Shifts
|9.|Administrators| DBA, Network Admin, Server Admin, Storage Admin, etc.| 13 (DC) + 4 (DR) 
||| Working Hours| 8 hours per shift x 3 Shift
|10.|Internet Subscriber| No. of Internet Users|22.5 million (September 2017)
|||No. of Internet Users|16.9 million (September 2016)
|||Annual growth rate| Annual growth of 33% (10 years)
|11.|Estimated Users| No. of Internet Subscribers| 10% of Internet Subscribers
|12.|Concurrency Citizen| Concurrency of Internet Users|2.5% of estimated users
|13.| Permanent Service Centres|Citizen Service Centres |2000
|14.| Workload Volume| 	Number of Registrations Per Day Per Kit	|15 enrolments during Phase-I and 25 enrolments during Phase-II|
## 27. Technical Parameters
### <p align="center"> **Table 8: _Technical Parameters_**
|**S. No.**|**Parameter**|**Description**|**Sizing Estimations**|
|:----:|----|----|----|
|1.|Network Connectivity |Network Connectivity (DC-DR Replication Link)| Dual links of 1 Gbps capacity
||*(For future usage the router sized for 2-5 Gbps is recommended)|Network Connectivity (DC-NDC-DR Replication Link)|Dual links of 150 Mbps capacity
|||Network Connectivity (Internet) at the Data Centre|Initially 150 Mbps internet connectivity
|||Network Connectivity (Data Validation) at the Data Centre| Initially 150 Mbps leased line
|||Network Connectivity (TSPs) at the Data Centre|To be provisioned by respective TSP, based on their transaction projections
|2.|CPU |Utilization upper limits|60% only for non-ABIS component
|3.|Re-size/ headroom|Virtual Cores, Memory, and Storage Seamlessly|25% of the base capacity, only for non-ABIS components in permanent Data Centre
|4.|Storage|Static & Transaction data|2,600 TB
|5.|Reports|Total|25 types of reports
|||Break-up|5 Complex Report Type,
||||10 Medium Report Type,
||||10 Simple Report Type
|6.|Communication with External Systems|External interfaces that are likely to interact with the RNP System|Social Benefit Programs (RAMED, TAYSSIR, DAAM, etc.), Financial Switch for Social Benefit Disbursement, Validation with CNIE and Civil Registration, etc.
|7.|RTO and RPO |For Pilot, the DC-DR will be in same city. Subsequently, the DC and DR will be more than 100 KMs apart| Refer to Section 28.
|8.|Online data retention| NID Data|Always
|||Biometric Centre data| Always
|9.|Backup window| Incremental data back up every day and full back up every week| 6-8 hrs
## 28. RTO and RPO
### <p align="center"> **Table 9: _RTO and RPO_**
|**S. No.**|**Process**|**Criticality**|**RTO**| **RPO**|**Business Rationale for RPO and RTO**|
|:----:|----|----|----|----|----|
|1.|Enrolment|High|24 hours|~ZERO|**RTO**: Enrolment is an offline process and officers are required to upload packets once a day hence 24 hrs. is affordable 
||||||**RPO (Enrolment Databases)**: It is a business requirement that no data shall be lost in the ecosystem (IDMS and CSC)
|2.|Authentication| High|~ZERO|~ZERO|**RTO**: Authentication is an online process and it is anticipated that majority of government and private organizations in Morocco will use this service to be able to provide further services. Hence RTO is 0
||||||**RPO (Authentication databases including logs)**: It is a business requirement that no authentication data shall be lost
|3.|Critical Portals | High|~ZERO|~ZERO|**RTO**: These portals could be resident facing and any downtime could have major reputational impact
||||||**RPO (Logs databases and enrolment, Authentication databases)**: It is a business requirement that no data is lost from the logs database. Authentication and Enrolment databases also have ~ZERO RPOs
|4.|CRM|High|~ZERO|~ZERO|**RTO**: CRM is a resident facing service and any downtime could have major reputational impact 
||||||**RPO (CRM database, call recordings etc.)**: It is a business requirement that no data is lost from the CRM databases and maintenance of the databases also may be necessary for compliance to legal requirements. 
|5.|SOC|High|~ZERO|~ZERO|**RTO**: SOC is a very important security operation for IDMS. SOC should never be down as logs from various devices are collected by SOC tool and it is important that logs are always available for investigation purposes
||||||**RPO (Logs file system, SOC configuration etc.)**: It is a business and legal requirement that logs are always available 
|6.|Email|High|~ZERO|~ZERO|**RTO**: Email is very critical service as lot of other services depend upon email such as email to residents when PIN generated or when resident authenticates 
||||||**RPO (Emails)**: Email is a very critical service and lot of internal and partner communications take place on email hence it is a critical service.
|7.|Other Portals|Medium|~ZERO|~ZERO if data other than logs ~24 hrs if only logs|**RTO**: It is understood that these portals are not resident facing and criticality 
||||||**RPO (Logs databases and enrolment, Authentication databases)**: It is a business requirement to ensure there is no data loss in case data other than logs is present.
|8.|NOC|Medium|~ZERO|~24 hrs.|**RTO**: It is understood that NOC is an important process to monitor the availability of service
||||||**RPO (Ticketing database etc.)**: Ticketing database is not a critical database and hence loss of 24 hrs. of tickets can be afforded
|9.|Office|Medium|24 - 48 hours|N/A (No data is stored)	