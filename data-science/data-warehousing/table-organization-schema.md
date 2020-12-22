---
description: 'Star, Snowflake'
---

# Table organization schema

> The star schema and the snowflake schema are ways to organize data marts or entire data warehouses using relational databases. Both of them use dimension tables to describe data aggregated in a fact table.

\([source](https://vertabelo.com/blog/data-warehouse-modeling-star-schema-vs-snowflake-schema/)\)

The key difference is the **normalization of dimension tables**.

* Dimension tables in a **star** schema are not normalized, while
* Dimension tables in a **snowflake** schema are normalized.

  The line "dimension tables are normalized" can also be expressed as "Hierarchies for the dimensions are stored in the dimensional table."

This key difference leads to several **implications**:

* **Shape**. With dimension tables normalized, the sub-dimension tables surround higher-level dimension tables. This leads to the local "stars" in the snowflake schema.
* **Space usage**. Normalization \(by definition\) avoids saving redundant data, thus it saves space. Notice that here the overhead of storing metadata for each table is ignored.
* **Query complexity**. Since separate tables would require multiple joins, queries for a snowflake schema can be complex.

There are lesser-known variants:

* **galaxy schema** \(a.k.a. Fact Constellation Schema\): multiple fact tables sharing several dimension tables. Each fact table and its dimension tables make a star schema.
* **star cluster schema**: hybrid between star and snowflake

## fact table and dimension table

> The fact table contains business facts \(or measures\), and foreign keys which refer to candidate keys \(normally primary keys\) in the dimension tables. Contrary to fact tables, dimension tables contain descriptive attributes \(or fields\) that are typically textual fields \(or discrete numbers that behave like text\).

