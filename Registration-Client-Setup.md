**Registration Client - Application Setup Process:** 
***

This document contains the information about the 'Registration client' application initial setup process to be followed by the Registration officers to setup the same into their local desktop machine.     

The Registration client application is delivered into two parts:  
   1. Zip file - Contains Application Base folder structure with installed derby DB.      
   2. Application Binaries.  - Contains the application runtime jars.  


**Installation at Desktop Machine:**   
***  
**Zip file:**  
   1. User login to the Admin portal and download the client application ZIP file.  
   2. Once downloaded then unzip the file into a particular location. It contains the following structure.    
      - lib : it contains the library required for the application to start.  
      - prop : it contains the property file that will be used by application.    
      - log : the application log file would be written under this folder.    
      - db : it contains the derby database, tables and few table with the data.      
   3. Store the DB boot key into the TPM [Trusted Platform Module].  
   
**Application Binaries:**  
When user clicks on the 'main.jar' it does the following :  
   1. It loads the binary repository URL from property file.
   2. Communicate with the  JFrog repository through secured connection.  
   3. Download the latest build [TBD] Manifest.mf file from server, where all the jars (including shared lib) name and checksums are provided.  
   4. Compare the checksum of local version of jar files with the data present in Manifest.mf file.    
   5. Identify the list of binary files to be downloaded and initiate the secured connection to JFrog repo.  
   6. Download the required jars.  
   7. Start the application.      

**Anti Virus:**  
   Installation of Open Source Anti Virus Software [ClamAV]:  
   1.	Download the ClamAV from the below url  
   		https://www.clamav.net/downloads  
   		
   	2.	Install the downloaded .exe file.  
   	
   ClamAV Config Setup:  

    1.Copy C:\Program Files\ClamAV\conf_examples\clamd.conf.sample file  
      Paste as C:\Program Files\ClamAV\conf_examples\clamd.conf  

    2.Copy C:\Program Files\ClamAV\conf_examples\ freshclam.conf.sample file  
      Paste as C:\Program Files\ClamAV\conf_examples\ freshclam.conf  
        
    3.Comment the line# 8(Example) in both the files    

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

   **Once all the Configurations are done run the “freshclam.exe” and then run “clamd.exe”.**  

**Database:**  
   - The Derby database will be used to store the local transaction information along with Master and configuration data.   
   - The data stored into the database would be encrypted using a particular boot key password.   
   - The key would be maintained in TPM and same will be used during communication with database from application.   
   - Initial provided DB contains all the required tables with few are only having data.    
   - During sync process the data will be updated into the local database.  

**Application Startup:**     
   - Once application launched then connect to the TPM and pull the required key to communicate with the DB.  
   - Check the data availability in the local DB, if no data available then initiate the Sync [Master/ Configure/ User] process to download the machine [MAC ID] specific center level data from MOSIP server environment.  
   - During initial setup, until the data gets synch from server the user can't use the application.     
   - Before initialize the installation process, user should make sure that the local system meets the runtime / hardware requirement.    


**Update Process:**
***
   **Database update:**  
   If database to be updated to the next version then update the same in the Docker image [JFROG repository] and that will get downloaded through the respective Docker pull statement. Docker pull only download the updated layer [not all layers]
   
   **Application update:**  
   Through application the version of Docker Image between the local repository and remote repository will be validated. If there is any difference in the version, then prompt the user to complete the current process [Registration and pushing packet] and initiate the software update process.
   

**User Mapping to the Local machine:** 
***  
   User can do the self-mapping to the local machine by using their user id and password [which is provided by admin user] and OTP shared to their mobile/ email id. 
   The existing user configured in Admin portal for a particular registration center can only be tagged to the local machine. 

    	
**Security:** 
***
   **Data Security:**  
   While storing the data into the local database the data would be encrypted and same would be decrypted while retrieving the same from db. The key required for the database encryption/decryption would be stored into the TPM and same will be fetched when the application start up.  
The packet created during registration process and downloaded from pre-registration application would be encrypted using asymmetric and symmetric key.   
The asymmetric key received from MOSIP server will be used for encryption of registration packet and it can only be decrypted at server end only. At regular interval the encryption public key at Registration client would be updated.
The Symmetric key would be generated on runtime and same will be used during the pre-registration packet decryption.  
   
   
   **Key management:**  
   The key required for encryption / decryption at different process of an application would be maintained in database [encrypted format] and TPM.
   
   TPM  - it will hold the DB encryption and decryption key.
   DB 	- it will hold the pre-registration symmetric key, which is generated during runtime and it will not be downloaded from server.  
       - it will also hold the center specific public key to encrypt the Registration packet, which is downloaded and refreshed from server at a regular interval.      
 
   **REST Service integration Authentication:**  
   When application is having online connectivity, it may need to push and pull the packet and the respective status from server.
Whenever communication happening with online services the OAuth token need to be generated and should be attached to the header of the http request. 
To generate the OAuth token the client secret key / login user id / password would be passed to the â€˜Loginâ€™ REST service. If success it will provide us the valid OAuth token in the http response. The same token would be passed during rest of REST service communication. 


**System Prerequisites:**
*** 
   -CPU - Dual Core Processor - 2GHZ  
   -Ram - 8 GB  
   -Local Storage Disk Space - 500 GB 
   -USB 2.0 ports or equivalent hub.  
   -Physical machine with TPM facility.   
 
**Data Setup:**  
***
In Registration client application, only user mapping to the local machine can be performed. Rest of the data setup should be taken care at MOSIP Admin portal.
Through sync process the data would be sync between local machine and server based on machine mac-id and center id.

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


**Archival Policy:**
***
   At the regular interval the old / historical transactional data in the client database / logs would be deleted.
   The batch process which is running at the client application, will do this process based on the defined configuration in DB table.

   **List of data to be archived:** 
   1.	Transaction data in database
   2.	Audit log in database
   3.	Logs in local machine.
   4.	Generated Registration and Pre-Registration packet.


**To Be Discussed:**   
***  
   1. Need to decide whether we need to follow the Auto update/ manual update approach?  	
   2. How to load key into TPM? The respective rotation policy?  
   3. How to update the DB password/ encryption key?  
   4. If any db table structure got changed / new table added then how to syncup the same in client machines?  
  
  
   