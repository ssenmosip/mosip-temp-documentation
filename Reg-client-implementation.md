# Registration Client Developer Documentation

*** 
This document guide the developer to find the traceability between functionality and the respective technical component.  The provided technical classes are available in the package of 'registration-service' module. In this module the required functions are exposed as public method and that can be used to obtain the required features.  

It doesn't detail about each methods level information since that are covered in the [javadoc](https://github.com/mosip/mosip/tree/master/docs/javadocs/registration/apidocs) of this module.   


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
|**Auth:**| Auth token required for external services. |  
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



