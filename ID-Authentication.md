MOSIP ID Authentication provides an API based authentication mechanism for entities to validate Individuals. ID Authentication is the primary mode for entities to validate an Individual before providing any service.

Following are the pre-requisites for an entity to do authentication of an individual
* ID Authentication requests must come to MOSIP only via trusted parties who are white listed in MOSIP. The trusted parties are referred to as TSPs (Trusted Service Provider) in MOSIP
* The biometric devices used for authentication must be registered with MOSIP

## ID Authentication Process flow
Please refer to https://github.com/mosip/mosip/wiki/Process-view#id-authentication for the process flow of ID Authentication

## Architecturally Significant Use Cases
### Authenticate an Individual in a secure and trusted way

### Capture of biometrics data must be in a standard way

### Authenticate an Individual based on his basic identity data (Demographic & Biometric) captured via MOSIP

### Authenticate an Individual based on a second factor in addition to basic identity data

### Authentication API must have High Availability (HA) to ensure smooth service

### Authentication API must be scalable to cater to the growing population of a country

### Authentication API must protect an Individual's identity from request-replay attacks

## Logical View