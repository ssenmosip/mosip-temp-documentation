Registration Processor processes the data (demographic and biometric) of an Individual for quality and uniqueness and then issues a Unique Identification Number (UIN). The source of data are primarily from
- MOSIP Registration Client
- Existing ID system(s) of a country

## Registration Processor process flow
Please refer to the following link for the detailed process flow : https://github.com/mosip/mosip/wiki/Process-view#registration-processor

## Architecturally significant use cases
### Registration processor must provide guaranteed packet processing

### Registration processor must have the capability to add new processing step(s) without changing existing steps

### Registration processor must have the capability to integrate with multiple ABIS providers

### Each processing step must be scalable independently based on the load

### Each step must be highly available for uninterrupted processing of packets

### Upgradeability : Each step in the processor must be independent of other steps such that logic of a step can be changed to improve efficiency without affecting the overall flow

## Logical view