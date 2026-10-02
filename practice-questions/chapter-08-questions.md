## Chapter 8: Real-Time Intelligence: KQL for Streaming Data — Practice Questions

**Q1.** A retail company ingests point-of-sale transaction events continuously and needs a dashboard that operations staff monitor for fraud spikes, refreshing every few seconds. Which Fabric solution BEST meets this requirement?

A) Load events hourly via a Data pipeline into a Warehouse, build a Power BI DirectQuery report
B) Ingest via Dataflow Gen2 into a Lakehouse table and schedule a 5-minute refresh Power BI import dataset
C) Ingest via Eventstream into a KQL database (Eventhouse) and build a Real-Time dashboard
D) Use a Notebook with a scheduled Spark job every minute to append to a Delta table, then build a Power BI report

<details>
<summary>Answer</summary>

**Correct: C**

Eventstream to a KQL database is purpose-built for continuous, low-latency event ingestion, and Real-Time dashboards query the KQL database live for near-instant refresh.

**Why the others are wrong:**
- Hourly batch loading and DirectQuery on a Warehouse cannot meet a seconds-level latency requirement.
- Import mode requires scheduled refresh and is not truly real-time, and refresh frequency is capacity-limited.
- A per-minute scheduled Spark job is still batch-based polling, adding latency versus native streaming ingestion.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Which Fabric item is the primary entry point for ingesting data from Azure Event Hubs, IoT Hub, or Kafka into a KQL database without writing custom ingestion code?

A) Data pipeline
B) Dataflow Gen2
C) Eventstream
D) Real-Time hub

<details>
<summary>Answer</summary>

**Correct: C**

Eventstream is the no-code streaming ingestion engine that connects sources like Event Hubs, IoT Hub, and Kafka to destinations such as a KQL database.

**Why the others are wrong:**
- Data pipelines orchestrate scheduled/batch copy and control-flow activities, not continuous stream processing.
- Dataflow Gen2 performs Power Query-based batch/incremental transforms, not streaming ingestion.
- Real-Time hub is a discovery and catalog surface for streaming sources, not an ingestion engine itself.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Which KQL operator combines rows into aggregated groups, such as computing an average value per device?

A) project
B) extend
C) summarize
D) where

<details>
<summary>Answer</summary>

**Correct: C**

summarize performs aggregation, grouping rows by specified columns and computing aggregate functions.

**Why the others are wrong:**
- project selects or renames columns without any aggregation.
- extend adds a per-row calculated column without grouping rows.
- where filters rows based on a condition; it does not aggregate.

</details>

---

**Q4.** You need to filter a KQL table to only rows from the last 1 hour before further processing. Which clause do you use immediately after the table name?

A) | extend Recent = ago(1h)
B) | summarize count() by bin(Timestamp,1h)
C) | project Timestamp, ago(1h)
D) | where Timestamp > ago(1h)

<details>
<summary>Answer</summary>

**Correct: D**

where with the ago() function filters rows to a relative time window, here restricting results to the past hour.

**Why the others are wrong:**
- extend creates a new column value but does not remove rows outside the time window.
- summarize aggregates counts per time bin but does not itself restrict the query to the last hour.
- project only returns a column value; it does not filter rows.

</details>

---

**Q5.** Which statement BEST describes the difference between a Fabric Real-Time dashboard and a Power BI report built on the same KQL database?

A) Real-Time dashboards support DAX measures while Power BI reports only support KQL
B) Power BI reports can only visualize batch data, never streaming data
C) Real-Time dashboards are built directly from KQL queries with near-instant auto-refresh, while Power BI reports typically use DirectQuery/Import and are better suited for polished, scheduled business reporting
D) Real-Time dashboards can only display a single tile per dashboard

<details>
<summary>Answer</summary>

**Correct: C**

Real-Time dashboards are native, KQL-query-driven surfaces optimized for near-instant refresh, while Power BI reports offer richer formatting and business-oriented reporting typically on a slightly less immediate refresh cadence.

**Why the others are wrong:**
- This reverses the languages: Real-Time dashboards use KQL, while Power BI reports can leverage DAX over a semantic model.
- Power BI reports can connect via DirectQuery to a KQL database and reflect near-real-time data; it is not limited to batch only.
- Real-Time dashboards support multiple tiles, not just one.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A data engineer wants a single place to browse and connect to all streaming data sources available across the organization's Fabric tenant, including sample data and Azure Event Hubs feeds. Which Fabric feature should they use?

A) OneLake catalog
B) Eventhouse
C) Real-Time hub
D) Data pipeline gallery

<details>
<summary>Answer</summary>

**Correct: C**

Real-Time hub is the centralized catalog specifically for discovering and connecting to streaming data sources across the tenant.

**Why the others are wrong:**
- OneLake catalog focuses on broader item and data asset discovery, not streaming source management specifically.
- Eventhouse is the container that hosts KQL databases; it does not discover external streaming sources.
- There is no dedicated 'data pipeline gallery' feature for discovering streaming sources.

</details>

---

**Q7.** A team ingests sensor telemetry into a KQL database for real-time alerting, but a separate data science team also needs to join this data with historical Lakehouse tables in a Spark notebook, without duplicating data via a nightly export. What should they do?

A) Export the KQL table to CSV daily into the Lakehouse Files section
B) Rebuild the entire pipeline using a Lakehouse instead of a KQL database
C) Use Dataflow Gen2 to copy the KQL table into the Lakehouse every 15 minutes
D) Enable OneLake availability on the KQL table so it is mirrored to OneLake in Delta format and accessible as a shortcut

<details>
<summary>Answer</summary>

**Correct: D**

OneLake availability automatically mirrors KQL database tables into OneLake in Delta Parquet format, letting Spark notebooks and Lakehouses access the data via a shortcut without duplicating or re-engineering the pipeline.

**Why the others are wrong:**
- Manual daily CSV export adds latency, duplication, and manual maintenance overhead.
- Rebuilding on a Lakehouse abandons the low-latency real-time alerting capability the original team relies on.
- A scheduled Dataflow Gen2 copy is redundant batch duplication when native OneLake availability already solves this.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** An organization currently uses a Lakehouse with hourly batch pipelines for reporting. Leadership now wants operational dashboards that reflect events within seconds of occurring, sourced from a continuous Kafka stream. What is the minimal architecture change needed?

A) Increase the pipeline schedule frequency to every minute
B) Add an Eventstream to ingest the Kafka topic into a KQL database (Eventhouse) and build a Real-Time dashboard on top
C) Convert the Lakehouse to a Warehouse for faster queries
D) Add more capacity units to the existing batch pipeline

<details>
<summary>Answer</summary>

**Correct: B**

Introducing Eventstream and a KQL database provides native streaming ingestion and low-latency querying suited to a seconds-level requirement, paired with a Real-Time dashboard for live monitoring.

**Why the others are wrong:**
- Even minute-level batch scheduling still introduces latency and does not scale to true streaming requirements.
- Converting to a Warehouse does not address the fundamental need for streaming ingestion.
- Adding capacity does not change the batch nature of the existing pipeline; it only runs the same batch faster/more often at cost.

</details>

---

