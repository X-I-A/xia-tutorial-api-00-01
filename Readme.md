# X-I-A API Tutorial - 00-01: Descriptive Data Model Design
## Introduction
Descriptive data model describes data without considering how data should be stored.
If we consider the data as a live form, then the main goal of the data model is drawing a precise portrait.
Stability comes automatically with the precision, so a great data model doesn't change often overtime.

The descriptive data model also separates the business logic (application) and technical logic (backend).

## Poly-backend support
There is no perfect database which could handle any task. Even it exists, it will be very expensive. 

When every database share the same data model, it is possible to build a poly-backend. Here are the common use cases:

### OLAP + OLTP hybrid data engine
Using OLTP optimized database to ingest data and keep OLAP updated. 

The transactional application will use OLTP database while analytical application will use OLAP database.

Example: Firestore as OLTP and Bigquery as OLAP

### OLTP + OLTP migration data engine
It is simple to move from old OLTP backed to new OLTP backend by using migration engine.

During the migration, each read operation results in write operation on the new backend if the data doesn't exist yet.

Combining with batch export / import, the data migration is transparent for end users.

### OLAP + OLAP Multiple Analytic Engine
Different OLAP database has different capacities. 
For the reason of performance or cost, an analytical request might be better to be handled by one than the other.
So a multiple OLAP analytic Engine will help.

Example: SAP HANA + Bigquery


## Descriptive Data Model

### Data relationship

Only two relationship are defined

#### Part of

Data A is part of data B.
* Data field is part of a document
* Data field is part of an embedded document
* An embedded document is part of a document
* An embedded document is part of another embedded document

#### Relation

Data A has relation with Data B. The relationship must be self-contained in Data A.

Self-contained means:
* Data A must store some information in itself to find Data B.

Example:
* A purchase order has a client ID. With the ID Number, it is possible to retrieve client information if needed.


### Data Forms

Data doesn't change but the form could be different. The data form describes better the data itself.

#### Three basic data forms

Descriptive data model grant the data with three basic forms:
* database form: data ready to be saved into database (database irrelevant)
* internal form: data as runtime objects
* display form: data to be presented

A perfect example is datetime object, its tri-forms are:
* database form: float (linux epoch time)
* internal form: datetime.datetime (in the case of using python)
* display form: a formatted datetime string, such as (2023-01-17 00:00:00)

#### Two complex data forms
We don't need all data all the time. 
Using purchase order with client ID as example, we don't need the client information unless explicitly requested. 
So we keep the least information at internal form and display form (it is called "lazy mode"). 
When needed, the following form switch will occur to provide the detail value of data.
* internal form to runtime form 
* display form to detail form


