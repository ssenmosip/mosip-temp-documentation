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

|:------:|-----|
|**Table Name**| biometric_attribute |
|**Detail of table**| Information about biometric attribute will be stored in db from master sync |

|:------:|-----|
|**Table Name**| biometric_type |
|**Detail of table**| Information about biometric type will be stored in db from master sync |

|:------:|-----|
|**Table Name**| blacklisted_words |
|**Detail of table**| Black Listed words will be stored in db from master sync |

|:------:|-----|
|**Table Name**| device_master |
|**Detail of table**| device master related information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| device_spec |
|**Detail of table**| device specifiaction related information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| device_type |
|**Detail of table**| device type related information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| doc_category |
|**Detail of table**| document category information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| doc_type |
|**Detail of table**| document type information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| gender |
|**Detail of table**| gender information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| id_type |
|**Detail of table**| identity type information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| language |
|**Detail of table**| language information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| location |
|**Detail of table**| location information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| machine_master |
|**Detail of table**| machine master details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| machine_spec |
|**Detail of table**| machine specification details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| machine_type |
|**Detail of table**| machine type details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reason_category |
|**Detail of table**| packet rejection reason category details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reason_list |
|**Detail of table**| packet rejection reason list details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reg_center_device |
|**Detail of table**| center device info will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reg_center_machine |
|**Detail of table**| center machine info will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reg_center_machine_device |
|**Detail of table**| center machine device info will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reg_center_type |
|**Detail of table**| center type details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reg_center_user |
|**Detail of table**| center user details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| reg_center_user_machine |
|**Detail of table**| center user machine details will be stored in db from master sync |

|:------:|-----|
|**Table Name**| registration_center |
|**Detail of table**| registration center information will be stored in db from master sync |

|:------:|-----|
|**Table Name**| template |
|**Detail of table**| Template details  will be stored in db from master sync |

|:------:|-----|
|**Table Name**| template_type |
|**Detail of table**| Template type details  will be stored in db from master sync |

|:------:|-----|
|**Table Name**| title |
|**Detail of table**| Title details  will be stored in db from master sync |

|:------:|-----|
|**Table Name**| valid_document |
|**Detail of table**| Valid documnet details  will be stored in db from master sync |

|:------:|-----|
|**Table Name**| sync_job_def|
|**Detail of table**| Sync jobs related data will be inserted into db from master sync|

|:------:|-----|
|**Table Name**| screen_authorization |
|**Detail of table**| Screen authorization related data will be inserted into db from master sync|

|:------:|-----|
|**Table Name**| app_authentication_method|
|**Detail of table**| authentication type related data will be inserted into db from master sync|

|:------:|-----|
|**Table Name**| app_detail|
|**Detail of table**| application details will be inserted into db from master sync|

|:------:|-----|
|**Table Name**| app_role_priority |
|**Detail of table**| application roles priority details will be inserted into db from master sync|

|:------:|-----|
|**Table Name**| role_list |
|**Detail of table**| role related details will be inserted into db from master sync|

|:------:|-----|
|**Table Name**| GLOBAL_PARAM |
|**Detail of table**| Cofiguration related data |

|:------:|-----|
|**Table Name**| user_detail|
|**Detail of table**| User related data will be inserted into db from user detail sync|

|:------:|-----|
|**Table Name**| user_pwd |
|**Detail of table**| User password related data will be inserted into db from user detail sync|


|:------:|-----|
|**Table Name**| user_role |
|**Detail of table**| User role related data will be inserted into db from user detail sync|

|:------:|-----|
|**Table Name**| user_biometric|
|**Detail of table**| User biometric related data will be inserted into db while onBoarding|

|:------:|-----|
|**Table Name**| key_store|
|**Detail of table**| Public key , Packet creation key will be inserted into db while Public key Sync and Policy sync |

|:------:|-----|
|**Table Name**| sync_control |
|**Detail of table**| Succesful sync jobs will stored along with its last time stamp|

|:------:|-----|
|**Table Name**| sync_transaction|
|**Detail of table**| All sync transaction related data will be stoted in DB |

|:------:|-----|
|**Table Name**| sync_transaction|
|**Detail of table**| All sync transaction related data will be stoted in DB |

|:------:|-----|
|**Table Name**| registration |
|**Detail of table**| Registration Packet related data will be stoted in DB |

|:------:|-----|
|**Table Name**| registration_transaction |
|**Detail of table**| Transactions of registration Packet data will be stoted in DB |

|:------:|-----|
|**Table Name**| process_list |
|**Detail of table**| Authentication process data will be stoted in DB |

|:------:|-----|
|**Table Name**| pre_registration_list |
|**Detail of table**| pre registration data will be stoted in DB |

|:------:|-----|
|**Table Name**| audit_log_control|
|**Detail of table**| All auditing detail data will be stoted in DB |













