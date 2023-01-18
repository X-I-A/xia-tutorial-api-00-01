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
