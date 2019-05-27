# Guide to use apache directory studio

Follow the below guidelines to use Apache Directory Studio.

## Download Apache Directory Studio

Download apache directory studio from [here](//directory.apache.org/studio/downloads.html).
Look for a ZIP file or a TAR ball.

## Install Apache Directory Studio

To install extract the downloaded ZIP or TAR files in to a particular location.

## Run Apache Directory Studio

Run the ./ApacheDirectoryStudio application in the root path of the installation.

## Create to LDAP server connection

Click on the create connection button.
![Apache-Directory-Studio-1.png](_images/auth/Apache-Directory-Studio-1.png)

On the dialog that opens enter the following details
![Apache-Directory-Studio-2.png](_images/auth/Apache-Directory-Studio-2.png)

Click next and enter the following details in the Auhentication tab

Password for default connection : secret
![Apache-Directory-Studio-3.png](_images/auth/Apache-Directory-Studio-3.png)

Now your connection is configured.

## Connect to LDAP server

Select the connection and click on connect/disconnect as shown in the figure below.
![Apache-Directory-Studio-4.png](_images/auth/Apache-Directory-Studio-4.png)


## Import schemas

* To import entries, select your parent node, right click on it and select import > LDIF import...
* Now select a ldif file which has the entries that you require.
* A sample ldif file for initial entries is [here](_files/auth/mosip.ldif) for reference.


## Create a partition (Not Required, Sample LDIF has this already created)

To create a partition, select the connection and right click to select Open Configuration option.
![Apache-Directory-Studio-5.png](_images/auth/Apache-Directory-Studio-5.png)

In the window opened in the center of the screen, select the partitions tab in the bottom and add a partition as shown in the figure.
![Apache-Directory-Studio-6.png](_images/auth/Apache-Directory-Studio-6.png)

Once you are done with the configuration press ctrl+s to save the configurations.

**Note:** When ever the configuration of the connection is changed, restart the LDAP server for the changes to take place.

## Add Custom Attributes in LDAP (Not Required, Sample LDIF has this already created)
* Create new LDIF file [ file -> new -> LDIF file ] in Apache Directory Studio.
* Follow the below given template to create a custom attribute.
      
      ```
      dn: cn=schema
      changetype: modify
      add: attributeTypes
       attributeTypes: ( 1.2.840.113556.1.8000.2554.12865.17093.34908.18682.41797.31809.44595.29324
        NAME 'rid'
        EQUALITY caseIgnoreMatch
        SUBSTR caseIgnoreSubstringsMatch
        SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )
        -
        add: objectClasses
        objectClasses:1.2.840.113556.1.8000.2554.44227.5563.64568.17995.39112.51716.43355.13724
       NAME 'regid'
       DESC 'regid'
       SUP inetOrgPerson
       STRUCTURAL
       MAY  (rid)
       Note : LDIF record must be ended with empty line.
       
      )
      
      ```
**Description**

* Here, we have created one object class named regid & added custom attribute rid.LDAP does not
allow to create custom attribute in an existing object class.

* Each attribute and object class have unique OID (for e.g. 2.25.1284...) to avoid any conflict with other attributes within LDAP instance. You can use the above OID for experimental purpose.

* SUP inetOrgPerson : specifies that samplePerson object class inherits inetOrgPerson.
  STRUCTURAL : specifies that samplePerson is type of structural object class & able to add entry.
  
* MAY (rid) : samplePerson class have a optional attribute. So when user select samplePerson as object class then it is not mandatory to the attribute in user entry.

* Save the file to the file system. In order to add the custom attribute follow the below image.
![ApacheDs-Custom-Attribute.png](_images/auth/ApacheDs-Custom-Attribute.png)

**Note** : If it is not showing your newly created class then just click on Refresh of Available Object Class list.

* Try to add objectclass and attribute to the created user entry. In the attribute search list, now you will be able to see the newly introduced custom attributes.

For more info [Follow](https://directory.apache.org/apacheds/basic-ug/2.3.1-adding-schema-elements.html) this link.


## Object classes

For documentation about Object classes, schemas and it's attributes, click [here](//directory.apache.org/apacheds/basic-ug/2.3-introducing-schema.html)