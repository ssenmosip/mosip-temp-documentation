# Registration Client UI Developer Documentation

*** 
This document guides the developer to find the traceability between UI and the respective controller components.  The provided technical classes are available in the package of 'registration-client' module. In this module, the required controllers are bind with the FXML screens. 

It doesn't detail about each methods level information since that is covered in Javadoc of each component and Design Documents.   

## UI Screen Vs Controller mapping: 

|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**FXML and Controller class**| **RegistrtaionLogin.fxml**  --> **LoginController.java** and **Authentication.fxml** --> **AuthenticationController.java**. For each controller always the **initialization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped to the Controllers of public methods|   


|**Functionality:**| Officer Information Header Screen  |  
|:------:|-----|  
|**Technical Detail:**| After successful login, the Home screen displayed with the officer's information as a header.|  
|**FXML and Controller class**| **Header.fxml**  --> HeaderController.java. For each controller always the **initialization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons, text fields, Radio buttons, On-click events directly mapped to the Controllers of public methods.|   


|**Functionality:**| Main / Home Screen  |  
|:------:|-----|  
|**Technical Detail:**| After successful login to the application, the application launches the home screen where the operator can do the new registration/UIN update/ Lost UIN / Pending Approval/ Update operator Bio-metrics operations|  
|**FXML and Controller class**| **RegistrationOfficerLayout.fxml, RegistrationOfficerPacketLayout.fxml**  --> PacketHandlerController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons, text fields, Radio buttons, On-click events directly mapped ot the Controllers of public methods.|   


|**Functionality:**| Registration Header Screen  |  
|:------:|-----|  
|**Technical Detail:**| On Click of any registration/UIN update or Lost UIN the screen header loaded with Registration Header screen, which indicates to the operator currently which data are we going to capture. It highlights with bold color.|  
|**FXML and Controller class**| **RegistrationHeader.fxml**  --> RegistrationHeaderController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initialization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons, text fields, Radio buttons, On-click events directly mapped to the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   

|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   

|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   

|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   


|**Functionality:**| Login with UserName and Password/ OTP/ BIO  |  
|:------:|-----|  
|**Technical Detail:**| Login screen with User ID will be loaded initially and after successful valudation of the user id the respective authenitcaiton screen [if multi-factor more than one authenticaiton] will be loaded|  
|**Main Controller class and FXML files:**| RegistrtaionLogin.fxml  --> LoginController.java and Authentication.fxml --> AuthenticationController.java. For each controller always the **initalization()** method will be called from the controller to initialize the screen|  
|**Input parameter:**| The required buttons,text fields, Radio buttons, On-click events directly mapped ot the Controllers.|   
