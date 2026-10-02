## Lakehouse vs Warehouse Cheat Sheet

### Structural Comparison
| Feature | Lakehouse | Warehouse |
|---|---|---|
| Data areas | Files (any format) + Tables (Delta) | Tables only (Delta, T-SQL managed) |
| Primary engine | Spark (notebooks, Spark SQL) | Full T-SQL relational engine |
| Write access via T-SQL | ❌ Read-only (SQL analytics endpoint) | ✅ Full DDL/DML (INSERT/UPDATE/DELETE/MERGE) |
| Write access via Spark/notebooks | ✅ Yes | ❌ No native Spark engine |
| Stored procedures | ❌ Not supported | ✅ Supported |
| Multi-table transactions | Table-level Delta ACID only | Full multi-table T-SQL transactions |
| Best for | Data engineers, ML, unstructured/semi-structured data | SQL-first BI teams, governed relational modeling |
| Underlying format | Delta Parquet | Delta Parquet |
| Storage layer | OneLake | OneLake |

### The Two Endpoints
- **SQL analytics endpoint (Lakehouse)**: auto-generated the instant Tables exist; **read-only**; exposes only the Tables area, not Files.
- **Warehouse T-SQL endpoint**: full read-write relational engine; supports schemas, stored procs, views, multi-table transactions.
- Both endpoints are queried with T-SQL and both are readable by Power BI / cross-item queries — the difference is **write capability**.

### Decision Rule
- Need Spark, notebooks, ML, raw/unstructured files → **Lakehouse**
- Need governed T-SQL writes, stored procedures, strict relational modeling → **Warehouse**
- Need both → build Lakehouse for ingestion/engineering, curate into Warehouse for BI, or query across both.

### Cross-Item Querying
- Warehouse can query Lakehouse tables (and vice versa via SQL analytics endpoint) using **three-part naming**: `ItemName.SchemaName.TableName`.
- Works because both items store data as Delta Parquet on **OneLake** — no data copy or ETL job required for cross-querying.

### OneLake Essentials
- Single, tenant-wide storage layer under every Fabric item.
- **OneCopy** principle: one physical copy of Delta data can be referenced by multiple items via **shortcuts**, avoiding duplication.
- Enables the SQL analytics endpoint, Warehouse, Power BI, and Spark to all read the same physical files.

### Common Exam Traps
1. Assuming SQL analytics endpoint write failures are permission issues — they are **read-only by design**.
2. Forgetting raw Files in a Lakehouse are **not** queryable via SQL until moved/converted into Tables.
3. Choosing Lakehouse for a team that explicitly needs stored procedures and multi-table transactional writes — that's a **Warehouse** requirement.
