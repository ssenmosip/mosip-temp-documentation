To generate the first UIN in MOSIP eco-system, refer below for the process.

### 1. Register first user in LDAP:
1. Create Roles in LDAP. For example, Registration Processor, Supervisor, etc.
1. Create individual x in LDAP > Map role “Registration Processor” and “Supervisor”
1. Provide preferred User name/password
### 2. Relevant Master data should be created:
All data to be stored as part of id object, for example, Gender, Location hierarchy, templates, etc. should be setup - Through csv utility
#### 2.1 Master data of User, machine, device and center should be created
All necessary Centre-machine-device-user mappings should be completed – Through csv utility
### 3. Generation of RID/UIN for first user:
1. Registration Processor to call RID Generator for RID generation
1. Registration Processor to call UIN Generator for UIN generation for individual x
1. Registration Processor to request storage of the newly generated UIN of individual x in ID Repo  (ID object)
### 4. LDAP: Update the generated RID of individual x in LDAP
### 5. User Onboarding:
Supervisor can now login to Reg. Client with the above Username/Password and generate RIDs for subsequent probable Operators
