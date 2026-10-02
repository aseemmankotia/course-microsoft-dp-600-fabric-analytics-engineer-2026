# Chapter 10 Cheat Sheet: Storage Modes

## Domain
Implement and manage semantic models (25–30%). Heavily tested: Direct Lake fallback behavior, Import vs DirectQuery tradeoffs, framing/refresh.

## Mode Comparison

| Mode | Data Location | Freshness | Query Speed | Refresh Needed? |
|---|---|---|---|---|
| Import | Vertipaq (in-memory copy) | As of last refresh | Fastest | Yes, scheduled |
| DirectQuery | Stays in source | Always live | Depends on source, higher latency | No (query-time) |
| Direct Lake | Read directly from OneLake Delta files | Near-live via reframing | Near in-memory speed | Reframing, not full copy |

## Direct Lake Fallback Triggers
- Calculated columns / calculated tables referenced
- Table exceeds row group / file guardrails (~1,000 row groups)
- Querying views instead of native Delta tables
- `Direct Lake behavior` property set to `DirectQuery`
- Unsupported query constructs

## Direct Lake Behavior Property Values
| Value | Effect |
|---|---|
| Automatic (default) | Falls back silently to DirectQuery when needed |
| DirectLakeOnly | No fallback — errors instead (useful for diagnosing) |
| DirectQuery | Forces DirectQuery for all queries |

## Framing
- Framing = mapping model columns to a specific consistent version of OneLake Parquet files.
- New Lakehouse data is NOT visible until reframing occurs (scheduled refresh, manual refresh, or API/pipeline trigger).
- Reframing is lightweight vs Import's full data copy.

## Import Mode Refresh Limits
| Capacity | Scheduled refreshes/day |
|---|---|
| Pro / Shared | 8 |
| Premium / Fabric | 48 |

## DirectQuery Notes
- Default max rows returned per query: 1,000,000 (Max Intermediate Row Set Count) — raising this hurts performance, not recommended.
- Use aggregation tables (Import) over DirectQuery detail tables to cache common query results and reduce source load.

## Composite / Hybrid Models
- Mix storage modes per table in one model: e.g., Direct Lake fact + DirectQuery live dimension + Import reference table.
- `Dual` storage mode: table can serve as Import or DirectQuery depending on query context — common for shared dimensions.

## Capacity & Performance
- Direct Lake requires a Fabric capacity (F SKU); not available without capacity.
- Guardrails (row/file limits before fallback) scale with SKU size — larger SKUs tolerate larger tables before fallback risk increases.
- V-Order optimization on Delta tables improves Direct Lake read performance and reduces row group count, lowering fallback likelihood.

## Exam Traps
- Assuming Direct Lake behaves like Import (no — no explicit copy/refresh step, uses framing).
- Forgetting calculated columns/tables break Direct Lake for that table.
- Confusing DirectLakeOnly (errors on fallback) with DirectQuery (forces live query mode).
- Assuming Pro capacity supports Direct Lake — it requires Fabric capacity.
