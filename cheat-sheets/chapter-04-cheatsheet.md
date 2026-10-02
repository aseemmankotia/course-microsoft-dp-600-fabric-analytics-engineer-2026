# Chapter 4 Cheat Sheet — Ingestion Foundations

## Domain
Prepare data (45-50%) — heavily tested: Dataflow Gen2 vs pipeline selection, OneLake shortcuts, pipeline activities/triggers

## Tool Selection Matrix
| Requirement | Best Tool |
|---|---|
| GUI joins/merges/unpivot, no code | Dataflow Gen2 |
| Bulk move data, minimal/no transform | Pipeline Copy activity |
| Orchestration, branching, notifications, stored procs | Data pipeline |
| Custom Python/Spark, ML feature engineering, large-scale control | Notebook (PySpark) |
| Reference external/other-workspace data w/o copying | OneLake shortcut |

## OneLake Shortcuts
| Type | Points To | Copies Data? |
|---|---|---|
| Internal | Another Lakehouse/Warehouse/workspace inside OneLake | No |
| External | ADLS Gen2, Amazon S3, S3-compatible, Google Cloud Storage, Dataverse | No |

- Shortcuts are virtual references — physical data stays at source.
- No duplicate storage cost; billed for read/compute only.
- Appear in Lakehouse Explorer as native folders/tables.

## Dataflow Gen2 Essentials
- Engine: Power Query Online (M language), low-code.
- Default: stages data internally (Lakehouse-backed) before loading destination → consumes Fabric CUs.
- **Fast Copy**: accelerates bulk data movement for large sources, bypasses row-by-row processing.
- **Incremental refresh**: requires `RangeStart` / `RangeEnd` parameters (Date/DateTime type) bound to a source filter step; only reprocesses the changed window.
- Generally consumes more CU than an equivalent Copy activity — prefer Copy activity for simple move-only scenarios.

## Data Pipeline Essentials
- **Copy activity**: moves data between 30+ connectors, supports column mapping, no complex transform logic.
- **Orchestration activities**: If Condition, ForEach, Invoke Pipeline, Stored Procedure, Web/Notification activities.
- **Triggers**:
  - Schedule trigger — recurring, time-based (e.g., daily at 2 AM).
  - On-demand — manual run.
  - Invoke Pipeline activity — chains pipelines together (not itself a trigger type).

## Common Exam Traps
- Choosing Copy activity when the scenario requires actual transformation logic (joins/dedup) → should be Dataflow Gen2.
- Assuming shortcuts copy or sync data — they do not; data remains at source.
- Forgetting incremental refresh requires Date/DateTime-typed RangeStart/RangeEnd parameters, not Text.
- Confusing 'On-demand run' with a scheduling mechanism — it is manual, not automated.
- Picking Dataflow Gen2 for large-scale custom Python/ML workloads — that's a Notebook use case.
