 # 1.  Overview
 ##  1. principles
      * microservice based architecture
      * Data validation are done in UI.
      * User Interface is reference implementation and current one reflects the requirements of Morocco.
      * Master data and services are considered as part of Pre registration foundation. ##  2. Key NFR
     
 
## 2. design pattern 
      aggregate service pastern
      proxy design pattern
      dependency injection
      
# 2. Architecture view
     Following gives a high level architecture and design of pre registration.
## 1. Use case
    
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
   

## 2. conceptual view
Technical flow and logical component
![technical component and flow](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/_images/preregd_tech_flow.png)
## 3. service view
TBD- WOULD MERGE LOCAL BRANCH TO MASTER BY EOD.
## 4. technical stack


