## Chapter 10: Semantic Model Storage Modes: Direct Lake, Import, DirectQuery — Practice Questions

**Q1.** A semantic model uses Direct Lake mode against a Lakehouse Delta table with 50 million rows. A developer adds a calculated column to the model to concatenate two text fields. After publishing, query performance drops significantly. What is the MOST likely cause?

A) The calculated column forced the model to fall back to DirectQuery for that table
B) The capacity was throttled due to CPU smoothing
C) The Delta table needs to be re-framed before calculated columns work
D) Calculated columns automatically switch the entire workspace to Import mode

<details>
<summary>Answer</summary>

**Correct: A**

Direct Lake does not support calculated columns or calculated tables computed over Direct Lake data; any table containing them falls back to DirectQuery, which is slower because it queries the Lakehouse live instead of reading OneLake columns directly.

**Why the others are wrong:**
- CPU smoothing affects background operations across the capacity, not a specific fallback caused by a modeling feature
- Framing refreshes which OneLake data version is visible; it does not enable calculated column support
- Fallback is scoped to the affected table/model, not the entire workspace, and does not convert the model to Import

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company wants near-instant reflection of new Delta table data in OneLake without a scheduled refresh, while keeping query performance close to in-memory speed for a 2 billion row fact table on an F64 capacity. Which storage mode BEST meets these requirements?

A) Import mode with 48 scheduled refreshes per day
B) DirectQuery mode against the Lakehouse SQL endpoint
C) Direct Lake mode reading the Delta table directly from OneLake
D) Composite model with the fact table set to Dual mode

<details>
<summary>Answer</summary>

**Correct: C**

Direct Lake reads Delta Parquet files directly from OneLake without duplicating data into Vertipaq via import, giving near in-memory query speed while automatically reflecting new data through reframing — no scheduled data copy required.

**Why the others are wrong:**
- Import still requires a refresh cycle, so data isn't instantly current and 2 billion rows is costly to duplicate and refresh
- DirectQuery avoids duplication but incurs live query latency against the source for every request, failing the performance requirement
- Dual mode is for smaller dimension tables in composite models, not appropriate as the primary strategy for a 2 billion row fact table

</details>

---

**Q3.** Users report that dashboards built on a DirectQuery semantic model against an Azure SQL Database are slow during business hours, with report visuals timing out. What is the BEST first step to address this?

A) Switch every table in the model to Direct Lake immediately
B) Increase the DirectQuery Max Intermediate Row Set Count
C) Disable query reduction options in Power BI Desktop
D) Add aggregation tables in Import mode over the DirectQuery detail tables to answer common queries from cache

<details>
<summary>Answer</summary>

**Correct: D**

Aggregation tables let Power BI answer high-level queries from an in-memory cache while falling back to DirectQuery detail tables only when needed, reducing load on the source and improving perceived latency — the standard pattern for DirectQuery performance issues.

**Why the others are wrong:**
- Direct Lake only applies to Delta tables in OneLake/Lakehouse, not arbitrary Azure SQL Database sources
- Raising the row set limit increases data returned per query, which can worsen latency, not fix it
- Disabling query reduction options increases the number and size of queries sent to the source, worsening the problem

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A model needs a small, frequently changing currency exchange rate table to always show live values from a source system, while the large sales fact table should be Direct Lake for performance. Which modeling approach fits this requirement?

A) Use a composite model with the exchange rate table in DirectQuery and the fact table in Direct Lake
B) Set the entire model to DirectQuery so all tables stay live
C) Import both tables and schedule refresh every 15 minutes
D) Use Dual storage mode for the sales fact table only

<details>
<summary>Answer</summary>

**Correct: A**

Composite models allow mixing storage modes per table, so the volatile small dimension can remain DirectQuery for freshness while the large fact table uses Direct Lake for performance — this is the documented use case for composite/hybrid models.

