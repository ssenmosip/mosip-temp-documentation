# ID Repository Dependencies List

### 1 Prerequisites : <br><sub>Dependent DB/External applications and services</sub></br>
Dependency|Component|Description (If any)
-----|--------------|----------------
DB|mosip_idrepo|Required for persisting Identity service data.
DB|mosip_idmap|Required for persisting VID service data.



### 2 Prerequisites : <br><sub>Internal Service Dependencies</sub></br>
Module|Component|Description (If any)
-------|--------------|----------------
Kernel|Kernel-Audit Service| Service for auditing
Kernel|Kernel AuthManager Service|Send OTP, Get RID for UserID, Authenticate with ClientId-SecretKey, Validate Token
Kernel|Kernel Crypto Manager service|Encrypt, Decrypt data
Kernel|Kernel ID Validator - UIN|Java API
Kernel|Kernel ID Validator - VID|Java API
Kernel|Kernel ID Generator – VID|Java API
Kernel|Kernel ID Generator – Token ID|Java API
Kernel|Kernel cbeffutil api|Java API
Kernel|Kernel fsadapter hdfs|Java API
Kernel|Kernel idobjectvalidator|Java API
Kernel|Kernel logger logback|Java API


