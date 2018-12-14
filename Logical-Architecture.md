# Key Design Considerations
The key design aspects considered for MOSIP are

## Ecosystem approach
MOSIP on its own will not be able to meet the requirements of a country. On one side device vendors and ABIS providers are key to process an individual's data and prove uniqueness and MOSIP should be able to integrate with devices and ABIS that conform to the standards to achieve the stated goals. On the other side, MOSIP should be able to cater to a diverse set of institutions wanting to authenticate an Individual against the data stored in MOSIP.
So, key parameters are
* All public/external facing interfaces of MOSIP must be standards based for interoperability

## Configurability
MOSIP should be flexible for countries to configure the base platform according to their specific requirements. Some of the examples of configurability are
* Country should be able to choose the features required. For example, it must be possible for a country to turn off Finger Print capture
* Country should be able to configure the attributes of an ID Object
* Country should be able to define the length of the UIN number

## Extensibility
MOSIP should be flexible to extend functionality on top of the basic platform. Some of the examples of extensibility are
* A country should be able to introduce a new step in processing data
* Integrate MOSIP with other ID systems and include it as part of the MOSIP data processing flow

## Modularity
All components in MOSIP should be modular and their features exposed via interfaces such that the implementation behind the interface can be changed without affecting other modules. Some examples of modularity are
* UIN generator algorithm provided by the platform can be replaced by a country with their own implementation
* The default demographic deduplication algorithm provided by MOSIP can be changed to a different one without impacting the process flow

# Solution Principles
MOSIP will adopt the following Architecture patterns & principles to achieve the stated design considerations

## Microservice based architecture for all platform services
* Services must be stateless to scale out horizontally
* Services must be idempotent
* Services must have well defined interfaces

This will help achieve modularity, better maintainability and scalability.

## Staged Event Driven Architecture (SEDA) for processing Registration data
* Each processing step must be a stage
* Stages must be connected with event bus
* Process flow must be configured outside code

This will help achieve extensibility and scale out stages independently.

## Thick client architecture for Registration client
* Client must run on a desktop/laptop in offline mode also
* Client must integrate with devices in a secure manner


![Logical Architecture](_images/arch_diagrams/MOSIP_logical_architecture_v0.1.png)