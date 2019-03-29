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
![Apache-Directory-Studio-3.png](_images/auth/Apache-Directory-Studio-3.png)

Now your connection is configured.

## Connect to LDAP server

Select the connection and click on connect/disconnect as shown in the figure below.
![Apache-Directory-Studio-4.png](_images/auth/Apache-Directory-Studio-4.png)

## Create a partition

To create a partition, select the connection and right click to select Open Configuration option.
![Apache-Directory-Studio-5.png](_images/auth/Apache-Directory-Studio-5.png)

In the window opened in the center of the screen, select the partitions tab in the bottom and add a partition as shown in the figure.
![Apache-Directory-Studio-6.png](_images/auth/Apache-Directory-Studio-6.png)

Once you are done with the configuration press ctrl+s to save the configurations.

**Note:** When ever the configuration of the connection is changed, restart the LDAP server for the changes to take place.

## Import schemas

* To import entries, select your parent node, right click on it and select import > LDIF import...
* Now select a ldif file which has the entries that you require.
* A sample ldif file for initial entries is [here](_files/auth/mosip.ldif) for reference.
* A sample ldif file for sub entries used for authorization are [here](_files/auth/mosip_auth.ldif)

## Object classes

For documentation about Object classes, schemas and it's attributes, click [here](//directory.apache.org/apacheds/basic-ug/2.3-introducing-schema.html)