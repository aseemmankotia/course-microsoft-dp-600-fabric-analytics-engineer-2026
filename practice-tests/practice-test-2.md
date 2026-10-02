# Practice Test 2: DP-600 Microsoft Fabric Analytics Engineer Exam Prep

- **Questions:** 44
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A Fabric workspace contains a lakehouse used by multiple departments. The Finance team must be able to read only the files under Files/finance-reports/ in the lakehouse, but must not see any other folders, tables, or workspace items. The workspace already has other users with Viewer and Contributor roles. Which approach BEST meets this requirement?

A) Add the Finance security group to the workspace with the Viewer role
B) Create a OneLake data access role scoped to the Files/finance-reports/ folder and assign the Finance security group to it
C) Grant the Finance security group Read item permission on the lakehouse
D) Configure row-level security on the SQL analytics endpoint for the lakehouse

---

**Q2.** Two developers work on the same Fabric workspace connected to a Git branch. Developer A modifies a report in the workspace and commits it to Git. Meanwhile, Developer B pulls the branch, edits the same report definition file directly in Git, and pushes a change. When the workspace attempts to sync 'Update from Git,' a conflict is detected on that report item. Which statement correctly describes how Fabric resolves this conflict?

A) Fabric automatically performs an object-level merge, combining both sets of changes into the report
B) The change committed most recently by timestamp always overwrites the other automatically
C) You must choose to keep either the entire workspace version or the entire Git version of the conflicting item; there is no automatic field-level merge
D) Fabric blocks all further commits to the branch until the conflict is resolved through a pull request in the Git provider

---

**Q3.** A Fabric Warehouse table stores customer credit card numbers in a column named CardNumber, formatted as 16 digits. Compliance requires that most users see only the last four digits (e.g., XXXX-XXXX-XXXX-1234) when querying the table, without altering the underlying stored data. Which masking function should you apply in the dynamic data masking rule?

A) default()
B) email()
C) partial(0,"XXXX-XXXX-XXXX-",4)
D) random(1,9999)

---

**Q4.** An organization uses a Fabric deployment pipeline with Dev, Test, and Production stages. A semantic model in each stage must connect to a warehouse that is unique to that stage (DevWarehouse, TestWarehouse, ProdWarehouse). Currently, after every deployment to Production, an engineer manually edits the semantic model's data source connection to point to ProdWarehouse. Which change eliminates this manual step going forward?

A) Configure a deployment rule on the Production stage that overrides the data source connection value for that semantic model
B) Enable 'Update from Git' after each deployment to reset the connection automatically
C) Assign a workspace identity to the Production workspace so it auto-detects the correct warehouse
D) Move the semantic model to Direct Lake mode so no explicit connection string is required

---

**Q5.** A capacity administrator reviews the Fabric Capacity Metrics app and observes that interactive Power BI report queries are being rejected due to capacity overload, while a scheduled dataflow refresh on the same capacity continues running despite sustained high utilization. Which explains this difference in behavior?

A) Interactive operations are smoothed over a 5-minute window while background operations are smoothed over a 24-hour window, so background jobs tolerate longer bursts before rejection
B) Background operations run on a separate Power BI Premium capacity, isolated from Fabric capacity throttling
C) Background jobs are permanently exempt from all capacity throttling policies
D) The dataflow refresh is consuming capacity units from a different, unrelated workspace

---

**Q6.** A team is building a semantic model in Direct Lake storage mode over a Fabric lakehouse. They define row-level security (RLS) roles with DAX filter expressions directly in the semantic model. A colleague asks whether they must also configure matching OneLake data access roles on the lakehouse tables for the semantic model's RLS to be enforced. What is the correct answer?

A) Yes — Direct Lake bypasses the semantic model's security layer, so OneLake data access roles must replicate the RLS logic exactly
B) Direct Lake does not support row-level security at all, so the model must be switched to Import mode
C) RLS is enforced only when the semantic model is queried through the XMLA endpoint; DAX queries from Power BI reports ignore RLS in Direct Lake mode
D) No — RLS defined in the semantic model is enforced by the Fabric query engine regardless of storage mode; lakehouse-level access controls are independent and do not need to mirror the model's RLS

---

