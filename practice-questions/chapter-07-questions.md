## Chapter 7: T-SQL and the SQL Analytics Endpoint — Practice Questions

**Q1.** A data engineer writes a Spark notebook that appends new rows to a lakehouse Delta table every 5 minutes. Analysts querying the SQL analytics endpoint report seeing stale data immediately after the notebook run completes. Which action addresses this most directly?

A) Convert the lakehouse table to a Warehouse table
B) Rebuild the Direct Lake semantic model
C) Manually refresh the SQL analytics endpoint metadata or wait for the automatic sync
D) Grant the db_datareader role to the analysts

<details>
<summary>Answer</summary>

**Correct: C**

SQL analytics endpoint metadata sync lags behind Delta writes; a manual refresh (or waiting for auto-sync) forces the endpoint to reflect the new files.

**Why the others are wrong:**
- Converting the item removes lakehouse capabilities and is disruptive, not the direct fix for a sync delay
- Semantic model refresh is a separate Power BI concern, unrelated to the SQL endpoint's own metadata cache
- Permissions have no effect on data freshness/staleness

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** You must implement a multi-step process that inserts, updates, and deletes rows across three related tables as a single parameterized, schedulable unit written in T-SQL. Where should this logic live?

A) A view on the SQL analytics endpoint
B) A stored procedure in a Fabric Warehouse
C) A Power BI calculated table
D) A Dataflow Gen2 in the lakehouse

<details>
<summary>Answer</summary>

**Correct: B**

Warehouse is the only Fabric item supporting stored procedures, full DML, and transaction control needed for encapsulated multi-table transformations.

**Why the others are wrong:**
- Views are read-only definitions and cannot contain DML or procedural logic
- Calculated tables live inside the semantic model and cannot perform warehouse-side DML
- Dataflow Gen2 is a low-code ETL tool, not a T-SQL procedural object

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A report developer joins a lakehouse table with a warehouse table in the same Fabric workspace using three-part naming in a single T-SQL query. Which statement about this is correct?

A) It requires both items to reside in the same workspace and be exposed via SQL endpoints
B) It requires configuring an on-premises data gateway
C) It only works if both items are lakehouses
D) It requires the warehouse table to first be mirrored into the lakehouse

<details>
<summary>Answer</summary>

**Correct: A**

Cross-item T-SQL querying works across lakehouses and warehouses within the same workspace because both are exposed through SQL endpoints backed by OneLake.

**Why the others are wrong:**
- Gateways apply to on-premises data sources, not to native Fabric items in the same workspace
- Cross-item queries work between a lakehouse and a warehouse, not only lakehouse-to-lakehouse
- No mirroring step is required; both items are natively queryable via three-part names

</details>

---

**Q4.** You need to create reusable filtered and aggregated logic on top of lakehouse tables that multiple Power BI reports will query directly through the SQL analytics endpoint. Which object should you create?

A) A stored procedure
B) A view
C) A Spark temporary view
D) A Dataflow Gen2

<details>
<summary>Answer</summary>

**Correct: B**

Views are supported on the SQL analytics endpoint and provide reusable, queryable logic for downstream BI tools.

**Why the others are wrong:**
- Stored procedures are not supported on the SQL analytics endpoint, only on Warehouse
- Spark temp views are session-scoped and invisible to SQL/BI clients
- Dataflow Gen2 is an ETL construct, not a queryable T-SQL object exposed to reports

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which Fabric item's SQL surface supports CREATE PROCEDURE along with full INSERT, UPDATE, and DELETE statements?

A) Warehouse
B) Lakehouse SQL analytics endpoint
C) KQL database
D) Semantic model

<details>
<summary>Answer</summary>

**Correct: A**

Warehouse is the only Fabric item offering a full read-write T-SQL surface, including stored procedures and transactions.

**Why the others are wrong:**
- The SQL analytics endpoint is read-only with no DML or stored procedure support
- KQL databases use Kusto Query Language for writes, not T-SQL DML
- Semantic models don't execute DML statements at all

</details>

---

**Q6.** A complex T-SQL query against a 500-million-row Warehouse fact table performs poorly, and the execution plan shows inaccurate cardinality estimates. What should you check first?

A) Whether statistics exist and are current on the join/filter columns
B) Whether the table has a manually rebuilt clustered columnstore index
C) Whether Direct Lake mode is enabled for the report
D) Whether the workspace capacity SKU is F64 or higher

<details>
<summary>Answer</summary>

**Correct: A**

The query optimizer relies on column statistics for cardinality estimates; after large loads, stale or missing statistics are the most direct cause of poor plans.

**Why the others are wrong:**
- Warehouse tables use Delta/Parquet storage; there's no traditional clustered columnstore index to manually rebuild
- Direct Lake is a Power BI storage mode concept unrelated to Warehouse T-SQL execution plans
- Capacity SKU affects overall throughput but doesn't directly fix a cardinality estimation problem

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which T-SQL construct should replace a self-join used to calculate a running total per customer, to improve both readability and performance?

A) A window function such as SUM(amount) OVER (PARTITION BY customer_id ORDER BY order_date)
B) A CTE combined with UNION ALL
C) A correlated subquery placed in the SELECT list
D) A recursive CTE

<details>
<summary>Answer</summary>

**Correct: A**

Window functions compute running totals in a single pass without needing a self-join, directly improving performance and readability.

**Why the others are wrong:**
- UNION ALL with a CTE doesn't address a running total calculation
- Correlated subqueries typically evaluate row-by-row and are slower than window functions
- Recursive CTEs are unnecessary overhead for a simple running total

</details>

---

**Q8.** What is the primary architectural difference between a Fabric lakehouse's SQL analytics endpoint and a Fabric Warehouse?

A) The SQL analytics endpoint provides read-only, auto-generated T-SQL access over Delta tables, while Warehouse supports full read-write T-SQL DML
B) The SQL analytics endpoint stores data in a proprietary format while Warehouse uses Delta Parquet
C) The SQL analytics endpoint supports stored procedures while Warehouse does not
D) The SQL analytics endpoint is only accessible from Power BI, while Warehouse is only accessible from T-SQL clients

<details>
<summary>Answer</summary>

**Correct: A**

This is the core architectural distinction tested throughout this domain: read-only auto-exposed endpoint vs. full read-write engine.

**Why the others are wrong:**
- Both ultimately persist data as Delta Parquet in OneLake
- This is reversed — stored procedures exist only in Warehouse, not the SQL analytics endpoint
- Both items are accessible from standard T-SQL clients (e.g., SSMS) as well as Power BI

</details>

---

