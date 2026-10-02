# Practice Test 1: DP-600 Microsoft Fabric Analytics Engineer Exam Prep

- **Questions:** 45
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A Fabric workspace admin wants to add a new team member who will build and publish reports, create lakehouses, and modify semantic models, but who must NOT be able to add other users to the workspace or change workspace-level settings. Which workspace role should be assigned?

A) Member
B) Admin
C) Viewer
D) Contributor

---

**Q2.** A lakehouse contains a Files section with subfolders for Finance, HR, and Sales data. You need to grant an external audit team read-only access to only the Finance subfolder, without exposing any other folder or the SQL analytics endpoint's other tables. Which Fabric feature should you configure?

A) Workspace-level Viewer role for the audit team
B) Row-level security on the lakehouse SQL analytics endpoint
C) A OneLake data access role scoped to the Finance folder path
D) A shareable link to the lakehouse item

---

**Q3.** You are configuring row-level security (RLS) on a Fabric semantic model. Each sales representative should see only rows in the Sales table where the SalesRepEmail column matches the email address of the signed-in Power BI Service user. Which DAX table filter expression should you use in the RLS role definition?

A) [SalesRepEmail] = USERNAME()
B) [SalesRepEmail] = USERPRINCIPALNAME()
C) [SalesRepEmail] = CUSTOMDATA()
D) [SalesRepEmail] = USERCULTURE()

---

**Q4.** A Fabric Warehouse table stores customer email addresses in a column named Email. You need to ensure that users without unmask permission see a masked version of the email (e.g., aXX@XXXX.com) when querying the table, while the underlying data remains unchanged. Which T-SQL statement should you run?

A) GRANT SELECT ON dbo.Customers (Email) TO [ReadOnlyRole]
B) CREATE SECURITY POLICY EmailMaskPolicy ADD FILTER PREDICATE dbo.fn_MaskEmail(Email) ON dbo.Customers
C) ALTER TABLE dbo.Customers ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()')
D) ALTER TABLE dbo.Customers ADD CONSTRAINT CK_Email CHECK (Email LIKE '%@%')

---

**Q5.** Your team uses a Fabric deployment pipeline with Dev, Test, and Prod stages to promote a lakehouse, a warehouse, and several reports. Before deploying from Test to Prod, you want to see exactly which items have changed and selectively deploy only the updated semantic model without deploying the unchanged lakehouse. What should you do?

A) Use the deployment pipeline's compare view to review differences, then deploy only the selected item
B) Manually export and re-import the semantic model item into the Prod workspace
C) Delete and recreate the Prod workspace to force a full resync of all items
D) Configure a Git branch for Prod and merge only the semantic model's commit

---

**Q6.** Report load times on a Fabric F64 capacity have degraded, and users occasionally see a message indicating operations are being delayed. You need to identify which specific items are consuming the most Capacity Units (CUs) and whether the capacity is being throttled. Which tool should you use?

A) Microsoft Fabric Capacity Metrics app
B) Power BI usage metrics report
C) Azure Monitor Activity Log
D) Microsoft Purview compliance portal

---

**Q7.** A company uses a Fabric deployment pipeline with Dev, Test, and Prod stages. Each stage must connect a Lakehouse-based semantic model to a different SQL analytics endpoint connection string, but the report and model logic should remain identical across stages. Which Fabric feature should they configure to avoid manually editing connections after every deployment?

A) Separate Power BI Desktop files maintained manually for each environment
B) Deployment rules that override the connection string parameter for each stage
C) A single dataflow parameter shared globally across all workspaces
D) Git branch protection rules applied only to the Prod workspace

---

**Q8.** A data engineer needs to grant a group of analysts read access to only the 'sales/2026' folder inside a Lakehouse's OneLake storage, without giving them broader workspace access or access to other folders in the same Lakehouse. Which feature should be used?

A) Configure a OneLake data access role scoped to the specific folder path
B) Assign the analysts the workspace Viewer role
C) Grant item-level Read permission on the Lakehouse
D) Create a row-level security role in the semantic model

---

**Q9.** A Warehouse table stores customer national ID numbers in a column named NationalID. Analysts need to see only the last 4 digits (e.g., XXXXX1234) when querying, while the underlying data remains unchanged. Which T-SQL approach implements this?

