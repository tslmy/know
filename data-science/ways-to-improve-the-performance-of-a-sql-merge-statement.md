# Ways to improve the performance of a SQL MERGE statement

Suppose the MERGE statement is in the form of:

```text
MERGE target AS TARGET  
USING source AS SOURCE   
ON condition
WHEN MATCHED THEN UPDATE                       
WHEN NOT MATCHED BY TARGET THEN INSERT                        
WHEN NOT MATCHED BY SOURCE THEN DELETE;
```

Ways to improve the performance:

1. **Create indexes**: Ensure that the columns referenced in the `condition` are properly indexed.
2. **Separate filtering from matching**: Ensure that the `condition` only compares columns across the two tables \(e.g., `target.user_id=source.u_id`\), not a column with a constant \(e.g., `source.account_status='ACTIVE'). For comparisons between columns and constants, use the`WHEN\` clause.
3. **Use** [**query hints**](https://logicalread.com/mysql-query-hints-improve-performance-mc12/): For certain SQL engines, specify query hints may help. For example, when we are confident some index `idx1` will have few hits compared to some other index, we can hint the engine to `IGNORE INDEX (idx1)`.
4. **Read the Query Plan**: We may find out more ways to enhance the performance by reading the Query Plan. For example, the join order of tables or type of loop may not be ideal for the use case. They can be tweaked by adding other query hints to our statement.

References:

* For SQL Server: [https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/cc879317\(v=sql.105\)?redirectedfrom=MSDN](https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/cc879317%28v=sql.105%29?redirectedfrom=MSDN)