**Q7.** A company stores sales data in a Fabric lakehouse organized into folders by region: /Files/US, /Files/EU, /Files/APAC. A newly acquired subsidiary's analysts need read-only access to only the /Files/APAC folder and its underlying delta tables, without being granted access to the workspace or the other regional folders. Which approach BEST meets this requirement with the least administrative overhead?

A) Add the analysts as Viewer role members of the workspace and rely on folder-level NTFS permissions.
B) Create a OneLake data access role scoped to the /Files/APAC folder and grant the analysts' security group the Read permission on that role.
C) Grant the analysts Contributor role on the workspace but restrict access using a warehouse view.
D) Create a separate lakehouse for APAC data and share it via a deployment pipeline.

---

**Q8.** A hospital's Fabric warehouse stores patient records including full credit card numbers used for billing. Analysts must be able to run aggregate queries (e.g., total billed amount) across the full dataset, but must not be able to view or export full, unmasked credit card numbers. Which security feature should be applied to the credit card column?

A) Row-level security (RLS)
B) Object-level security (OLS)
C) Dynamic data masking
D) Column-level security (CLS)

---

**Q9.** A team uses Fabric deployment pipelines to promote a warehouse from Dev to Test to Prod. The warehouse connection string and a lookup table's source parameter must automatically change to environment-specific values during each deployment, without manual editing after every promotion. What should the team configure?

A) Git integration with separate branches per environment
B) Deployment pipeline rules (deployment rules) for the affected parameters/connections
C) Dataflow Gen2 parameters bound to pipeline variables
D) A tenant-level connection override in the Admin portal

---

**Q10.** An F64 capacity in Fabric frequently experiences background jobs (e.g., dataflow refreshes) that push utilization far beyond 100%, causing throttling that affects interactive Power BI report users. The capacity admin wants background operations to be rejected once a smoothing threshold is exceeded, while still allowing interactive operations to run. Which tenant/capacity setting should the admin configure?

A) Enable autoscale for the capacity
B) Increase the capacity SKU from F64 to F128
C) Configure Surge Protection with the action set to reject background jobs above a defined threshold
D) Enable the "Users can create Fabric items" tenant switch

---

**Q11.** In Fabric lifecycle management, what is the key difference between using Git integration and using deployment pipelines for a workspace?

A) Deployment pipelines version-control source code changes; Git integration promotes content across environments.
B) Git integration tracks and version-controls item changes within a single workspace; deployment pipelines move and promote content between separate Dev/Test/Prod workspaces.
C) Git integration is used only for Power BI reports; deployment pipelines are used only for lakehouses and warehouses.
D) Both features perform identical functions and can be used interchangeably for any lifecycle management task.

---

**Q12.** A user has been assigned the Viewer role on a Fabric workspace containing a lakehouse. The user reports being able to view Power BI reports connected to the lakehouse's default semantic model, but cannot query the underlying tables directly through the SQL analytics endpoint. What is the MOST likely reason?

A) The Viewer role only grants access to consume Power BI content; querying the SQL analytics endpoint requires additional item-level or OneLake data access permissions.
B) The lakehouse has been corrupted and needs to be recreated.
C) SQL analytics endpoints are disabled by default for all workspace roles and must be enabled per-user by a tenant admin.
D) The user's F-SKU capacity does not support SQL endpoint queries for Viewer-role users.

---

**Q13.** A Fabric lakehouse contains a fact table with 800 million rows that must be incrementally upserted every hour using complex merge logic based on multiple business keys and change-detection columns. The current process uses Dataflow Gen2 and is failing to complete within the required time window. Which approach BEST meets the requirement?

A) Increase the Dataflow Gen2 refresh frequency and add more query steps to handle the merge logic
B) Rewrite the incremental logic in a PySpark notebook using Delta Lake MERGE, scheduled via a pipeline
C) Replace Dataflow Gen2 with a Copy Data pipeline activity using upsert mode
D) Split the fact table into smaller Dataflow Gen2 outputs and merge them using Power Query

---

**Q14.** Your organization has parquet files stored in an existing Azure Data Lake Storage Gen2 account, managed and maintained by another team outside Fabric. You need these files to be queryable as native tables from within a Fabric lakehouse without copying or duplicating the underlying data. What should you do?

A) Use a Dataflow Gen2 to import the parquet files into the lakehouse
B) Mount the ADLS Gen2 account as a mirrored database
C) Create a OneLake shortcut in the lakehouse pointing to the ADLS Gen2 location
D) Use a pipeline Copy activity to copy the files into the lakehouse Files section daily

