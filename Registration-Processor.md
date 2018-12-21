Registration Processor processes the data (demographic and biometric) of an Individual for quality and uniqueness and then issues a Unique Identification Number (UIN). The source of data are primarily from
- MOSIP Registration Client
- Existing ID system(s) of a country

## Registration Processor process flow
Please refer to the following link for the detailed process flow : https://github.com/mosip/mosip/wiki/Process-view#registration-processor

## Architecturally significant use cases
### Registration processor must provide guaranteed packet processing
Once the packet is received on the server, processor must guarantee packet processing. So, the solution has to take care of the following
- Not lose the packet once received on the server
- Handle server failure, recovery and re-submission of packets for processing automatically

### Registration processor must have the capability to add new processing step(s) without changing existing steps
MOSIP will only define and implement the basics registration packet processing flow. However, every country will have their own processing requirements and MOSIP should be flexible to include new processing steps. For example, a country may want to integrate with their existing ID system and fetch data from it, validate it with data captured in MOSIP before processing. So, MOSIP should provide the option to include a new step.

### Registration processor must have the capability to integrate with multiple ABIS providers


### Each processing step must be scalable independently based on the load

### Each step must be highly available for uninterrupted processing of packets

### Upgradeability : Each step in the processor must be independent of other steps such that logic of a step can be changed to improve efficiency without affecting the overall flow

## Logical view