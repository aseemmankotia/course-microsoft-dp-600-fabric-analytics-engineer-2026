## Chapter 6 Cheat Sheet: Notebooks & PySpark in Fabric

### Default Lakehouse
| Feature | Behavior |
|---|---|
| Attach default lakehouse | Enables relative `Tables/` and `Files/` access, no full ABFSS path needed |
| Read table | `spark.read.table("TableName")` |
| Read file | `spark.read.format("csv").load("Files/folder/file.csv")` |
| Multiple lakehouses | Only ONE can be default; others added as non-default reference |

### Reading & Writing Delta
```python
df = spark.read.table("Sales")
df.write.format("delta").mode("overwrite").saveAsTable("SalesClean")
df.write.format("delta").mode("append").save("Files/staging/output")
```
Exam note: `saveAsTable` writes a managed table registered in the lakehouse metastore; `.save(path)` writes unmanaged files.

### notebookutils (replaces mssparkutils)
| Submodule | Use |
|---|---|
| `notebookutils.fs` | File ops: ls, mv, cp, mount |
| `notebookutils.credentials` | getSecret, getToken |
| `notebookutils.notebook` | `run()`, `exit()` for chaining/pipeline output |
| `notebookutils.session` | Session/runtime context info |

### %%sql Magic
```sql
%%sql
SELECT Region, SUM(Sales) FROM Sales GROUP BY Region
```
Runs Spark SQL for that cell only; rest of notebook stays in PySpark. Exam trap: switching the whole notebook's default language is unnecessary and disruptive.

### Notebook as Pipeline Activity
- Mark exactly one cell as the **parameters cell**.
- Pipeline Notebook activity → **Base parameters** must match variable names exactly.
- Return values to pipeline: `notebookutils.notebook.exit(value)`.
- Chain notebooks directly: `notebookutils.notebook.run("OtherNotebook", timeoutSeconds, {params})`.

### Spark Pool Sizing
| Node Size | vCores | RAM |
|---|---|---|
| Small | 4 | 32 GB |
| Medium | 8 | 64 GB |
| Large | 16 | 128 GB |
| X-Large | 32 | 256 GB |
| XX-Large | 64 | 512 GB |

- Starter pool: fast start, default 20-min idle session timeout, fixed sizing.
- Custom pool: configurable node size + autoscale, better for heavy shuffles/joins.
- CU consumption = node size × node count × session duration (idle time counts until timeout).

### Copilot in Notebooks
- Requires **F64 capacity or higher** (or Fabric trial capacity).
- Generates PySpark/SQL from natural-language prompts; always review before running.
- Not available on lower SKUs regardless of pool type or lakehouse attachment.

### Common Exam Traps
1. Using full ABFSS path when a relative table name was expected (or vice versa).
2. Forgetting to mark the parameters cell before a pipeline can inject Base parameters.
3. Assuming Copilot is a pool/lakehouse setting rather than a capacity SKU gate.
