# **Vendor Device Manager - Specification**

This document provides the detail of VDM spec to be adhere by the vendor to adopt their devices to the MOSIP platform 
to capture the biometric data and manipulate on the same. 


![VDM Spec view](https://github.com/mosip/mosip/blob/DEV/design/_images/registration/vdm-spec-design.png)

* Following points has been considered while designing the VDM spec:
   - Vendor should follow this spec and create the device specific VDM service to integrate with the application.
   - Device specific code and integration with device should be available with in this scope.
   - Any security related to the device can be implemented at single stage rather doing at application end.
   - VDM upgrade or SDK upgrade shouldn't impact the application code. 
   - VDM should be provided along with the GUI to register and manage the running devices port .
   - VDM should have capabilities to integrate with multiple devices like : Finger Print, IRIS and Face Reader. 
   

* VDM - The Vendor Device Manager, provided by the device vendor, which manages the device, and allows for biometric data capture.   
* DM  - The vendor independent Device Manager, which orchestrates the discovery, of the VDMs by the application, and manages connectivity to the VDM.
* Application - The Application that needs to use the biometric devices for capture. 

### Vendor Device Manager 
   The vendor must provide this as installer (and Uninstaller) to install and configure the VDM specific to the requirement. During initial
   setup the required configuration to be completed using the respective GUI. The DM port should be configured during initial setup.
   
   Once the VDM has been started then communicate with the DM through socket **TBD** and register the VDM listening port.
   
   The communication with the VDM happens through the socket **TBD** from application. The VDM should listen to a particular port to send and 
   receive the command from application. There is a separate socket should be opened to receive the Video streams and Biometric samples. 
      
   It provides following functionality, which will be triggered from the application based on the user actions. 
   1. Subscribe 
   2. Un-subscribe 
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
   
   **Sequence of process**
   1. VDM senses that a device under it’s control is connected to the system. 
   2. VDM creates a Device Arrival event and sends it to the DM through socket and port. 
   3. The event contains information about the device, and it’s capabilities. 
   4. It accepts the request from application through the port and communicate with the device through the respective driver. 
   5. Send response back to the application based on the request. 
   
### Device Manager 
   
   The DM is responsible for managing the list of all connected applications, VDMs, and 
   devices. Whenever a device arrives, it must register with the DM, and continue to send 
   a heartbeat event at regular intervals. Failure to send the heartbeat is treated as a 
   removal event. The DM sends a list of all connected devices to the application after the 
   initial connection, by forwarding stored Arrival events. 

   Multiple devices can be communicate with the DM and register with the respective available port for communication. 

   The DM service will be provided by the MOSIP. The DM responds to the following requests: 
   1. Connect        - VDM and application uses this api to initiate communication with DM. 
   2. Device Arrival - VDM uses this api to inform the DM when the device connected. 
   3. Device Removal - VDM uses this api to inform the DM when the device disconnected.
   4. Ping           - This is used as a heartbeat event, to notify the DM that a VDM, is still alive.  
   
   The DM provides applications with the following events.
   1. Device Arrival 
   2. Device Removal 

The DM listens on a TCP/IP port (specified later in this document). Applications and the 
VDMs must connect to this port once, and communicate over this open connection. 

### Device Management 

    1. When the VDM senses that a device under it’s control is connected to the system, it 
       creates a Device Arrival event and sends it to the DM
    2. The DM must acknowledge the receipt of this event, forward it to all applications, and 
       maintain a copy of this event (for all applications that may connect in the future). 
    3. Application further uses this port number to communicate with the VDM service. 
    4. VDM further communicates with the Device through the respective driver.    
    
   **Sequence of process**
![Sequence process](_images/registration/vdm-spec-design-sequence.png)


### API Methods
   - This specifies the request and response messages that are exchanged between
   the Application, DM and VDM. All messages are in XML.
   - All requests and responses carry a requestId, which is a numeric value (128 bit),
   represented as a 36 character UUID format string in XML. Since the API is asynchronous, 
   the requestId is used to connect requests with the appropriate response.
   - The VDM, DM and Application must not use requestId outside the scope of a request,
   since this could be recycled.

   TBD

### Security Considerations 

