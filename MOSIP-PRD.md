1.	**MOSIP-INTRODUCTION**

**Scope**

The scope of this document is to describe high level business objectives along with explicit functional requirements of MOSIP (Modular Open source Identity management platform) completely, accurately and unambiguously in Technology-independent manner. 

**Intended audience**

The main intended audience for this document are the business owners of the proposed system. They must be able to verify that their business requirements have been documented here completely, accurately and unambiguously. 
Data Architects, Application Architects and Technical Architects would also find the information in this document useful when they need to design a solution that will address these business requirements. 
Since the requirements are documented here in Technology-independent manner, the end-users of the system should be able to comprehend the requirements fairly easily from this document.
 
2.	**MOSIP -FOR IDENTITY MANAGEMENT**

**What-is an identity management system**

To better understand and serve citizens, countries are placing increasing attention on establishing national identification systems .The ability to formally identify oneself has increasingly become integral to many aspects of civic participation and inclusion. Proponents argue that formalized identity management systems have the potential to establish strategic partnerships between the state and citizen’s .Failure to register populations and provide identity documents is believed to have detrimental effects for both the individual and the state.

The complexity of government administration in “the modern world” is a major problem in developing countries. Often, individual government programs have their own database of beneficiaries that are not digitized and therefore cannot be easily merged. Delivering public services efficiently and providing financial inclusion to the poor in partnership with the private sector depends on accurate identification and authentication of citizens and residents. Hence Government programs must have the capacity to cross-reference databases and information.

**Identity management systems in the digital era**

Technological innovations have opened up new possibilities for governments to develop comprehensive identity management systems that link peoples’ identities through their entire life from birth certificate, civil registration, driver’s license, to marriage certificate, voter registration and national identity card. At the same time, governments in developing countries are expected to carry out many of the same functions that richer countries are capable of performing; these functions include providing universal access to healthcare and education, implementing know your customer (KYC) rules for financial institutions, and administering a wide variety of transfer programs.

As identification technology evolves, so do identification systems. It is estimated that as of 2012, over 1 billion people in developing countries have had their biometrics captured for one or more purposes. Incorporating biometric technologies in national identity systems is particularly useful for the growth of electronic government (e-government) as well as providing both public and private services. 

As compared to manual, paper-based registers, advanced electronic capture and storage of data are able to reduce costs and human error as well as increase administrative efficiency (World Bank, 2014).  Electronic and biometric identification systems also have the potential to link national identity to multiple functional applications (World Bank, 2015). With electronic identity programs, a wide range of services can be delivered on computers or mobile devices. Biometrics have also been used beyond authentication to secure identities in order to fulfill KYC requirements for opening bank accounts, to register and de-duplicate beneficiaries, to authenticate cash or in-kind transfers at the point of service, and to fulfill various other services such as health, voting and civil service reform (Gelb & Clark, 2013).
 
A World Bank report quoted several projections showing that the number of “digital government/citizen transactions worldwide will grow to about $67 billion by 2020” (World Bank, 2015). As a result of linkages between national ID programs and financial services, these programs are also believe to have the potential to promote financial inclusion.

**Why-an identity management system is needed**
A well-established identity management system can help countries to verify their people’s identity by issuing unique identity number which one can use to go into any institution and be readily accepted. The following are some key reasons why a country needs as Identity management system


	Provide a convenient and simplified process for enrollment into the national identity database for the issuance and use of the national identification number

	Help protect you from identity theft and fraud by providing a simple, reliable, sustainable and universally acceptable means of confirming your identity at all time 

	Make life easier by providing you with an easy and convenient means of providing your identity anywhere in the country and beyond

	Help reform our political process by facilitating the work of the managers of electoral process

	Make it harder for criminal to use false or multiple/duplicate/ghost identities

**How-Setting the stage for MOSIP. (How MOSIP as a product\platform wants to position itself)**

