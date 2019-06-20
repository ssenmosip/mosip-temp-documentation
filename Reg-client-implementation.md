# Registration Client Developer Documentation

*** 
This document guide the developer to find the traceability between functionality and the respective technical component.  The provided technical classes are available in the package of 'registration-service' module. In this module the required functions are exposed as public method and that can be used to obtain the required features.  

It doesn't detail about each methods level information since that are covered in the [javadoc](https://github.com/mosip/mosip/tree/master/docs/javadocs/registration/apidocs) of this module.   


## Functionality Vs Technical Component mapping: 

|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Post successful login, session context would be created. That will be used throughout the application at the required places. The user detail and the respective roles are encapsulated inside the context. Without creation of this context object, the packet can't be created. |  
|**Main Service class and method:**| SessionContext.create(UserDTO userDTO, String loginMethod, boolean isInitialSetUp, boolean isUserNewToMachine, AuthenticationValidatorDTO authenticationValidatorDTO) |  
|**Input parameter:**| UserDTO – It should contain info of id, name, roles, center-id. loginMethod – possible values are PWD, OTP, FINGERPRINT, FACE, IRIS. isInitialSetUp – true/false, isUserNewToMachine – true/false,  AuthenticationValidatorDTO – should contain id, password, otp|  
|**Auth:**| Not required. |  
|**External Connectivity:**| Service and DB |  


|**Functionality:**| Packet Creation - New Registation / Update UIN/ Lost UIN |   
|:------:|-----|  
|**Technical Detail:**| Based on the business need [New Registation / Update UIN/ Lost UIN] this 'RegistrationDTO' object should be populated with the relevant  data and also pass the 'RegistrationMetaDataDTO.RegistrationCategory' as [New/ Update/ Lost].  |
|**Main Service class and methods**| PacketHandlerService.handle(RegistrationDTO registrationDTO)|  
|**Input Parameter:**|  The RegistrationDTO object contains the RID, PRID, registration details of the individual and also contains the officer and supervisor details. This object has the following sub-classes: a. DemographicDTO - Details of the Demographic and Documents, b. BiometricDTO - Biometrics (Fingerprints, Irises, Face and Exception Face) of the individual, parent (or guardian), officer and supervisor, c.  RegistrationMetaDataDTO - Meta data related to registration and d. OSIDataDTO - Details of the officer and supervisor who had authenticated the registration.  |  
|**Auth:**| SessionContext is required for creating the packet |  
|**External Connectivity**| DB, File system |  

     
|**Functionality:**| Packet Upload |   
|:------:|-----|  
|**Main Service class and method:**| PacketUploadService.pushPacket(File packet)|  
|**Input Parameter:**|	File object, which contains the packet to be uploaded.  |  
|**Auth:**| Authentication token required while doing file upload. Based on the SessionContext object the advice would attach the token and invoke the required service call. |  
|**External Connectivity:**| Service, DB, File system |  


|**Functionality:**| Packet Export |  
|:------:|-----|  
|**Main Service class and method:**| PacketExportService.getSynchedRecords() - to fetch the packet to be exported. updateRegistrationStatus(List<PacketStatusDTO> exportedPackets) - update the status once exported. |  
|**Input Parameter:**|	List of packet object. |  
|**Auth:**| No. |  
|**External Connectivity:**| DB, File system |  


|**Functionality:**| Sync Data from Server to Client and Vice Versa. |   
|:------:|-----|  
|**Technical Detail:**| This functionality will be executed as specified as sync-frequency in local DB. During start of the application, the scheduler would be loaded with the jobs configured in db and trigger the job. The scheduler would trigger the jobs at the configured frequency. While running the jobs, based on the functionality it would invoke the respective services and invoke the required external services to sync the data from server to client and vice versa. Post completion or every state of the job execution, the status would be updated in local db.|  
|**Main Service class and methods**|  JobConfigurationServiceImpl.executeAllJobs() - This would load all the active jobs from the local db and trigger the jobs.|  
|**Input Parameter:**|  - |    
|**Auth:**| Auth token required for external services. This would be automatically taken care within this method. Nothing explicitly to be passed.|  
|**External Connectivity:**| REST API calls, DB|



|**Functionality:**|  MDM Integration – Register Device |   
|:------:|-----|  
|**Technical Detail:**| This method automatically scans all devices by connecting to the MDM service, which is running in a particular port and stores it in device registry. |
|**Main Service class and method:**| MosipBioDeviceManager - init()|  
|**Input Parameter:**|  No parameter needed.  |  
|**Auth:**| Not required |  
|**External Connectivity:**| deviceInfo - MDM service REST call |  


