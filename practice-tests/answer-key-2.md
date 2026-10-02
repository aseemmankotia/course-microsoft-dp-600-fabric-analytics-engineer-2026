# Answer Key — Practice Test 2

**Q1. Correct: B**

OneLake data access roles let you define folder- or file-level scoped permissions directly on OneLake data, independent of workspace or item-level permissions, which is exactly the granularity needed here.

---

**Q2. Correct: C**

Fabric Git integration detects conflicts at the item level when the same item changed in both the workspace and Git; resolution requires selecting whether to keep the workspace version or the Git version for that item, since Fabric does not merge internal item contents automatically.

---

**Q3. Correct: C**

The partial() masking function lets you specify a prefix length to hide, a custom padding string, and a suffix length to expose — exactly matching the requirement to show only the last four digits with a custom prefix pattern.

---

**Q4. Correct: A**

Fabric deployment pipelines support deployment rules, which let you define stage-specific override values (such as a different connection string or parameter) that are automatically applied every time content is deployed into that stage, removing the need for manual post-deployment edits.

---

**Q5. Correct: A**

Fabric capacity uses different smoothing windows depending on operation type: interactive operations are smoothed over 5 minutes, making overages trigger rejection quickly, while background operations are smoothed over 24 hours, allowing them to absorb bursts of usage for much longer before throttling or rejection occurs.

---

**Q6. Correct: D**

RLS defined on a semantic model is enforced by the Fabric/Analysis Services engine at query time for any client, regardless of whether the model uses Import, DirectQuery, or Direct Lake storage mode. Lakehouse-level security (like OneLake data access roles) governs direct access to lakehouse data separately and doesn't need to duplicate model-level RLS.

---

**Q7. Correct: B**

OneLake data access roles let you define granular folder/table-scoped read permissions and assign security groups without granting broader workspace or item-level access.

---

**Q8. Correct: C**

Dynamic data masking obscures column values (e.g., showing only last 4 digits) for non-privileged users at query time while still allowing the column to be used in queries and aggregations, without physically restricting access to the column.

---

**Q9. Correct: B**

Deployment pipeline rules let you specify a different value for a parameter or connection per stage, and Fabric automatically applies that rule value every time content is deployed to that stage.

---

**Q10. Correct: C**

Surge Protection is a capacity setting that lets admins define a utilization threshold and choose an action (such as reject) specifically for background operations, protecting interactive workloads from being starved.

---

**Q11. Correct: B**

Git integration connects a workspace to a repository for source control (commit/sync history), while deployment pipelines handle promoting and deploying items across a chain of workspaces representing environments.

---

**Q12. Correct: A**

The Viewer workspace role grants read access to consume reports and semantic models but does not automatically grant direct query access to the underlying lakehouse tables via the SQL analytics endpoint; that requires an explicit item permission (e.g., Read all SQL Endpoint data) or a OneLake data access role.

---

**Q13. Correct: B**

PySpark notebooks using Delta Lake MERGE scale efficiently for very large datasets with complex conditional upsert logic and can be scheduled/orchestrated via a pipeline; the Dataflow Gen2 mashup engine is not designed for this scale of transformation.

---

**Q14. Correct: C**

OneLake shortcuts create a virtualized reference to external storage such as ADLS Gen2, exposing the files as native lakehouse tables without duplicating or moving the underlying data.

---

**Q15. Correct: A**

Fabric Warehouse auto-creates some statistics, but columns used in joins or filters that lack up-to-date statistics can cause the optimizer to pick a poor plan; manually creating statistics with CREATE STATISTICS gives the optimizer better cardinality estimates.

---

**Q16. Correct: C**

An Eventhouse (KQL Database) within Real-Time Intelligence is purpose-built for high-velocity streaming ingestion via Eventstream and supports native KQL time-series functions like series_decompose() with low-latency query performance.

---

**Q17. Correct: B**

A bridge (associative) table holding the valid key combinations is the standard star-schema pattern for resolving many-to-many relationships between two dimensions while preserving correct, unambiguous filter propagation.

---

**Q18. Correct: C**

Copilot-generated code must always be reviewed and validated against actual business requirements; Copilot cannot infer unstated business rules such as excluding returns, so verification and correction before deployment is required.

---

**Q19. Correct: D**

OneLake caching for shortcuts caches data accessed through cross-cloud or cross-region shortcuts, so repeated reads are served from a local cache rather than re-fetching across the network each time, directly reducing latency without duplicating data.

---

**Q20. Correct: D**

Spark notebooks scale to large and growing data volumes and support arbitrary custom code (pagination handling, custom hashing) plus native Delta Lake MERGE syntax for efficient upserts, making this the recommended pattern for complex, high-volume, code-driven ingestion.

---

**Q21. Correct: A**

OPTIMIZE compacts many small Parquet files into larger ones, and V-ORDER applies sorting and encoding specifically optimized for fast reads through the SQL analytics endpoint and Power BI, directly resolving fragmentation caused by frequent small streaming writes.

---

**Q22. Correct: B**

Fabric Warehouse T-SQL supports CTAS, which materializes a query's result set as a new physical table in a single statement, minimizing custom ETL code and providing the best downstream read performance for repeated BI queries.

---

**Q23. Correct: D**

bin() is the correct KQL function for rounding datetime values down into fixed-size time buckets, and it is the standard pattern used with summarize for time-series aggregation in KQL databases.

