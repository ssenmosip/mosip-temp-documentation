**Registration Client - Installation and Configuration:** 
***

This document contains the 'Registration client' application initial setup and configuration process at local machine.     

![Registration client Setup](_images/registration/reg-client-app-install-process1.png)   

**Prerequisites:**  
***
**System Prerequisites:**  
   - CPU - Dual Core Processor - 2GHZ  
   - Ram - 16 GB  
   - Local Storage Disk Space - 500 GB 
   - USB 2.0 ports or equivalent hub.  
   - Physical machine with TPM 2.0 facility.   
   - Windows OS [10 v] 

**Application Prerequisites:**  
   Before running the 'Registration client' application, following prerequisites to be completed.
	
   - User should have online connectivity to the application JFrog repository. 
     {13.71.87.138:8040/artifactory/libs-release/io/mosip/registration/registration-client/}	   
   - User setup in MOSIP Admin Portal and IAM system.  
   - Machine [machine name or mac id] and center configuration.  
   - Machine with center mapping configuration.  
        
**Anti Virus - ClamAV Setup and Configuration in local machine:**  
***  
   Installation of Open Source Anti Virus Software [ClamAV]:  
   1.	Download the ClamAV (Version: 0.101.2) Anti Virus Software - [link](http://www.clamav.net/downloads)  
   2.	Install the downloaded .exe file.  
   	
   **ClamAV Config Setup:**     
     1. Rename the **clamd.conf.sample** to **clamd.conf** from the installed directory of ClamAV.   
        Ex: C:\Program Files\ClamAV\conf_examples\clamd.conf.sample file   
            save as  C:\Program Files\ClamAV\conf_examples\clamd.conf   
    2.Rename the **freshclam.conf.sample** to **freshclam.conf** from the installed directory of ClamAV.
        Ex: C:\Program Files\ClamAV\conf_examples\ freshclam.conf.sample file  
            save as C:\Program Files\ClamAV\conf_examples\ freshclam.conf  
    3.Comment the line# 8(Example) in both the files  
    4. Update Config files:   
      
    **clamd.conf file changes:**  
      1.	Uncomment LogFile "C:\Program Files\ClamAV\clamd.log"(Line 14)
   
    **freshclam.conf file changes:**  
     Uncomment the below mentioned lines in the file,  
    1.	DatabaseDirectory - "C:\Program Files\ClamAV\database"(Line 13)  
    2.	UpdateLogFile     - "C:\Program Files\ClamAV\freshclam.log"(Line 17)  
    3.	DatabaseMirror    - db.XY.clamav.net(Line 69)  change XY to our country code  
    4.	DatabaseMirror    - database.clamav.net(Line 75)   
    5.	Checks 24(Line 113)  
    6.	LocalIPAddress aaa.bbb.ccc.ddd(Line 131)  change to our machine IP address   

   **Once all the Configurations are done run the freshclam.exe and then run clamd.exe. If required, restart the machine.**   
 
**Installation at Desktop Machine:**   
***  
**Zip file:**  
   
   1. User login to the JFROG Binary portal and download the client application ZIP file [mosip-sw-0.*.*.zip].   
   2. Once downloaded then unzip the file into a particular location. It contains the following folder structure.  
      - bin : It contains the client UI and service executable in encrypted format.
      - lib : it contains the library required for the application to start.  
      - prop : it contains the property file that will be used by application.    
      - cer  : it contains the certificate used to communicate with the MOSIP server.
      - log : the application log file would be written under this folder.    
      - db : it contains the derby database, tables and few table with the data.  
      - run.jar : Executable jar to download the s/w.
      - MANIFEST.MF : Third Party libraries information.
   3. Click the 'run.jar or run.bat' to initiate the setup process.  
   
   When user clicks on the 'run.jar' it does the following :  
   1. It loads the binary repository URL from property file.  
   2. Communicate with the  JFrog repository through secured connection and download the maven-metadata.xml file to identify the latest jar versions.    
   3. Download the latest build Manifest.mf file from server, where all the jars (including shared lib) name and checksums are provided.  
   4. Compare the checksum of local version of jar files with the data present in latest downloaded Manifest.mf file.    
   5. Identify the list of binary files and Download the required jars.  
   6. Once download completed then communicate with TPM to decrypt the key, which is used to decrypt the UI and service jars.  
   7. Place the jar to the User temp directory and start the application.  
   
**Application Startup:**  
   - Once application launched then connect to the TPM and pull the required key to communicate with the DB.  
   - User should initially be online to validate their authentication against the MOSIP server. Post which, the sync process would be initiated.     
   - Check the data availability in the local DB, if no data available then initiate the Sync [Master/ Configure/ User] process to download the machine [MAC ID] specific center level data from MOSIP server environment.  
   - During initial setup, the application should have online connectivity with the MOSIP server to synch the configuration detail from server to local machine.       
   - Before initialize the installation process, user should make sure that the local system meets the runtime / hardware requirement.    

**External hardware Driver(s):**
   This section covers the list of drivers required to communicate with the external devices.  
   - To integrate with Scanner, windows WIA libraries are used. So, the respective service should be running and also the scanner specific driver should also be installed.  
   - The application has been currently tested with CANON LiDE 120.  
   - Printer should be available to take the print out from application and the respective driver should be installed.    
   - Camera and the respective driver should be available to capture the applicant photo. Application tested with Logitech camera.  
   - TPM 2.0 should be enabled to secure the application.  

**Configuration:**  
   Application provided with the facility of multiple configurations for different set of parameters. Each attribute level configuration changes should be performed at 'Config' server and same should be sync to the local machine to reflect the changes.  

|**S.No.**| **Config Key**| **Description**|**Possible Values**|
|:------:|-----|---|---|
|1	.|	mosip.registration.iris_threshold									   | 60							|	
|2	.|	mosip.registration.leftslap_fingerprint_threshold                      | 70							|	
|3	.|	mosip.registration.num_of_fingerprint_retries                          | 3							|	
|4	.|	mosip.registration.num_of_iris_retries                                 | 3							|	
|5	.|	mosip.registration.rightslap_fingerprint_threshold                     | 80							|	
|6	.|	mosip.registration.thumbs_fingerprint_threshold                        | 80							|	
|7	.|	mosip.registration.loginmode                                           | bootable dongle			|	
|8	.|	mosip.registration.facequalitythreshold                                | 25							|	
|9	.|	mosip.registration.faceretry                                           | 12							|	
|10	.|	mosip.registration.supervisorverificationrequiredforexceptions         | true						|	
|11	.|	mosip.registration.operatorregsubmissionmode                           | fingerprint				|	
|12	.|	mosip.registration.supervisorauthmode                                  | iris						|	
|13	.|	mosip.registration.emailnotificationtemplateotp                        | hello $user the otp is $otp|	
|14	.|	mosip.registration.smsnotificationtemplateotp                          | otp for your request is $otp|	
|15	.|	mosip.registration.emailnotificationtemplatenewreg                     | hello $user the otp is $otp|	
|16	.|	mosip.registration.smsnotificationtemplatenewreg                       | otp for your request is $otp|	
|17	.|	mosip.registration.emailnotificationtemplateregcorrection              | hello $user the otp is $otp|	
|18	.|	mosip.registration.smsnotificationtemplateregcorrection                | otp for your request is $otp|	
|19	.|	mosip.registration.emailnotificationtemplateupdateuin                  | hello $user the otp is $otp|	
|20	.|	mosip.registration.smsnotificationtemplateupdateuin                    | otp for your request is $otp|	
|21	.|	mosip.registration.emailnotificationtemplatelostuin                    | hello $user the otp is $otp|	
|22	.|	mosip.registration.smsnotificationtemplatelostuin                      | otp for your request is $otp|	
|23	.|	mosip.registration.passwordexpirydurationindays                        | 3							|	
|24	.|	mosip.registration.keyvalidityperiodregpack                            | 3							|	
|25	.|	mosip.registration.keyvalidityperiodpreregpack                         | 3							|	
|26	.|	mosip.registration.retentionperiodaudit                                | 3							|	
|27	.|	mosip.registration.automaticsyncfreqservertoclient                     | 25							|	
|28	.|	mosip.registration.blockregistrationifnotsynced                        | 10							|	
|29	.|	mosip.registration.maxdurationregpermittedwithoutmasterdatasyncindays  | 10							|	
|30	.|	mosip.registration.maxdurationwithoutmasterdatasyncindays              | 7							|	
|31	.|	mosip.registration.modeofnotifyingindividual                           | mobile						|	
|32	.|	mosip.registration.nooffingerprintauthtoonboarduser                    | 10							|	
|33	.|	mosip.registration.noofirisauthtoonboarduser                           | 10							|	
|34	.|	mosip.registration.multifactorauthentication                           | true						|	
|35	.|	mosip.registration.gpsdistanceradiusinmeters                           | 3							|	
|36	.|	mosip.registration.officerauthtype                                     | password					|	
|37	.|	mosip.registration.supervisorauthtype                                  | password					|	
|38	.|	mosip.registration.defaultdob                                          | 1-jan						|	
|39	.|	mosip.registration.maxdocsizeinmb                                      | 150						|	
|40	.|	mosip.registration.modeofcommunication                                 | sms,email					|	
|41	.|	mosip.registration.masterSyncJob.frequency                             | 190						|	
|42	.|	mosip.registration.preRegistrationDataSyncJob.frequency                | 190						|	
|43	.|	mosip.registration.packetSyncStatusJob.frequency                       | 190						|	
|44	.|	mosip.registration.keyPolicySyncJob.frequency                          | 190						|	
|45	.|	mosip.registration.registrationDeletionJob.frequency                   | 190						|	
|46	.|	mosip.registration.synchConfigDataJob.frequency                        | 190						|	
|47	.|	mosip.registration.deleteAuditLogsJob.frequency                        | 190						|	
|48	.|	mosip.registration.regUserMappingSyncJob.frequency                     | 190						|	
|49	.|	mosip.registration.preRegistrationPacketDeletionJob.frequency          | 190						|	
|50	.|	mosip.registration.registrationPacketSyncJob.frequency                 | 190						|	
|51	.|	mosip.registration.Login_Credentials_Sync.frequency                    | 190						|	
|52	.|	mosip.registration.Registration_Client_Setup_Sync.frequency            | 190						|	
|53	.|	mosip.registration.Registration_Client_Config_Sync.frequency           | 190						|	
|54	.|	mosip.registration.User_Role_Setup_Sync.frequency                      | 190						|	
|55	.|	mosip.registration.packet.maximum.count.offline.frequency              | 100						|	
|56	.|	mosip.registration.distance.from.machine.to.center                     | 230						|	
|57	.|	mosip.registration.geo.capture.frequency                               | n							|	
|58	.|	mosip.registration.user_on_board_threshold_limit                       | 1							|	
|59	.|	mosip.registration.fingerprint_disable_flag                            | y							|	
|60	.|	mosip.registration.iris_disable_flag                                   | y							|	
|61	.|	mosip.registration.face_disable_flag                                   | y							|	
|62	.|	mosip.registration.document_disable_flag                               | y							|	
|63	.|	mosip.registration.supervisor_authentication_configuration             | y							|	
|64	.|	mosip.registration.username_pwd_length                                 | 50							|	
|65	.|	mosip.registration.finger_print_score                                  | 100						|	
|66	.|	mosip.registration.quality_score                                       | 60							|	
|67	.|	mosip.registration.capture_time_out                                    | 100000						|	
|68	.|	mosip.registration.document_size                                       | 1000000					|	
|69	.|	mosip.registration.pre_reg_no_of_days_limit                            | 5							|	
|70	.|	mosip.registration.document_scanner_dpi                                | 75							|	
|71	.|	mosip.registration.document_scanner_brightness                         | 10							|	
|72	.|	mosip.registration.document_scanner_contrast                           | 10							|	
|73	.|	mosip.registration.document_scanner_doctype                            | jpg						|	
|74	.|	mosip.registration.uin_update_config_flag                              | y							|	
|75	.|	mosip.registration.uin.update.configured.fields                        | name,age,gender,address,phone,email,parentOrGuardianDetails,foreigner,biometrics,cnieNumber|	
|76	.|	mosip.registration.re_capture_time                                     | 10							|	
|77	.|	mosip.registration.key_policy_sync_threshold_value                     | 1							|	
|78	.|	mosip.registration.max_reg_packet_size                                 | 5							|	
|79	.|	mosip.registration.registartion_center                                 | 20916						|	
|80	.|	mosip.registration.reg_pak_max_cnt_apprv_limit                         | 100						|	
|81	.|	mosip.registration.reg_pak_max_time_apprv_limit                        | 30							|	
|82	.|	mosip.registration.eod_process_config_flag                             | y							|	
|83	.|	mosip.registration.audit_log_deletion_configured_days                  | 10							|	
|84	.|	mosip.registration.reg_deletion_configured_days                        | 45							|	
|85	.|	mosip.registration.pre_reg_deletion_configured_days                    | 45							|	
|86	.|	mosip.registration.sync_transaction_no_of_days_limit                   | 5							|	
|87	.|	mosip.registration.invalid_login_count                                 | 3							|	
|88	.|	mosip.registration.invalid_login_time                                  | 2							|	
|89	.|	mosip.registration.gps_device_enable_flag                              | y							|	
|90	.|	mosip.registration.gps_device_model                                    | gpsbu343connector			|	
|91	.|	mosip.registration.gps_port_timeout                                    | 1000						|	
|92	.|	mosip.registration.gps_serial_port_linux                               | /dev/ttyusb0				|	
|93	.|	mosip.registration.gps_serial_port_windows                             | com4						|	
|94	.|	mosip.registration.ui_sync_data                                        | y							|	
|95	.|	mosip.registration.last_export_registration_config_time                | 10							|	
|96	.|	mosip.registration.cbeff_only_unique_tags                              | N							|	
|97	.|	mosip.registration.audit_application_id                                | REG						|	
|98	.|	mosip.registration.audit_application_name                              | REGISTRATION				|	
|99	.|	mosip.registration.audit_default_host_ip                               | 120.0.0.0					|	
|100.|	mosip.registration.audit_default_host_name                             | localhost					|	
|101.|	mosip.registration.packet_store_date_format                            | dd-MMM-yyyy				|	
|102.|	mosip.registration.identity_class_name                                 | io.mosip.registration.dto.demographic.MoroccoIdentity|	
|103.|	mosip.kernel.jsonvalidator.property-source			                  |  LOCAL						|	
|104.|	mosip.kernel.jsonvalidator.file-storage-uri                           | LOCAL						|	
|105.|	mosip.registration.registration_packet_store_location              | ..//PacketStore			|	
|105.|	mosip.registration.max_age                                         | 150						|	
|107.|	mosip.registration.age_limit_for_child                             | 3							|	
|108.|	mosip.registration.face_recapture_time                             | 10							|	
|109.|	mosip.registration.sync_data_freq                                  | 0 0 11 * * ?				|	
|110.|	mosip.registration.registration_pre_reg_packet_location            | ..//PreRegPacketStore		|	
|111.|	mosip.registration.otp_channels                                    | mobile						|	
|112.|	mosip.kernel.xsdstorage-uri                                       |  LOCAL						|	
|113.|	mosip.kernel.xsdfile                            |  LOCAL						|	
|114.|	mosip.registration.ideal_time                                      |  600						|	
|115.|	mosip.registration.refreshed_login_time                            | 540						|	
|116.|	mosip.registration.leftslap_fingerprint_threshold                  | 80							|	
|117.|	mosip.registration.rightslap_fingerprint_threshold                 | 80							|	
|118.|	mosip.registration.thumbs_fingerprint_threshold                    | 80							|	
|119.|	mosip.kernel.transliteration.arabic-language-code                           | ara	|	
|120.|	mosip.kernel.transliteration.franch-language-code        |  fra	|	
|121.|	mosip.registration.lost_uin_disable_flag                    |  y|	
|122.|	mosip.registration.softwareUpdateCheck_configured_frequency                                     |  10|	
|123.|	mosip.registration.is_software_update_available                                     |  Y|	
|124.|	mosip.registration.consent_eng                              | I provide my consent for storage and utilization of my personal data.	|	
|125.|	mosip.registration.consent_ara                             |.|
|126.|	mosip.registration.consent_fra                                |Je donne mon consentement pour le stockage et l'utilisation de mes données personnelles.|
|127.|	mosip.registration.webcam_name                           |logitech|
|128.|	mosip.registration.webcam_library_name                   | sarxos|
|129.|	mosip.registration.document_scanner_enabled				|no|
|130.|	mosip.registration.send_notification_disable_flag        |y|
|131.|	mosip.kernel.idobjectvalidator.file-storage-uri     | LOCAL|
|132.|	mosip.kernel.idobjectvalidator.schema-name       |mosip-identity-json-schema.json|
|133.|  mosip.kernel.idobjectvalidator.property-source | LOCAL|

**Database:**  
   - The Derby database will be used to store the local transaction information along with Master and configuration data.   
   - The data stored into the database would be encrypted using a particular boot key password, which is secured in TPM.     
   - The initial DB contains all the required empty tables along with few tables are having data.    
   - Through sync process the data would be updated into the local database from server.  
   - The user mapped to the local machine would be pushed to the server through sync process.  
   

**Update Process:**
***
   **Application update:**
   - The application binary update is validated during startup of the application by downloading maven-metadata.xml file from JFROG repository. If any library version difference found with the version available at the local system then display the message to the user to initiate the update process. User can either choose the 'Update Now' or 'Update Later' option to initiate the update process or postponed to implement it later. User can initiate the 'Update' process post login to the application.  
   
   **Database update:**  
   - The database update would be rolled out through the binary update process. If any changes in the script then the respective script would be attached inside registration-service/resource/sql this folder and deliver the jar with newer version. During update process the jar would be downloaded and script inside the jar would be executed.  It would also contains the 'rollback' script if update process to be rollbacked due to any technical error. 

    	
**Initial - Data Setup:**  
***
In Registration client application, only user mapping to the local machine can be performed. Rest of the data setup should be performed at MOSIP Admin portal.
Through sync process the data would be sync between local machine and server based on machine's mac-id and center id.

   **Sync Service :**  
   The following data would be sync from Server to local db through the multiple sync jobs and the same to be setup at server by Admin.   
   
   1.	User Profile Setup. 
   2.	User Authentication Setup. 
   3.	Role Setup. 
   4.	Master Data Setup at application level. 
   5.	Application configuration setup. 
   6.	Device Configuration. 
   7.	Registration Center Configuration. 
   8.	Machine Configuration. 
   9.	Center to Machine mapping. 
   10.	Center User mapping. 
   11.  Policy sync.  


**Archival Policy:**
***
   At the regular interval the old / historical transactional data in the client database / logs would be deleted.
   The batch process which is running at the client application, will do this process based on the defined configuration in DB table.

   **List of data to be archived:** 
   1.	Transaction data in database
   2.	Audit log in database
   3.	Logs in local machine.
   4.	Generated Registration and Pre-Registration packet.


