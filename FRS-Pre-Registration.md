## Table Of Content

* [1. Overview](#1-overview)
* [2. Features](#2-features)
  * [2.1 Login/Creating an User Account](#21-logincreating-an-user-account) 
    * [2.1.1 Login using Email](#211-login-using-email) _(MOS_PFM_PRG_FR_1)_
    * [2.1.2 Login using Phone Number](#212-login-using-phone-number) _(MOS_PFM_PRG_FR_2)_
    * [2.1.3 Automatic Account Creation on First Login](#213-automatic-account-creation-on-first-login) _(MOS_PFM_PRG_FR_3)_
    * [2.1.4 Logout/Session Timeout](#214-logoutsession-timeout) _(MOS_PFM_PRG_FR_4)_
  * [2.2 Creating an Application](#22-creating-an-application) 
    * [2.2.1 Provide Demographic Data](#221-provide-demographic-data) _(MOS_PFM_PRG_FR_5)_
    * [2.2.2 Create Multiple Applications](#222-create-multiple-applications) _(MOS_PFM_PRG_FR_6)_
    * [2.2.3 Provide Data in Preferred Language](#223-provide-data-in-preferred-language) _(MOS_PFM_PRG_FR_7)_
    * [2.2.4 Viewing "My Applications" (covers status)](#224-viewing-my-applications-covers-status) _(MOS_PFM_PRG_FR_8)_
    * [2.2.5 Modify Application Data](#225-modify-application-data) _(MOS_PFM_PRG_FR_9)_
    * [2.2.6 Discard Application](#226-discard-application) _(MOS_PFM_PRG_FR_10)_
  * [2.3 Attaching Documents to the Application](#23-attaching-documents-to-the-application) 
    * [2.3.1 Document Categories and Applicable Document Types](#231-document-categories-and-applicable-document-types) _(MOS_PFM_PRG_FR_11)_
    * [2.3.2 Referring to already Uploaded Documents](#232-referring-to-already-uploaded-documents) _(MOS_PFM_PRG_FR_12)_
  * [2.4 Booking an Appointment](#24-booking-an-appointment) 
    * [2.4.1 Choosing a Registration Center for Appointment](#241-choosing-a-registration-center-for-appointment) _(MOS_PFM_PRG_FR_13)_
      * [2.4.1.1 Recommended Centers based on Postal Code](#2411-recommended-centers-based-on-postal-code) _(MOS_PFM_PRG_FR_14)_
      * [2.4.1.2 Nearby Centers based on User Geo-location](#2412-nearby-centers-based-on-user-geo-location) _(MOS_PFM_PRG_FR_15)_
      * [2.4.1.3 Find a Center](#2413-find-a-center) _(MOS_PFM_PRG_FR_16)_
    * [2.4.2 Choosing Appointment Slots](#242-choosing-appointment-slots) 
      * [2.4.2.1 Get Slots Availability](#2421-get-slots-availability) _(MOS_PFM_PRG_FR_17)_
    * [2.4.3 Cancel Appointment](#243-cancel-appointment) _(MOS_PFM_PRG_FR_18)_
    * [2.4.4 Re-book Appointment](#244-re-book-appointment) _(MOS_PFM_PRG_FR_19)_
  * [2.5 Appointment Acknowledgement (PRID)](#25-appointment-acknowledgement-prid) 
    * [2.5.1 Download Acknowledgement](#251-download-acknowledgement) _(MOS_PFM_PRG_FR_20)_
    * [2.5.2 Send Acknowledgement to Email/Phone](#252-send-acknowledgement-to-emailphone) _(MOS_PFM_PRG_FR_21)_
  * [2.6 Registration Client Services](#26-registration-client-services)
    * [2.6.1 Get Appointment for the Day](#261-get-appointment-for-the-day) _(MOS_PFM_PRG_FR_22)_
    * [2.6.2 Retrieve Application Data by PRID](#262-retrieve-application-data-by-prid) _(MOS_PFM_PRG_FR_23)_
  * [2.7 List of Configurable Parameters](#27-list-of-configurable-parameters) _(MOS_PFM_PRG_FR_24)_
# 1. Overview
The pre-registration module enables an user to book an appointment for one or many individuals for registration. It allows an user to enter their demographic details and book appointment by choosing a suitable registration center and time slot and then notifies user on successful booking.This module also has the provision for appointment rescheduling and cancellation.

# 2. Features
## 2.1 Login/Creating an user account
### 2.1.1 Login using Email
The Individual can login to the Pre-registration Portal by providing his/her Email Id. The System validates the email ID, once validated sends an OTP to the email ID as provided. The Individual enters the OTP as received. The System validates the OTP entered and redirects the Individual to fill Demographic form (if first time) or Dashboard.

### 2.1.2 Login using Phone Number
The Individual can login to the Pre-registration Portal by providing his/her Mobile Number. The System validates the Mobile Number, once validated sends an OTP to the email ID as provided. The Individual enters the OTP as received. The System validates the OTP entered and redirects the Individual to fill Demographic form (if first time) or Dashboard.

### 2.1.3 Automatic Account Creation on First Login
The Individual logs in to the Pre-Registration portal with his/her Mobile Number or Email ID. After successful Authentication, the system check if the Individual is first time user or not. If the Individual is first time user, the system creates a new record in the database. All the Pre-registration Ids created from there on will be mapped to this User ID.

### 2.1.4 Logout/Session Timeout
The Individual wishes to logout of the Pre-Registration system and clicks on the Logout. The Token issued during the Authentication of User Login is deleted and the User gets logged out of the system.

## 2.2 Creating an Application
### 2.2.1 Provide Demographic Data
The Individual is provided with Demographic form for new pre-registration application, Individual Fills Demographic Details (Full Name, Age/DOB, Gender, Residential status, Address Lines (1,2,3), Region, Province, City, Local Administrative Authority, Mobile Number, Email ID, CNIE/EC Number, Postal Code). The System validates the Fields entered, the system also checks for the Mandatory fields. Once validated the Pre-Registration Id is generated and the Demographic details provided gets mapped to that PRID.

### 2.2.2 Create Multiple Applications
The Individual can create Multiple Applications, once the Demographic Details and the Documents are uploaded the Individual can add an applicant from the Preview page. The Individual can also add applicants from Dashboard by clicking on Create New Application. The System provides the Individual with Demographic form to fill. The System associates the pre-registration Id to the new Application(s) created.

### 2.2.3 Provide Data in Preferred Language
The Individual can select his/her language of preference (from list of languages as set by Admin) from the Login Screen. The Individual can then provide data in the preferred language as selected

### 2.2.4 Viewing "My Applications" (covers status)
The Pre-Registrations created will be associated with User Id. The Individual can view all the Pre-Registrations created by him/her in the Dashboard. The Pre-Registration can be in 3 different status (Pending Appointment, Booked, Expired)

|Status|Description|
|------|-----|
|**Pending Appointment**|Appointment is yet to be booked|
|**Booked**|  Appointment is booked successfully| 
|**Expired**| Appointed date has passed| 

### 2.2.5 Modify Application Data
The Individual Can Modify the Pre-Registration data by selecting the Modify Information from the Dashboard. The system provides the Demographic form with pre-filled demo details. The Individual can edit the required changes. The system associates the modified demo details with the Pre-Registration Id for which modifies information is initiated.

### 2.2.6 Discard Application
The Individual can discard the Pre-Registration by clicking on the Delete icon for the Pre-Registration Id for which he/she wishes to discard. The System provides the Individual with two options: ‘Discard entire Application’ or ‘Cancel Appointment’. The Individual choses to discard entire Application. The System deletes all the data mapped to the Pre-Registration Id and cancels the appointment (if any).

## 2.3 Attaching Documents to the Application
### 2.3.1 Document Categories and Applicable Document Types
1. When an individual provides his/her Demographic data, the Pre-registration system captures the data. 
1. Based on the parameters (From Config file) used for Applicant type determination, the Pre-Registration system sends the Id to the mapping.
1. Based on the Applicant type, the Applicable Document categories are received from the Mapping. The Pre-Registration system then displays only applicable categories.
1. The Document Category and type of documents in each category to be uploaded varies based on the applicant type. Pre-registration system displays only those types to the applicant.

### 2.3.2 Referring to already Uploaded Documents
1. An Individual logs in to the pre-registration system and opts to Update\modify a Pre-Registration Application 
1. The system redirects the Individual to the Demographic Details saved in the system earlier
1. The Individual can update the required data (Basic Demographic) and can proceed to upload Documents.
1. The Individual may then opt to delete an existing document and upload new document if he\she wants to update the document uploaded (for any of POI, POA, POB, and supporting Document)
1. The Individual should then review and Confirm Details before proceeding to book appointment


## 2.4 Booking an Appointment
### 2.4.1 Choosing a Registration Center for Appointment

#### 2.4.1.1 Recommended Centers based on Postal Code
1. The system fetches the Location Hierarchy as defined in the Master Data and recommends registration centers based on the postal code
1. The search results have the following information about the Registration center: Name, Address, Working Hours, Contact Person, Center Type, and Contact Number

#### 2.4.1.2 Nearby centers based on User Geo-location
1. An individual can  enable location services,  in the device/machine in order to select nearby centers
1. The System checks for Lat-Long values of the individual and  fetches all the Registration centers within 2 KM Radius (configurable)
1. The First Registration center as per the search criteria is shown to the individual on Map by default

#### 2.4.1.3 Find a Center
An individual may opt to  perform text search to find a center based on which the system displays the registration centers

### 2.4.2 Choosing Appointment Slots

#### 2.4.2.1 Get Slots Availability
1. The System displays 7 calendar days (configurable) for the Individual to select a slot
1. Calendar day\s which are  Holidays for the selected Registration center are Greyed out or not shown to the user
1. For a Selected Registration Center 8 hours (configurable) are considered as working hours
1. An individual can view time slots of 15 mins (configurable) each for the selected calendar day and view Available spots for every time slot shown in the selected calendar day

### 2.4.3 Cancel Appointment
1. An individual can opt to cancel selected Appointment\s against application which is\are in Booked Status.
1. In such case the system notifies the user about the successful cancellation 
1. Following a successful Appointment Cancellation the system unlocks the time slot of the Pre-Registration 

### 2.4.4 Re-book Appointment
1. The System provides the User with a default appointment selection: Select Consecutively available Appointment spots
1. An individual can select any of the Appointment Date available and any of the Appointment Spot available
1. The individual has to select against which Pre-Registration ID the Appointment spot is being booked
1. The System maps appointment spot with all the Pre-Registration IDs which are selected for Appointment Booking. 
1. If any Pre-Registration ID does not have Booking mapped, the User is notified if he wants to continue without booking
1. An individual at this stage may opt to search Registration center. In this case the appointment -booking (Time Slot selected) done is removed
1. An individual can not  Re-book the Appointment if the appointment Booking is less than 48 hrs (configurable) from time of booking

## 2.5 Appointment Acknowledgement (PRID)
1. An Acknowledgement is triggered after Successful completion of Pre-Registration (Booking an appointment)
1. The acknowledgement contains the following information: Name, Pre-Registration ID, Age/DoB, Mobile Number, Email ID and Registration center Details, Appointment Date, Appointment Time)

### 2.5.1 Download Acknowledgement
Individual can Choose to print the Acknowledgement or can Download the Acknowledgement as PDF and print later 
### 2.5.2 Send Acknowledgement to Email/Phone
The System sends an acknowledgement to the  applicant through SMS, Email and on-screens as per the details provided in Demographic details
## 2.6 Registration Client Services
### 2.6.1 Get Appointment for the Day
1. An Individual logs in to the pre-registration system  and opts to Book Appointment for Pre-Registration Application or Modify Appointment
1. The system presents a  list of Centers to the user to select the required Registration center 
1. The Time selection with calendar days along with number of spots available per calendar day will be displayed 
1. Individual can select any of the calendar day which he\she wishes to Book Appointment.
1. Time slots of 15 minutes each are displayed.
1. Each time slot with Available spots will be displayed.
1. The Individual can select a slot and proceed to Book Appointment or can go back to select another Registration center

### 2.6.2 Retrieve Application Data by PRID
Upon receiving the Registration Center ID, Date Range (Start Date, End Date) for the List of Pre-Registrations, User ID (Registration Officer/Supervisor) from Registration client the Pre-Registration system processes the information.
1. The System generates a Transaction ID
1. The System then Fetches all the Pre-Registrations within the Date Range (Start Range, End Date) and for the Registration Center ID received and calculates the count of the Pre-Registration IDs being sent.
1. The System sends the List of Pre-Registration Ids along with count of Pre-Registrations.
1. The System receive the Pre-Registration ID/IDs for which Pre-Registration Data has to be sent.
1. The System sends the zip file per Pre-Registration ID consisting of Demo Data, Files, and Appointment Time.

## 2.7 List of Configurable Parameters and Processes

1. [Configuration Parameters](https://github.com/mosip/mosip/blob/master/docs/requirements/MOSIP_Configurations_Consolidated%20List_Updated_14Nov18_CV_Final.xlsx)
1. [Configurable Processes](https://github.com/mosip/mosip/blob/master/docs/requirements/MOSIP_Processes_Consolidated%20List_External.xlsx)  
