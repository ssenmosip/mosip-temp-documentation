Kernel is on which MOSIP services are built. Kernel is a platform to build higher-level services as well as a secure sandbox within which the higher-level service functions. 

## Architecturally significant requirements
Kernel as a distinct module is not brought out in the system requirements. The need for Kernel is identified during the architecture process. Hence, there are no ASRs specific to Kernel that are derived from system requirements. Kernel components contributes towards achieving the overall system requirements and hence the high-level ASRs are applicable to Kernel as well.

### Architectural Constraints
The architectural constraints for the overall MOSIP kernel are also applicable for Kernel.

### Architectural Principles
#### Provide a common technical platform to build higher-level functional services
#### Provide a common framework that provides essential features as a service
#### Provide a common framework that abstracts all common and routine concerns
#### Provide secure sandbox for higher-level services to operate in
#### Ensure security as a critical concern is handled by the system

## Functional Architecture
Kernel components provide defined functional API for use by higher-level services. Kernel components may also expose REST API wherever needed. Following are the various components in the Kernel module. 

Audit Manager

Exception Manager

Log Manager

Data Access Manager

Data Validator

Context Manager

Cache Manager

Encryption/Decryption Manager

Authentication

Key Management

Virus Manager

UIN Generator

OTP Manager

Config Manager

Data Sync Manager

ID Manager

Master Data Manager

Doc Quality Checker

FTP Manager

Language Manager

Data Mapper

Template Manager

Notification Manager

PDF Generator

## Logical view
![Kernel Components](https://raw.githubusercontent.com/mosip/mosip/DEV/design/_images/Kernel_logical_diagram.jpg?token=ApNuIDdMnCPIOH58PjNpuDg9MfwnJ5H_ks5cM0hmwA%3D%3D&_sm_au_=iVVvPQk61T31jn37)