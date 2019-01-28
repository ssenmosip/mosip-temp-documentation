# Pre-Registration
## 1. Authentication
### 1.1 Login
Log in to the pre-registration system with mobile or email with OTP so that you can access the pre-registration system
### 1.2 Logout
Log out from the pre-registration system
## 2. Language Data Manager
### 2.1 Translation
Translation of the language as per the pre-configured primary and secondary language of a country
### 2.2 Transliteration
Transliteration of the language as per the pre-configured secondary language for a country
## 3. Pre-Registration Sync
### 3.1 Pre-Registration Data Sync
1. Synchronizes the pre-registration data with the registration-client 
1. Synchronizes status of pre-ID with registration processor
## 4. Appointment Scheduler
### 4.1 RC Identifier
Provides search facility for available registration centers so that applicant can book an appointment  
### 4.2 Availability Checker  
Getting availability of slots in the chosen registration center
### 4.3 Appointment Booking  
Booking\re-booking the selected slot in the chosen registration-center for registration
## 5. Pre-Registration Application Manager
### 5.1 Pre-Registration Application Manager
Collects (create\modify\delete) demographic data and documents from the user\applicant
### 5.2 Acknowledgement
Generates acknowledgement for successful pre-registration
# Registration
## 1. Registration Client Setup
### 1.1 Registration Client Installation
Installs the registration-client on the machine 
### 1.2 Registration Client Launch
Helps in launching the registration-client
### 1.3 Registration Client Software Update
Updates the client software 
## 2. System Health Checker
### 2.1 Connectivity Checker
Checks if the client machine is connected to the network
### 2.2 Security Scan
Virus scan of the data packets and the application software
### 2.3 Disk Space Checker
Checks whether there is enough space in the client machine\dongle to store the registration packet
## 3. Registration Officer Authentication
### 3.1 Login
Enables logging in to the client machine by password, OTP or biometrics
### 3.2 Logout
Logging out from the client application
## 4. User Onboarding/Manager
### 4.1 User Registration
Enables mapping between the user and machine\dongle. Allows a user to onboard themselves on a machine
## 5. Language Manager
### 5.1 Translation
Translates the static messages as per the configures primary and secondary languages
### 5.2 Transliteration
Translates the user entered text from primary to secondary language
## 6. Registration Application Manager - New
### 6.1 Location Geotagging
Captures the GPS co-ordinates of the client machine to ensure data integrity
### 6.2 Individual Category Selection
Helps to distinguish if an applicant is an adult or a child
### 6.3 Demo Data Capture
Captures the demographic data of the applicant
### 6.4 Document Upload
Enables scan and upload supporting doc such as POA and POI
### 6.5 Fingerprint Capture
Captures the finger print data and determines the quality of the data
### 6.6 Iris Capture
Captures the iris data and determines the quality of the data
### 6.7 Face Capture
Captures the face photograph 
### 6.8 Biometric Exception Capture
1. Captures the exception photograph
1. Marks the biometric exceptions
### 6.9 Registration Checks
1. Preview of the registration details
1. Operator authentication for submitting the registration
1. Supervisor authentication for submitting registration with exception
1. End of day approval
1. Re-registration
### 6.10 Acknowledgement
Renders the acknowledgement page after successful registration and allows printing
### 6.11 Notification
Renders email and SMS notification for various events such as successful registration
## 7. Registration Officer Authorization
### 7.1 Registration Officer Authorization
Determines the user roles and provides access based on the privileges
## 8. Registration Packet Manager
### 8.1 Packet Creation
Creates the encrypted data packets
### 8.2 Packet Exporter
Allows sending packets to the processing server
1. Using the upload feature of the client
1. Copying packets to an external storage device
## 9. Sync Handler
### 9.1 Master Data Syncher
Synchronizes master data between server to client
### 9.2 Packet Syncher
Send registration packet IDs from client to processor so that to ensure data security
### 9.3 Registration Packet Status Reader
Read the status of the packets from processor into the client to ensure resend or deleting of packets as required
### 9.4 Registration Client Configuration Syncher
Synchronizes configuration data between server to client
### 9.5 User Role Setup Syncher
Synchronizes user and role data between server to client
### 9.6 Policy Syncher
Synchronizes encryptions Keys between server to client
### 9.7 Pre-Registration Data Syncher
Synchronizes pre-registration data between server to client
### 9.8 Login Credentials Syncher
Synchronizes login data (password) between server to client
### 9.9 Audit Log Syncher
Synchronize the audit log from client to server
## 10. Individual UIN - Update
### 10.1 UIN Update
Allows the UIN holder to update their data (A specific set of data as defined by the country)
## 11. Reporting
### 11.1 Registration Reports
Generates reports on end of day process and re-registration
## 12. Clean Up
### 12.1 Data Clean Up
Deletes the following data from the client machine after successful registration:
1. Registration
1. Pre-registration
1. Audit
# Registration Processor
## 1. Registration Packet Handler
### 1.1 Packet Mover
To move packets from one folder location to another in registration-processor workflow
### 1.2 Packet File Virus Scanner
Performs virus scan of the encrypted and decrypted packet
### 1.3 Packet Store
A distributed file system to store decrypted data packets
### 1.4 Archive Packets
Makes the data packets available for archival
### 1.5 Packet Decryptor
Decrypts the data packets for further processing
## 2. Registration Status Service
### 2.1 Registration Status Updater
As the per the stage driven architecture this utility updates the status in the DB for the data packet at every stage
## 3. Registration Packet Processor
### 3.1 Packet Structure Validator
It performs integrity validation (checksum) and file validation
### 3.2 Packet Data Extractor
Extracts data from JSON object and store in DB 
### 3.3 OSI Data Validator
Authenticate operator, supervisor and introducer information received in data packet and validate the metadata captured during packet creation
### 3.4 Demo De-Dupe
Demographic de-duplication of name, gender and DOB
### 3.5 Biometric Quality Checker
Checks the quality of biometric data against a configured standard
### 3.6 Biometric De-Dupe
Biometric de-duplication of biometrics using ABIS
## 4. UIN Generator
### 4.1 UIN Generator
Generates UIN as per the defined logic
### 4.2 UIN Acknowledgement Generator (Provided By Core Kernel)
Generates a PDF acknowledgement of the UIN card
## 5. Notification Manager
### 5.1 Notification-SMS
Send SMS notification for registration success and failure scenarios 
### 5.2 Notification-Email
Send email notification for registration success and failure scenarios 
## 6. Print
### 6.1 Print Queue 
Make the UIN data available for printing and postal services
## 7. UIN Lifecycle Manager
### 7.1 UIN De-Activator
De-activates a UIN
### 7.2 UIN Re-Activate
Re-activates a UIN
### 7.3 UIN Updater
Updates UIN data of an existing UIN
## 8. Minutiae Extractor
### 8.1 Minutiae Extraction Algorithm
Extract minutiae from finger print image to store in ID repository
# ID-Authentication
## 1. TSP/UA Authentication
### 1.1 TSP Authentication 
Validates if the TSP and UA are authenticated sources to initiate the individual's authentication request
### 1.2 Authentication Mode Verifier
Verifies if the UA holds permission to initiate the mode of authentication in the authentication request
## 2. TSP/UA Authorization 
### 2.1 TSP Authorization
Determines if the TSP and UA are authorised entities to initiate the individual's authentication request
## 3. Individual  Authentication
### 3.1 Biometric Authentication
Verifies the authenticity of an individual using biometric attributes provided in the authentication request
### 3.2 Demographic Authentication
Verifies the authenticity of an individual using demographic attributes provided in the authentication request
### 3.3 OTP Authentication
1. Enables an individual to receive OTP
1. Verifies the authenticity of an individual using OTP provided in the authentication request
### 3.4 Static PIN Authentication
1. Enables storage of static pin set by an individual in MOSIP Resident Services Portal
1. Verifies the authenticity of an individual using static pin provided in the authentication request
### 3.5 E-KYC Authentication Services   
Provides E-KYC details of an individual to the UA post successful authentication of the individual
## 4. Integrated Individual Authentication 
### 4.1 Multiple Components
Verifies the authenticity of an individual using multiple attributes provided  in the authentication request






