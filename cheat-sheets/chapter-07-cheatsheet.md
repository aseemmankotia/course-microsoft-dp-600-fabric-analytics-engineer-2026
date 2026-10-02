# Chapter 7 Cheat Sheet: T-SQL & SQL Analytics Endpoint

## SQL Analytics Endpoint vs Warehouse
| Feature | SQL Analytics Endpoint (Lakehouse) | Warehouse |
|---|---|---|
| Access mode | Read-only | Read-write |
| DML (INSERT/UPDATE/DELETE) | No | Yes |
| Stored procedures | No | Yes |
| Views | Yes | Yes |
| Schema creation | Auto-generated from Delta tables | Explicit CREATE TABLE |
| Transactions | N/A | BEGIN TRAN/COMMIT/ROLLBACK |
| Underlying storage | Delta Parquet in OneLake | Delta Parquet in OneLake |

## Metadata Refresh Behavior (Heavily Tested)
- Lakehouse writes (Spark, pipelines) don't appear on the SQL analytics endpoint instantly — sync has latency.
- Fix: manually trigger **Refresh** in the workspace item context menu, or build a wait/refresh step into pipelines.
- Gotcha: frequent small-file writes increase sync lag — exam scenario often shows 'analysts see stale data right after ingestion.'

## Cross-Item Querying Rules
- Use **three-part naming**: `ItemName.schema.table`
- Works between lakehouse ↔ warehouse **in the same workspace only**
- No gateway needed; both share the SQL engine over OneLake
- Cross-**workspace** direct queries are NOT supported (need shortcuts/mirroring instead)

## Views & Stored Procedures
- Views: reusable read-only logic; valid in both SQL analytics endpoint and Warehouse
- Stored procedures: **Warehouse only** — used to encapsulate multi-step, parameterized, transactional transformation logic

## Window Functions Quick Reference
| Function | Use Case |
|---|---|
| `ROW_NUMBER() OVER (PARTITION BY... ORDER BY...)` | Unique rank, dedup pattern |
| `RANK() / DENSE_RANK()` | Ranking with/without gaps |
| `SUM()/AVG() OVER (...)` | Running totals, moving averages |
| `LAG()/LEAD()` | Prior/next row comparison |

**Exam tip:** replace self-joins/correlated subqueries with window functions for performance.

## Performance & Statistics
- Query optimizer depends on **statistics** for cardinality estimates.
- After large bulk loads: run `CREATE STATISTICS` / `UPDATE STATISTICS` on join/filter columns if plans look off.
- Warehouse tables use Delta/Parquet — no traditional clustered columnstore index management like dedicated SQL pools.
- Avoid `SELECT *`; filter early; prefer set-based operations over cursors/loops.

## Common Exam Traps
1. Assuming SQL analytics endpoint supports stored procedures (it does not).
2. Forgetting metadata refresh delay after Spark writes.
3. Assuming cross-item queries work across workspaces without shortcuts.
4. Choosing self-joins over window functions for running totals/rankings.
