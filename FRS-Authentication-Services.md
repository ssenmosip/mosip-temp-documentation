* [4. Authentication Services]()
  * [4.1 Single factor Authentication]() (MOS_PFM_IDA_FR_1)
    * [4.1.1 Biometric Authentication]()
    * [4.1.2 Demographic Authentication]()
    * [4.1.3 OTP Authentication]()
    * [4.1.4 Static PIN Authentication]()
  * [4.2 Multi-factor Authentication]() (MOS_PFM_IDA_FR_2)
  * [4.3 Offline Authentication]() (MOS_PFM_IDA_FR_3)
    * [4.3.1 QR Code based Authentication]()
  * [4.4 KYC Service]() (MOS_PFM_IDA_FR_4)
    * [4.4.1 Profile Sharing]()
    * [Full Profile]()
    * [Limited Profile Sharing - Policy Based]()
    * [4.4.2 KYC Partners]()
    * [Authorized Partners]()
    * [Application based policy]()
    * [Partner Licensing]()
  * [4.5 Authentication Device Support]() (MOS_PFM_IDA_FR_5)
  * [4.5.1 Registered Devices and Open Devices (Architects to contribute)]()


Partner Licensing - API Key issues to partner is used to sign packets.

What is a factor - It is one of
"What you know" - Password, Static Pin, Date of Birth, My first pet
"What you have" - OTP - Mobile, OTP - Email, RSA Token, Smart Card
"What you are" - Biometrics: Fingerprint, Iris, Face, Voice, ....
  Pin + Biometric, OTP + Biometric
A combination of modes in the same factor

   Application is a use case for KYC. Eg. Bank Account opening, Telco SIM purchase. Same organization might have different use cases. Each use case is governed by a different policy.

