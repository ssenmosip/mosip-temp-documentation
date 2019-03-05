* [4. Authentication Services]()
  * [4.1 Single factor Authentication]() 
    * [4.1.1 Biometric Authentication]() _(IDA_FR_1.1)_
    * [4.1.2 Demographic Authentication]() _(IDA_FR_1.2)_
    * [4.1.3 OTP Authentication]() _(IDA_FR_1.3)_
    * [4.1.4 Static PIN Authentication]() _(IDA_FR_1.4)_
  * [4.2 Multi-factor Authentication]() _(IDA_FR_2)_
  * [4.3 Offline Authentication]()
    * [4.3.1 QR Code based Authentication]() _(IDA_FR_3.1)_
  * [4.4 KYC Service]() 
    * [4.4.1 Profile Sharing]() _(IDA_FR_4.1)_
    * [Full Profile]()
    * [Limited Profile Sharing - Policy Based]()
    * [4.4.2 KYC Partners]() _(IDA_FR_4.2)_
    * [Authorized Partners]()
    * [Application based policy]()
    * [Partner Licensing]()
  * [4.5 Authentication Device Support]() _(IDA_FR_5)_
  * [4.5.1 Registered Devices and Open Devices (Architects to contribute)]() _(IDA_FR_5.1)_


Partner Licensing - API Key issues to partner is used to sign packets.

What is a factor - It is one of
"What you know" - Password, Static Pin, Date of Birth, My first pet
"What you have" - OTP - Mobile, OTP - Email, RSA Token, Smart Card
"What you are" - Biometrics: Fingerprint, Iris, Face, Voice, ....
  Pin + Biometric, OTP + Biometric
A combination of modes in the same factor

   Application is a use case for KYC. Eg. Bank Account opening, Telco SIM purchase. Same organization might have different use cases. Each use case is governed by a different policy.

