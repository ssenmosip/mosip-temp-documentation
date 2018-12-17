An entity wishing to validate the identity of an Individual must use MOSIP's ID Authentication API. MOSIP will support the following types of authentication

* Basic authentication where an entity can send an Individual's demographic and/or biometric details to be validated

* The following authentications on top of the basic authentication
  - TOTP based authentication
  - Challenge Response authentication

Following are the pre-requisites for an entity to do authentication of an individual
* ID Authentication requests must come to MOSIP only via trusted parties who are white listed in MOSIP
* The biometric devices used for authentication must be registered with MOSIP