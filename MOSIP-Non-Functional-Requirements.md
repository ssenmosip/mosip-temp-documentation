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
Provides an implementation for DAO (Data Access Manager) interface 
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
1. Generate certificate for new machines, devices and users through a batch job using a defined algorithm
1. Stores certificates in a password protected Key Store
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
Performs a word to word validation against a configured list of blacklisted words
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
Merges an pre-configured template with dynamic values
## 16. PDF Generator
### 16.1 PDF Generator
This utility enables PDF file creation of received content (e.g. acknowledge and notification templates)
## 17. Notification Manager
### 17.1 Notification-SMS
Provides an interface to send a SMS notification
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
Provides multi language support through translation for admin configured primary and secondary languages for a country
### 19.2 Transliteration
Provides multi language support through transliteration for admin configured primary and secondary languages for a country
## 20. QR Code Generator
### 20.1 QR Code Generator
This utility enable QR code generation for pre-registration, registration and UIN acknowledgement
## 21. FTP\Packet Uploader
### 21.1 FTP - Upload Packet
Provides an upload portal for registration client to upload packets for sending it to registration processor
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
## TBD-WIP sections 22-25
## 22. Interface Requirements
[Describe the user interfaces that are to be implemented by the system.]
### 22.1 Hardware Interfaces
[Define hardware interfaces supported by the system, including logical structure, physical addresses, and expected behavior.]
### 22.2 Software Interfaces
[Name the applications with which the subject application must interface.  State the following for each such application: name of application, external owner of application, interface details (only if determined by the other application).

It is acceptable to reference an interface control document for details of the interface interactions.]
### 22.3 Communications Interfaces
[Describe communications interfaces to other systems or devices, such as local area networks.]
## 23. Data Conversion Requirements
[Describe the requirements needed for conversion of legacy data into the system.]
## 24. Hardware/Software Requirements
[Provide a description of the hardware and software platforms needed to support the system.]
## 25. Operational Requirements
[Provide the operational requirements in this section.

Do not state how these requirements will be satisfied.  For example, in the Reliability section, answer the question, “How reliable must the system be”? Do not state what steps will be taken to provide reliability.

Distinguish preferences from requirements.  Requirements are based on business needs, preferences are not.  If, for example, the user requires a special response but does not have a business-related reason for it, that requirement is a preference.

Other applicable requirements on system attributes may be added to the list of subsections below.]

Operational requirements describe how the system will run and communicate with operations personnel.
### 25.1 Security and Privacy
[Provide a list of the security requirements using the following criteria:

State the consequences of the following breaches of security in the subject application:
1. Loss or corruption of data
1. Disclosure of secrets or sensitive information
1. Disclosure of privileged/privacy information about individuals
1. Corruption of software or introduction of malware, such as viruses
### 25.2 Reliability
[State the following in this section:

State the damage can result from failure of this system—indicate the criticality of the software, such as:
1. Loss of human life
1. Complete or partial loss of the ability to perform a mission-critical function
1. Loss of revenue
1. Loss of employee productivity

What is the minimum acceptable level of reliability?

State required reliability:
1. Mean-Time-Between-Failure is the number of time units the system is operable before the first failure occurs.
1. Mean-Time-To-Failure is the number of time units before the system is operable divided by the number of failures during the time period.
1. Mean-Time-To-Repair is the number of time units required to perform system repair divided by the number of repairs during the time period.]

_Reliability is the probability that the system processes work correctly and completely without being aborted._
### 25.3 Recoverability
[Answer the following questions in this section:
1. In the event the application is unavailable to users (down) because of a system failure, how soon after the failure is detected must function be restored?
1. In the event the database is corrupted, to what level of currency must it be restored?  For example “The database must be capable of being restored to its condition of no more than 1 hour before the corruption occurred”.
1. If the processing site (hardware, data, and onsite backup) is destroyed, how soon must the application be able to be restored?]

_Recoverability is the ability to restore function and data in the event of a failure._
### 25.4 System Availability
[State the period during which the application must be available to users.  For example, _“The application must be available to users Monday through Friday between the hours of 6:30 a.m. and 5:30 p.m. EST_.  If the application must be available to users in more than one time zone, state the earliest start time and the latest stop time.  Consider daylight savings time, too.

Include use peak times.  These are times when system unavailability is least acceptable.]

_System availability is the time when the application must be available for use.  Required system availability is used in determining when maintenance may be performed._
### 25.5 General Performance
[Describe the requirements for the following:
1. Response time for queries and updates
1. Throughput
1. Expected rate of user activity (for example, number of transactions per hour, day, or month, or cyclical periods)

Specific performance requirements, related to a specific functional requirement, should be listed with that functional requirement.
### 25.6 Capacity
[List the required capacities and expected volumes of data in business terms.  Do not state capacities in terms of system memory requirements or disk space—if growth trends or projections are available, provide them]
### 25.7 Data Retention
[Describe the length of time various forms of data must be retained and the requirements for its destruction.

For example, “The system shall retain application information for 3 years”.  Different forms of data include: system documentation, audit records, database records, and access records.]
### 25.8 Error Handling
[Describe system error handling.]
### 25.9 Validation Rules
[Describe System Validation Rules.]
### 25.10 Conventions/Standards
[Describe system conventions and standards followed.

For example: Microsoft standards are followed for windows, Institute of Electrical and Electronics Engineers (IEEE) for data formats, etc.]


**APPENDIX A - GLOSSARY**

[Define terms, acronyms, and abbreviations used in the FRD.] 