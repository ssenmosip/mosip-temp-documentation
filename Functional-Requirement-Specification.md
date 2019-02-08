## Table Of Content
* [1. Pre-Registration](
  * [1.1 Log in- Log out Feature](
  * [1.2 Language Data Manager](
    * [1.2.1 Translation](
    * [1.2.2 Transliteration](
  * [1.3 Pre-Registration Sync](
  * [1.4 Appointment Booking](
    * [1.4.1 Search Registration center](
    * [1.4.2 Choose the Registration center from the search result and check available slots](
    * [1.4.3 Choose an available time slot and book an appointment](
    * [1.4.4 Reschedule a booked appointment](
    * [1.4.5 Cancel an appointment](
  * [1.5 Pre-Registration Application Manager](
    * [1.5.1 Pre-Registration Application Manager](
    * [1.5.2 Acknowledgment](
    * [1.5.3 PRID Generator](
* [2. Registration](
  * [2.1 Registration Client Setup](
  * [2.2 System Health Checker](
  * [2.3 Registration Officer Authentication](
  * [2.4 User Onboarding/Manager](
  * [2.5 Language Manager](
  * [2.6 Registration Application Manager – New](
  * [2.7 Registration Officer Authorization](
  * [2.8 Registration Packet Manager](
  * [2.9 Sync Handler](
  * [2.10 Individual UIN – Update](
  * [2.11 Clean Up](
* [3. Registration Processor](
  * [3.1 Registration Packet Handler](
  * [3.2 Registration Status Service](
  * [3.3 Registration Packet Processor](
  * [3.4 UIN Generator](
  * [3.5 Print](
  * [3.6 UIN Lifecycle Manager](
  * [3.7 External System Integration](
* [4. ID-Authentication](
  * [4.1 TSP/UA Authentication](
    * [4.1.1 TSP Authentication](
    * [4.1.2 Authentication Mode Verifier](
  * [4.2 TSP/UA Authorization](
  * [4.3 Individual Authentication](
    * [4.3.1 Biometric Authentication](
    * [4.3.2 Demographic Authentication](
    * [4.3.3 OTP Authentication](
    * [4.3.4 Static PIN Authentication](
    * [4.3.5 E-KYC Authentication Service](
  * [4.4 Integrated Individual Authentication](
* [5. Admin Setup (TBD WIP)](
* [6. Reporting (TBD WIP)](
* [7. Platform Level Features and Utilities](
  * [7.1 Features](
  * [7.2 Utilities](
## 1. Pre-Registration
### 1.1 Log in- Log out Feature
### 1.2 Language Data Manager
#### 1.2.1	Translation
#### 1.2.2	Transliteration
### 1.3 Pre-Registration Sync
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

### 1.5 Pre-Registration Application Manager
#### 1.5.1	Pre-Registration Application Manager
#### 1.5.2	Acknowledgment
#### 1.5.3    PRID Generator
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
## 5. Admin Setup (TBD WIP)
## 6. Reporting (TBD WIP)
## 7. Platform Level Features and Utilities
### 7.1 Features
### 7.2 Utilities
