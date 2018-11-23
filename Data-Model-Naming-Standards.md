## Audience
* Data Modelers
* DBAs
* Application Developers

A simple and consistent naming convention for database objects, when followed rigorously, can help database application developers greatly.  This is because developers, once they get used to the convention, can quickly identify objects belonging to their application and are less likely to make mistakes regarding the contents of columns.  In fact, an inadequate or improperly followed convention can actually increase the development effort by unnecessarily tying the application code to intricacies of the database physical design and by making application developers overly dependent on the DBA’s.

The intended audience for this document is data modelers, DBA’s and database application developers.

The purpose of this document is to propose a simple and consistent naming mechanism for all the objects in a database schema.  The naming convention is aimed at reducing the dependence of the application developers on the database administrator by naming objects in a way that unambiguously defines their contents.  Where applicable, there is also a mention of how not to name the object and the reasons for this.

Of course, there can be no one absolute convention that will solve all naming problems and have universal appeal.  The conventions offered in this document are merely one way of naming things that appears to work.  The reader is free to modify these to suit individual project needs.

Since most of the objects of MOSIP is created on their own databases, we will not have any prefix or suffix of the application / module name or abbreviation to the table or object name.

# 1. Common Naming Standards

To name an object within the DB, the following common standards are followed

* Singular Names to the entities
* Object name length to be less than 30 chars
* Lower case object names separated by underscore (_)
* Only defined abbreviations are used
* No prefix or suffix to the table names
* Each table is defined an alias, this alias is used in constraints and index names
