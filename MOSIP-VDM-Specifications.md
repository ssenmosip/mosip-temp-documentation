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
   

* VDM - The Vendor Device Manager, provided by the device vendor, which manages the device, and allows for biometric data capture.   
* DM  - The vendor independent Device Manager, which orchestrates the discovery, of the VDMs by the application, and manages connectivity to the VDM.
* Application - The Application that needs to use the biometric devices for capture. 

### Vendor Device Manager 
   The vendor must provide this as installer (and Uninstaller) to install and configure the VDM specific to the requirement. During initial
   setup the required configuration to be completed.
   
   The communication with the VDM happens through the socket from application. The VDM should listen to the socket to send and receive the command from application. 
   There is a separate socket should be opened to receive the Video streams and Biometric samples. 
   
   
   It provides following functionality, which will be triggered from the application based on the user actions. 
   1. Subscribe 
   2. Unsubscribe 
   3. Start Capture 
   4. Stop Capture 
   5. Force Capture 
   6. Get Frame 
   7. Get Sample 

   The following notifications are provided by the VDM to the application when the respective operations are completed. 
   1. Capture Complete 
   2. Detection 
   3. User Actionable Feedback 

   There is an additional configuration utility expected to provided by the vendor to provide GUI 
   that will help the users to manage the device with the following operations:
   1. Configuration, including port number override
   2. Device Self Test
   3. Device Reset / Reinitialization
   4. Device Calibration
   5. Device Startup
   6. Device Shutdown
   
   
### Device Manager 
   

   The DM service will be provided by the MOSIP. The DM responds to the following requests: 
   1. Connect 
   2. Device Arrival 
   3. Device Removal 
   4. Ping 
   
   The DM provides applications with the following events.
   1. Device Arrival 
   2. Device Removal 

The DM listens on a TCP/IP port (specified later in this document). Applications and the 
VDMs must connect to this port once, and communicate over this open connection. 

