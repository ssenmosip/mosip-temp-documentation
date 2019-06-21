# ID-Authentication Dependencies List

### 1 Prerequisites : <br><sub>Dependent DB/External applications and services</sub></br>
Dependency|Component|Description (If any)
-----|--------------|----------------
DB|mosip_ida|Required for persisting Authentication Transactions.


### 2 Prerequisites : <br><sub>Dependent module/component with their respective versions should be mentioned here</sub></br>
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


