This page puts together all the **interfaces** a running instance MOSIP Platform needs to effectively be a foundational ID system.

## Biometrics related interfaces

* ABIS
    * [ABIS Interface](Automated-Biometric-Identification-System-(ABIS)-Interface)
    * [ABIS APIs](ABIS-APIs)
* Biometric SDK
    * [Biometric Functions API Specification](Biometric-Functions-API-Specification)
* Devices 
    * [MOSIP Device Service Specification](MOSIP-Device-Service-Specification)

---
## Low Level Design Documents

1. Transliteration Interface
    * [Design and Background](/mosip/mosip-platform/tree/master/design/kernel/kernel-transliteration.md
)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-transliteration-icu4j
)
2. Validator API
    * [Design and Background](/mosip/mosip-platform/tree/master/design/kernel/kernel-idobjectvalidator.md)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-idobjectvalidator)

3. SMS gateway

    * [Design and Background](/mosip/mosip-platform/tree/master/design/kernel/kernel-smsnotification.md)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-smsnotification-service)

4. Email Gateway

    * [Design and Background](/mosip/mosip-platform/tree/master/design/kernel/kernel-emailnotification.md)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-emailnotification-service)


5. HSM

    * [Design and Background](/mosip/mosip-platform/tree/master/design/kernel/kernel-keymanager-softhsm.md)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-keymanager-softhsm)
6. Antivirus

    * [Design and Background](/mosip/mosip-platform/tree/master/design/kernel/kernel-virusscanner.md)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-virusscanner-clamav)
7. File System 
    * [Design and Background](/mosip/mosip-platform/blob/master/design/kernel/kernel-filesystemadapter.md)
    * [Implementation](/mosip/mosip-platform/tree/master/kernel/kernel-fsadapter-hdfs)
8. [QR Code scanner](/mosip/mosip-docs/wiki/Pre-Registration-Services#generate-qr-code-service-public)

9. [Kernel services](Kernel-APIs)

[All Low-level design documents](/mosip/mosip-platform/tree/master/design)