---

**Q24. Correct: A**

Microsoft's guidance for Copilot in Fabric is that generated code and queries must always be reviewed and validated by the engineer, since Copilot can produce logically incomplete code, such as missing null-handling or tie-breaking logic in deduplication scenarios.

---

**Q25. Correct: A**

Shortcuts create a reference to external storage (ADLS Gen2, S3, another lakehouse, etc.) inside OneLake without copying data, exposing it as a table to both Spark and the SQL analytics endpoint while it physically stays in the source location.

---

**Q26. Correct: A**

OPTIMIZE compacts small files into larger ones, and enabling V-Order additionally sorts and encodes the data for faster reads by the SQL analytics endpoint and Power BI — this is the standard maintenance operation for small-file problems in Fabric lakehouses.

---

**Q27. Correct: A**

Real-Time Intelligence in Fabric uses Eventstream to capture high-velocity streaming data and route it into a KQL database (within an Eventhouse), which is purpose-built for sub-second time-series ingestion and query latency at massive scale.

---

**Q28. Correct: D**

A Fabric Warehouse supports materialized views and gives full write/DDL control, allowing pre-computed aggregations to be stored and served with far better performance than the read-only SQL analytics endpoint over a lakehouse, which cannot add indexes or materialized views.

---

**Q29. Correct: D**

Copilot accelerates code generation but does not guarantee logical correctness for business-specific rules; best practice (and exam guidance) is to always review and validate Copilot output against expected results before using it in production.

---

**Q30. Correct: D**

SCD Type 2 preserves historical versions of dimension rows with surrogate keys and effective/expiry date ranges, allowing each fact row to join to the customer attributes that were valid at the time of the transaction — the correct star-schema pattern for this requirement.

---

**Q31. Correct: C**

At this scale and with custom Python/REST logic, a Spark notebook gives full programmatic control and scales far better than the Power Query mashup engine. Orchestrating it with a Data Pipeline schedule trigger meets the 15-minute cadence requirement. This is the pattern Microsoft recommends for large-scale, code-heavy transformations.

---

**Q32. Correct: C**

A Lakehouse SQL analytics endpoint is read-only, so it cannot serve the gold layer's write requirements. A Warehouse item supports full read-write T-SQL (INSERT/UPDATE/MERGE). Populating the Warehouse from lakehouse silver tables (via pipeline, notebook write, or cross-item query) is the standard pattern for teams needing both Spark transforms and T-SQL writes on the same underlying OneLake data.

---

**Q33. Correct: C**

OPTIMIZE ... ZORDER BY co-locates rows with similar CustomerID values within the same files, which improves data skipping and predicate pushdown for queries filtered on that column — this is the correct compaction/clustering technique for Delta tables in Fabric, complementary to the default V-Order writer optimization.

---

**Q34. Correct: D**

Calculated columns (and calculated tables) require row-by-row DAX evaluation that Direct Lake's columnar OneLake reading engine doesn't support, so any such objects force the engine to fall back to DirectQuery for the affected queries.

---

**Q35. Correct: A**

Calculation items support a Format String Expression property that lets each item dynamically override the display format of any measure it's applied to — exactly the pattern used for switching a ratio result to percentage format without touching the base measure.

---

**Q36. Correct: C**

The 'Large semantic model storage format' setting removes the default dataset size limit and is only available for models hosted in workspaces on Fabric (or Premium) capacities such as F64 — exactly the situation described.

---

**Q37. Correct: D**

Incremental refresh policies with RangeStart/RangeEnd apply to tables that are actually loaded into the model (Import mode, including the Import partitions of hybrid tables). They define how Power Query partitions and refreshes data on a schedule.

---

**Q38. Correct: B**

Dual storage mode lets small dimension tables be cached in memory (like Import) for fast, local filtering while still being usable in DirectQuery queries against the live fact table — the standard composite-model pattern for this exact scenario.

---

**Q39. Correct: B**

When a Direct Lake table exceeds capacity guardrails and Fallback Behavior is set to Automatic, Fabric silently falls back to DirectQuery for queries against that specific table so the report keeps working, while unaffected tables remain in Direct Lake mode.

---

**Q40. Correct: D**

Power BI requires two Power Query parameters named exactly RangeStart and RangeEnd, typed as Date/Time (or Date), used in a filter step on the table, before the Incremental Refresh configuration dialog becomes available.

---

**Q41. Correct: A**

When a user belongs to multiple RLS roles, Power BI and Fabric apply an OR (union) logic across the roles' filters. Since SalesManager has no filter, it permits all rows, so the union with SalesEast still results in the user seeing all rows.

---

**Q42. Correct: B**

Dual storage mode lets the engine cache the table like Import for performance when combined with Import tables, while still allowing the engine to push queries to the source (like DirectQuery) when joined with DirectQuery fact tables from different sources, satisfying both scenarios simultaneously.

---

**Q43. Correct: B**

When a model has multiple calculation groups, each calculation group table must have a unique Precedence value. Fabric/Power BI will raise a validation error if two calculation groups in the same model share the same Precedence value.

---

**Q44. Correct: D**

The full DateTime column has extremely high cardinality (near one distinct value per row due to milliseconds), which prevents effective Vertipaq compression. Removing the unused Time component and keeping only Date drastically reduces cardinality, enabling far better run-length and value encoding and shrinking the table's memory footprint.

---

