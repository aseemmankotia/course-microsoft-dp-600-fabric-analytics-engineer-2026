## Chapter 4: Ingestion Foundations: Dataflows Gen2, Pipelines & OneLake Shortcuts — Practice Questions

**Q1.** A business analyst with no coding experience needs to join two tables, remove duplicate rows, and reshape column headers before loading the result into a Lakehouse table. Which Fabric tool BEST meets this requirement?

A) A Spark notebook using PySpark DataFrame transformations
B) A Dataflow Gen2 using the Power Query Online editor
C) A Data pipeline Copy activity with column mapping
D) A KQL queryset in a Real-Time Intelligence eventhouse

<details>
<summary>Answer</summary>

**Correct: B**

Dataflow Gen2 exposes the full Power Query M editor (low-code, GUI-driven joins, merges, unpivots) and is designed for citizen data engineers who need transformation logic without writing code.

**Why the others are wrong:**
- A notebook requires PySpark/Python coding skills the analyst doesn't have.
- Copy activity moves data as-is (with basic column mapping) but cannot perform joins, dedup, or unpivot logic.
- KQL querysets are for querying eventhouse/KQL database data, not for building reusable ETL transforms into a Lakehouse.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team needs to make 200 GB of Parquet files stored in an external ADLS Gen2 storage account queryable from a Fabric Lakehouse, without duplicating the data or setting up a recurring copy job. What should they configure?

A) A scheduled Data pipeline Copy activity that copies the files nightly
B) A Dataflow Gen2 with Fast Copy enabled to load the files
C) A mirrored database pointing at the ADLS Gen2 account
D) An external OneLake shortcut pointing to the ADLS Gen2 container

<details>
<summary>Answer</summary>

**Correct: D**

An external OneLake shortcut creates a virtual reference to the ADLS Gen2 location. Data stays in place (no duplication, no copy job), and it appears in OneLake as if it were native Lakehouse data.

**Why the others are wrong:**
- A Copy activity physically duplicates the data and requires ongoing schedule maintenance — the requirement explicitly avoids duplication.
- Dataflow Gen2 with Fast Copy still lands data into a destination, duplicating storage rather than referencing it.
- Mirroring is for supported operational databases (e.g., Azure SQL, Snowflake, Cosmos DB), not for generic ADLS Gen2 file storage.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A 500 million-row fact table is refreshed nightly in a Dataflow Gen2, but only the last 3 days of rows actually change. Refreshing the full table each night is causing capacity throttling. What should be configured to fix this?

A) Configure incremental refresh using RangeStart and RangeEnd parameters on a datetime column
B) Enable query folding on the destination step
C) Split the dataflow into multiple smaller Dataflow Gen2 items
D) Switch the destination from Lakehouse to Warehouse

<details>
<summary>Answer</summary>

**Correct: A**

Dataflow Gen2 incremental refresh requires defining RangeStart and RangeEnd parameters (of type Date/DateTime) bound to a filter on the source query, so only the changed date range is reprocessed rather than the full table.

**Why the others are wrong:**
- Query folding pushes transformation logic to the source but doesn't limit which rows are reprocessed each run.
- Splitting the dataflow adds complexity without solving the root cause — reprocessing all historical rows.
- Changing the destination engine doesn't reduce the volume of source data being reprocessed.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A workflow must copy files from an FTP server, wait for the copy to finish, then conditionally run one of two stored procedures depending on row count, and finally send a Teams notification. Which Fabric item is the correct choice for building this workflow?

A) A Dataflow Gen2 with conditional columns
B) A single PySpark notebook cell chain
C) A Data pipeline using Copy, If Condition, and Web/Office 365 Outlook activities
D) A semantic model with calculated tables

<details>
<summary>Answer</summary>

**Correct: C**

Data pipelines are built for orchestration: sequencing activities (Copy, Stored Procedure, If Condition, notification activities) with control flow and dependencies — exactly this multi-step conditional workflow.

**Why the others are wrong:**
- Dataflow Gen2 only performs data transformation logic; it has no concept of conditional branching between stored procedures or sending notifications.
- A notebook could technically script this, but it lacks native connectors/activities for FTP, conditional branching UI, and Teams integration that pipelines provide out of the box.
- Semantic models are for reporting/analytics, not orchestration of ETL steps.

</details>

---

**Q5.** An engineering team needs to apply custom Python machine-learning feature engineering logic across 2 TB of data with full control over partitioning and parallelism. Which tool should they use?

A) A Fabric notebook using PySpark
B) Dataflow Gen2
C) A Data pipeline Copy activity
D) A Power BI paginated report

<details>
<summary>Answer</summary>

**Correct: A**

Notebooks running Spark give full code-level control, custom Python libraries, and explicit control over partitioning/parallelism at scale — capabilities Dataflow Gen2's low-code engine doesn't expose.

**Why the others are wrong:**
- Dataflow Gen2 is low-code Power Query and doesn't support custom Python ML libraries or manual partition control.
- Copy activity only moves data; it has no transformation/feature-engineering capability.
- Paginated reports are a presentation/reporting tool, not a data engineering tool.

</details>

---

**Q6.** Which parameter data type is required when configuring incremental refresh on a Dataflow Gen2 query?

A) Text
B) Date/DateTime
C) Decimal Number
D) Binary

<details>
<summary>Answer</summary>

**Correct: B**

Incremental refresh in Dataflow Gen2 relies on RangeStart and RangeEnd parameters of type Date or DateTime, used to filter the source query to only the changed range.

**Why the others are wrong:**
- Text parameters can't be used for range-based date filtering logic.
- Decimal parameters have no meaning for defining a time-based refresh window.
- Binary parameters are used for file/blob content, not for defining refresh ranges.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A Fabric Data pipeline needs to run automatically every day at 2:00 AM without any manual intervention. Which trigger configuration should be used?

A) A Schedule trigger set to a daily recurrence at 2:00 AM
B) An On-demand run started manually each day
C) An Invoke Pipeline activity nested inside itself
D) A Power BI dataset refresh trigger

<details>
<summary>Answer</summary>

**Correct: A**

A Schedule trigger defined on the pipeline with a daily recurrence at the specified time automates execution without manual action.

**Why the others are wrong:**
- On-demand runs require someone to manually trigger the pipeline — the opposite of automation.
- Invoke Pipeline is used to call another pipeline from within a pipeline's activities, not to schedule execution.
- A Power BI dataset refresh trigger schedules semantic model refreshes, not data pipeline runs.

</details>

---

**Q8.** What is the key architectural difference between an internal OneLake shortcut and an external OneLake shortcut?

A) Internal shortcuts reference another location within OneLake (e.g., another workspace's Lakehouse); external shortcuts reference storage outside Fabric such as ADLS Gen2 or S3
B) Internal shortcuts copy data locally while external shortcuts stream data in real time
C) Internal shortcuts only work with Warehouses; external shortcuts only work with Lakehouses
D) Internal shortcuts require Fabric admin approval; external shortcuts do not

<details>
<summary>Answer</summary>

**Correct: A**

Internal shortcuts point to data already inside OneLake (another Lakehouse/Warehouse/workspace); external shortcuts point to data outside Fabric entirely (ADLS Gen2, Amazon S3, S3-compatible, Google Cloud Storage, Dataverse). Neither type copies the underlying data.

**Why the others are wrong:**
- Neither shortcut type copies data or streams it — both are virtual references, that's the whole point of shortcuts.
- Both shortcut types can target either Lakehouses or Warehouses; there's no such restriction.
- Shortcut creation follows workspace permissions, not a special approval workflow distinguishing internal vs external.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

