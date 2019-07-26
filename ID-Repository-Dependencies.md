### 1. Database Dependencies
Dependency|Component|Description (If any)
-----|--------------|----------------
DB|mosip_idrepo|DB scripts are available here - https://github.com/mosip/mosip-platform/tree/master/db_scripts/mosip_idrepo
DB|mosip_idmap|DB scripts are available here - https://github.com/mosip/mosip-platform/tree/master/db_scripts/mosip_idmap 



### 2.  Internal Service Dependencies
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


### 3.  LDAP Roles
Service|LDAP Roles|Description (If any)
--------|-----|--------------
Add Identity|REGISTRATION_PROCESSOR|For Registration Processor
Retrieve Identity by UIN|REGISTRATION_PROCESSOR|For Registration Processor
Retrieve Identity by UIN|ID_AUTHENTICATION|For ID Authentication
Retrieve Identity by RID|REGISTRATION_ADMIN|For Registration Processor
Retrieve Identity by RID|REGISTRATION_SUPERVISOR|For Registration Processor
Retrieve Identity by RID|REGISTRATION_OFFICER|For Registration Processor
Retrieve Identity by RID|ID_AUTHENTICATION|For ID Authentication
Retrieve Identity by RID|REGISTRATION_PROCESSOR|For Registration Processor
Update Identity|REGISTRATION_PROCESSOR|For Registration Processor
Create VID|REGISTRATION_PROCESSOR|For Registration Processor
Retrieve UIN by VID|ID_AUTHENTICATION|For ID Authentication
Update VID|ID_AUTHENTICATION|For ID Authentication