A) CREATE ROW LEVEL SECURITY POLICY on NationalID
B) ALTER TABLE ... ALTER COLUMN NationalID ADD MASKED WITH (FUNCTION = 'partial(0,"XXXXX",4)')
C) GRANT DENY SELECT ON NationalID TO analysts_role
D) ALTER TABLE ... ALTER COLUMN NationalID ADD ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CEK1)

---

**Q10.** A semantic model has a Region column, and business rules require that a regional sales manager can only see rows for their assigned region when browsing a published report. Before publishing, the developer wants to confirm the security rule behaves correctly for a specific manager in Power BI Desktop. What should they do?

A) Enable column-level security on the Region column
B) Publish the report to the Fabric workspace and test directly in the Service
C) Apply dynamic data masking to the Region column
D) Define an RLS role with a DAX filter on Region and use 'View As Roles' to test it

---

**Q11.** A Fabric workspace is already connected to an Azure DevOps repository for source control. A team member needs to make changes to reports and commit them back to Git, but should not be able to disconnect the workspace from Git or change the Git connection settings. Which is the minimum workspace role that satisfies this requirement?

A) Viewer
B) Admin
C) Member
D) Contributor

---

**Q12.** Users report intermittent 'This visual has exceeded the available resources' errors on interactive reports during business hours. The Fabric Capacity Metrics app shows CU (Capacity Unit) utilization sustained above 100% for extended periods each afternoon. What is the BEST immediate action to diagnose and address this?

A) Use the Capacity Metrics app to identify the top consuming items, then scale up the SKU or enable autoscale/surge protection
B) Delete all semantic models on the capacity to free up storage
C) Disable Git integration on all workspaces assigned to the capacity
D) Move all lakehouses to a different region

---

**Q13.** A data engineering team must transform 500 GB of raw JSON files daily using complex custom Python logic, including machine learning feature engineering, before landing the results as Delta tables in a lakehouse. Which Fabric tool should they use for this transformation?

A) Notebook with PySpark
B) Pipeline Copy activity
C) Power Query in Excel
D) Dataflow Gen2

---

**Q14.** A team creates a OneLake shortcut in a lakehouse that points to an existing ADLS Gen2 container containing Parquet files. What happens to the data as a result of creating this shortcut?

A) Data remains in the ADLS Gen2 account and is virtually referenced from OneLake without duplication
B) Data is automatically converted to Delta format
C) Data is copied into OneLake storage
D) Data becomes read-only in the original location

---

**Q15.** A team requires full T-SQL INSERT, UPDATE, and DELETE support with multi-statement transactional guarantees on their structured tables in Fabric. Which item should they create to meet this requirement?

A) Lakehouse
B) Warehouse
C) KQL Database
D) Dataflow Gen2

---

**Q16.** For a star-schema semantic model optimized for DAX performance in Fabric, which approach to handling dates is recommended?

A) Dedicated shared date dimension table marked as a date table with a single active relationship to each fact table
B) Embed date columns directly in each fact table without a separate dimension
C) Create separate date dimension tables per fact table
D) Use bidirectional relationships from the date table to all fact tables

---

**Q17.** A data engineer uses Copilot in Fabric within a notebook to generate PySpark code that deduplicates a large customer table based on a subset of columns. What should the engineer do before running this code against the production table?

A) Review and validate the generated code against business logic and test on sample data before running in production
B) Discard the code entirely and write all logic manually since Copilot output cannot be trusted for PySpark
C) Only use Copilot in Fabric for DAX expressions, not for PySpark notebook code
D) Run the code immediately in production since Copilot output requires no review

---

**Q18.** A retail company ingests millions of IoT sensor events per second and needs near real-time analytical queries using time-series functions over this streaming data. Which Fabric item is BEST suited for storing and querying this data?

A) Dataflow Gen2
B) Warehouse
C) Lakehouse with Delta tables
D) KQL Database in an Eventhouse

---

**Q19.** A company stores raw sensor data as Parquet files in an Azure Data Lake Storage Gen2 account in a different Azure tenant. Analysts need to query this data from a Fabric lakehouse in near real time without duplicating the storage or incurring ongoing copy costs. Which solution BEST meets these requirements?

A) Use a pipeline Copy activity to copy the files into the lakehouse
B) Create a OneLake shortcut to the ADLS Gen2 location
C) Use Fabric mirroring to replicate the ADLS Gen2 storage account into the lakehouse
D) Use a Dataflow Gen2 to import the data into the lakehouse

---

**Q20.** A data engineering team must transform 500 GB of raw data stored in a Fabric lakehouse using complex joins and a custom Python library not available in Power Query. The transformation must scale efficiently across the full dataset. Which Fabric tool should they use?

