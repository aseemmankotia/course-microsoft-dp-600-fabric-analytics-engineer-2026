## Chapter 5: Lakehouse vs Warehouse: Choosing the Right Storage Item — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Can you run INSERT/UPDATE/DELETE against a Lakehouse via its SQL analytics endpoint? | No — the SQL analytics endpoint is read-only. Writes must go through Spark, notebooks, or Dataflows. Exam tip: pick Warehouse if the team needs T-SQL DML. |
| 2 | What storage format do Lakehouse Tables and Warehouse tables both use under the hood? | Delta Parquet. Exam tip: this is why cross-item Delta-based querying and OneLake integration work seamlessly. |
| 3 | Which Fabric item auto-generates a read-only SQL endpoint the moment you create it? | Lakehouse — the SQL analytics endpoint is created automatically over the Tables/Delta area. Exam tip: no endpoint is auto-created for raw Files, only for Tables. |
| 4 | Choose Lakehouse or Warehouse: SQL-first BI team needing stored procedures and multi-table transactions? | Warehouse — full T-SQL DDL/DML engine with stored procs and transactions. Exam tip: Warehouse = relational engine; Lakehouse = Spark-first. |
| 5 | What is OneLake in Microsoft Fabric? | The single, unified, tenant-wide storage layer beneath every Fabric item (Lakehouse, Warehouse, KQL DB, etc.), storing data once in Delta Parquet. Exam tip: enables cross-item querying with no data duplication ('OneCopy'). |
| 6 | Lakehouse structure: name its two top-level sections. | Files (any format, unmanaged) and Tables (managed, Delta format). Exam tip: only Tables are exposed through the SQL analytics endpoint. |
| 7 | How can a Warehouse query data stored in a Lakehouse in the same workspace? | Cross-database (cross-item) T-SQL queries using three-part naming (Lakehouse.Schema.Table). Exam tip: works because both sit on Delta/OneLake. |
| 8 | Which item type would a data engineer choose to run PySpark notebooks against unstructured JSON/image data? | Lakehouse — provides Spark compute and a Files area for raw/unstructured data. Exam tip: Warehouse has no native Spark/notebook support. |
| 9 | True or False: The Warehouse T-SQL endpoint is read-only like the Lakehouse SQL analytics endpoint. | False. Warehouse endpoint supports full read-write DDL/DML. Exam tip: this is the #1 tested distinction between the two endpoints. |
| 10 | What must happen to a CSV file loaded into a Lakehouse's Files section before it's queryable via the SQL analytics endpoint? | It must be loaded/converted into the Tables section as a Delta table (e.g., via 'Load to Tables' or Spark). Exam tip: raw Files are invisible to the SQL analytics endpoint. |
| 11 | Which underlying table format enables both Lakehouse and Warehouse to be queried by the same SQL engine layer? | Delta Lake (Delta Parquet) format. Exam tip: Fabric's SQL engine reads Delta transaction logs regardless of item type. |
| 12 | Warehouse vs Lakehouse: which supports native multi-statement ACID transactions across multiple tables via T-SQL? | Warehouse. Exam tip: Lakehouse Spark supports Delta ACID at table level, but multi-table T-SQL transactions require Warehouse. |
