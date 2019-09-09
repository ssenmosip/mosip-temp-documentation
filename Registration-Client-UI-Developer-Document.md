# Registration Client UI Developer Documentation

*** 
This document guides the developer to find the traceability between UI and the respective controller components.  The provided technical classes are available in the package of 'registration-client' module. In this module, the required controllers are bind with the FXML screens. 

It doesn't detail about each methods level information since that is covered in Javadoc of each component and Design Documents.   

## UI Screen Vs Controller mapping: 

|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   