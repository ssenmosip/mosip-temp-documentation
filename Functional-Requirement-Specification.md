## Table Of Content
* 1. Pre-registration
  * [Click here](https://github.com/mosip/mosip/wiki/FRS-Pre-Registration#25-appointment-acknowledgement-prid)
* [2. Registration](#2-registration)
  * [2.1 Registration Client Setup](#21-registration-client-setup)
  * [2.2 System Health Checker](#22-system-health-checker)
  * [2.3 Registration Officer Authentication](#23-registration-officer-authentication)
  * [2.4 User Onboarding/Manager](#24-user-onboardingmanager)
  * [2.5 Language Manager](#25-language-manager)
  * [2.6 Registration Application Manager – New](#26-registration-application-manager--new)
  * [2.7 Registration Officer Authorization](#27-registration-officer-authorization)
  * [2.8 Registration Packet Manager](#28-registration-packet-manager)
  * [2.9 Sync Handler](#29-sync-handler)
  * [2.10 Individual UIN – Update](#210-individual-uin--update)
  * [2.11 Clean Up](#211-clean-up)
* [3. Registration Processor](#3-registration-processor)
  * [3.1 Registration Packet Handler](#31-registration-packet-handler)
  * [3.2 Registration Status Service](#32-registration-status-service)
  * [3.3 Registration Packet Processor](#33-registration-packet-processor)
  * [3.4 UIN Generator](#34-uin-generator)
  * [3.5 Print](#35-print)
  * [3.6 UIN Lifecycle Manager](#36-uin-lifecycle-manager)
  * [3.7 External System Integration](#37-external-system-integration)
* [4. ID-Authentication](#4-id-authentication)
  * [4.1 TSP/UA Authentication](#41-tspua-authentication)
    * [4.1.1 TSP Authentication](#411-tsp-authentication)
    * [4.1.2 Authentication Mode Verifier](#412-authentication-mode-verifier)
  * [4.2 TSP/UA Authorization](#42-tspua-authorization)
  * [4.3 Individual Authentication](#43-individual-authentication)
    * [4.3.1 Biometric Authentication](#431-biometric-authentication)
    * [4.3.2 Demographic Authentication](#432-demographic-authentication)
    * [4.3.3 OTP Authentication](#433-otp-authentication)
    * [4.3.4 Static PIN Authentication](#434-static-pin-authentication)
    * [4.3.5 E-KYC Authentication Service](#435-e-kyc-authentication-service)
  * [4.4 Integrated Individual Authentication](#44-integrated-individual-authentication)
* [5. Resident Services (TBD WIP)](#5-resident-services-tbd-wip)
* [6. Admin Setup (TBD WIP)](#6-admin-setup-tbd-wip)
* [7. Reporting (TBD WIP)](#7-reporting-tbd-wip)
* [8. Platform Level Features and Utilities](#8-platform-level-features-and-utilities)
  * [8.1 Features](#81-features)
  * [8.2 Utilities](#82-utilities)
## 1. Pre-Registration
### 1.1 Log in- Log out Feature
### 1.2 Pre-Registration Application Manager
#### 1.2.1	Pre-Registration Application Manager
#### 1.2.2	PRID Generator
### 1.3 Language Data Manager
#### 1.3.1	Translation
#### 1.3.2	Transliteration
### 1.4 Appointment Booking
This component enables a user\individual to Book\re-schedule an appointment for selected slot in the chosen registration center for registration. It also allows user to cancel a booked appointment.

The functional capabilities of this component are detailed out below:

The system provides the provision to a user to select at-least one Pre-Registration application and perform the following tasks 
#### 1.4.1 Search Registration center
1. The System provides the User search criteria, with which user can search a center
1. The System allows the user to perform text search to find a center
1. The System allows a user to enable location, if the Location sharing is disabled in the device/machine and allows the user to select nearby centers
1. The System checks for Lat-Long values of the User. Then system fetches all the Registration centers within 2 KM Radius (configurable)
1. The system fetches the Location Hierarchy as defined in the Master Data. This Location Hierarchy will be the search criteria to find a suitable center
1. The system displays the Registration centers based on the search criteria in a tabular format (Registration center name, Address, Working Hours, Contact Person, Center Type, and Contact Number)
1. The System displays the First Registration center on Map by default
#### 1.4.2 Choose the Registration center from the search result and check available slots
1. The System displays 7 calendar days (configurable) for the Individual to select
1. The Systems disable (Grey out) the Calendar day which is a Holiday for the selected Registration center
1. The System displays time slots of 15 mins(configurable) each for the selected calendar day
1. The System considers 8 hours (configurable) as working hours for Selected Registration Center
1. System provides Available spots for every time slot shown in the selected calendar day
#### 1.4.3 Choose an available time slot and book an appointment
1. The System provides the User with a default appointment selection system to select consecutively available Appointment spots
1. The System allows the User to select any of the Appointment Date available and any of the Appointment Spot available
1. The System asks against which Pre-Registration ID the Appointment spot is being booked
1. The System maps appointment spot with all the Pre-Registration IDs which are selected for Appointment Booking. If any Pre-Registration ID does not have Booking mapped, system notifies user if he opts to continue without booking
1. The System allows the user to click on Previous and redirect him to search Registration center. In this case the appointment booking done should be removed and system does not save any previous selection(s)
1. The System enables the Booking if at least one applicant is selected for an Appointment Slot. If only one applicant is present then he should be selected for an Appointment slot.
1. The System does not allow to book spots for dates for which spots are un-available
#### 1.4.4 Reschedule a booked appointment
1. The System provides the User with a default appointment selection: Select Consecutively available Appointment spots
1. The System allows the User to select any of the Appointment Date available and any of the Appointment Spot available
1. The System asks against which Pre-Registration ID the Appointment spot is being booked
1. The System maps appointment spot with all the Pre-Registration IDs which are selected for Appointment Booking. If any Pre-Registration ID does not have Booking mapped, system notifies User if he wants to continue without booking.
1. The System allows the user to click on Previous and redirect him to search Registration center. In this case the appointment Re-booking (Time Slot selected) done is removed
1. The System does not allow the User to Rebook the Appointment if the appointment Booking is less than 48 hrs(configurable) from time of booking
1. The System does not display the previously existing appointment data
#### 1.4.5 Cancel an appointment
1. The system provides an option to cancel selected Appointment\s against application which is\are in Booked Status and notifies the user about the successful cancellation 
1. Following a successful Appointment Cancellation the system unlocks the time slot of the Pre-Registration 

### 1.5 Acknowledgment
* The System triggers an Acknowledgement after Successful completion of Pre-Registration (Booking an appointment)
* The System sends an acknowledgement to the  applicant through SMS, Email and on-screens as provided in Demographic details
* The acknowledgement contains the following information: Name, Pre-Registration ID, Age/DoB, Mobile Number, Email ID and Registration center Details, Appointment Date, Appointment Time)
* Individual can Choose to print the Acknowledgement or can Download the Acknowledgement as PDF and print later 

### 1.6 Pre-Registration Sync
## 2. Registration
### 2.1 Registration Client Setup
### 2.2 System Health Checker
### 2.3 Registration Officer Authentication
### 2.4 User Onboarding/Manager
### 2.5 Language Manager
### 2.6 Registration Application Manager – New
### 2.7 Registration Officer Authorization
### 2.8 Registration Packet Manager
### 2.9 Sync Handler
### 2.10 Individual UIN – Update
### 2.11 Clean Up
## 3. Registration Processor
### 3.1 Registration Packet Handler
### 3.2 Registration Status Service
### 3.3 Registration Packet Processor
### 3.4 UIN Generator
### 3.5 Print
### 3.6 UIN Lifecycle Manager
### 3.7 External System Integration
## 4. ID-Authentication
### 4.1 TSP/UA Authentication
#### 4.1.1 TSP Authentication
#### 4.1.2 Authentication Mode Verifier
#### 4.2 TSP/UA Authorization
### 4.3 Individual Authentication
#### 4.3.1 Biometric Authentication
#### 4.3.2 Demographic Authentication
#### 4.3.3 OTP Authentication
#### 4.3.4 Static PIN Authentication
#### 4.3.5 E-KYC Authentication Service
### 4.4 Integrated Individual Authentication
## 5. Resident Services (TBD WIP)
## 6. Admin Setup (TBD WIP)
## 7. Reporting (TBD WIP)
## 8. Platform Level Features and Utilities
### 8.1 Features
### 8.2 Utilities
