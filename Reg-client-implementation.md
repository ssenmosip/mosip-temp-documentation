# Registration Client Developer Documentation

*** 
This document guide the developer to find the traceability between functionality and the respective technical component.  The provided technical classes are available in the package of 'registration-service' module. In this module the required functions are exposed as public method and that can be used to obtain the required features.  

It doesn't detail about each methods level information since that are covered in the [javadoc](https://github.com/mosip/mosip/tree/master/docs/javadocs/registration/apidocs) of this module.   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Post successful login, session context would be created. That will be used throughout the application at the required places. The user detail and the respective roles are encapsulated inside the context. Without creation of this context object, the packet can't be created. |  
|**Main Service class and method:**| SessionContext.create(UserDTO userDTO, String loginMethod, boolean isInitialSetUp, boolean isUserNewToMachine, AuthenticationValidatorDTO authenticationValidatorDTO) |  
|**Input parameter:**| UserDTO – It should contain info of id, name, roles, centerid. 
  loginMethod – possible values are PWD, OTP, FINGERPRINT, FACE, IRIS. 
  isInitialSetUp – true/false, isUserNewToMachine – true/false,  AuthenticationValidatorDTO – should contain id, password, otp|  
|**Auth:**| Not required. |  
|**External Connectivity:**| Service and DB |  

     
|**Functionality:**| Packet Upload |   
|:------:|-----|  
|**Main Service class and method:**| PacketUploadService.pushPacket(File packet)|  
|**Input Parameter:**|	File object, which contains the packet to be uploaded. |  
|**Auth:**| Required during packet upload to MOSIP server. |  
|**External Connectivity:**| Service, DB, File system |  


|**Functionality:**| Packet Export |  
|:------:|-----|  
|**Main Service class and method:**| PacketExportService.getSynchedRecords() - to fetch the packet to be exported.  
   updateRegistrationStatus(List<PacketStatusDTO> exportedPackets) - update the status once exported. |  
|**Input Parameter:**|	List of packet object. |  
|**Auth:**| No. |  
|**External Connectivity**| DB, File system |  

