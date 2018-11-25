# **Architecture**

### This application provides the feature to capture the Biometric and Demographic detail of every individuals at country level. 

![Component view](https://github.com/mosip/mosip/blob/DEV/design/_images/MOSIP_RegistrationClient_Component_Architecture.png)

### Diagram represents the high level component architecture of Registration client application. 

* It is a thick client application.
* It interacts with pre-registration application to download the appointment packets.
* It interacts with the registration processor application to upload the registration packet captured from individuals.
* It interacts with the bio-metric device to capture every individuals bio-metric detail and send the same along with the packet to the registration processor.
* The registration packet generated from this application is encrypted and it can only be decrypted at registration processor.

### Installation Guide

### Bundling of application

### Application update


* 