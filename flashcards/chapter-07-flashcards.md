## Chapter 7: T-SQL and the SQL Analytics Endpoint — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Does the SQL analytics endpoint support INSERT/UPDATE/DELETE on lakehouse tables? | No — it is read-only. Writes must go through Spark/Dataflows. Exam tip: DML and stored procedures exist only in Fabric Warehouse. |
| 2 | Which Fabric item supports CREATE PROCEDURE? | Warehouse only. The lakehouse SQL analytics endpoint does not support stored procedures. Exam tip: 'encapsulated transformation logic' = Warehouse. |
| 3 | How do you force the SQL analytics endpoint to reflect new Delta table changes immediately? | Manually trigger 'Refresh' in the workspace UI instead of waiting for automatic metadata sync. Watch for scenarios where analysts see stale data right after a Spark write. |
| 4 | Can you query a lakehouse and a warehouse together in one T-SQL query? | Yes, using three-part naming (ItemName.schema.table), as long as both are in the same workspace. Cross-workspace direct queries are NOT supported. |
| 5 | Best T-SQL construct to replace a self-join for running totals or rankings? | Window functions: SUM(x) OVER (PARTITION BY ... ORDER BY ...), ROW_NUMBER(), RANK(). Exam favors window functions over self-joins/subqueries for performance. |
| 6 | What object provides reusable, read-only filtered/aggregated logic queryable by BI tools via the SQL analytics endpoint? | A VIEW (CREATE VIEW). Supported on both the lakehouse SQL analytics endpoint and Warehouse. |
| 7 | What should you check when a Warehouse query shows poor cardinality estimates after a large bulk load? | Statistics — run CREATE STATISTICS / UPDATE STATISTICS on filter and join columns; the optimizer may need refreshed stats after bulk loads. |
| 8 | Does Fabric Warehouse support multi-statement transactions? | Yes — BEGIN TRAN/COMMIT/ROLLBACK with full DML and stored procedures. The SQL analytics endpoint does not support this. |
| 9 | Which JOIN returns matched rows plus unmatched rows from both sides? | FULL OUTER JOIN. Exam tests distinguishing INNER vs LEFT vs RIGHT vs FULL OUTER results against sample data sets. |
| 10 | Why does SQL analytics endpoint metadata sometimes appear out of sync right after Spark writes? | Automatic metadata sync has inherent latency, worsened by frequent small-file writes. Known gotcha — pipelines may need an explicit refresh/wait step. |
| 11 | Which window function assigns a unique sequential integer per partition, useful for de-duplication? | ROW_NUMBER() OVER (PARTITION BY col ORDER BY col). Common pattern: CTE + WHERE rn = 1 to remove duplicates. |
| 12 | Which Fabric SQL surface auto-generates its schema from Delta tables with no explicit CREATE TABLE needed? | The SQL analytics endpoint — it automatically reflects lakehouse Delta tables. Warehouse tables must be explicitly created/managed via T-SQL. |
