# **Vendor Device Manager - Specification**

This document provides the detail of VDM spec to be adhere by the vendor to adopt their devices to the MOSIP platform 
to capture the biometric data and manipulate on the same. 

![VDM Spec view](https://github.com/mosip/mosip/blob/DEV/design/_images/registration/vdm-spec-design.png)

* Following points has been considered while designing the VDM spec:
   - Vendor should follow this spec and create the device specific VDM service to integrate with the application.
   - Device specific code and integration with device should be available with in this scope.
   - Any security related to the device can be implemented at single stage rather doing at application end.
   - VDM upgrade or SDK upgrade shouldn't impact the application code.
   - VDM should be provided along with the GUI to register the running devices port .
   

* VDM - The Vendor Device Manager, provided by the device vendor, which manages the device, and allows for biometric data capture   
* DM  - The vendor independent Device Manager, which orchestrates the discovery, of the VDMs by the application, and manages connectivity to the VDM.
* Application - The Application that needs to use the biometric devices for capture. 

### Vendor Device Manager

### Device Manager

