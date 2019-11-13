

Welcome to MOSIP's documentation!
=================================

.. toctree::
   :maxdepth: 3
   :caption: Contents:

   Platform-Documentation
   Interfaces
   Privacy-and-Security
   Getting-Started   

   ## 1. INTRODUCTION
   This document describes the objectives and explicit functional requirements of MOSIP. It also gives an overview of architecturally significant features, APIs and standards followed in MOSIP. Lastly, it provides necessary information on implementation, customization and set up.

   ## 2. FUNCTIONAL OVERVIEW[**[↑]**](#table-of-contents)
   Further details are available on each modules under [Requirement Specifications](#4-requirement-specifications)
   ### 2.1 Pre-Registration

   Pre-registration is the web channel of the MOSIP. This module enables a user to:  
   1. Book an appointment for registration
   1. Enter demographic data & upload supporting documents
   1. Appointment notification, rescheduling and cancellation
   1. Send resident data to registration center before appointment, which can be used during registration

   [Detailed functional specifications of pre-registration module](FRS-Pre-Registration)

   ### 2.2 Registration Services
   Registration Client application captures the demographic and biometric details of an individual along with supporting information (proof documents & information about parent/guardian/introducer) and packages the information in a secure way. This module provides the following capabilities:
   1. Provides a secure way of capturing an individual's demographic and biometric data
   1. Provides interfaces to biometric devices that comply to industry standards
   1. Works in online and offline mode to capture data
   1. Provides option to transfer data to server when online and helps in uninterrupted registrations
   1. Client has the ability to update itself for patch upgrades (bug fixes/enhancements) in a remote way. There could be hundreds of client instances running on laptops/desktops. Updates on all of them are controlled by the client and a central server.
   1. Registration client is secured such that it cannot be tampered with or misused

   [Detailed functional specifications of registration services](FRS-Registration-Services)
