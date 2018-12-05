**Design - Registration Packet Structure**

This document illustrates the Packet structure created at Registration client application post capturing of
individual's data. 

**Solution**

The detailed technical process for Registration packet creation is
provided below:

**Packet Structure**
	![Packet Design view](_images/registration/packet_creation_overview.png)

-   Create date wise folder, if not exists. \[Sample: 12-SEP-2018 \]

-   Biometric and Demographic folders should have the below sub folder
    structure.

    -   Applicant
    -   Introducer
    -   HOF
    
    **Biometric File :**

    ![BioMetric Files](_images/registration/bioMetric_folder.png)

   **Demographic :**
   ![Demographic Files](_images/registration/demographic_folder.png)

Folder level Data: 

1.  **Biometric**

a.  Applicant

    -   LetThumb.jpg/png
    -   RightThumb.jpg/png
    -   LeftPalm.jpg/png
    -   RightPalm.jpg/png
    -   LeftEye.jpg/png
    -   RightEye.jpg/png

b.  HOF

    -   **HOF LeftThumb.jpg/png**

c.  Introducer

    -   **LeftThumb.jpg/png**

2.  **Demographic**

    a.  Applicant

        -   ProofOfIdentity.docx
        -   ProofOfResidenty.docx
        -   ProofOfAddress.docx
        -   ApplicantPhoto.jpg/png
        -   ExceptionPhoto.jpg/png \[If Exceptional cases\]
        -   Registration Acknowledgement.jpg

    b.  Demographic\_info.json  - Follwed the Mosip ID spec and generated this Json structure. It contains the entire text data captured in the UI application. 
	
3.  **RegistrationID.txt**
4.  **HMAC File.txt**
5.  **Packet\_MetaInfo.json
6.  **Registration Officer Bio Image\[JPEG\]**
7.  **Registration Supervisor Bio Image\[JPEG\]**


-   Hash :

    -   Generate the Hash for the Biometric, Demographic and EID of
        Resident Information.

    -   Use the HMAC generation from Java 8 \[MD5 Hashing -- SHA256\]

-   Store the generated Hash in a file and append to the created Zip
    object.

-   Capture the Registration Officer/Supervisor Authentication finger
    image from the respective DTO object and append to the Zip object.

-   Create the Packet Info JSON file, which contains the **Meta data**
    information about packet and appended to the existing Zip object.

-   Session Key Encryption:

    -   Session key generation is \[MAC of machine + EO Id + Timestamp\]
        should not exceed 32 characters.

    -   Pass the created Zip object \[in-memory\] through the AES-256
        bit encryption.

    -   Pass the Random Session Key as a seed to this AES encryption.

    -   Get the Registration Officer Id from user context object. 

-   RSA Public Key Encryption:

    -   AES Session key bytes pass through the RSA public key
        encryption.

-   Use the "\#KEY\_SPLITTER\#" as a key separator for the AES encrypted
    bytes and the RSA Public key encrypted Session key seed.

-   Append the RSA Public key Encrypted Session Key, Key Separator to
    the AES encrypted bytes.

-   Save the encrypted data as a ZIP in local file system under the
    defined location in configuration file.

-   Append the EO and machine information as a META-INFO JSON file and
    create another ZIP out of it. \[Packet Zip + META-INFO JSON\]

-   The final zip name should be as enrollemntid+CurrentTimestamp \[28
    digit\].

-   Timestamp format is \[DDMMYYYYHHMMSSS\]


