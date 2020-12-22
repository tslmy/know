# Data ingestion pipeline types

distringuishing between ETL, ELT:

* Extract, Transform, and Load \(ETL\)
  * data flow: **source** -Extract-&gt; **staging** -Load-&gt; **data warehouse** 
    * only the "data warehouse" part is considered "**our own system**"
    * staging area can be implemented with a **temporary storage** \(i.e., it should be often cleaned to make space for newer data\).
  * **Transformation** happens in the staging area. Advantages:
    * staging area can be implemented with a **fast storage** \(think: staging area is on SSD, while the data warehouse is on HDD\), thus the transformation can be fast.
    * **policy-compliance** type of cleaning can happen in the staging area. Since no data is yet commited to a permanent storage \(i.e., the data warehouse\), we are compliant.
* Extract, Load, and Transform \(ELT\): 
  * data flow: **source** -Extract--Load-&gt; **data lake** -Transform-&gt; **data warehouse**
    * both the "data lake" and the "data warehouse" is considered "**our own system**". In other words, data is considered "saved" once it enters the lake, even before reaching the warehouse.
    * data lake is a **permanent storage** \(i.e., it's not expected to be cleaned regularly\).
  * **Transformation** happens in the lake-to-warehouse process.

What do they refer to?

* **Extract**: Extraction refers to pulling the source data from the original database or data source. 
  * With ETL, the data goes into a temporary staging area. 
  * With ELT, it goes immediately into a data lake storage system.
* **Transform**: Transformation refers to the process of changing the structure of the information, so it integrates with the target data system and the rest of the data in that system.
* **Load**: Loading refers to the process of depositing the information into a data storage system.

  \([source](https://www.xplenty.com/blog/etl-vs-elt/)\)