|**Functionality:**|  MDM Integration -Capture bio-metric |   
|:------:|-----|  
|**Main Service class and method:**| BioServiceImpl  - getFingerPrintImageAsDTOWithMdm(FingerprintDetailsDTO fpDetailsDTO, String fingerType) |  
|**Input Parameter:**|    FingerprintDetailsDTO – dto contains the finger print related details, fingerType – Type of the device like Fingerprint/ Iris/Face etc |  
|**Auth:**| Not required |  
|**External Connectivity:**| Capture - MDM service REST call |  


|**Functionality:**|  MDM Integration  - Validate bio-metric against the bio value already captured and stored in Database. |   
|:------:|-----|  
|**Main Service class and method:**| BioServiceImpl  - validateFingerPrint(String userId) - based on provided user Id the relevant bio information would be fetched from database and same would be validated against the bio data received from MDM service. |  
|**Input Parameter:**|   mosipBioDeviceManager – scan(String deviceType)|  
|**Auth:**| Not required |  
|**External Connectivity:**| DB, Capture - MDM service REST call |  


|**Functionality:**|  MDM Integration  - Display video stream |   
|:------:|-----|  
|**Main Service class and method:**| Yet to be implemented |  
|**Input Parameter:**|    |  
|**Auth:**| Not required |  
|**External Connectivity:**| |  


|**Functionality:**| TPM Public Key Sync |   
|:------:|-----|  
|**Technical Detail:**| This service will be executed during initial set-up of registration client application. This service gets the Public Part of the Key used for signing from the TPM. Uploads this public key along with the machine name to the server. This service returns the key index which will be used for Master Sync Service|  
|**Main Service class and method:**| TPMPublicKeySyncService.syncTPMPublicKey()|  
|**Input Parameter:**|  NA |  
|**Auth:**| TPM 2.0 is required for this service |  
|**External Connectivity:**| TPM, Web Service |


## Table Detail :

|**Table Name**| **Description** |
|:------:|-----|
|biometric_attribute| Information about biometric attribute will be stored in db from master sync |
|biometric_type | Information about biometric type will be stored in db from master sync |
|blacklisted_words| Black Listed words will be stored in db from master sync |
|device_master| device master related information will be stored in db from master sync |
|device_spec| device specifiaction related information will be stored in db from master sync |
|device_type| device type related information will be stored in db from master sync |
|doc_category| document category information will be stored in db from master sync |
|doc_type| document type information will be stored in db from master sync |
|gender| gender information will be stored in db from master sync |
|id_type| identity type information will be stored in db from master sync |
|language| language information will be stored in db from master sync |
|location| location information will be stored in db from master sync |
|machine_master| machine master details will be stored in db from master sync |
|machine_spec| machine specification details will be stored in db from master sync |
|machine_type| machine type details will be stored in db from master sync |
|reason_category| packet rejection reason category details will be stored in db from master sync |
|reason_list| packet rejection reason list details will be stored in db from master sync |
|reg_center_device| center device info will be stored in db from master sync |
|reg_center_machine| center machine info will be stored in db from master sync |
|reg_center_machine_device| center machine device info will be stored in db from master sync |
|reg_center_type| center type details will be stored in db from master sync |
|reg_center_user| center user details will be stored in db from master sync |
|reg_center_user_machine| center user machine details will be stored in db from master sync |
|registration_center| registration center information will be stored in db from master sync |
|template| Template details  will be stored in db from master sync |
|template_type| Template type details  will be stored in db from master sync |
|title| Title details  will be stored in db from master sync |
|valid_document| Valid documnet details  will be stored in db from master sync |
|sync_job_def| Sync jobs related data will be inserted into db from master sync|
|screen_authorization| Screen authorization related data will be inserted into db from master sync|
|app_authentication_method| authentication type related data will be inserted into db from master sync|
|app_detail| application details will be inserted into db from master sync|
|app_role_priority| application roles priority details will be inserted into db from master sync|
|role_list| role related details will be inserted into db from master sync|
|GLOBAL_PARAM| Cofiguration related data |
|user_detail| User related data will be inserted into db from user detail sync|
|user_pwd| User password related data will be inserted into db from user detail sync|
|user_role| User role related data will be inserted into db from user detail sync|
|user_biometric| User biometric related data will be inserted into db while onBoarding|
|key_store| Public key , Packet creation key will be inserted into db while Public key Sync and Policy sync |
|sync_control| Succesful sync jobs will stored along with its last time stamp|
|sync_transaction| All sync transaction related data will be stoted in DB |
|sync_transaction| All sync transaction related data will be stoted in DB |
|registration| Registration Packet related data will be stoted in DB |
|registration_transaction| Transactions of registration Packet data will be stoted in DB |
|process_list| Authentication process data will be stoted in DB |
|pre_registration_list| pre registration data will be stoted in DB |
|audit_log_control| All auditing detail data will be stoted in DB |

