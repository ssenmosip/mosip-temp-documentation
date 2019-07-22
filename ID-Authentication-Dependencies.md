# ID-Authentication Dependencies

### 1.  Database Dependencies
Dependency|Component|Description (If any)
-----|--------------|----------------
DB|mosip_ida|DB Scripts available here - https://github.com/mosip/mosip-platform/tree/master/db_scripts/mosip_ida


### 2.  Dependent module/component with their respective versions should be mentioned here
Module|Component|Description (If any)
-----|-------------|--------------
ID Repository|ID Repository Identity Service|Get Identity for UIN, Get Identity for RID
ID Repository|ID Repository VID Service|Get UIN for VID
Kernel|Kernel-Audit Service| 
Kernel|Kernel OTP Validator Service|
Kernel|Kernel AuthManager Service|Send OTP, Get RID for UserID, Authenticate with ClientId-SecretKey, Validate Token
Kernel|Mail Notification Service|
Kernel|SMS Notification Service|
Kernel|Master Data Service|Titles, Gender, Templates
Kernel|Kernel Crypto Manager service|Encrypt, Decrypt
Kernel|Kernel Crypto Signature|Sign
Kernel|Kernel UIN Validator|Java API
Kernel|Kernel VID Validator|Java API
Kernel|Kernel Pin Validator|Java API
Kernel|ID Object Validator|Java API
Kernel|Kernel ID Generator – Token ID|Java API
Kernel|Kernel Crypto JCE|Java API - Encryptor
Kernel|Kernel Bio API Provider|Java API - Mock BioAPI provider


### 3.  LDAP Roles required
Service|LDAP Roles|Description (If any)
--------|-----|--------------
Internal Authentication|REGISTRATION_PROCESSOR|For Registration Processor
Internal Authentication|REGISTRATION_ADMIN|For Registration Client
Internal Authentication|REGISTRATION_OFFICER|For Registration Client
Internal Authentication|REGISTRATION_SUPERVISOR|For Registration Client