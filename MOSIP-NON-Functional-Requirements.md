Non Functional Requirements
Utilities
MOSIP provides the following utilities
1.String utility
2.Calendar utility
3.Math utility
4.File utility
5.Hash utility

Batch-spring 
This utility provide a framework for other modules to schedule and run batch jobs
OTP Manager	
•	Otpgenerator
Generates OTP for unique key,The length and expiry of the OTP is configurable

•	Otpvalidator
Validates the OTP against a unique key

Key Management
•	Key Generator

1. Generate key pair for encryption and decryption 
2. Store key pairs in DB 
3. Update validity status of the Key-pair
4. Audit with common attributes
•	Certificate Generator
Generate certificate for new machines, devices and users through a batch job using a defined algorithm
2. Store certificates in a password protected Key Store
3. Update validity status of the Key-pair
4. Audit with common attributes
•	Key Services
Track usage and validity of Key-pair/Certificate

Data Access Manager
Security
•	Fileencryptor:
Encrypts the data packets to secure the data
•	Filedecryptor
Decrypts the data packets for further processing
•	Authentication
Authenticates the internal and external communications across the platform
•	Authorization
Authorizes the user as per the privileges

Data Mapper
Facilitate data mapping between DTO (Data Transfer Object) and Entity 

Data Validator
Mobile validator
Performs the pattern validation on the mobile number based on the configured length
Email validator
Performs the pattern validation on email ID based on the configured parameters
Blacklisted Words Validator
Performs a word to word validation against a configured list of blacklisted words

