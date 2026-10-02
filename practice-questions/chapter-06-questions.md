## Chapter 6: Transforming Data with Notebooks and PySpark — Practice Questions

**Q1.** A data engineer's notebook performs a shuffle-heavy join across 500GB of Delta tables and repeatedly runs out of executor memory on the Starter pool. Which configuration BEST resolves this while controlling Capacity Unit consumption?

A) Keep the Starter pool but reduce the number of partitions in the DataFrame
B) Switch to a custom Spark pool with Large or X-Large nodes and enable autoscale
C) Increase the notebook's session timeout value in workspace settings
D) Split the notebook into two notebooks run sequentially by a pipeline

<details>
<summary>Answer</summary>

**Correct: B**

Shuffle-heavy jobs need more executor memory and cores; a custom pool with larger node sizes and autoscale right-sizes compute for the workload without over-provisioning idle capacity.

**Why the others are wrong:**
- Reducing partitions on undersized nodes doesn't add memory per executor and can worsen skew
- Session timeout controls idle release, not per-job memory available for shuffles
- Splitting notebooks doesn't change the underlying node size or memory available per executor

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A pipeline must run the same notebook once per region, passing a different 'RegionCode' value each run. What must the engineer configure for this to work?

A) Hardcode each region value in a copy of the notebook per region
B) Mark a cell as the parameters cell and set 'RegionCode' in the Notebook activity's Base parameters
C) Use notebookutils.fs.mount to bind the region value to storage
D) Add a %%sql magic cell that queries the region from a lookup table

<details>
<summary>Answer</summary>

**Correct: B**

Fabric notebooks accept external values only through a designated parameters cell; the pipeline Notebook activity injects matching variable names via Base parameters.

**Why the others are wrong:**
- Duplicating notebooks per region is unmaintainable and not how the platform is designed to work
- notebookutils.fs.mount is for binding storage paths, not passing scalar parameters
- %%sql cells query data but cannot receive pipeline-supplied parameter values on their own

</details>

---

**Q3.** A notebook has LakehouseA attached as its default lakehouse. Which code reads the 'Sales' Delta table WITHOUT specifying a full ABFSS path?

A) spark.read.csv("Sales")
B) spark.read.table("Sales")
C) notebookutils.fs.ls("Sales")
D) spark.read.format("delta").load("abfss://container@account.dfs.core.windows.net/Sales")

<details>
<summary>Answer</summary>

**Correct: B**

When a lakehouse is attached as default, managed Delta tables are addressable by name alone via spark.read.table(), no path required.

**Why the others are wrong:**
- read.csv expects a file path and format, not a managed table name, and is the wrong reader for a Delta table
- notebookutils.fs.ls lists directory contents; it does not load data into a DataFrame
- This uses a full ABFSS path, which directly contradicts the requirement to avoid specifying the full path

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team wants to quickly query a lakehouse Delta table using familiar SQL syntax in a single cell, without changing the notebook's default PySpark language for the entire notebook. What should they use?

A) Change the notebook's default language setting to SQL
B) Call notebookutils.session.sql() before every PySpark cell
C) Export the table to Power BI and query it there
D) Use a %%sql magic cell

<details>
<summary>Answer</summary>

**Correct: D**

%%sql is a cell-level magic that lets a single cell run Spark SQL against attached lakehouse tables while the rest of the notebook stays in PySpark.

**Why the others are wrong:**
- Changing the notebook default language affects every cell, not just one
- notebookutils.session.sql() is not a valid API for ad hoc SQL querying in Fabric notebooks
- Exporting to Power BI adds unnecessary steps and breaks the in-notebook exploration workflow

</details>

---

**Q5.** Which library should new Fabric notebooks use for file system operations and credential passthrough, replacing the older Synapse-era library?

A) mssparkutils
B) notebookutils
C) pyspark.fs
D) azure.storage.blob

<details>
<summary>Answer</summary>

**Correct: B**

notebookutils is the Fabric-native utility library (fs, credentials, notebook, session submodules) that supersedes mssparkutils.

**Why the others are wrong:**
- mssparkutils is the legacy Synapse library; still usable in some contexts but not the recommended Fabric API
- pyspark.fs is not a real module
- azure.storage.blob is a general Azure SDK, not integrated with lakehouse-relative paths or session context

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** By default, an idle Spark session on a Fabric Starter pool ends after how many minutes, and where is this changed?

A) 20 minutes; configured in the Environment item's Spark compute settings
B) 60 minutes; configured in Workspace settings
C) 10 minutes; configured in notebook properties
D) Sessions never time out unless the capacity is paused

<details>
<summary>Answer</summary>

**Correct: A**

Starter pools default to a 20-minute idle session timeout, adjustable via the Spark compute configuration in an Environment item attached to the notebook.

**Why the others are wrong:**
- 60 minutes is not the Starter pool default
- 10 minutes and notebook properties are not where this setting lives
- Idle sessions do time out independent of capacity pause state, to release Spark compute

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A workspace runs on F32 capacity, and Copilot options in notebooks appear unavailable to users. What is the most likely cause?

A) Copilot requires a Power BI Premium Per User license
B) Copilot only works with custom Spark pools, not Starter pools
C) Copilot requires F64 capacity or higher (or a Fabric trial capacity)
D) Copilot is disabled because no default lakehouse is attached

<details>
<summary>Answer</summary>

**Correct: C**

Copilot features in Fabric notebooks require a minimum F64 capacity SKU or a Fabric trial capacity; lower SKUs like F32 do not expose Copilot.

**Why the others are wrong:**
- Copilot licensing is tied to Fabric capacity SKU, not Power BI Premium Per User
- Copilot works regardless of Starter vs custom pool selection
- Lakehouse attachment affects table access, not Copilot availability

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the primary purpose of attaching a default lakehouse to a Fabric notebook?

A) It is required before any PySpark code can execute
B) It automatically converts all CSV files in the lakehouse to Delta format
C) It enables relative Tables/Files path access without specifying full storage paths
D) It grants the notebook admin permissions over the workspace

<details>
<summary>Answer</summary>

**Correct: C**

A default lakehouse gives the notebook a resolvable root context so code can reference Tables/ and Files/ by relative name instead of full ABFSS URIs.

**Why the others are wrong:**
- PySpark code can run without any lakehouse attached, e.g. against external paths
- Attaching a lakehouse does not trigger any automatic file format conversion
- Lakehouse attachment is a data-access convenience, unrelated to workspace-level permissions

</details>

---

