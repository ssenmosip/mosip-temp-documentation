**Registration Client - Installation and Configuration:** 
***

This document contains the 'Registration client (Reg Client App)' application initial setup, update and configuration process.       

Registration Client application is a desktop based application, that can be used to captures the Demographic and Biometric details of an Individual along with supporting information (proof documents & information about parent /guardian /introducer) and packages the information in a secure way using RSA based algorithm. The information packet can be sent to the server in an online or offline mode for processing.  

The Registration client application leverages the TPM capabilities and secure the data and mark the senders identity in the request before sending to external system. The MOSIP server would validate the request and make sure that the request received from the right source. Every individual machine's TPM public key should be registered at MOSIP server to accept and process the data send by them.   

A Trusted Platform Module (TPM) is a specialized chip on a local machines that stores RSA encryption keys specific to the host system for hardware authentication. Each TPM chip contains an RSA key pair called the Endorsement Key (EK). The pair is maintained inside the chip and cannot be accessed by software. By leveraging this security feature every individual machine would be uniquely registered and identified by the MOSIP server component. 

![Registration client Setup](_images/registration/reg-client-app-install-process1.png)   


**Application Build:**  
***
   **Registration client application is build with four different modules.**     
     registration-client - it contains only UI related code.  
     registration-libs - it contains the code to generate the initial run.bat.   
     registration-mdm-service - Mosip Device Manager service to integrate with BIO device and render the required data in standard format and that will be consumed by the 'registration-services' module.   
     registration-services - it contains the Java API, which would be called from UI module to render the services to the User and capture the detail from User and store it in db or send to external systems through services.    

   **Following files to be modified before build the application:**  
       mosip-application.properties - [registration-libs module] - Contains the environment variable.  
       spring-<env>.properties - [registration-services module] - It contains the environment based REST client url to make different service calls.       

	Post completion of above mentioned changes, build 'mosip-parent' pom.xml file to build the application.  

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
	
   - Before building the 'registration-services' module, all the services URLs should be configured in the **environment specific 'spring-<env>.properties'** file.     
   - Property file **[mosip-application.properties]** should be updated with right environment [env] and other detail.     
   - All **Master data** should be loaded at MOSIP kernel database [Refer MOISP document](https://github.com/mosip/mosip/wiki/Getting-Started#7-configuring-mosip-).    
   - User, machine, center mapping and all other required table and data setup should exists in MOSIP kernel database along with the profile configuration in LDAP server.    [This is required until the Admin module is delivered. Post delivery, all the configuration can be done through Admin module.]   
   - User's machine should have online connectivity to access the JFrog artifactory repository, where the application binaries are available.   
   - If TPM enabled, logged in user to windows machine should have permission to get the public key from TPM device.  
   - The initial DB embedded with the setup process, should contains all the required tables along with the data for few tables.    
   - Through sync process the data would be updated into the local database from server.  
   - All the required **REST services** should be installed and the respective **url should be configured in 'spring'** configuration file.  
        
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
    4.Download the Antivirus database from the following urls and placed it in the database folder(C:\Program Files\ClamAV\database)  
       - http://database.clamav.net/main.cvd  
       - http://database.clamav.net/daily.cvd  
       - http://database.clamav.net/bytecode.cvd  
    5. Update Config files:  
    **clamd.conf file changes:**  
      1.	Uncomment LogFile "C:\Program Files\ClamAV\clamd.log"(Line 14)
   
    **freshclam.conf file changes:**  
     Uncomment the below mentioned lines in the file,  
    1.	DatabaseDirectory - "C:\Program Files\ClamAV\database"(Line 13)  
    2.	UpdateLogFile     - "C:\Program Files\ClamAV\freshclam.log"(Line 17)  
    3.	DatabaseMirror    - db.XY.clamav.net(Line 69)  change XY to our country code [Eg: IN]
    4.	DatabaseMirror    - database.clamav.net(Line 75)   
    5.	Checks 24(Line 113)  
    6.	LocalIPAddress aaa.bbb.ccc.ddd(Line 131)  change to our machine IP address   

   **Once all the Configurations are done run the freshclam.exe and then run clamd.exe. If required, restart the machine.**   
 
**Registration Client installation:**   
***  
**Download - Application Initial Setup file:**  
   
   1. User login to the JFROG artifactory portal and download the client application initial setup ZIP file [mosip-sw-0.12.*.zip].   
   2. Once downloaded then unzip the file into a particular location. It contains the following folder structure.  
      - bin : It contains the client UI and service binaries in encrypted format.
      - lib : It contains the library required for the application to run.  
      - props : It contains the property file that will be used by application.    
      - cer  : It contains the certificate used to communicate with the MOSIP server.  
      - db : It contains the encrypted derby database.   
      - run.bat : batch file to launch the application.  
      - jre : It contains the java runtime engine along with the required dlls. 
      
   3. Click the 'run.bat' to initiate the setup process.  
   
   When user clicks on the 'run.bat' it does the following :  
   1. Loads the binary repository URL from property file.  
   2. Communicate with the  JFrog repository through secured connection and download the maven-metadata.xml file to identify the latest jar versions.    
   3. Download the latest build Manifest.mf file from server, where all the jars (including shared lib) name and checksums are provided.  
   4. Compare the checksum of local version of jar files with the data present in latest downloaded Manifest.mf file.    
   5. Identify the list of binary files and Download the required jars.  
   6. Once download completed then communicate with TPM to decrypt the key{if TPM enabled}, which is used to decrypt the UI and service jars and start the application.   
   
**Application Startup:**  
   - User should initially be online to validate their authentication against the MOSIP server. Post which, the sync process would be initiated.     
   - Once the sync process completed then restart the application to pick the local configuration.  
   - User should perform the self onboarding before start using the application.  


**Update Process:**
***
   **Application update:**
   - During the startup of the application, the software check will be validating against the maven-metadata.xml file from artifactory repository. If any diffs found, application prompts the user with 'Update Now' or 'Update Later' options to install immediately or later. Apart from this there is another menu option available in the application to trigger the 'Update' process post login to the application. The update process would update both the application binaries and DB.
        
   **Database update:**  
   - The database update can be rolled out through the binary update process. If any changes in the script then the respective script would be attached inside 'registration-service/resource/sql' folder and deliver the jar with newer version. During update process the jar would be downloaded and script inside the jar would be executed.  It would also contains the 'rollback' script if update process to be rollbacked due to any technical error.  


**Configuration:**  
***
   Application provided with the facility of multiple configurations for different set of parameters. Each attribute level configuration changes should be performed at 'Config' server and same should be sync to the local machine through kernel services.  Here few of the configurations are listed out that provide the facility to enable and disable the biometric. 

Refer the configuration maintained in [QA](https://github.com/mosip/mosip-configuration/blob/master/config/registration-qa.properties) environment. 

|**S.No.**| **Config Key**| **Sample Values**|**Description**|
|:------:|-----|---|---|
|1	.|	mosip.registration.fingerprint_enable_flag                            | y	/ n			| To disable the fingerprint capture. |	
|2	.|	mosip.registration.iris_enable_flag                                   | y	/ n			| To disable the IRIS capture. |	
|3	.|	mosip.registration.face_enable_flag                                   | y	/ n			| To disable the Face capture. |	
|4	.|	mosip.registration.document_enable_flag                               | y	/ n			| To disable the document capture. | 	
|5	.|	mosip.registration.iris_threshold									   | 0 - 100				|	
|6	.|	mosip.registration.leftslap_fingerprint_threshold                      | 0 - 100				|	
|7.|	mosip.registration.rightslap_fingerprint_threshold                 | 0 - 100				|	
|8.|	mosip.registration.thumbs_fingerprint_threshold                    | 0 - 100					|	
|9	.|	mosip.registration.num_of_fingerprint_retries                          | 3				|	
|10	.|	mosip.registration.num_of_iris_retries                                 | 3				|	
|11	.|	mosip.registration.supervisorverificationrequiredforexceptions         | true			| To capture Supervisor approval for exception case. |
|12	.|	mosip.registration.gpsdistanceradiusinmeters                           | 3				|	
|13	.|	mosip.registration.packet.maximum.count.offline.frequency              | 100			| No. of packets can be created in offline mode. |	
|14	.|	mosip.registration.user_on_board_threshold_limit                       | 1				| No. of biometric required to be captured. |	
|15	.|	mosip.registration.finger_print_score                                  | 100			|	
|16	.|	mosip.registration.pre_reg_no_of_days_limit                            | 5				|	
|17	.|	mosip.registration.reg_pak_max_cnt_apprv_limit                         | 100			| Max No. of packets waiting for approval.	|
|18	.|	mosip.registration.reg_pak_max_time_apprv_limit                        | 30				| Max time wait for approval in mins. |	
|19	.|	mosip.registration.eod_process_config_flag                             | y	/ n			| Enable/ Disable EOD process. |
|20	.|	mosip.registration.invalid_login_count                                 | 3				| 	
|21	.|	mosip.registration.invalid_login_time                                  | 2				|	
|22	.|	mosip.registration.gps_device_enable_flag                              | y	/ n			| Enable / Disable GPS |	
|23	.|	mosip.registration.uin_update_config_flag                              | y	/ n		    | Enable / Disable update feature. |
|24.|	mosip.registration.lost_uin_disable_flag                    |  y	/ n| Enable / Disable Lost UIN functionality. |
|25.|	mosip.registration.webcam_name                           |logitech|
|26.|	mosip.registration.document_scanner_enabled				|no|
|27.|	mosip.registration.send_notification_disable_flag        |y	/ n| Enable/ Disable additional notification. |  


**Property File:**

   There are few properties which can be configured at local machine based on the local system requirement.    
     Eg: TPM - enable / disable flag, artifactory url, environment name.   
   
   **File Location:** props/mosip-application.properties 
     - mosip.env= qa, preqa { environment name. Use the same value in spring profile config.}  
     - mosip.client.url = {JFrog repository url.}  
     - mosip.xml.file.url = {JFrog repository url with maven-metadata.xml file.}  
     - mosip.cerpath= /cer//mosip_cer.cer  
    	
**Sync and Upload Services:**  
***  
   In Registration client application, only user mapping to the local machine can be performed. Rest of the data setup should be performed at MOSIP Admin portal.
Through sync process the data would be sync between local machine and server based on machine's mac-id and center id.  There are other services are available to send the created packet from local machine to remote system.   


|**S.No.**| **Service Name**| **Service Description**|
|:------:|-----|---|
|1	.|	User Detail Sync  | To synchronize the user related information. |	
|2	.|	User salt Sync  | To synchronize the user related salt. |	
|3	.|	Master Data Sync  | To download the master data. |	
|4 	.|	Application configuration Sync  | To synchronize the application configuration from config server. |	
|5	.|	Policy Sync  | To synchronize the key required for packet creation based on center and machine id. |	
|6	.|	MOSIP public key Sync  | To synchronize the MOSIP public key. |	
|7	.|	Pre-registration Data Sync  | To download the center specific pre-registration packet data. |	
|8	.|	Packet Sync  | To upload the list of packet related information before uploading packet . |	
|9	.|	Packet Status reader  | At regular interval read the status of the uploaded packet. |	
|10	.|	Packet Upload  | To upload the packet generated out out New/ Lost UIN / Update UIN process to MOSIP server. |	
|11	.|	Send OTP  | To send the OTP message. |	
|12	.|	Auth Service - UserName and Password  | To get the auth token based on user provided user name and password. |	
|13	.|	Auth Service - UserName and OTP | To get the auth token based on user provided user name and OTP. |	
|14	.|	Auth Service - Client id and Secret Key  | To get the auth token based on client id and secret key. |	
|15	.|	Validate / Invalidate auth Token  | To validate and invalidate the generated token. |	
|16	.|	Notification Service (SMS / EMAIL) | To send notification through SMS / Email channel. |	
|17	.|	ID-Authentication API | To onboard the user based on user's bio authentication. |	



**External hardware Driver(s):**
***
   This section covers the list of drivers required to communicate with the external devices.  
   - To integrate with Scanner, windows WIA libraries are used. So, the respective service should be running and also the scanner specific driver should also be installed.  
   - The application has been currently tested with CANON LiDE 120.  
   - Printer should be available to take the print out from application and the respective driver should be installed.    
   - Camera and the respective driver should be available to capture the applicant photo. Application tested with Logitech camera.  
   