---

**Q15.** A Fabric Warehouse contains a large fact table. Reporting queries that join this fact table to a dimension table on a non-key column are running slowly. The clustered columnstore index and row-group elimination are functioning correctly, but the query optimizer keeps choosing an inefficient join plan. What should you do to improve performance?

A) Create statistics manually on the join column using CREATE STATISTICS
B) Rebuild the clustered columnstore index on the fact table
C) Convert the fact table to a Delta table stored in a lakehouse instead
D) Add a non-clustered index on the join column

---

**Q16.** Your company ingests high-velocity IoT sensor telemetry (50,000 events/second) and requires sub-second analytical queries using time-series functions such as series_decompose() over the streaming data, with results feeding real-time dashboards. Which Fabric item should you use to store and query this data?

A) A Warehouse with a materialized view refreshed every minute
B) A lakehouse table refreshed via a scheduled Dataflow Gen2
C) An Eventhouse (KQL Database) fed by an Eventstream
D) A Power BI DirectQuery semantic model connected to the source system

---

**Q17.** You are modeling a semantic model using a star schema. The Products dimension and the Promotions dimension have a many-to-many relationship: a product can be part of multiple promotions, and a promotion can apply to multiple products. Which modeling approach BEST resolves this while maintaining accurate filtering behavior?

A) Merge Products and Promotions into a single denormalized dimension table
B) Create a bridge table containing ProductKey and PromotionKey combinations, and relate it to both dimensions
C) Set the relationship between Products and Promotions to bidirectional cross-filtering
D) Duplicate the Promotions table once for each product category

---

**Q18.** A data engineer uses Copilot in a Fabric notebook to generate PySpark code that aggregates total sales by region from a sales fact table. The code runs successfully and produces output, but the business requirement specifies that returned orders (negative quantity) must be excluded from the total. What should the engineer do?

A) Trust the Copilot output since it executed without errors, and deploy it to production
B) Ask Copilot to regenerate the code with a different prompt, and use whichever version runs faster
C) Review the generated code, confirm it excludes returns per the business rule, and modify it if needed before deploying
D) Disable Copilot for this notebook and write all future transformations manually to avoid this issue

---

**Q19.** A Fabric lakehouse contains a shortcut to a large dataset stored in an Amazon S3 bucket in a different cloud region. Data engineers repeatedly query the same S3 data through Spark notebooks, and query latency is high due to cross-cloud network round trips. Without permanently copying the data into OneLake, which action BEST improves subsequent read performance?

A) Convert the shortcut into a Copy activity that copies data nightly into the lakehouse
B) Increase the Spark pool's executor memory to speed up shortcut reads
C) Move the S3 bucket data into a Fabric Dataflow Gen2 staging table before querying
D) Enable OneLake caching for shortcuts so subsequent reads are served from a local cache in the workspace region

---

**Q20.** A team must ingest roughly 500 GB per day from a paginated REST API, apply row-level deduplication using a custom hashing algorithm, and upsert the results into an existing Delta table. Volume is expected to grow to multiple terabytes per day within the year. Which Fabric tool BEST fits this requirement?

A) Dataflow Gen2 with Power Query M transformations
B) Pipeline Copy activity with binary copy mode
C) A KQL database with update policies
D) A Spark notebook using PySpark to call the API, apply custom logic, and perform a Delta MERGE

---

**Q21.** A Fabric lakehouse Delta table receives thousands of small file writes daily from a streaming pipeline. Query performance against the table through the SQL analytics endpoint has degraded significantly over time. Which action BEST addresses this?

A) Run OPTIMIZE on the table with V-ORDER enabled to compact small files for read optimization
B) Convert the lakehouse table into a Warehouse table
C) Increase the Spark pool node size for the ingestion pipeline
D) Create additional shortcuts pointing to the same table

---

**Q22.** A data engineer needs to persist the result set of a complex T-SQL query as a new physical table in a Fabric Warehouse, so downstream BI reports can query it repeatedly without re-executing the full logic each time. Which T-SQL statement should be used?

A) CREATE EXTERNAL TABLE AS SELECT (CETAS)
B) CREATE TABLE AS SELECT (CTAS)
C) SELECT INTO
D) CREATE VIEW

---