A) A Spark notebook using PySpark
B) A Dataflow Gen2 with Power Query transformations
C) A pipeline Copy activity
D) A KQL queryset

---

**Q21.** A workspace administrator wants their team to use Copilot in Fabric notebooks to generate and explain PySpark transformation code. Which prerequisite must be satisfied for Copilot to be available in that workspace?

A) The user must have a Power BI Pro license only, regardless of capacity
B) The notebook must be attached to a warehouse instead of a lakehouse
C) The workspace must be assigned to a Fabric capacity (F64 or higher, or a trial capacity) and Copilot must be enabled at the tenant level by an admin
D) The user must write all code in T-SQL rather than PySpark

---

**Q22.** You are designing a star schema in a Fabric lakehouse to support efficient DAX queries against a semantic model. Which type of key should be used to join fact tables to dimension tables?

A) Business/natural keys inherited directly from the source system
B) GUID keys generated by the source system
C) Surrogate integer keys generated during the ETL/transformation process
D) Composite keys made of multiple string columns

---

**Q23.** A retail company streams IoT sensor events into the SensorEvents table of a Fabric Eventhouse. They need a KQL query that returns the average temperature per store, grouped into 1-hour buckets. Which query is correct?

A) SensorEvents | extend avg(Temperature) by StoreId
B) SensorEvents | project avg(Temperature), StoreId, Timestamp
C) SensorEvents | summarize avg(Temperature) by StoreId, bin(Timestamp, 1h)
D) SensorEvents | where Timestamp > ago(1h) | avg(Temperature)

---

**Q24.** A data engineer loads new data into a Delta table using a Spark notebook in a Fabric lakehouse but notices that queries against the SQL analytics endpoint do not immediately reflect the new rows. What best explains this behavior?

A) The SQL analytics endpoint only reads from the warehouse, not the lakehouse
B) The SQL analytics endpoint requires a pipeline to explicitly copy data before it becomes queryable
C) Delta tables cannot be queried through the SQL analytics endpoint
D) The SQL analytics endpoint automatically syncs with lakehouse metadata after each write, though sync can lag briefly and a manual refresh can be triggered from the UI

---

**Q25.** A retail company stores 50 TB of historical sales files in an Azure Data Lake Storage Gen2 account that is used by several non-Fabric applications. An analytics engineer needs to make this data available in a Fabric lakehouse for use in Spark notebooks, but must NOT copy or duplicate the data, and any updates made by the external applications must be immediately visible in Fabric. Which approach BEST meets these requirements?

A) Use a Dataflow Gen2 to import the data into the lakehouse's managed Files area on a nightly schedule
B) Use a Copy Data activity in a Fabric pipeline to copy the files into the lakehouse Tables folder
C) Create a OneLake shortcut in the lakehouse that points to the ADLS Gen2 location
D) Mount the ADLS Gen2 account as an external table in a Fabric warehouse and query it from the lakehouse

---

**Q26.** An organization ingests telemetry from thousands of IoT devices and needs to run sub-second aggregation queries over the last 24 hours of data as it arrives, using a query language similar to Azure Data Explorer. Which Fabric experience should the analytics engineer choose to store and query this data?

A) A Fabric Warehouse queried with T-SQL
B) A KQL Database in Real-Time Intelligence
C) A Lakehouse with Delta tables queried via the SQL analytics endpoint
D) A Power BI semantic model with DirectQuery over a Dataflow Gen2

---

**Q27.** Analysts report that a large fact table in a Fabric Warehouse is being scanned in full for every query, even when filtering on a single date. The table has no indexes or statistics defined, and query plans show inaccurate row-count estimates. What should the analytics engineer do FIRST to improve query performance?

A) Convert the warehouse table into a lakehouse Delta table instead
B) Rewrite all queries to use SELECT * instead of specific column lists
C) Increase the Fabric capacity SKU to the next tier
D) Create statistics on the frequently filtered columns using CREATE STATISTICS

---

**Q28.** An analytics engineer uses Copilot in a Fabric notebook to generate a PySpark transformation that deduplicates a large Delta table based on a business key and keeps the most recent record per key. What is the correct next step after Copilot generates the code?

