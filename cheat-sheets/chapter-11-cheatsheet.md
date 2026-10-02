# Chapter 11 Cheat Sheet: DAX, Calc Groups, Performance, Security

## Context Transition Rules
| Trigger | Causes Context Transition? |
|---|---|
| Measure reference inside row context (iterator, calc column) | Yes (implicit CALCULATE) |
| CALCULATE / CALCULATETABLE | Yes |
| FILTER (used as argument only) | No |
| ALL / ALLEXCEPT / ALLSELECTED (filter modifiers) | No (they modify filter context, don't create it) |

**Rule of thumb:** if you see a measure evaluated where a row context exists, assume implicit CALCULATE wraps it.

## Calculation Groups
- One calculation group table per grouping concept (e.g., "Time Intelligence").
- Calculation items = reusable formulas (YTD, QTD, PY) applied to any base measure.
- `Precedence` property resolves conflicts when multiple calc groups apply.
- Use `SELECTEDMEASURE()` inside calculation items to reference whichever measure is on the visual.
- Built natively in Power BI Desktop model view (no Tabular Editor required as of recent releases).

## Aggregations (Composite Models)
| Layer | Mode | Purpose |
|---|---|---|
| Aggregation table | Import | Fast, pre-summarized (e.g., by month/region) |
| Detail fact table | DirectQuery | Handles drillthrough / unmatched granularity |

- Configure via **Manage Aggregations**: map GroupBy columns and Sum/Count/Min/Max per column.
- Queries auto-route to aggregation table when the visual's grain matches; else fallback to DirectQuery.

## Incremental Refresh
- Requires parameters named exactly **RangeStart** / **RangeEnd** (datetime type).
- Policy = "Store rows in last N [years/months/days]" + "Refresh rows in last N [days]".
- Optional: **Detect data changes** (needs a modified-date column) to skip unchanged partitions.
- Only works fully in Import mode (hybrid tables allow a DirectQuery "real-time" partition on top).

## Vertipaq Optimization
| Factor | Impact |
|---|---|
| High column cardinality | Larger dictionary, worse compression |
| Sorted, low-cardinality columns | Better RLE compression |
| Unused high-cardinality columns (GUIDs, IDs) | Remove — no analytical value, wastes memory |
| Calculated columns | Stored like regular columns — no special compression benefit |
| Data type choice | Integers compress better than text/decimals for high-volume columns |

Use **VertiPaq Analyzer** / **Model Metrics** view to identify largest columns by size.

## Security
| Feature | Grain | Config Location |
|---|---|---|
| RLS (dynamic) | Rows, per logged-in user via USERPRINCIPALNAME() | Power BI Desktop → Manage Roles |
| RLS (static) | Rows, hardcoded per role | Power BI Desktop → Manage Roles |
| OLS | Tables/Columns hidden entirely | Tabular Editor |

Test with **View As Roles** before publishing.

## Copilot for DAX
- Generates candidate DAX from model metadata (table/column/relationship names).
- Always requires human review before accepting — not guaranteed business-logic correct.
- Available in DAX query view / Copilot pane in Fabric-enabled workspaces.
