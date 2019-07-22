## 1. Tables Names:
1. Registration Centers: **master-registration_center**
1. Machines: **master-machine_master**
1. Users: **master-user_detail**
1. Devices: **master-device_master**
1. Center-Machine Mapping: **master-reg_center_machine**
1. Center-Device Mapping: **master-reg_center_device**
1. Center-User Mapping: **master-reg_center_user**
1. Center-Machine-Device Mapping: **master-reg_center_user_machine**
1. Center Machine User Mapping: **master-reg_center_machine_device**
## 2. Steps to Add a Mac-Address Machine:
### 2.1 Create a Registration Center:
1. **Center ID**: This should be a 5-digit ID and Ideally should be in an incremental sequence for each center added. The sequence should start from 10000. Keeping the lenght other than 5 digits will fail validations as the same Center ID is used to generate the Request ID (Registration ID)
1. **Center Name**: This can be a Random name that a country chooses
1. **Center Type Code**: Should be kept as “REG”. Center Type Code will come from a Center Type Masterdata which currently have one center Type defined as “Regular” and Code as “REG”
1. **Address Line 1**: It is an Optional Field but should be defined to be visible to the resident on the Pre-Registration UI
1. **Address Line 2**: It is an Optional Field
1. **Address Line 3**: It is an Optional Field
1. **Latitude**: Should be defined in format **XX.XXXX**. minimum 4 digits are need after the decimal for the accuracy to be atleast 11 meters on the GPS map
1. **Longitude**: Should be defined in format **XX.XXXX**. minimum 4 digits are need after the decimal for the accuracy to be atleast 11 meters on the GPS map
1. **Location Code**: Should be a location code from the location MasterData table. This code cannot be other than the location defined in the location MasterData table and should always be the code of the location which is at the lowest hierarchy level
1. **Contact Phone**: Can be a random number
1. **Contact Person**: Can be a random name
1. **Number of Kiosk**: This number is used by the pre-registration to calculate slots for registration. This should always be equal to the number of machines assigned to the Center. Refer point 5 in steps below
1. **Working Hours**: Should be the difference of “**Center Start Time**” and “**Center End Time**”. Should be in format **hh:mm:ss**
1. **Per Kiosk Processing time**: Is used by pre-Registration to calculate appointment slots. Should be in format **hh:mm:ss**
1. **Center Start Time**: _Will be time Center would start working at_. Is used by pre-Registration to calculate appointment slots. Should be in format **hh:mm:ss**
1. **Center End Time**: _Will be the time Center would close at_. Is used by pre-Registration to calculate appointment slots. Should be in format **hh:mm:ss**
1. **Lunch Start Time**: _Starting of Lunch Time the Center would have in-between the Working hours_. Is used by Pre-Registration to calculate appointment slots. Should be in format **hh:mm:ss**
1. **Lunch End Time**: _Ending of Lunch Time the Center would have in-between the Working hours_. Is used by Pre-Registration to calculate appointment slots. Should be in format **hh:mm:ss**
1. **Time Zone**: (GTM+01:00) CENTRAL EUROPEAN TIME
1. **Holiday Location Code**: Should come from the Location master table. Current values can only be “**KTA**” or “**RBT**” as holidays are only defined for these two location codes.
1. **Language Code**: Should be the language code for the languages supported by the Country as primary and secondary Language. Currently can be “fra” or “ara”
1. **Is_Active**: TRUE. If set as false, this Registration will not be shown up in Pre-Registration UI and no appointments will be generated for this Center
1. **Cr_by**: `<username>` ideally name of the admin
1. **cr_dtimes**: now()
<br>**Note**: A Registration Center is needed to be created in all the languages supported by the country. This is currently configured as Primary – French and Secondary – Arabic. For this, create the same registration twice. One with language code as **fra** for French and one with language code as **ara** for Arabic. Center ID should be same for both the records as both the records are for one center only.<br>
### 2.2 Create a Machine:
1. **Machine ID**: This should be a 5-digit ID and Ideally should be in an incremental sequence for each machine added. The sequence should start from 10000. Keeping length other than 5 digits will fail validations as the same Machine ID is used to generate the Request ID(Registration ID)
1. **Machine Name**: Machine Host name
1. **Machine Mac-Address**: Machine’s Mac-Address
1. **Serial Number**: `<Random Number>`
1. **IP Address**: Leave it blank
1. **Mspecid**: 1001. These values come from a Machine Spec table. Putting any value other than these will throw an error
1. **Lang_code**: eng
1. **Is_active**: True
1. **cr_by**: `<username>` ideally name of the admin
1. **cr_dtimes**: now()
### 2.3 Create a User
1. Create a User in LDAP (User ID/Password)
1. Create a User in DB
   1. **Id**: ID used in LDAP
   1. **UIN**: Leave it black
   1. **Email**: Email used in LDAP
   1. **Mobile**: Mobile used in LDAP
   1. **Status Code**: ACT
   1. **Lang_code**: eng
   1. **last_login_method**: PWD
   1. **Is_active**: True
   1. **cr_by**: `<username>` ideally name of the admin
   1. **cr_dtimes**: now()
### 2.4 Create a Device
1. **Device ID**: This can be a random ID.
1. **Device Name**: `<Random name>`
1. **Device Mac-Address**: `<Random mac-address>`
1. **Serial Number**: `<Random Number>`
1. **IP Address**: Leave it blank
1. **Dspecid**: Can be either 165(fingerprint scanner), 327 (iris scanner), 736(web camera), 801(Document scanner) or 920(Printer). These values come from a Device Spec table. Putting any value other than these will throw an error
1. **Lang_code**: eng
1. **Is_active**: True
1. **cr_by**: `<username>` ideally name of the admin
1. **cr_dtimes**: now()

### 2.5 Map the Machine to a Center
1. **Center ID**: from **master-registration_center**
1. **Machine ID**: from **master-machine_master** (newly created machine)
1. **Lang_code**: eng
1. **Is_active**: True
1. **cr_by**: `<username>` ideally name of the admin
1. **cr_dtimes**: now()
### 2.6 Map the User to a Center
Follow the above example in [point 2.4](#24-create-a-device).
### 2.7 Map the Device to a Center
Follow the above example in [point 2.4](#24-create-a-device).
### 2.8 Map Center-Machine-Device
Follow the above example in [point 2.4](#24-create-a-device).
### 2.9 Map Center-Machine-User
Follow the above example in [point 2.4](#24-create-a-device).
### 2.10 Final step (Suggest heading)
After adding all these data in the DB, we would need to create the same records in all the History tables for every table mentioned in the “**Tables Names**” section.
1. Each history table has an extra attribute “effective date” other than the standard attributes mentioned for each table. 
1. The Effective date should be now().and all the attributes should be same as they are stored in the standard tables.
1. Find the table names below for history tables
   1. Registration Centers: **master-registration_center_h**
   1. Machines: **master-machine_master_h**
   1. Users: **master-user_detail_h**
   1. Devices: **master-device_master_h**
   1. Center-Machine Mapping: **master-reg_center_machine_h**
   1. Center-Device Mapping: **master-reg_center_device_h**
   1. Center-User Mapping: **master-reg_center_user_h**
   1. Center-Machine-Device Mapping: **master-reg_center_user_machine_h**
   1. Center Machine User Mapping: **master-reg_center_machine_device_h**