A) Deploy the notebook to production immediately since Copilot-generated code is pre-validated against Fabric best practices
B) Run the generated code against a representative sample and manually verify the deduplication logic and output row counts before trusting the result
C) Discard the Copilot suggestion entirely, since Copilot in Fabric cannot generate valid PySpark syntax
D) Ask Copilot to also handle capacity scaling for the notebook, since it can directly modify workspace compute settings

---

**Q29.** An analytics engineer needs to allow business analysts to write ad hoc T-SQL queries against Delta tables in a lakehouse without giving them the ability to insert, update, or delete rows. Which Fabric component should they use to grant this access?

A) Grant the analysts Contributor role on the lakehouse item
B) Have analysts connect to the lakehouse Files section using T-SQL
C) Create a Dataflow Gen2 that exposes the tables through a Power BI dataset
D) Have analysts query the lakehouse's SQL analytics endpoint

---

**Q30.** An analytics engineer is designing a star schema in a Fabric warehouse for a sales reporting solution. A dimension table for 'Product' can have its category and price change over time, and the business requires historical reports to reflect the category and price that were in effect at the time of each sale. Which dimension design technique should the engineer use?

A) Store only the current product category and price in the dimension, overwriting old values when they change
B) Implement a Type 2 slowly changing dimension with a surrogate key and effective date columns for each version of a product
C) Remove the Product dimension entirely and store category and price directly in the fact table for every sale
D) Create a separate fact table for each historical version of the product catalog

---

**Q31.** A retail analytics team ingests semi-structured JSON files containing deeply nested arrays. The transformation logic requires custom Python libraries (e.g., a proprietary geocoding SDK) and must scale to process 500GB of files per day as part of an automated pipeline. Which Fabric tool should be used to perform the transformation step?

A) A Dataflow Gen2 with Power Query M transformations
B) The SQL analytics endpoint of a lakehouse
C) A dataflow refresh scheduled inside Power BI Desktop
D) A notebook running PySpark code

---

**Q32.** A team has 20TB of Parquet files already stored in an external Azure Data Lake Storage Gen2 account. They want to make this data queryable from a Fabric lakehouse alongside other OneLake tables, but must not duplicate or move the 20TB of source data due to cost and compliance constraints. Which Fabric feature should they use?

A) A Data pipeline Copy Data activity into the lakehouse Files section
B) Database mirroring configured on the ADLS account
C) A OneLake shortcut pointing to the ADLS Gen2 location
D) A Dataflow Gen2 that loads the Parquet files into a lakehouse table

---

**Q33.** In a Fabric eventhouse (KQL database), you need to write a KQL query that computes the average temperature per DeviceId, aggregated into 5-minute time buckets, from a streaming telemetry table. Which query correctly achieves this?

A) Telemetry | summarize avg(Temperature) by DeviceId, bin(Timestamp, 5m)
B) Telemetry | extend Timestamp = ago(5m) | project DeviceId, Temperature
C) Telemetry | join kind=inner (Telemetry) on DeviceId | summarize avg(Temperature)
D) Telemetry | order by Timestamp desc | take 5

---

**Q34.** A company runs a Direct Lake semantic model on an F64 Fabric capacity. One of the underlying lakehouse tables grows beyond the row-count guardrail defined for F64. By default, what happens when a report visual queries that specific table?

A) The report fails immediately with a hard error and returns no data
B) The entire semantic model permanently switches to Import mode
C) Fabric automatically upgrades the capacity to the next SKU tier
D) The query for that table automatically falls back to DirectQuery mode

---

**Q35.** A financial services company continuously loads high-volume transaction data into a Fabric warehouse throughout the day. Analysts need Power BI reports that reflect changes within seconds, without scheduled refreshes and without duplicating the underlying data into the semantic model. Which storage mode should you choose?

A) Import
B) Direct Lake
C) DirectQuery
D) Composite (Import + DirectQuery)

---

**Q36.** You need dynamic row-level security so that each salesperson viewing a report sees only rows where Sales[SalesRegion] matches their assigned region, stored in a Regions table with a UserPrincipalName column. Which DAX filter expression should you use in the RLS role defined on the Sales table?

A) [SalesRegion] = USERNAME()
B) [SalesRegion] = USERPRINCIPALNAME()
C) [SalesRegion] = LOOKUPVALUE(Regions[Region], Regions[UserPrincipalName], USERPRINCIPALNAME())
D) FILTER(Sales, [SalesRegion] = "Region")

---

**Q37.** What are calculation groups primarily used for in a Power BI semantic model?