MOSIP (Modular Open Source Identity Platform) helps governmen
ts of countries to build a digital identity system. Using this, every Individual of a country can be given a Unique Identity Number (UIN). This helps in inclusivity and accessibility of all Individuals without disparity or discrimination.

Fig: 1 MOSIP basic features

Fig: 2 Key objectives of the platform

3.	MOSIP FUNCTIONAL OVERVIEW

https://github.com/mosip/mosip/wiki


Fig 3: MOSIP functional overview

4.	MOSIP-SYSTEM ARCHITECTURE-PATTERNS AND PRINCIPLES
MOSIP adopts the following Architectural patterns & principles to achieve modularity, better maintainability, scalability and extensibility.

Fig: 4 MOSIP Architectural patterns and principles

Fig 5: MOSIP Thick client architecture

5.**	MOSIP PLATFORM FEATURES**


**Key Design Considerations**
This sections lists out some of the Key design considerations for MOSIP

**Ecosystem approach**
Device vendors and ABIS providers are key to process an individual's data and prove uniqueness. MOSIP can integrate with devices and ABIS that conform to the standards to achieve the stated goals. On the other side, MOSIP also caters to a diverse set of institutions wanting to authenticate an Individual against the data stored in MOSIP. So, key parameters are-All public/external facing interfaces of MOSIP standards set for interoperability

**A Highly configurable open source design approach**
MOSIP is highly flexible for countries to configure the base platform according to their specific requirements. Some of the examples of configurability are
•	Country can to choose the features required. For example, it must be possible for a country to turn off Finger Print capture and turn on Face recognition or Vice versa as the need be
•	Country can configure the attributes of an ID Object
•	Country can define the length of the UIN number

**Extensibility**

MOSIP is flexible to extend functionality on top of the basic platform. Some of the examples of extensibility are
•	A country can introduce a new step in processing data
•	Integrate MOSIP with other ID systems and include it as part of the MOSIP data processing flow

**Modularity**

All components in MOSIP are modular and their features exposed via interfaces such that the implementation behind the interface can be changed without affecting other modules. Some examples of modularity are
•	UIN generator algorithm provided by the platform can be replaced by a country with their own implementation
•	The default demographic deduplication algorithm provided by MOSIP can be changed to a different one without impacting the process flow

**Multi-modal Automated Biometric Identification System (ABIS) Interface**

Providing unique identity for an individual is one of key features of MOSIP platform. To do this MOSIP 
•	Uses multi modal biometric information of an individual
•	Leverages Automated Biometric Identification System (ABIS) to de-duplicate Individual's biometric data
•	Designed for integrating with multiple ABIS providers to leverage expertise of different ABIS providers
•	Not use ABIS for authentication (deduplication only)
Fig 5: ABIS interface configuration in MOSIP

**Biometric Standards for inter-operability**

Multi modal biometrics (Fingerprint, Iris, Face) is the key component in MOSIP to identify and provide a unique identity to an Individual. Hence MOSIP follows certain data standards during biometric data acquisition and verification

**6.	SECURITY**

Multiple aspects of security like confidentiality, privacy, integrity of data are key in ensuring an Individual's identity is not compromised. Below are the security design principles MOSIP follows
•	Direct access to data stored in database is discouraged. Data can only be accessed via API's
•	An Individual's Identity data at is always encrypted to ensure confidentiality of data
•	Access controls is implemented on all API's to ensure data privacy  and who can see what

**Database encryption**

As a principle, MOSIP does not use any mechanism in-built in a database for encryption. All sensitive data to be stored in a DB is encrypted/decrypted outside the DB.

•	All the data is encrypted using a symmetric key algorithm. MOSIP supports AES 256 algorithm by default. However, the specific algorithm to be used is configurable

•	Each record gets encrypted using its own symmetric key and same key will not be used to encrypt multiple records

•	The symmetric key itself is encrypted using a master public key. The corresponding private must be managed in a HSM
•	HSM stores an asymmetric key pair for each application/service and can be rotated periodically as per configuration

•	The encrypted symmetric key is appended to the data itself and not stored separately



