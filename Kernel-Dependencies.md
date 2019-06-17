# Kernel Dependencies List

### 1 Prerequisites : <br><sub>Dependent DB/External applications and services</sub></br>
Dependency|Component|Description (If any)
-----|--------------|----------------
DB|mosip_iam|Required for kernel-auth-service.
DB|mosip_master|Required for kernel-masterdata-service.
DB|mosip_audit|Required for kernel-audit-service.
DB|mosip_kernel|Required for all other kernel services.
LDAP|ApaacheDS|Required for kernel-auth-service. <br> [External Dependency Setup](https://github.com/mosip/mosip/wiki/Getting-Started#65-steps-to-install-and-configuration-ldap)
KeyStore|SoftHsm|Required for kernel-keymanager-softhsm. <br> [External Dependency Setup](https://github.com/mosip/mosip/wiki/Getting-Started#67-steps-to-install-kernel-key-manager-service)
DFS|HDFS|Required for kernel-fsadaptor-hdfs. <br> [External Dependency Setup](https://github.com/mosip/mosip/wiki/Getting-Started#66-steps-to-install-and-configuration-hdfs)
SMS Gateway|msg91.com|Required for kernel-smsnotification-service. <br> [External Dependency Setup](https://github.com/mosip/mosip/wiki/Getting-Started#68-register-on-httpscontrolmsg91comsignup-as-developer-and-get-an-authkey-replace-the-same-in-kernelproperties-used-by--kernel-smsnotification-service-)



### 2 Prerequisites : <br><sub>Internal Service Dependencies</sub></br>
Service|Dependencies|Description (If any)
-------|--------------|----------------
All Services|kernel-auth-service|For Authentication and Validation
kernel-auth-service| id-repository-identity-service <br> kernel-otpmanager-service <br> kernel-emailnotification-service <br> kernel-smsnotification-service| For UIN based login to sendOtp <br> For OTP generation and validation <br> For Sending Notification
kernel-syncdata-service|kernel-keymanager-service <br> kernel-auth-service <br> kernel-syncjob-service|For public key <br> For  Role and User details <br> For Syncjob defination Details
kernel-cryptomanager-service|kernel-keymanager-service| For public key and private key decryption
kernel-signature-service|kernel-keymanager-service|For public key and private key siginig


