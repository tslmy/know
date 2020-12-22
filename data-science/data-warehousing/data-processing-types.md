---
description: 'OLTP, OLAP, ROLAP, MOLAP, HOLAP'
---

# Data processing types

Distinguishing between data processing types in data warehousing :

* **batch processing**: the running of jobs that can run without end user interaction \([source1](https://www.ibm.com/support/knowledgecenter/zosbasics/com.ibm.zos.zconcepts/zconc_whatisbatch.htm), [source2](https://www.google.com/books/edition/Benchmarking_Transaction_and_Analytical/fV0NAAAAQBAJ?hl=en&gbpv=1&bsq=batch%20processing)\). It's a concept in \#DBMS. No user interaction is involved.
* **Online transaction processing** \(OLTP\): A system that facilitate & manage transaction-oriented applications. It's a concept in \#DBMS. User interaction is involved.
* **Online Analytical Processing** \(OLAP\): A system that answers multi-dimensional analytical \(MDA\) queries. It's a concept in business intelligence \(BI\). User interaction is involved.
  * **Relational Online Analytical Processing** \(ROLAP\): OLAP done with RDBMS, with queries computed on-demand.
    * Results for user queries are computed on-demand.
  * **Multidimensional Online Analytical Processing** \(MOLAP\)
    * Results for user queries are pre-computed. Variables in the user query are represented as dimensions of the data.
  * **Hybrid Online Analytical Processing** \(HOLAP\): some data in ROLAP, some in MOLAP.

## \#distinguishing-between OLTP and OLAP

[source](https://en.wikipedia.org/wiki/Online_transaction_processing)

* OLAP has much more complex queries, 
* OLAP may operate in a smaller volume, 
* OLAP is for the purpose of BI or reporting, rather than to process transactions. 
* OLTP systems process all kinds of queries \(read, insert, update and delete\), OLAP is generally optimized for read only \(and might not even support other kinds of queries\).