**Q23.** A Real-Time Intelligence solution ingests streaming telemetry into a KQL database. An analyst needs to aggregate event counts into fixed 5-minute time buckets for a streaming dashboard. Which KQL query correctly performs this aggregation?

A) summarize count() by Timestamp / 5m
B) summarize count() by floor(Timestamp, 5m)
C) summarize count() by window(Timestamp, 5m)
D) summarize count() by bin(Timestamp, 5m)

---

**Q24.** A data engineer asks Copilot in a Fabric notebook to generate PySpark code that deduplicates records based on a business key, keeping only the most recent record per key. Which statement about this use of Copilot is correct?

A) Copilot output should always be reviewed and validated before use, since it can miss edge cases such as NULL keys or timestamp ties
B) Copilot-generated code does not need review because Fabric automatically certifies its correctness
C) Copilot in Fabric notebooks can only generate DAX and KQL, not PySpark
D) Copilot automatically deploys the generated code to production pipelines without requiring approval

---

**Q25.** A lakehouse in Fabric needs to expose 40 TB of Parquet data stored in an existing Azure Data Lake Storage Gen2 account, partitioned by ingestion date. The data must remain in ADLS Gen2 (no duplication allowed) but must appear as native tables for both Spark notebooks and the SQL analytics endpoint. What should you implement?

A) A OneLake shortcut in the lakehouse pointing to the ADLS Gen2 container
B) A Dataflow Gen2 that copies the data into the lakehouse nightly
C) A pipeline Copy activity scheduled hourly to sync the folder into OneLake
D) A notebook that reads the ADLS Gen2 path and writes a managed Delta table

---

**Q26.** A streaming pipeline writes small batches of records into a lakehouse Delta table every few seconds, producing thousands of tiny Parquet files. Query performance from the SQL analytics endpoint has degraded significantly. Which command should you run in a notebook to consolidate the files and improve read performance?

A) OPTIMIZE table_name with V-ORDER enabled
B) TRUNCATE TABLE followed by a full reload
C) OPTIMIZE table_name VACUUM
D) CREATE STATISTICS on all columns of the table

---

**Q27.** A company ingests millions of IoT telemetry events per second and needs sub-second latency dashboards with time-series analytics over the incoming data. Which combination of Fabric items should be used?

A) Eventstream feeding a KQL database in an Eventhouse
B) Dataflow Gen2 loading into a Warehouse
C) A pipeline Copy activity loading into a Lakehouse table hourly
D) A notebook using Spark Structured Streaming to write to a Lakehouse

---

**Q28.** Analysts run repeated aggregation queries through the SQL analytics endpoint of a lakehouse against a 2-billion-row Delta table, and performance is unacceptable. The SQL analytics endpoint does not support creating indexes or materialized views, and you cannot change how data is ingested. What should you do to improve query performance for these aggregations?

A) Create a nonclustered index directly on the SQL analytics endpoint table
B) Enable result set caching on the lakehouse table
C) Create a T-SQL view in the SQL analytics endpoint that performs the same aggregation
D) Migrate the table into a Fabric Warehouse and create a materialized view for the aggregation

---

**Q29.** An analytics engineer uses Copilot in a Fabric notebook to generate a PySpark transformation that deduplicates and reshapes a sales dataset. What must the engineer do before promoting this code to a production pipeline?

A) Trust the output as-is because Copilot is grounded in the workspace's actual data
B) Only confirm the code has no syntax errors before deploying
C) Skip testing since Copilot-generated code is automatically optimized for production use
D) Validate the generated code's output against expected schema and business rules in a test environment

---

**Q30.** A fact table with 500 million rows references a Customer dimension whose attributes (address, tier) change over time. Reports must accurately reflect the customer's attributes as they existed at the time of each historical transaction. Which modeling approach should be used?

A) Overwrite the Customer dimension in place whenever an attribute changes (Type 1)
B) Flatten all customer history into the fact table so no dimension join is needed
C) Store customer attribute changes only in an M query parameter applied at report render time
D) Implement an SCD Type 2 Customer dimension with surrogate keys and effective/expiry dates, joined to the fact table via the surrogate key

---

**Q31.** A finance team needs to ingest 500 million rows nightly from an on-premises SQL Server into a Fabric lakehouse. The ingestion requires custom Python logic to deduplicate records and call an internal REST API for currency conversion before landing the data. The job must run on a 15-minute schedule via orchestration. Which approach BEST meets these requirements?

