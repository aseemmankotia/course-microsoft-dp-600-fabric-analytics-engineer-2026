## Chapter 5: Lakehouse vs Warehouse: Choosing the Right Storage Item — Practice Questions

**Q1.** A BI team writes nightly ETL using complex T-SQL stored procedures with multi-table INSERT, UPDATE, and MERGE statements wrapped in transactions. Which Fabric item should host this workload?

A) Lakehouse Files section
B) Warehouse
C) Lakehouse SQL analytics endpoint
D) KQL Database

<details>
<summary>Answer</summary>

**Correct: B**

Warehouse is a full T-SQL DDL/DML relational engine supporting stored procedures, multi-table transactions, and writes.

**Why the others are wrong:**
- Files are not directly queryable with T-SQL DML.
- The SQL analytics endpoint over a lakehouse is read-only — no INSERT/UPDATE/MERGE.
- KQL Database is built for log/telemetry analytics, not relational ETL with stored procedures.

</details>

---

**Q2.** A data engineering team needs to process 500GB of semi-structured JSON logs with PySpark notebooks, apply ML libraries, then expose curated tables for BI. Which Fabric item best fits this workload?

A) Warehouse
B) Dataflow Gen2 alone
C) SQL analytics endpoint only
D) Lakehouse

<details>
<summary>Answer</summary>

**Correct: D**

Lakehouse provides a Files area for unstructured/semi-structured data plus Spark compute for notebooks and ML, with Tables exposed for BI.

**Why the others are wrong:**
- Warehouse has no native Spark/notebook engine for processing raw JSON or running ML libraries.
- Dataflow Gen2 alone lacks the Spark notebook environment needed for custom ML processing.
- The SQL analytics endpoint only reads existing Delta Tables — it cannot process raw Files or run Spark jobs.

</details>

---

**Q3.** An analyst runs an UPDATE statement against a table through a lakehouse's SQL analytics endpoint and receives an error. What is the root cause?

A) The table is not in Delta format
B) The user lacks Contributor role on the workspace
C) The SQL analytics endpoint is read-only
D) A OneLake shortcut to the table is broken

<details>
<summary>Answer</summary>

**Correct: C**

The SQL analytics endpoint auto-generated over a lakehouse only supports read (SELECT) queries; writes are rejected regardless of permissions.

**Why the others are wrong:**
- Lakehouse Tables are always Delta format, so this isn't the cause.
- Permission level doesn't matter here — even an Admin cannot write through this endpoint.
- A broken shortcut would cause a data-not-found error, not an UPDATE rejection.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which storage layer underlies both Lakehouse and Warehouse items in Microsoft Fabric, enabling cross-engine querying without duplicating data?

A) Azure Data Lake Storage Gen2 mounted per workspace
B) Azure Synapse dedicated SQL pool storage
C) Azure Blob Storage hot tier
D) OneLake

<details>
<summary>Answer</summary>

**Correct: D**

OneLake is Fabric's single, tenant-wide storage layer that every item (Lakehouse, Warehouse, KQL DB, etc.) writes to and reads from, in Delta Parquet, with one physical copy of data.

**Why the others are wrong:**
- ADLS Gen2 is not manually mounted per workspace in Fabric — OneLake is the abstraction layer, not raw ADLS.
- Synapse dedicated SQL pool storage is a legacy Azure Synapse concept, unrelated to Fabric's Warehouse.
- Blob Storage hot tier is a generic Azure storage tier, not the Fabric-specific unified layer.

</details>

---

**Q5.** Which table format do Warehouse tables and Lakehouse managed Tables both use natively for storage?

A) Avro
B) Delta Parquet
C) ORC
D) CSV

<details>
<summary>Answer</summary>

**Correct: B**

Both item types store their managed/Tables data as Delta Lake tables on Parquet files, which is what allows both engines to read the same underlying data.

**Why the others are wrong:**
- Avro is a row-based serialization format not used as the native table format in Fabric.
- ORC is a Hive/Hadoop columnar format, not the format Fabric standardizes on.
- CSV is a raw file format used in the Files area, not the managed Tables format.

</details>

---

**Q6.** You created a lakehouse and loaded a folder of CSV files into the Files section. Which additional step is required before this data becomes queryable via the auto-generated SQL analytics endpoint?

A) Nothing — Files are automatically queryable
B) Manually create a OneLake shortcut to itself
C) Load the data into the Tables section as a Delta table
D) Convert the lakehouse into a warehouse

<details>
<summary>Answer</summary>

**Correct: C**

The SQL analytics endpoint only exposes the Tables (Delta) area of a lakehouse. Raw Files must be loaded/converted into Tables (e.g., via 'Load to Tables' or a Spark write) to become queryable via T-SQL.

**Why the others are wrong:**
- Files remain invisible to the SQL analytics endpoint until converted to Delta Tables.
- A self-referencing shortcut is unnecessary and doesn't expose Files as SQL-queryable tables.
- Converting the item type is not required and would discard the lakehouse's Spark/Files capabilities.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which mechanism lets a single T-SQL query in the Warehouse read data from tables located in a Lakehouse within the same workspace?

A) Requires an ADF pipeline copy first
B) It is not possible in Fabric
C) Cross-database (cross-item) queries using three-part naming
D) Only Spark notebooks can join across items

<details>
<summary>Answer</summary>

**Correct: C**

Fabric supports cross-item/cross-database T-SQL queries, referencing the lakehouse's tables using three-part naming (e.g., LakehouseName.dbo.TableName), because both sit on Delta/OneLake.

**Why the others are wrong:**
- No pipeline copy is needed since both items share the same underlying Delta/OneLake storage.
- Cross-item querying is explicitly supported and heavily tested — this option is factually wrong.
- T-SQL cross-database queries work directly; Spark notebooks are not the only way to join lakehouse and warehouse data.

</details>

---

**Q8.** What is the primary architectural distinction between a lakehouse's SQL analytics endpoint and a warehouse's T-SQL endpoint?

A) The SQL analytics endpoint supports writes while the warehouse endpoint is read-only
B) They are identical, differing only in naming
C) The SQL analytics endpoint only works with Spark, and the warehouse endpoint only works with Power BI
D) The SQL analytics endpoint is auto-generated and read-only over Delta tables, while the warehouse endpoint is a full read-write T-SQL engine

<details>
<summary>Answer</summary>

**Correct: D**

This is the core exam distinction: lakehouse's SQL analytics endpoint is auto-created, read-only, over the Delta Tables area; the warehouse endpoint is a full-featured, read-write T-SQL relational engine.

**Why the others are wrong:**
- This reverses the actual read/write capabilities of the two endpoints.
- They differ fundamentally in capability, not just naming.
- Both endpoints are T-SQL based and both can be queried by Power BI; Spark is unrelated to either endpoint directly.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

