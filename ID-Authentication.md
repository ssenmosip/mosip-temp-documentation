MOSIP ID Authentication provides an API based authentication mechanism for entities to validate Individuals. ID Authentication is the primary mode for entities to validate an Individual before providing any service.

Following are the pre-requisites for an entity to do authentication of an individual
* ID Authentication requests must come to MOSIP only via trusted parties who are white listed in MOSIP
* The biometric devices used for authentication must be registered with MOSIP

## Architecturally Significant Use Cases



* Basic authentication where an entity can send an Individual's demographic and/or biometric details to be validated

* The following authentications on top of the basic authentication
  - TOTP based authentication
  - Challenge Response authentication