A) Build a Dataflow Gen2 with Fast Copy enabled and a scheduled refresh every 15 minutes
B) Use a Copy activity with an inline Data Flow transformation step inside a Data Pipeline
C) Use a Spark notebook to perform the ingestion, deduplication, and API calls, orchestrated by a Data Pipeline with a scheduled trigger
D) Create a KQL database and use an eventstream to ingest the SQL Server data on a timer trigger

---

**Q32.** An analytics engineering team stores curated gold-layer tables that must support full T-SQL write operations (INSERT, UPDATE, MERGE) executed directly against the SQL engine. A separate team uses PySpark notebooks to build the silver layer from raw files using the same OneLake data. Which combination of Fabric items should be used to satisfy both requirements?

A) Use a single Lakehouse only, and have the gold-layer team write T-SQL directly against its SQL analytics endpoint
B) Use two Warehouses connected by OneLake shortcuts, and run the PySpark notebooks directly against the Warehouse's SQL engine
C) Use a Lakehouse for the Spark-based silver layer transformations, and a separate Warehouse fed from the lakehouse for the T-SQL read-write gold layer
D) Use a KQL database for both layers, since it supports T-SQL writes and Spark notebook execution natively

---

**Q33.** A Delta table in a Fabric lakehouse is partitioned by date and is queried heavily via Direct Lake mode in Power BI, with most report filters applied on CustomerID. Read performance is poor despite V-Order being enabled by default. Which command should be run in a notebook to specifically improve predicate pushdown for CustomerID filters?

A) VACUUM lakehouse.SalesTable RETAIN 168 HOURS
B) ALTER TABLE lakehouse.SalesTable SET TBLPROPERTIES ('delta.autoOptimize.optimizeWrite' = 'true')
C) OPTIMIZE lakehouse.SalesTable ZORDER BY (CustomerID)
D) CREATE INDEX idx_customer ON lakehouse.SalesTable (CustomerID)

---

**Q34.** A Direct Lake semantic model in Fabric runs on an F64 capacity. A developer adds a calculated column to the Sales fact table that uses the RELATED() function to pull a category name from a dimension table. After publishing, capacity metrics show the model executing DirectQuery operations instead of using Direct Lake mode. What is the MOST likely cause?

A) The F64 capacity SKU does not meet the minimum guardrail for Direct Lake and must be upgraded
B) The dimension table used in RELATED() must first be optimized with V-Order before calculated columns can run in Direct Lake
C) RELATED() is a DirectQuery-only DAX function and cannot be used in any Fabric semantic model
D) Calculated columns are not supported in Direct Lake storage mode, so the engine falls back to DirectQuery to evaluate them

---

**Q35.** You create a calculation group named 'Time Calcs' containing a calculation item 'YoY %' that returns a DIVIDE() expression producing a ratio. When report authors apply this item to the Total Sales measure, the visual displays the result as currency instead of a percentage. Which change correctly fixes the display without altering the base measure's format?

A) Set the calculation item's Format String Expression property to "0.0%"
B) Change the base measure Total Sales to use a percentage format string
C) Add a new explicit measure that wraps the YoY % output with FORMAT() to a text string
D) Set the calculation group's precedence value to a lower number than any other calculation group

---

**Q36.** A semantic model hosted in a Fabric workspace grows to 14 GB after adding several years of transaction history. Refresh operations begin failing with an error referencing the maximum size for the current storage format. The workspace is assigned to an F64 Fabric capacity. What should you do to resolve this without reducing the amount of data in the model?

A) Move the semantic model to a Power BI Pro workspace to remove the 10 GB size restriction
B) Switch every table in the model to DirectQuery mode so Vertipaq no longer stores the data in memory
C) Enable the large semantic model storage format setting on the dataset, which is available because the workspace is on Fabric capacity
D) Reduce the number of calculation groups in the model, since each calculation group has a fixed 2 GB memory reservation

---

**Q37.** A team is designing a semantic model with a 200 million row fact table. They want to configure an Incremental Refresh policy using RangeStart and RangeEnd parameters to only refresh recent partitions on a schedule. Which storage mode configuration supports this feature?

A) Direct Lake, because incremental refresh policies control which Delta table partitions are reframed
B) DirectQuery only, because incremental refresh reduces the number of queries sent to the source
C) Any storage mode, since incremental refresh is a workspace-level setting independent of table storage mode
D) Import mode (or the Import portion of a hybrid table), because incremental refresh loads and partitions data during scheduled refreshes

