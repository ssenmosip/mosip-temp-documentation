Steps to generate the first User in MOSIP eco-system, refer below for the process:

### 1. Creating the First User in LDAP
* First the roles for MOSIP users need to be created in LDAP ([**Refer to the link for more details**](Getting-Started#65-steps-to-install-and-configuration-ldap)). _For example, Registration Processor, Supervisor, Registration Officer, etc._
* An Individual say 'X' has to be created in LDAP and the roles “Registration Processor” and “Supervisor” needs to be mapped
* Preferred User ID and Password should be set for the Individual 'X' and the same User ID should be present as part of Master Data as mentioned below
 
### 2. Creating the Relevant Master Data
* All data to be required as part of ID Object, for example, Gender, Location hierarchy, templates, etc. should be setup in the database through the CSV Utility
* Master data of user, machine, device and center should be created and uploaded through the CSV Utility _(Note - the user id for the Individual 'X' should be present in Master data of the user)_
* All necessary centre-machine-device-user mappings should be completed through the CSV Utility

### 3. Creating the First User in MOSIP
* A RID for the Individual 'X' is created using the Swagger API of RID Generator
* A UIN for the Individual 'X' is created using the Swagger API of UIN Generator 
* The ID Object for the Individual 'X' is created using the generated RID and UIN _(The ID object consists of the demographic and bio-metric data of the individual 'X')_
* The ID Object of the Individual 'X' is stored in ID Repository using the Swagger API of ID Repository

### 4. Allocating the RID to the User Created in LDAP
* The RID created for the Individual 'X' is updated in the LDAP

### 5. User On-boarding
* The Individual 'X' can now login to Registration Client with the above Username/Password and register the subsequent  Officers and Supervisors
* But the User details of the subsequent Officers and Supervisor must be created in LDAP with appropriate roles assigned (as per Step 1) and their RIDs should be mapped in LDAP (as per Step 4) so that they can login to Registration Client