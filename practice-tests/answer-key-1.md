# Answer Key — Practice Test 1

**Q1. Correct: D**

Contributor can create, edit, and publish content (reports, lakehouses, semantic models) within the workspace but cannot manage workspace access or update workspace settings.

---

**Q2. Correct: C**

OneLake data access roles let you define folder-level permissions inside a lakehouse (via one or more folder paths) and assign specific users or groups read access to only that scope, independent of workspace roles.

---

**Q3. Correct: B**

USERPRINCIPALNAME() returns the UPN (typically the email address) of the signed-in user in the Power BI Service, making it the correct function to match against an email-formatted column for RLS.

---

**Q4. Correct: C**

Dynamic Data Masking in Fabric Warehouse (T-SQL) is applied with ALTER TABLE ... ALTER COLUMN ... ADD MASKED WITH (FUNCTION = 'email()'), which obfuscates the email format for users lacking UNMASK permission while leaving stored data intact.

---

**Q5. Correct: A**

The Fabric deployment pipeline compare view highlights differences between stages (new, modified, unchanged items) and allows selective deployment of individual items, letting you deploy only the changed semantic model.

---

**Q6. Correct: A**

The Fabric Capacity Metrics app (installed from AppSource) provides per-item CU consumption, utilization trends, and throttling/overage status for a Fabric capacity, making it the correct tool to diagnose capacity-related slowdowns.

---

**Q7. Correct: B**

Deployment rules in Fabric deployment pipelines let you define stage-specific parameter values (like connection strings) that automatically apply on every deployment, keeping content identical while the underlying connection changes per stage.

---

**Q8. Correct: A**

OneLake data access roles allow fine-grained, folder-level (or table-level) access control within a Lakehouse's OneLake storage, letting admins scope access to specific paths for specific security groups.

---

**Q9. Correct: B**

Dynamic data masking's partial() function masks a column while showing a defined portion of the original value; the syntax masking all but the last 4 characters with 'X' matches this requirement exactly, and the underlying stored data is untouched.

---

**Q10. Correct: D**

Row-level security roles are defined with DAX filter expressions in Power BI Desktop's Manage Roles dialog, and the 'View As Roles' feature lets the developer preview exactly what a user assigned that role would see, before publishing.

---

**Q11. Correct: D**

Contributor role permits committing and syncing changes with an already-connected Git repository, but does not include the permission to connect or disconnect the workspace from Git, which is reserved for Admin.

---

**Q12. Correct: A**

The Fabric Capacity Metrics app surfaces which items/operations are consuming the most Capacity Units, allowing admins to pinpoint the cause of throttling; scaling the SKU up or enabling autoscale/surge protection is the standard remediation for sustained overutilization causing interactive request rejections.

---

**Q13. Correct: A**

Spark notebooks support full custom Python code, distributed processing at scale, and libraries for ML feature engineering — Dataflow Gen2's Power Query M engine cannot handle this level of custom logic or volume efficiently.

---

**Q14. Correct: A**

Shortcuts create a virtual reference to data in its original location (ADLS Gen2, S3, or another Fabric item) so it can be accessed as if it were in OneLake, without any physical data movement or duplication.

---

**Q15. Correct: B**

A Fabric Warehouse provides a full T-SQL engine with complete DML support (INSERT/UPDATE/DELETE) and multi-table transactions, matching traditional data warehouse semantics.

---

**Q16. Correct: A**

Best practice is one shared, marked date dimension with a single-direction active relationship to each fact table's date key, enabling consistent time intelligence and efficient DAX evaluation across the model.

---

**Q17. Correct: A**

Copilot in Fabric is an AI accelerator that speeds up code generation, but its output must always be reviewed and validated against actual business requirements and tested on representative data before production use, since it may miss context-specific rules.

---

**Q18. Correct: D**

A KQL Database inside an Eventhouse (Real-Time Intelligence) is purpose-built for high-throughput streaming ingestion and provides native time-series and log-analytics query functions via KQL, ideal for IoT telemetry.

---

**Q19. Correct: B**

OneLake shortcuts create a virtual reference to data in external storage (including cross-tenant ADLS Gen2) without moving or duplicating it. Queries against the shortcut read the source data directly, so it stays current with no ongoing copy job or storage duplication.

---

**Q20. Correct: A**

Spark notebooks in Fabric run distributed PySpark code, support installing and importing custom Python libraries, and scale efficiently to large datasets with complex joins — exactly what this scenario requires.

---

**Q21. Correct: C**

Copilot in Fabric requires the workspace to run on a paid Fabric capacity of F64 or above (or an eligible trial capacity), and a tenant administrator must explicitly enable the Copilot tenant switch before any user in that tenant can access it.

---

**Q22. Correct: C**

Surrogate keys are integer values generated during ETL specifically to relate fact and dimension tables. Integer keys compress and index far more efficiently than strings/GUIDs and are stable even if source business keys change, giving optimal DAX and storage engine performance.

---

**Q23. Correct: C**

summarize with an aggregation function (avg()) grouped by both a dimension (StoreId) and a time bucket created with bin(Timestamp, 1h) is the standard KQL pattern for aggregating streaming data into fixed time windows.

---

**Q24. Correct: D**

The SQL analytics endpoint auto-syncs its metadata with Delta table changes made in the lakehouse, but this sync is not always instantaneous; there can be a short delay, and users can force an immediate metadata refresh from the workspace UI.

---

**Q25. Correct: C**