A) To physically group tables together for storage optimization on disk
B) To apply reusable calculation logic, such as time intelligence or currency conversion, as calculation items across multiple measures without duplicating DAX
C) To define row-level security roles for different user groups
D) To partition large fact tables for incremental refresh

---

**Q38.** You are configuring incremental refresh for a large Fabric semantic model that imports five years of sales data. Before you can define the incremental refresh policy in Power BI Desktop, what must you create in the model?

A) A calculated table listing every date in the desired range
B) A calculation group containing time intelligence calculation items
C) Two parameters named RangeStart and RangeEnd, of type Date/time
D) Two measures named RangeStart and RangeEnd

---

**Q39.** Your Import-mode semantic model on an F64 Fabric capacity workspace is approaching the default 10 GB dataset size limit. You want to allow the model to grow beyond this limit without changing capacity SKU. What should you do?

A) Convert the semantic model to DirectQuery mode
B) Split the model into multiple smaller datasets
C) Enable the "Large semantic model storage format" setting for the dataset
D) Enable Direct Lake mode for all tables in the model

---

**Q40.** A retail company has a Fabric semantic model used by sales representatives across five regions. Each rep must see only orders for their own region, and the mapping of reps to regions changes frequently as staff are reassigned. The security model must require no manual updates to Power BI when staff change regions. Which approach BEST meets these requirements?

A) Create a static RLS role per region and manually add each user as a member of the corresponding role
B) Create a dynamic RLS role that filters the Region table using USERPRINCIPALNAME() joined to a RepRegionMapping table maintained in the lakehouse
C) Apply a report-level filter on the Region column and distribute separate report copies per region
D) Enable object-level security to hide the Region column from all users except administrators

---

**Q41.** You are preparing a semantic model in Power BI Desktop so that it supports an incremental refresh policy once published to a Fabric workspace. Which action must you complete in Power Query BEFORE you can enable the incremental refresh policy?

A) Publish the report to a Fabric or Premium capacity workspace first, then configure refresh in the Service
B) Switch the storage mode of the table from Import to Direct Lake
C) Create RangeStart and RangeEnd parameters of type Date/DateTime and use them to filter the date column of the table
D) Create and validate row-level security roles for the table that will be incrementally refreshed

---

**Q42.** A Direct Lake semantic model reports against a Fabric lakehouse Delta table that receives frequent small append operations throughout the day. Report users notice query performance has degraded to levels typical of DirectQuery, even though the model is configured for Direct Lake. What is the MOST likely cause and the correct remediation?

A) The workspace capacity SKU does not support Direct Lake; upgrade to a higher Fabric SKU
B) RLS roles on the table are misconfigured, forcing the engine to bypass in-memory paging
C) The semantic model must be manually switched to Import mode to fix the fallback
D) The Delta table has accumulated many small files and row groups from frequent writes, causing Direct Lake to fall back to DirectQuery; run OPTIMIZE (table maintenance) on the table to compact files

---

**Q43.** Report authors need to let end users switch a matrix visual between Year-to-Date, Quarter-to-Date, and Month-to-Date views of the same base measures without the modeler creating a separate DAX measure for every combination of base measure and time period. Which semantic model feature should the modeler implement?

A) Field parameters that let users pick which column to display in a visual
B) What-if parameters bound to a disconnected table
C) A composite model that combines Import and DirectQuery tables
D) Calculation groups with calculation items that apply time intelligence logic to any selected measure

---

**Q44.** A semantic model in a Fabric workspace has grown to 18 GB after adding several years of transactional history, and refreshes are starting to fail due to the default dataset size limit. The workspace is on an F64 Fabric capacity. Which setting should be enabled to support this model going forward?

A) Enable the 'Large semantic model storage format' setting for the dataset, which is supported on capacities of sufficient size such as F64
B) Enable the XMLA endpoint in the workspace admin portal to allow larger datasets
C) Convert all tables in the model to DirectQuery to eliminate the size limitation
D) Enable Q&A on the semantic model to reduce in-memory footprint

---

**Q45.** A modeler is optimizing a large fact table in a semantic model to improve Vertipaq compression and query performance. Which modeling practice will have the GREATEST positive impact?

A) Reduce high-cardinality columns, such as splitting a full DateTime column into separate Date and Time columns and removing unused text columns
B) Add several calculated columns to the fact table to pre-compute values needed by reports
C) Increase the number of many-to-many relationships between the fact table and dimension tables
D) Store all numeric columns as text strings to ensure consistent formatting across visuals

---

