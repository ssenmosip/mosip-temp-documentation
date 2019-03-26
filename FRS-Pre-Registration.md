## Table Of Content

* [1. Overview](#1-overview)
* [2. Features](#2-features)
  * [2.1 Login/Creating a User Account](#21-logincreating-a-user-account) _(PRE_FR_1)_
    * [2.1.1 Login using Email](#211-login-using-email) _(PRE_FR_1.1)_
    * [2.1.2 Login using Phone Number](#212-login-using-phone-number) _(PRE_FR_1.2)_
    * [2.1.3 Automatic Account Creation on First Login](#213-automatic-account-creation-on-first-login) _(PRE_FR_1.3)_ 
    * [2.1.4 Logout/Session Timeout](#214-logoutsession-timeout) _(PRE_FR_1.4)_
  * [2.2 Creating an Application](#22-creating-an-application) _(PRE_FR_2)_
    * [2.2.1 Provide Demographic Data](#221-provide-demographic-data) _(PRE_FR_2.1)_
    * [2.2.2 Provide Consent](#222-provide-consent) _(PRE_FR_2.2)_
    * [2.2.3 Create Multiple Applications](#223-create-multiple-applications) _(PRE_FR_2.3)_
    * [2.2.4 Provide Data in Preferred Language (WIP)](#224-provide-data-in-preferred-language-wip) _(PRE_FR_2.4)_
    * [2.2.5 Viewing "My Applications" (covers status)](#225-viewing-my-applications-covers-status) _(PRE_FR_2.5)_
    * [2.2.6 Modify Application Data](#226-modify-application-data) _(PRE_FR_2.6)_
    * [2.2.7 Discard Application](#227-discard-application) _(PRE_FR_2.7)_
  * [2.3 Attaching Documents to the Application](#23-attaching-documents-to-the-application) _(PRE_FR_3)_
    * [2.3.1 Document Categories and Applicable Document Types](#231-document-categories-and-applicable-document-types) _(PRE_FR_3.1)_
    * [2.3.2 Referring to already Uploaded Documents](#232-referring-to-already-uploaded-documents) _(PRE_FR_3.2)_
  * [2.4 Booking an Appointment](#24-booking-an-appointment) _(PRE_FR_4)_
    * [2.4.1 Choosing a Registration Center for Appointment](#241-choosing-a-registration-center-for-appointment) _(PRE_FR_4.1)_
      * [2.4.1.1 Recommended Centers based on Postal Code](#2411-recommended-centers-based-on-postal-code) 
      * [2.4.1.2 Nearby Centers based on User Geo-location](#2412-nearby-centers-based-on-user-geo-location) 
      * [2.4.1.3 Find a Center](#2413-find-a-center) 
    * [2.4.2 Choosing Appointment Slots](#242-choosing-appointment-slots) _(PRE_FR_4.2)_
      * [2.4.2.1 Get Slots Availability](#2421-get-slots-availability) 
    * [2.4.3 Cancel Appointment](#243-cancel-appointment) _(PRE_FR_4.3)_
    * [2.4.4 Re-book Appointment](#244-re-book-appointment) _(PRE_FR_4.4)_
  * [2.5 Appointment Acknowledgement (PRID)](#25-appointment-acknowledgement-prid) _(PRE_FR_5)_
    * [2.5.1 Download Acknowledgement](#251-download-acknowledgement) _(PRE_FR_5.1)_
    * [2.5.2 Send Acknowledgement to Email/Phone](#252-send-acknowledgement-to-emailphone) _(PRE_FR_5.2)_
  * [2.6 Registration Client Services](#26-registration-client-services) _(PRE_FR_6)_
    * [2.6.1 Get Appointment for the Day](#261-get-appointment-for-the-day) _(PRE_FR_6.1)_
    * [2.6.2 Retrieve Application Data by PRID](#262-retrieve-application-data-by-prid) _(PRE_FR_6.2)_
  * [2.7 List of Configurable Parameters and Processes](#27-list-of-configurable-parameters-and-processes) _(PRE_FR_7)_
# 1. Overview
The pre-registration module enables a user to book an appointment for one or many Individuals for registration. It allows a user to enter their demographic details and book appointment by choosing a suitable registration center and time slot and then notifies user on a successful booking. This module also has the provision for appointment rescheduling and cancellation.

[**Link to Process View**](https://github.com/mosip/mosip/wiki/Process-view#pre-registration)

# 2. Features
## 2.1 Login/Creating a User Account
### 2.1.1 Login using Email
The Individual can login to the Pre-registration Portal by providing his/her Email Id. The system validates the email Id, once validated sends an OTP to the email Id as provided. The Individual enters the OTP as received. The system validates the OTP entered and redirects the Individual to fill Demographic form (if first-time) or Dashboard (if existing user).


### 2.1.2 Login using Phone Number
The Individual can login to the Pre-registration Portal by providing his/her Mobile Number. The system validates the Mobile Number, once validated sends an OTP to the Mobile Number as provided. The Individual enters the OTP as received. The system validates the OTP entered and redirects the Individual to fill Demographic form (if first-time) or Dashboard (if existing user).

### 2.1.3 Automatic Account Creation on First Login
The Individual logs in to the Pre-Registration portal with his/her Mobile Number or Email Id. After successful Authentication, the system checks if the Individual is first-time user or not. If the Individual is first-time user, the system creates a new record in the database. All the Pre-registration Ids created from there on will be mapped to this User Id.

### 2.1.4 Logout/Session Timeout
If the Individual wishes to logout of the Pre-Registration system, he/she can opt to select the Logout option. The Token issued during the Authentication of User Login is deleted and the user gets logged out of the system.

## 2.2 Creating an Application
### 2.2.1 Provide Demographic Data

The Individual is provided with Demographic form based on the id [Object Definition](https://github.com/mosip/mosip/wiki/MOSIP-ID-Object-definition)  for new pre-registration application, Individual Fills Demographic Details (e.g., Full Name, Age/DOB, Gender, Residential status, Address, Mobile Number, Email Id, etc.). The system validates the Fields entered, the system also checks for the Mandatory fields. 
Once validated the **Pre-Registration Id is generated** and the Demographic details provided gets mapped to that PRID.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-individual.md)

### 2.2.2 Provide Consent

An Individual Logs in to the pre-registration system with Mobile Number or Email ID and then opts to create a new Application form. Before filling the form, the Individual is advised to provide his/her consent for storage and utilization of his/her personal information. On providing his/her consent, the system redirects the Individual to start the Pre-Registration Application (Demographic Details). The data as part of the consent form is rendered as setup by the admin.

In case of closure of the Consent Pop-up, the following scenarios may arise:
1. First-time login: On closure, then system alerts the user that he will be logged out due to not providing consent.
1. Existing User login
   * Scenario 1 Create new Application from Dashboard: On closure, the Individual will be redirected to Dashboard page.
   * Scenario 2 Add Applicant from Preview Page: On closure, the individual will be redirected to Dashboard page.


### 2.2.3 Create Multiple Applications

Once the Demographic Details are filled and the Documents are uploaded, if the Individual wishes to add an applicant, he/she can opt to select 'Add An Applicant' option on the preview page or 'Create New Application' option on the Dashboard. The system provides the Individual with Demographic form based on the defined id Object Definition to fill. The system associates the pre-registration Id to the new Application(s) created.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-individual.md)

### 2.2.4 Provide Data in Preferred Language (WIP)

The Individual can select his/her language of preference, which is referred as Primary (from a list of 2 languages as set by Admin) from the Login screen, the other language from the list is considered as secondary. The Individual can then provide data in the preferred language (primary) as selected. The data in the right side of the Demographic page will be Transliterated to secondary language. The Individual can verify Transliterated data and edit if required. The data will be stored in the database along with language codes.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-multi-language.md)

### 2.2.5 Viewing "My Applications" (covers status)
The Pre-Registrations created will be associated with User Id. The Individual can view all the Pre-Registrations created by him/her in the Dashboard. The Pre-Registration can be in 3 different status (Pending Appointment, Booked, Expired)

|Status|Description|
|------|-----|
|**Pending Appointment**|Appointment is yet to be booked|
|**Booked**|  Appointment is booked successfully| 
|**Expired**| Appointed date has passed| 

If the individual visits the Registration Centre and consumes the appointment, then the application will be removed from the list

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-individual.md)

### 2.2.6 Modify Application Data
The individual can modify the pre-registration data by opting to select the “Modify” option for a specific application. The system provides the Demographic form with pre-filled demo details and allows the individual to edit the details as required. The system associates the modified demo details with the Pre-Registration Id for which Modify information is initiated.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-update.md)

### 2.2.7 Discard Application
The Individual can discard the Pre-Registration by clicking on the Delete icon for the Pre-Registration Id for which he/she wishes to discard. The system provides the Individual with two options: ‘Discard entire Application’ or ‘Cancel Appointment.' The Individual choses to discard entire Application. The system deletes all the data mapped to the Pre-Registration Id and cancels the appointment (if any).

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-individual.md)

## 2.3 Attaching Documents to the Application
### 2.3.1 Document Categories and Applicable Document Types
1. When an Individual provides his/her Demographic data, the Pre-registration system captures the data. 
1. Based on the parameters (from Config file) for example-The gender, age and residential status(Foreigner, National) from the demographic data applicant types are determined. The Pre-Registration system then sends the Id to the mapping.
1. Based on the Applicant type, the Applicable Document categories are received from the Mapping. The Pre-Registration system then displays only applicable categories.
1. The Document Category and type of documents in each category to be uploaded varies based on the applicant type. Pre-registration system displays only those types to the applicant.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-individual.md)

### 2.3.2 Referring to already Uploaded Documents

* The POA document could be uploaded or can be referred to an already uploaded POA of an existing applicant
* The individual could select a particular applicant document to which he wants to refer 



[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-individual.md)


## 2.4 Booking an Appointment
### 2.4.1 Choosing a Registration Center for Appointment

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-booking-service.md)

#### 2.4.1.1 Recommended Centers based on Postal Code
1. The system recommends registration centers based on the postal code(s) of all the applicants for whom the appointment is to be booked
1. The search results have the following information about the Registration Center: Name, Address, Working Hours, Contact Person, Center Type, and Contact Number

The First Registration Center as per the search criteria is shown to the Individual on Map by default

#### 2.4.1.2 Nearby centers based on User Geo-location
1. An Individual can  enable location services,  in the device/machine in order to select nearby centers
1. The system checks for Lat-Long values of the Individual and  fetches all the Registration Centers within 2 KM Radius (configurable)
1. The First Registration Center as per the search criteria is shown to the Individual on Map by default

#### 2.4.1.3 Find a Center
An Individual may opt to  perform text search to find a center based on which the system displays the registration centers

It is a contextual search where the individual selects a search criteria and based on the selected search criteria enters relevant text. 

The First Registration Center as per the search criteria is shown to the Individual on Map by default




### 2.4.2 Choosing Appointment Slots

#### 2.4.2.1 Get Slots Availability
The user opts to view the available slots for a selected registration center.
1. The system displays 7 calendar days (configurable) for the Individual to select a slot in the chosen center
1. Calendar day\s which are  Holidays for the selected Registration Center are Greyed out or not shown to the user
1. For a Selected Registration Center 8 hours (configurable) are considered as working hours
1. An Individual can view time slots of 15 minutes (configurable) each for the selected calendar day and view Available slots for every time slot shown in the selected calendar day
1. The system auto-suggest the closest available timeslot(s) to the chosen applicant(s) and allocates it 
1. An applicant however can further update the preference and choose the preferred timeslot
1. An individual can book the appointment for the preferred/chosen time slot – Subsequently the timeslots are locked


### 2.4.3 Cancel Appointment
1. An Individual can opt to cancel selected Appointment\s against application which is\are in Booked Status.
1. In such case the system notifies the user about the successful cancellation 
1. Following a successful Appointment Cancellation the system unlocks the time slot of the Pre-Registration 

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-booking-cancel-service.md)

### 2.4.4 Re-book Appointment
1. The system provides the user with a default appointment selection: Select Consecutively available Appointment Slots.
1. An Individual can select any of the Appointment Date available and any of the Appointment Slot available
1. The Individual has to select against which Pre-Registration Id the Appointment slot is being booked
1. The system maps appointment slot with all the Pre-Registration Ids, which are selected for Appointment Booking. 
1. If any Pre-Registration Id does not have Booking mapped, the user is notified if he wants to continue without booking
1. An Individual at this stage may opt to search Registration Center. In this case the appointment-booking (Time Slot selected) done is removed
1. An Individual cannot  Re-book the Appointment if the appointment Booking is less than 48 hours (configurable) from time of booking

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-re-booking-service.md)
## 2.5 Appointment Acknowledgement (PRID)
1. An Acknowledgement is triggered after Successful completion of Pre-Registration (Booking an appointment)
1. The acknowledgement contains the following information: Name, Pre-Registration Id, Age/DoB, Mobile Number, Email Id and Registration Center Details, Appointment Date, Appointment Time)

### 2.5.1 Download Acknowledgement
Individual can choose to print the Acknowledgement or can Download the Acknowledgement as PDF and print later

The acknowledgement template is language and channel (email, sms, on screen) specific.

[**Reference Templates**](https://github.com/mosip/mosip/tree/master/docs/requirements/Templates/Pre-registration) 
### 2.5.2 Send Acknowledgement to Email/Phone
The system sends an acknowledgement to the  applicant through SMS, Email and on-screens as per the details provided in Demographic details

In case of multiple application, the system sends notifications to each applicant (as defined in the demographic details of the applicant\s)

An individual can opt to manually trigger notification\s to the contact details of additional recipients.

## 2.6 Registration Client Services
### 2.6.1 Get Appointment for the Day
1. An Individual logs in to the pre-registration system  and opts to Book Appointment for Pre-Registration Application or Modify Appointment
1. The system presents a  list of Centers to the user to select the required Registration Center 
1. The Time selection with calendar days along with number of slots available per calendar day will be displayed 
1. Individual can select any of the calendar day which he\she wishes to Book Appointment.
1. Time slots of 15 minutes each are displayed.
1. Each time slot with Available slots will be displayed.
1. The Individual can select a slot and proceed to Book Appointment or can go back to select another Registration Center

[**Link to design**](https://github.com/mosip/mosip/tree/master/docs/design/pre-registration)
### 2.6.2 Retrieve Application Data by PRID
Upon receiving the Registration Center Id, Date Range (Start Date, End Date) for the List of Pre-Registrations, User Id (Registration Officer/Supervisor) from Registration client the Pre-Registration system processes the information.
1. The system generates a Transaction Id
1. The system then Fetches all the Pre-Registrations within the Date Range (Start Range, End Date) and for the Registration Center Id received and calculates the count of the Pre-Registration Ids being sent.
1. The system sends the List of Pre-Registration Ids along with count of Pre-Registrations.
1. The system receives the Pre-Registration Id/Ids for which Pre-Registration Data has to be sent.
1. The system sends the zip file per Pre-Registration Id consisting of Demo Data, Files, and Appointment Time.

[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/pre-registration/pre-registration-data-sync.md)
## 2.7 List of Configurable Parameters and Processes

1. [**Configurable Parameters**](Getting-Started#7-configuring-mosip)


Please refer to para 7.C in Getting started Guide.
1. [**Configurable Processes**](https://github.com/mosip/mosip/blob/master/docs/requirements/MOSIP_Processes_Consolidated%20List_External.xlsx)  