---

**Q38.** A composite model has a large DirectQuery fact table (Sales) sourced from a Fabric warehouse and several small dimension tables (Date, Product, Region) currently also set to DirectQuery. Report performance is slow because every slicer interaction re-queries the warehouse for dimension values. What change will BEST improve performance while keeping the fact table live?

A) Convert the Sales fact table to Import mode so the entire model loads into memory
B) Convert the dimension tables to Dual storage mode so Vertipaq can cache them in memory while still allowing DirectQuery joins with the fact table
C) Enable Direct Lake on the dimension tables only, leaving the fact table in DirectQuery
D) Add a bidirectional relationship between each dimension and the fact table to reduce query round-trips

---

**Q39.** A Direct Lake semantic model is hosted on an F64 Fabric capacity. One lakehouse table has grown past the row-count guardrail for that capacity SKU, and the model's Fallback Behavior property is set to Automatic. A report visual queries a measure that references this oversized table. What happens?

A) The visual returns an error because Direct Lake models cannot exceed capacity guardrails under any configuration
B) Fabric transparently reroutes just that table's query to DirectQuery against the same Delta table, while other tables continue to be queried in Direct Lake mode
C) The entire semantic model is automatically reprocessed and switched permanently to Import mode
D) Fabric automatically splits the oversized table into multiple partitions to bring it back under the guardrail

---

**Q40.** You are configuring an incremental refresh policy in Power BI Desktop for an Import-mode semantic model sourced from a Fabric warehouse. The fact table has an OrderDate column. You add two parameters and filter the query by OrderDate between them. Which requirement MUST be met before the Incremental Refresh dialog will let you define the policy?

A) The XMLA endpoint for the workspace must be set to Read/Write
B) The table's storage mode must first be changed to DirectQuery, then back to Import
C) The parameters must be whole-number (Int64) surrogate keys rather than dates
D) The two parameters must be named exactly RangeStart and RangeEnd and must be of Date/Time data type

---

**Q41.** A user in your organization is a member of both the SalesEast RLS role, which filters Sales[Region] = "East", and the SalesManager RLS role, which has no row filter defined. Both roles are assigned to this user's security group in the Fabric workspace. When this user opens a report connected to the semantic model, what data will they see?

A) All rows in the Sales table, because a user's visible rows are the union of everything each assigned role permits, and SalesManager has no filter
B) Only East region rows, because the most restrictive assigned role always overrides less restrictive roles
C) No rows at all, because Fabric intersects conflicting filters from multiple roles and returns an empty result
D) The report will fail to load and require the admin to remove one of the two conflicting role assignments

---

**Q42.** You are building a composite model in Fabric that includes a DirectQuery fact table from a Fabric warehouse and a small Region dimension table used as the many-side target for relationships to fact tables in two different DirectQuery sources. You want the best query performance for the dimension without breaking the ability to relate it to both DirectQuery sources. Which storage mode should you set on the Region dimension table?

A) DirectQuery
B) Dual
C) Import
D) Direct Lake

---

**Q43.** Your semantic model contains two calculation group tables: 'Time Intelligence' and 'Currency Conversion'. Both are set to apply to measures used in the same report visual. Which requirement must you satisfy regarding the Precedence property of these two calculation groups within the model?

A) Precedence values must start at 0 and increase sequentially with no gaps allowed
B) Each calculation group table must be assigned a unique Precedence value; no two calculation groups in the same model may share the same value
C) Only one calculation group per model is allowed to have a non-zero Precedence value
D) Precedence only matters if the calculation groups reference overlapping column names in their calculation items

---

**Q44.** A large Import-mode semantic model includes a DateTime column with millisecond-level timestamps, but reports only ever use it at the day level. Vertipaq memory consumption for this table is unusually high. Which modeling change would MOST reduce the in-memory size of this table?

A) Change the column's data type from DateTime to Text so Vertipaq can dictionary-encode it more efficiently
B) Sort the underlying Power Query table by the DateTime column before it loads into the model
C) Add a calculated column that wraps the DateTime column in DATEVALUE() and keep the original DateTime column alongside it
D) Split the column into separate Date and Time columns, then remove the Time column entirely since it is not used in reporting, keeping only the lower-cardinality Date column

---

