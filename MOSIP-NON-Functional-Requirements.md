# Audit Manager
## Auditmanager
1. Ability to store the audit logs
1. Ability to store the audit logs locally (in case of offline)
1. Ability to archive audit data based on defined archival policy
# Exception Manager (mosip-exception)
## Exception Handler 
1. Ability to provide base exception framework
1. Framework to include base exception parameters (Message, throwable, cause)
# Log Manager (mosip-logging)
## logging
Provide the following logging utility
1. Generate logs for implementation events across the application
1. Stores the generated logs in configured location
1. Each log can be generated as a file/console
1. Raise an alert in case of listed exceptions (File not found, No such file exists, to be identified)
1. Links various logs associated to one applicant
# Mosip-utils
## Util
MOSIP provides the following utilities
1. String utility
1. Calendar utility
1. Math utility
1. File utility
1. Hash utility
# Data Access Manager
## Dataaccess-hibernate
Provides a implementation for DAO (Data Access Manager) interface 
# OTP Manager
## Otpgenerator
Generates OTP for unique key, the length and expiry of the OTP is configurable
## Otpvalidator
Validates the OTP against a unique key
# Key Management
## Key Generator
1. Generate key pair for encryption and decryption 
1. Store key pairs in DB 
1. Update validity status of the Key-pair
1. Audit with common attributes
## Certificate Generator
1. Generate certificate for new machines, devices and users through a batch job using a defined algorithm
1. Store certificates in a password protected Key Store
1. Update validity status of the Key-pair
1. Audit with common attributes
## Key Services
Track usage and validity of Key-pair/Certificate
# Security
## fileencryptor
Encrypts the data packets to secure the data
## filedecryptor
Decrypts the data packets for further processing
## Authentication
Authenticates the internal and external communications across the platform
## Authorization
Authorizes the user as per the privileges
# Data Mapper (mosip-beanmapper)
## Data Mapper
Facilitate data mapping between DTO (Data Transfer Object) and Entity
# Data Validator 
## Mobile validator
Performs the pattern validation on the mobile number based on the configured length
## Email validator
Performs the pattern validation on email ID based on the configured parameters
## Blacklisted Words Validator
Performs a word to word validation against a configured list of blacklisted words
# Master Data Manager
## Masterdata
Performs CRUD(Create, Read, Update, Delete)operations on the masterdata
# UIN Generator
## uingenerator
Generates and validates UIN as per defined logic
# ID Manager
## RID Generator
Generates and validates RID(Registration ID) as per defined logic
## PRID Generator
Generates and validates PRID(Pre-Registration ID) as per defined logic
## VID Generator
Generates and validates VID(Virtual ID) as per defined logic
## Token ID Generator
Generates and validates token ID (Token ID) as per defined logic for TSPs(Third party service provider)
## Static PIN Generator
Generates and Validate static PIN for user authentication
## Registration Center ID Generator
Generates a registration center ID
## Machine ID generator
Generates a machine ID of the client machine
## TSP ID Generator
Generates and validates a TSP ID
# Virus Scanner
## virusscanner-clamav
Performs virus scan on registration and pre-registration packet
# Template Merger
## Template Merger
Merges an pre-configured template with dynamic values
# pdfgenerator
## pdfgenerator
This utility enables PDF file creation of received contente.g.acknoledge and notification templates
# Notification Manager
## notification-sms
Provides a interface to send a SMS notification
## notification-email
Provides an interface to send a Email notification
# Sync Handler
## Master data
Syncs master data between the MOSIP master data server and the client local database
## Public keys
Syncs public keys between the MOSIP DB and client DB
## Configuration changes
Syncs the configurations stored in  MOSIP config server with the locally stored configs of client
## List of Roles and users
Syncs user role data between the MOSIP  server and the client local database
# Multi-Language Manager
## translation
Provides multi language support through translation for admin configured primary and secondary languages for a country
## transliteration
Provides multi language support through transliteration for admin configured primary and secondary languages for a country
# QR Code Generator
## QR Code Generator
This utility enable QR code generation for Pre-reg, reg and UIN acknowledgement
# FTP\packet uploader
## FTP - Upload packet
Provides a upload portal for registration client to upload packets for sending it to registration processor