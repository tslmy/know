# Data storage systems

Distinguishing between:

* **Data Lake**: stores data **in its natural/raw format**, usually object blobs or files. 
  * is data structured? No. They are heterogeneous.
  * is data stored selectively? No. All data generated in the company are stored here.
  * used when:
    * you need to store a lot of different types of data cheaply
    * you don't have a plan for what to do with the data yet; you just know that you'll use them down the line
* A **data swamp** is a deteriorated and unmanaged data lake that is either inaccessible to its intended users or is providing little value.
* **Data Warehouse**: stores modeled/structured data
  * is data structured? Yes.
  * is data stored selectively? Yes.
* **Data Mart**: a subsection of the data-warehouse, designed and built specifically for a particular department/business function

references:

* [https://www.holistics.io/blog/data-lake-vs-data-warehouse-vs-data-mart/](https://www.holistics.io/blog/data-lake-vs-data-warehouse-vs-data-mart/)

