# Architecture and Stack
Architecture and tech stack related tracked items go here. This includes development and testing stacks and tools.
## Test Rig

## Deployment


[Test](mosip/mosip/wiki/frs/abc)

# Requirements
Open requirement issues go here
## Test Rig

## Kernel

## Pre-registration

## Registration Client

## Registration Processor
[19-11-2018]
* Can external systems such as CNIE add / update the ID Document before the UIN is generated? Under the data enrichment banner can the SI setup a step in the registration processor flow that results in a change to the data provided by the registration client? For example the CNIE system in morocco has the fingerprints. The registration client collects and sends the resident's CNIE number. The CNIE system can potentially return fingerprint minutiae that can be stored in the ID Document. Are such cases permitted? Or is the ID Document immutable other than by citizen intervention?

Approach: The ID Document is actually **derived** from a set of packets which are combined/applied in chronological order to get its **current** state. Each of the packets are read only and are stored as received. If the id document is present in the database out side of the packets, it is the current version that is stored, with references to the chronological list of updates.

## ID Authentication

## Admin Portal

## Launcher

## Configuration Manager


# Design / Implementation
## Test Rig

## Kernel

## Pre-registration
* Grammar and typo checks needed on github page
* Should APIs include an API Id, version field in the request? These are already part of the urls
* API Response should clearly specify which API it is and what is the version
* Err, response should be the last parameters in the API response

## 2.7.1 Login API
* This is actually an OTP request API
* How do we access the swagger configurations?
* Login API is marked as GET
* API url conventions are not consistent with the approach used in identity auth module

## 2.7.2 Login OTP Validation API
* This is the actual Auth API.
* OTP_VALIDATION_SUCESSFUL spelling is wrong. Need to see actual constants being returned by APIs

## 2.7.3 User ID Updation API
* How do I specify both email and phone number? Is it a one or the other restriction?

## 2.7.4 Create re-registration API
* Call it as Add Applicant or application
* label keys are not required in request json
* Why are we sending the statusCode?
* Label is not necessary in response
* How does the request information correlate with the id fields defined by a country? How will it impact if it is changed?

## 2.7.5 Retrieve all pre-registration API
* Success response status is false. It should be true

## 2.7.6 Retrieve Pre-registration status API
* application/status is not noun/verb
* Do we need this api? There are only user name and appointment time fields missing from retrieve api entities

## 2.7.7 Discard Pre-Registration API
* deletedby field - what is the expected value here?

## 2.7.8 Document Upload API
* Why does request have a status code
* Why is pre-regid in the request json? Should it be a url parameter?
* The response json has a message key rather than a response key. Not consistent with other APIs

## Registration Client

## Registration Processor
[19/11/2018]
* [Shravan] Camel configuration and VertX events are in Java code. Should these be in code or be in a declarative format such as XML? Final call on this by Shravan.
Decsion: XML will be used.
* [INFO] We have identified Verticles that operate in two mode
** Verticles such as the packet receiver listen on an HTTP end point and write to the EventBus when their job is complete. The event they post is targeted at Camel.
** Verticles such as antivirus scanner that run jobs in the process flow listen to messages on the EventBus from Camel. When their job is complete they send a message to Camel on the eventbus.
* [INFO] Integration scenarios can work with a combination of verticles that operate in the modes described above.
** Outbound integration - A call to an external system is initiated by a verticle job. One a message from Camel this job calls the external system and sends a message to Camel that the stage has started. For example - Sent for CNIE Verification. When the external component is done, it will call a verticle that is listening on an HTTP endpoint to give the result. This verticle will then end a message to Camel saying that the stage is done - CNIE Verification done. This provides an async integration mechanism. Synchronous integration needs only one verticle running as a job that calls the external system. Eg. Transliteration service.
** Inbound integration - A verticle will listen on an HTTP endpoint and will post a message to Camel. Do not see a direct case as most such cases will be post UIN generation and might not be part of the registration flow barring a correction packet. This is discussed separately.
* [INFO] All external systems including the registration client will be registered and use PKI for security and identity based on keys exchanged.
* [SHRAVAN] VertX provides High Availability and clustering support. The VertX modules will be dockerized and deployed. While HA is a desirable part of the VertX module will the clustering and provisioning of instances be handled by Kubernetes or VertX? This is an open question. Shravan to revert on this.
Decision: Kubernetes will be used. VertX clustering will be turned off.
* [SHRAVAN] VertX verticle instantiation could be done either by the launcher (using kubernetes) or on demand by VertX when Camel messages meant for the job are on the EventBus. The actual mechanism for this will need to be finalized. The idea is that when there are no jobs to be done the VertX clusters should not be using up infrastructure. Note: Shravan this is an afterthought to our discussion. Would like to hear your views. This is essentially about autoscale.
Decision: Autoscale to be handled by Kubernetes.
* There were some concerns on making Packet Receiver as a verticle becuase of the Hold logic. This needs to be resolved.
* All microservices seem to be spring jobs at this point. We need to move them to VertX
Decision: Spring boot is being removed.
* [Shravan] Correction packet and versioning of the packet are supported. Can this be used for integration scenario too? Can correction packets be introduced by any Verticle other than the Packet Receiver? If allowed, how do we ensure security and what process flow should these packets undergo? These are open questions that need answering. A potential case in point is CNIE integration which might provide an updated packet. Shravan to share thoughts and possible approach.
Decision: Update packets can be introduced by any stage.
* [Ramesh] What is data enrichment? Can ID Document data be filled in only by Registration client (Packet Receiver Service essentially)? Can other steps in the registration processor flow add / modify / enhance / enrich this data? Current thought process as Shravan expressed is that the packet is read only and does not change. The only mechanism to change data is through a correction packet which has to be sent to the Packet Receiver. Other than this mechanism the data (not just the packet) remains immutable across processor steps. I feel that this might restrict data enrichment steps in the processor. Accommodating changes is possible, but would require design tweaks. Questions asked in the previous points would arise. Ramesh to send out a clarification email to tech board for deciding on support for such data enrichment. Case in point can be CNIE that might return fingerprint minutiae for a given CNIE number, and this gets added to the ID Document.
Decision: Data enrichment is allowed. All data enrichment will be done using update packets.
* [Shravan]Parallelism in orchestration vs Handling that in code in a VertX Stage
Decision: We will address this during ABIS middleware design.
* [Ramesh]Lock-In to VertX - I hear that VertX is polyglot and node/python/other languages can be used to create stages on VertX. I will circle back on this with some reading of my own.
* [Shravan]EventBus interfacing uses TCP and not HTTP. Is this a problem? - Let us run this by Pramod once. If there is some mechanism, with an adapter if need be, that helps stages use HTTP as opposed to TCP, this opens up a lot more choices to the SI. Can we figure something out on this?
Ramesh Thoughts: Apache camel can orchestrate using EventBus or REST API. Can we have a reference implementation for the HTTP micro service for one stage?
* Are there too many toolkits in play and overlap of responsibilities?
Decision: Camel, VertX, Docker, Kubernetes will be used. VertX will have clustering turned off. Kubernetes will handle scaling and HA. Sprint Boot is eliminated.

## ID Authentication

## Admin Portal

## Launcher

## Configuration Manager

# Testing
## Automation

## Coverage

# Deployment
## Launcher
## Cloud Formation
## Migration
## Autoscale
