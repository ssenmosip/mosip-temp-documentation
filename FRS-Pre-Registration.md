## Table Of Content
**WIP*
* [1. Overview](#1-overview)
* [2. Features](#2-features)
  * [2.1 Login/Creating a User Account](#21-logincreating-an-user-account) _(MOS_PFM_PRG_FN_2.1)_
    * [2.1.1 Login using Email](#211-login-using-email) _(MOS_PFM_PRG_FN_2.1.1)_
    * [2.1.2 Login using Phone Number](#212-login-using-phone-number) _(MOS_PFM_PRG_FN_2.1.2)_
    * [2.1.3 Automatic Account Creation on First Login](#213-automatic-account-creation-on-first-login) _(MOS_PFM_PRG_FN_2.1.3)_
    * [2.1.4 Logout/Session Timeout](#214-logoutsession-timeout) _(MOS_PFM_PRG_FN_2.1.4)_
  * [2.2 Creating an Application](#22-creating-an-application) _(MOS_PFM_PRG_FN_2.2)_
    * [2.2.1 Provide Demographic Data](#221-provide-demographic-data) _(MOS_PFM_PRG_FN_2.2.1)_
    * [2.2.2 Create Multiple Applications](#222-create-multiple-applications) _(MOS_PFM_PRG_FN_2.2.2)_
    * [2.2.3 Provide Data in Preferred Language](#223-provide-data-in-preferred-language) _(MOS_PFM_PRG_FN_2.2.3)_
    * [2.2.4 Viewing "My Applications" (covers status)](#224-viewing-my-applications-covers-status) _(MOS_PFM_PRG_FN_2.2.4)_
    * [2.2.5 Modify Application Data](#225-modify-application-data) _(MOS_PFM_PRG_FN_2.2.5)_
    * [2.2.6 Discard Application](#226-discard-application) _(MOS_PFM_PRG_FN_2.2.6)_
  * [2.3 Attaching Documents to the Application](#23-attaching-documents-to-the-application) _(MOS_PFM_PRG_FN_2.3)_
    * [2.3.1 Document Categories and Applicable Document Types](#231-document-categories-and-applicable-document-types) _(MOS_PFM_PRG_FN_2.3.1)_
    * [2.3.2 Referring to already Uploaded Documents](#232-referring-to-already-uploaded-documents) _(MOS_PFM_PRG_FN_2.3.2)_
  * [2.4 Booking an Appointment](#24-booking-an-appointment) _(MOS_PFM_PRG_FN_2.4)_
    * [2.4.1 Choosing a Registration Center for Appointment](#241-choosing-a-registration-center-for-appointment) _(MOS_PFM_PRG_FN_2.4.1)_
      * [2.4.1.1 Recommended Centers based on Postal Code](#2411-recommended-centers-based-on-postal-code) _(MOS_PFM_PRG_FN_2.4.1.1)_
      * [2.4.1.2 Nearby Centers based on User Geo-location](#2412-nearby-centers-based-on-user-geo-location) _(MOS_PFM_PRG_FN_2.4.2)_
      * [2.4.1.3 Find a Center](#2413-find-a-center) _(MOS_PFM_PRG_FN_2.4.3)_
    * [2.4.2 Choosing Appointment Slots](#242-choosing-appointment-slots) _(MOS_PFM_PRG_FN_2.4.2)_
      * [2.4.2.1 Get Slots Availability](#2421-get-slots-availability) _(MOS_PFM_PRG_FN_2.4.2.1)_
      * [2.4.2.2 Block Slots for one or more Applications](#2422-block-slots-for-one-or-more-applications) _(MOS_PFM_PRG_FN_2.2.2)_
    * [2.4.3 Cancel Appointment](#243-cancel-appointment) _(MOS_PFM_PRG_FN_2.4.3)_
    * [2.4.4 Re-book Appointment](#244-re-book-appointment) _(MOS_PFM_PRG_FN_2.4.4)_
  * [2.5 Appointment Acknowledgement (PRID)](#25-appointment-acknowledgement-prid) _(MOS_PFM_PRG_FN_2.5)_
    * [2.5.1 Download Acknowledgement](#251-download-acknowledgement) _(MOS_PFM_PRG_FN_2.5.1)_
    * [2.5.2 Send Acknowledgement to Email/Phone](#252-send-acknowledgement-to-emailphone) _(MOS_PFM_PRG_FN_2.5.2)_
  * [2.6 Registration Client Services](#26-registration-client-services) _(MOS_PFM_PRG_FN_2.6)_
    * [2.6.1 Get Appointment for the Day](#261-get-appointment-for-the-day) _(MOS_PFM_PRG_FN_2.6.1)_
    * [2.6.2 Retrieve Application Data by PRID](#262-retrieve-application-data-by-prid) _(MOS_PFM_PRG_FN_2.6.2)_
    * [2.6.3 Update Appointment Status](#263-update-appointment-status) _(MOS_PFM_PRG_FN_2.6.3)_
  * [2.7 List of Configurable Parameters](#27-list-of-configurable-parameters) _(MOS_PFM_PRG_FN_2.7)_
# 1. Overview
# 2. Features
## 2.1 Login/Creating an user account
### 2.1.1 Login using Email
### 2.1.2 Login using Phone Number
### 2.1.3 Automatic Account Creation on First Login
### 2.1.4 Logout/Session Timeout
## 2.2 Creating an Application
### 2.2.1 Provide Demographic Data
### 2.2.2 Create Multiple Applications
### 2.2.3 Provide Data in Preferred Language
### 2.2.4 Viewing "My Applications" (covers status)
### 2.2.5 Modify Application Data
### 2.2.6 Discard Application
## 2.3 Attaching Documents to the Application
### 2.3.1 Document Categories and Applicable Document Types
### 2.3.2 Referring to already Uploaded Documents
## 2.4 Booking an Appointment
### 2.4.1 Choosing a Registration Center for Appointment
#### 2.4.1.1 Recommended Centers based on Postal Code
•	The system fetches the Location Hierarchy as defined in the Master Data and recommends registration centers based on the postal code
•	The search results have the following information about the Registration center :name, Address, Working Hours, Contact Person, Center Type, and Contact Number)

#### 2.4.1.2 Nearby centers based on User Geo-location
•	An individual can  enable location services,  in the device/machine in order to  to select nearby centers
•	The System checks for Lat-Long values of the individual and  fetches all the Registration centers within 2 KM Radius (configurable)
•	The First Registration center as per the search criteria is shown to the individual on Map by default
#### 2.4.1.3 Find a Center
•	
•	An individual may opt to  perform text search to find a center based on which the system displays the registration centers

### 2.4.2 Choosing Appointment Slots
#### 2.4.2.1 Get Slots Availability
•	The System displays 7 calendar days (configurable) for the Individual to select a slot
        Calendar day\s which are  Holidays for the selected Registration center are Greyed out or not shown to the user
        For a Selected Registration Center 8 hours (configurable) are considered as working hours
•	An individual can view time slots of 15 mins(configurable) each for the selected calendar day and view Available spots for every time slot shown in the selected calendar day

#### 2.4.2.2 Block Slots for one or more Applications
### 2.4.3 Cancel Appointment
•	An individual can opt to cancel selected Appointment\s against application which is\are in Booked Status.
In such case the system will notify the user about the successful cancellation 
•	Following a successful Appointment Cancellation the system unlocks the time slot of the Pre-Registration 

### 2.4.4 Re-book Appointment
•	The System provides the User with a default appointment selection: Select Consecutively available Appointment spots
•	An individual can select any of the Appointment Date available and any of the Appointment Spot available
•	The individual has to select against which Pre-Registration ID the Appointment spot is being booked
•	The System maps appointment spot with all the Pre-Registration IDs which are selected for Appointment Booking. If any Pre-Registration ID does not have Booking mapped, the User is notified if he wants to continue without booking
•	An individual at this stage may opt to search Registration center. In this case the appointment -booking (Time Slot selected) done is removed
•	An individual can not  Re-book the Appointment if the appointment Booking is less than 48 hrs(configurable) from time of booking

## 2.5 Appointment Acknowledgement (PRID)
•	An Acknowledgement is triggered after Successful completion of Pre-Registration (Booking an appointment)
•	The acknowledgement contains the following information: Name, Pre-Registration ID, Age/DoB, Mobile Number, Email ID and Registration center Details, Appointment Date, Appointment Time)
### 2.5.1 Download Acknowledgement
•	Individual can Choose to print the Acknowledgement or can Download the Acknowledgement as PDF and print later 
### 2.5.2 Send Acknowledgement to Email/Phone
•	The System sends an acknowledgement to the  applicant through SMS, Email and on-screens as per the details provided in Demographic details
## 2.6 Registration Client Services
### 2.6.1 Get Appointment for the Day
### 2.6.2 Retrieve Application Data by PRID
### 2.6.3 Update Appointment Status
## 2.7 List of Configurable Parameters
