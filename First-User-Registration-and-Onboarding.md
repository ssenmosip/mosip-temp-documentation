Steps to generate the first User in MOSIP eco-system, refer below for the process:

### 1. Register the first user in LDAP:
1. Create roles in LDAP. For example, Registration Processor, Supervisor, etc.
2. Create Individual say 'X' in LDAP and Map the role for the user as “Registration Processor” and “Supervisor”
3. Provide the preferred User ID and Password for the Individual 'X' 
### 2. Relevant Master data should be created:
1. All data to be stored as part of id object, for example, Gender, Location hierarchy, templates, etc. should be setup in the database through the csv utility
2. Master data of user, machine, device and center should be created and uploaded through the csv utility 
_(Note - the user id for the Individual 'X' should be present in Master data of the user)_
3. All necessary centre-machine-device-user mappings should be completed through the csv utility
### 3. Generation of RID/UIN for first user:
1. Use the swagger API for RID Generator to generate a RID for the individual 'X'
2. Use the swagger API for UIN Generator to generate a UIN for the individual 'X'
3. Create the ID Object (which has the demographic and bio-metric data of the individual 'X') using the RID and UIN generated
4. Use the swagger API for ID Repository to store the ID Object of the individual 'X' in ID Repository
### 4. LDAP: Update the generated RID of individual 'X' in LDAP
### 5. User On-boarding:
1. The Individual 'X' can now login to Registration Client with the above Username/Password and register the subsequent  Operators and Supervisors