OneLake shortcuts create a virtual, in-place reference to data in ADLS Gen2 (or other supported sources) without copying it. Because the shortcut reads directly from the source, changes made by external applications are immediately reflected in Fabric, satisfying the no-duplication and freshness requirements simultaneously.

---

**Q26. Correct: B**

KQL Databases in Real-Time Intelligence are purpose-built for high-velocity, high-volume streaming telemetry and support KQL, which is optimized for fast time-series aggregation over recent data with sub-second response times.

---

**Q27. Correct: D**

Fabric Warehouse relies on statistics to generate accurate query plans and estimate cardinality. Running CREATE STATISTICS on the filtered columns gives the query optimizer the information needed to choose efficient plans instead of scanning the entire table, directly addressing the described symptom.

---

**Q28. Correct: B**

Copilot in Fabric accelerates code generation but does not guarantee correctness for a specific dataset or business rule. The exam expects engineers to validate generated logic (e.g., confirming the correct 'most recent' record is retained and row counts match expectations) before relying on it in production.

---

**Q29. Correct: D**

The SQL analytics endpoint automatically exposes lakehouse Delta tables for read-only T-SQL querying. It is the correct mechanism for giving analysts ad hoc query access via T-SQL without allowing them to modify the underlying data, since the endpoint does not support write operations.

---

**Q30. Correct: B**

A Type 2 slowly changing dimension preserves historical attribute values by creating a new row (new surrogate key) with effective/expiry dates whenever a tracked attribute changes. Fact rows reference the surrogate key that was current at the time of the sale, ensuring historical reports correctly reflect the category and price in effect at that time.

---

**Q31. Correct: D**

Notebooks running Spark (PySpark/Scala) support arbitrary custom Python libraries, handle deeply nested semi-structured data efficiently via distributed processing, and scale to large daily volumes far better than Power Query-based Dataflow Gen2, which is optimized for lighter, more visual ETL and has practical scale/compute limits for this kind of workload.

---

**Q32. Correct: C**

A OneLake shortcut creates a reference to the external ADLS Gen2 location so it appears as if the data lives in the lakehouse, without copying or moving the underlying files — satisfying the no-duplication requirement while still making it queryable through the SQL analytics endpoint and Spark.

---

**Q33. Correct: A**

The bin() function groups the Timestamp column into fixed 5-minute intervals, and summarize avg(Temperature) by DeviceId, bin(Timestamp, 5m) computes the average temperature per device within each 5-minute bucket — the standard KQL pattern for time-windowed aggregation over streaming data.

---

**Q34. Correct: D**

When a Direct Lake table exceeds the capacity's row-count or size guardrails, Fabric automatically falls back to DirectQuery for queries against that table (fallback behavior is on by default and can be disabled).

---

**Q35. Correct: B**

Direct Lake reads Delta Parquet files directly from OneLake with near in-memory (Vertipaq-like) query performance and no scheduled refresh or data duplication, making it the optimal choice for near-real-time reporting on lakehouse/warehouse data.

---

**Q36. Correct: C**

LOOKUPVALUE correctly retrieves the region assigned to the currently signed-in user (via USERPRINCIPALNAME) from the Regions table and compares it against SalesRegion, implementing proper dynamic RLS.

---

**Q37. Correct: B**

Calculation groups let you define calculation items (e.g., YTD, PY, currency conversion) once and apply them to any measure at query time, dramatically reducing measure duplication and DAX maintenance overhead.

---

**Q38. Correct: C**

Incremental refresh in Power BI requires two Date/time parameters named exactly RangeStart and RangeEnd; Power Query uses these to filter the fact table and Power BI Desktop uses them to detect and configure the refresh policy dialog.

---

**Q39. Correct: C**

Enabling Large semantic model storage format on a Fabric capacity removes the default 10 GB dataset size limit, allowing the model to grow up to the memory limits of the assigned SKU while retaining Import-mode performance.

---

**Q40. Correct: B**

Dynamic RLS using USERPRINCIPALNAME() (or USERNAME()) filtered through a mapping table stored and maintained in the lakehouse automatically reflects staff reassignments without any changes to the Power BI model or roles, satisfying the 'no manual updates' requirement.

---

**Q41. Correct: C**

Incremental refresh in Power BI Desktop requires two parameters named RangeStart and RangeEnd of type Date/DateTime that are applied as a filter on the table's date column; this is the prerequisite step that unlocks the 'Incremental refresh and real-time data' dialog for that table.

---

**Q42. Correct: D**

Direct Lake falls back to DirectQuery when a Delta table exceeds guardrails such as too many row groups or excessive small files, typically caused by frequent small writes. Running OPTIMIZE (and optionally VACUUM) compacts the Parquet files and row groups, restoring Direct Lake's in-memory paging behavior.

---

**Q43. Correct: D**

Calculation groups let a modeler define a small set of calculation items (YTD, QTD, MTD) that apply their DAX logic dynamically to whichever base measure a user selects, avoiding the need to author a duplicate measure for every measure/time-period combination.

---

**Q44. Correct: A**

The 'Large semantic model storage format' setting removes the default dataset size cap (10 GB) and is available on Fabric/Premium capacities that meet the minimum size requirement (e.g., F64 or P SKUs and above), allowing models to grow according to the capacity's available memory.

---

**Q45. Correct: A**

Vertipaq compresses data by column, and compression ratio depends heavily on cardinality — fewer distinct values compress better. Splitting high-cardinality DateTime columns into lower-cardinality Date and Time columns, and dropping unused columns, directly reduces cardinality and improves both compression and query speed.

---

