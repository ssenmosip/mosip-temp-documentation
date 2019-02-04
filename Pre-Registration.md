 # 1.  Overview
       

Pre registration is the module which is the web channel of the MOSIP. Following are few key architectural style followed like microservice based architecture, Data validation are done in UI, User Interface is reference implementation and current one reflects the requirements of Morocco, Master data and services are considered as part of Pre registration foundation. Following are few key design pattern aggregate service pastern, proxy design pattern and dependency injection
      
# 2. Architecture view
     Following gives a high level architecture and design of pre registration.

## Process view
Below is the wiki link for pre registration.

[Process Flow](https://github.com/mosip/mosip/wiki/Process-view#Pre-registration)
## 1. Use case
![Use case diagram](https://github.com/mosip/mosip/blob/0.8.0/docs/design/pre-registration/_images/usecase_preregistration.jpg)
    
   ## 1.1 Fill up demographic details
            Actor- citizen
        ** Pre condition **- should be log in to system.
         scenario:
         * configured demographics data has been displayed.
         * virtual keyboard would be available for the corresponding language.
         * citizen fills up the details.
         * same information would be defined in right hand side as in secondary language.
        **post condition**
        Summary of the application created would be displayed in dashboard.
   
## 1.2 Upload document

     Actor- citizen
        ** Pre condition **- Demographic details have been filled.
         scenario:
         * configured document category and type would be displayed and citizen would select.
         * citizen would upload documents.
         * citizen could view the document uploaded.
        **post condition**
        Summary of the application created would be displayed in dashboard.
   
## 1.3 Search registration center

 Actor- citizen
        ** Pre condition **- Demographic details have been filled and documents have been uploaded.
         scenario:
         * configured search options should be visible.
         * user would search for the registration center.
         * Would display list of registration centers.
        **post condition**
        Citizen could select one registration center for booking.

## 1.4 Booking application

 Actor- citizen
        ** Pre condition **- User has selected the registration center.
         scenario:
         * Booking availability has been displayed for configured number of days.
         * User selects the slot.
         * User confirms booking.
        **post condition**
        User would get acknowledgement of the booking.


## 2. conceptual view
Technical flow and logical component
![technical component and flow](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/_images/preregd_tech_flow.png)

![Logical deployment view](https://github.com/mosip/mosip/blob/0.8.0/docs/design/pre-registration/_images/deployment_arch.jpg)
## 4. technical stack
For version, please refer architecture document.
      spring boot latest
       spring JPA
       postgresql
       spring core
       angular latest


