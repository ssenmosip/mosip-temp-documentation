# 1. Audit Manager
## 1.1 Audit manager
1. Ability to store the audit logs
1. Ability to store the audit logs locally (in case of offline)
1. Ability to archive audit data based on defined archival policy
# 2. Exception Manager (mosip-exception)
## 2.1 Exception Handler 
1. Ability to provide base exception framework
1. Framework to include base exception parameters (Message, throwable, cause)
# 3. Log Manager (mosip-logging)
## 3.1 logging
Provide the following logging utility
1. Generate logs for implementation events across the application
1. Stores the generated logs in configured location
1. Each log can be generated as a file/console
1. Raise an alert in case of listed exceptions (File not found, No such file exists, to be identified)
1. Links various logs associated to one applicant
# 4. Mosip-utils
## 4.1 Util
MOSIP provides the following utilities
1. String utility
1. Calendar utility
1. Math utility
1. File utility
1. Hash utility
# 5. Data Access Manager
## 5.1 Dataaccess-hibernate
Provides a implementation for DAO (Data Access Manager) interface 
# 6. OTP Manager
## 6.1 Otpgenerator
Generates OTP for unique key, the length and expiry of the OTP is configurable
## 6.2 Otpvalidator
Validates the OTP against a unique key
# 7. Key Management
## 7.1 Key Generator
1. Generate key pair for encryption and decryption 
1. Store key pairs in DB 
1. Update validity status of the Key-pair
1. Audit with common attributes
## 7.2 Certificate Generator
1. Generate certificate for new machines, devices and users through a batch job using a defined algorithm
1. Store certificates in a password protected Key Store
1. Update validity status of the Key-pair
1. Audit with common attributes
## 7.3 Key Services
Track usage and validity of Key-pair/Certificate
# 8. Security
## 8.1 fileencryptor
Encrypts the data packets to secure the data
## 8.2 filedecryptor
Decrypts the data packets for further processing
## 8.3 Authentication
Authenticates the internal and external communications across the platform
## 8.4 Authorization
Authorizes the user as per the privileges
# 9. Data Mapper (mosip-beanmapper)
## 9.1 Data Mapper
Facilitate data mapping between DTO (Data Transfer Object) and Entity
# 10. Data Validator 
## 10.1 Mobile validator
Performs the pattern validation on the mobile number based on the configured length
## 10.2 Email validator
Performs the pattern validation on email ID based on the configured parameters
## 10.3 Blacklisted Words Validator
Performs a word to word validation against a configured list of blacklisted words
# 11. Master Data Manager
## 11.1 Masterdata
Performs CRUD(Create, Read, Update, Delete)operations on the masterdata
# 12. UIN Generator
## 12.1 uingenerator
Generates and validates UIN as per defined logic
# 13. ID Manager
## 13.1 RID Generator
Generates and validates RID(Registration ID) as per defined logic
## 13.2 PRID Generator
Generates and validates PRID(Pre-Registration ID) as per defined logic
## 13.3 VID Generator
Generates and validates VID(Virtual ID) as per defined logic
## 13.4 Token ID Generator
Generates and validates token ID (Token ID) as per defined logic for TSPs(Third party service provider)
## 13.5 Static PIN Generator
Generates and Validate static PIN for user authentication
## 13.6 Registration Center ID Generator
Generates a registration center ID
## 13.7 Machine ID generator
Generates a machine ID of the client machine
## 13.8 TSP ID Generator
Generates and validates a TSP ID
# 14. Virus Scanner
## 14.1 virusscanner-clamav
Performs virus scan on registration and pre-registration packet
# 15. Template Merger
## 15.1 Template Merger
Merges an pre-configured template with dynamic values
# 16. pdfgenerator
## 16.1 pdfgenerator
This utility enables PDF file creation of received contente.g.acknoledge and notification templates
# 17. Notification Manager
## 17.1 notification-sms
Provides a interface to send a SMS notification
## 17.2 notification-email
Provides an interface to send a Email notification
# 18. Sync Handler
## 18.1 Master data
Syncs master data between the MOSIP master data server and the client local database
## 18.2 Public keys
Syncs public keys between the MOSIP DB and client DB
## 18.3 Configuration changes
Syncs the configurations stored in  MOSIP config server with the locally stored configs of client
## 18.4 List of Roles and users
Syncs user role data between the MOSIP  server and the client local database
# 19. Multi-Language Manager
## 19.1 translation
Provides multi language support through translation for admin configured primary and secondary languages for a country
## 19.2 transliteration
Provides multi language support through transliteration for admin configured primary and secondary languages for a country
# 20. QR Code Generator
## 20.1 QR Code Generator
This utility enable QR code generation for Pre-reg, reg and UIN acknowledgement
# 21. FTP\packet uploader
## 21.1 FTP - Upload packet
Provides a upload portal for registration client to upload packets for sending it to registration processor