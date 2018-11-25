# **Architecture**
![Component view](_images/arch_diagrams/RegistrationClient_Component_Architecture.png)
### This diagram represents the high level component architecture in Registration client application. It helps the Registration officers to capture the detail of every individuals at country level. 
* It is a thick client application.
* It interacts with pre-registration application to download the appointment packets.
* It interacts with the registration processor application to upload the registration packet captured from individuals.
* It interacts with the bio-metric device to capture every individuals bio-metric detail and send the same along with the packet to the registration processor.
* The registration packet generated from this application is encrypted and it can only be decrypted at registration processor.
* 