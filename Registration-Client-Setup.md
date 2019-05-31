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

Refer the configuration maintained in [QA](https://github.com/mosip/mosip-configuration/blob/master/config/registration-qa.properties) environment. 


|**S.No.**| **Config Key**| **Possible Values**|**Description**|
|:------:|-----|---|---|
|1	.|	mosip.registration.fingerprint_disable_flag                            | y							| To disable the fingerprint capture. |	
|2	.|	mosip.registration.iris_disable_flag                                   | y							| To disable the IRIS capture. |	
|3	.|	mosip.registration.face_disable_flag                                   | y							| To disable the Face capture. |	
|4	.|	mosip.registration.document_disable_flag                               | y							| To disable the document capture. | 	
|5	.|	mosip.registration.iris_threshold									   | 60							|	
|6	.|	mosip.registration.leftslap_fingerprint_threshold                      | 70							|	
|7.|	mosip.registration.rightslap_fingerprint_threshold                 | 80							|	
|8.|	mosip.registration.thumbs_fingerprint_threshold                    | 80							|	
|9	.|	mosip.registration.num_of_fingerprint_retries                          | 3							|	
|10	.|	mosip.registration.num_of_iris_retries                                 | 3							|	
|11	.|	mosip.registration.supervisorverificationrequiredforexceptions         | true						| To capture Supervisor approval for exception case. |
|12	.|	mosip.registration.gpsdistanceradiusinmeters                           | 3							|	
|13	.|	mosip.registration.packet.maximum.count.offline.frequency              | 100						| No. of packets can be created in offline mode. |	
|14	.|	mosip.registration.user_on_board_threshold_limit                       | 1							| No. of biometric required to be captured. |	
|15	.|	mosip.registration.finger_print_score                                  | 100						|	
|16	.|	mosip.registration.pre_reg_no_of_days_limit                            | 5							|	
|17	.|	mosip.registration.reg_pak_max_cnt_apprv_limit                         | 100						| Max No. of packets waiting for approval.	|
|18	.|	mosip.registration.reg_pak_max_time_apprv_limit                        | 30							| Max time wait for approval in mins. |	
|19	.|	mosip.registration.eod_process_config_flag                             | y							| Enable/ Disable EOD process. |
|20	.|	mosip.registration.invalid_login_count                                 | 3							| 	
|21	.|	mosip.registration.invalid_login_time                                  | 2							|	
|22	.|	mosip.registration.gps_device_enable_flag                              | y							| Enable / Disable GPS |	
|23	.|	mosip.registration.uin_update_config_flag                              | y							| Enable / Disable update feature. |
|24.|	mosip.registration.lost_uin_disable_flag                    |  y| Enable / Disable Lost UIN functionality. |
|25.|	mosip.registration.webcam_name                           |logitech|
|26.|	mosip.registration.document_scanner_enabled				|no|
|27.|	mosip.registration.send_notification_disable_flag        |y| Enable/ Disable additional notification. |

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


