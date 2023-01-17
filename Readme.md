# X-I-A API Tutorial - 00-01: Descriptive Data Model Design
## Introduction
Descriptive data model describes data without considering how data should be stored.
If we consider the data as a live form, then the main goal of the data model is drawing a precise portrait.
Stability comes automatically with the precision, so a great data model doesn't change often overtime.
This feature make data model high valuable, 
and it is the reason why X-I-A API framework use it as one of the design base.

## Three basic data forms
Descriptive data model grant the data with three basic forms:
* database form: data ready to be saved into database (database irrelevant)
* internal form: data as runtime objects
* display form: data to be presented

A perfect example is datetime object, its tri-forms are:
* database form: float (linux epoch time, each database has different format, but we are not care at data model level)
* internal form: datetime.datetime (in the case of using python)
* display form: a formatted datetime string, such as (2023-01-17 00:00:00)

Whatever form the data is actually on, the data itself doesn't change. 
As is explained in the introduction, three forms could better describe the data, which is the main goal of the design

## Two basic relationship of data
Data and data have relationships and the top 2 most important ones are:
* Part of: data A is part of data B.
* Relation: data A holds the data B's contact information and could get information of data B when needs.

Example of `Part of`: A purchase order will have a few articles. The line item holding each article is part of purchase order

Example of `Relation`: A purchase order has a buyer id field, and we could get the buyer's information by the stored id

## How to better describe the data
Like the real world, there is no absolute correct or wrong for any data design. 
You could also let a line item of a purchase order be as an independent data, 
and by using the purchase number, we could find the purchase order header information by `Relation`.

To get a "better" descriptive data model, we need recall the definition of the word "better":
* A great data model doesn't change often overtime

There are two golden methods to help:

### Referencing the existence:

Each domain should have lead software solution. Nothing is better than analyzing their data model as a start point.

Using SAP, the most successful ERP software, as example, we observe a lot of break changes during the past 30 years.
Such: Analytic tools of data, User interface of data, Communication protocol of data. 
With SAP's recent version S4/Hana, even the table structure has significant evolutions. 
**The only thing remains quite stable is the data model itself.**

For purchase order, the standard API for creating a purchase order is `BAPI_PO_CREATE`, 
which remains almost the same during 30 years. You will see that a purchase order line items is presented as `Part of`.

Attention, purchase order and purchase order line item are stored in two difference tables in SAP, 
but it is due to the limitation of relational database. 


* 


## ORM(Object–relational mapping)
