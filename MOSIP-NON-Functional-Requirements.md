
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
1. Generate logs for implentation events across the application
1. Stores the genrated logs in configured location
1. Each log can be genrated as a file/console
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
Autenticates the the intenal and external communications across the platform
## Authorization
Authorizes the user as per the previleges
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