**Why the others are wrong:**
- Forcing the whole model to DirectQuery sacrifices Direct Lake's performance benefit on the large fact table
- Scheduled refresh every 15 minutes still introduces staleness and does not meet a 'live values' requirement
- Dual mode is typically applied to shared dimension tables, not the large fact table, and doesn't address the currency table's freshness need

</details>

---

**Q5.** Which of the following will trigger a Direct Lake table to fall back to DirectQuery?

A) The table is stored as Delta format with V-Order applied
B) A DAX measure references a calculated table built on top of the Direct Lake table
C) The workspace is assigned to an F64 or higher Fabric capacity
D) The table has fewer than 100 row groups

<details>
<summary>Answer</summary>

**Correct: B**

Calculated tables are not supported in Direct Lake; any dependency on one forces fallback to DirectQuery for the affected query.

**Why the others are wrong:**
- V-Order optimized Delta format is the recommended, supported configuration for Direct Lake, not a fallback trigger
- Sufficient Fabric capacity is a prerequisite for Direct Lake, not a fallback cause
- A low row group count is well within guardrails and does not cause fallback

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator wants a Direct Lake semantic model to return an error to users rather than silently falling back to DirectQuery when guardrails are exceeded. Which setting should be configured?

A) Set the Direct Lake behavior property to DirectLakeOnly
B) Set the Direct Lake behavior property to DirectQuery
C) Disable scheduled refresh on the dataset
D) Set the Max Intermediate Row Set Count to 0

<details>
<summary>Answer</summary>

**Correct: A**

The DirectLakeOnly setting disables fallback entirely — queries that would normally fall back instead return an error, which is useful for diagnosing why fallback conditions are being hit.

**Why the others are wrong:**
- Setting the property to DirectQuery forces the model to always use DirectQuery, the opposite of the requirement
- Disabling scheduled refresh affects data freshness/framing, not fallback error behavior
- Setting the row set count to 0 is not a valid or relevant configuration for controlling fallback behavior

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A Pro workspace dataset in Import mode needs data refreshed more than 8 times per day. What is the correct way to achieve this?

A) Enable incremental refresh, which removes all refresh count limits regardless of capacity
B) Move the workspace to a Premium or Fabric capacity, which allows up to 48 scheduled refreshes per day
C) Switch the model to DirectQuery temporarily during business hours
D) Increase the dataset's Max Parallelism setting in the workspace

<details>
<summary>Answer</summary>

**Correct: B**

Pro/shared capacity workspaces are limited to 8 scheduled refreshes per day; Premium or Fabric capacity raises this limit to 48 scheduled refreshes per day.

**Why the others are wrong:**
- Incremental refresh reduces refresh duration and load but does not remove the platform's scheduled refresh count limit on Pro capacity
- Switching to DirectQuery changes the storage mode entirely and is not a refresh-frequency fix
- Max Parallelism controls concurrent partition processing during a refresh, not how many refreshes per day are allowed

</details>

---

**Q8.** Which statement correctly differentiates Direct Lake from Import mode?

A) Direct Lake reads Delta Parquet files directly from OneLake without a data copy, while Import loads and compresses a full copy into the Vertipaq in-memory cache
B) Direct Lake duplicates data into Vertipaq at refresh time, exactly like Import
C) Direct Lake always requires a live connection to the source query engine for every query, like DirectQuery
D) Import mode reads data directly from OneLake at query time without caching

<details>
<summary>Answer</summary>

**Correct: A**

Direct Lake loads column data on demand straight from OneLake Delta Parquet files into memory without a separate import/refresh copy step, whereas Import performs a full extract-transform-load into the Vertipaq columnar cache on a schedule.

**Why the others are wrong:**
- Import, not Direct Lake, performs the explicit copy-and-compress-at-refresh-time operation
- This describes DirectQuery's live-query behavior, not Direct Lake's OneLake-native read model
- Import caches data in Vertipaq; it does not query OneLake live at report run time

</details>

---

