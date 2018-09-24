### 1. Introduction:
Metadata in MOSIP is a core component which provides following key capabilities. Metadata would help in building the framework for MOSIP-which defines data applicability of various functionalities.
1. **Configurability:****
MOSIP as a platform is highly configurable. As an identity platform, MOSIP could be configured to cater requirements for different entities.
2. **Multitenancy**
MOSIP has multiple modules. Metadata could be common as much as possible. If required, we need to define module specific metadata. Common metadata would cater to all the modules.

Following things would be configured through metadata.

1. Business flows.
2. Enabling and disabling of major components.
3. Business rules
4. UI rendering

We would separate UI rendering to UI part.
Where different UI rendering principles could be applied.
One of them could be template.
### 2. Types of metadata:

Following are identified metadata.

**1. composite metadata.**
This would be group consists of multiple fields and internally may be group of fields. For pre registartion, pre registration form is an example.
**2. hierarchy metadata.**
This is common metadata where elements are present in a hierarchical order.  As s design principle, following practices should be followed.
a. a hierarchy would be fully referenced. Otherwise could result in resolving duplicate names.
b. there would be a single root.
c. the names of the labels should be unique.
d. the reference values may be duplicate, but refer to a single parent.

**3. typed metadata.**
these are fields with different data type. For example string,integer and date. Default data type for these fields would be string.
**4. Document type metadata.**
We may treat separately as document functionality needs to be handled accordingly.



Open point:

@rudratripathy@mindtree.com
Should we create a form data?





