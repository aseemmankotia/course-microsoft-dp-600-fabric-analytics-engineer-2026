# Real-Time Intelligence Cheat Sheet

## Core Pipeline Flow
`Streaming Source → Eventstream → KQL Database (in an Eventhouse) → Real-Time Dashboard / Power BI Report`

| Item | Role |
|---|---|
| Eventstream | No-code ingestion & routing engine; connects sources (Event Hubs, IoT Hub, Kafka, CDC, custom endpoint) to destinations |
| Eventhouse | Container item hosting one or more KQL databases |
| KQL Database | Stores time-series/event data in tables; queried with KQL |
| Real-Time hub | Tenant-wide catalog to discover/connect to streaming sources (not an ingestion or query engine) |
| Real-Time dashboard | Tiles built directly from KQL queries, near-instant auto-refresh |
| Data Activator (Reflex) | No-code monitoring/alerting on conditions in streaming data |

## Eventstream Destinations (fan-out supported)
- KQL Database / Eventhouse
- Lakehouse
- Reflex (Data Activator)
- Custom endpoint

## Core KQL Operators

| Operator | Purpose | Example |
|---|---|---|
| where | Filter rows | `where Timestamp > ago(1h)` |
| summarize | Aggregate rows into groups | `summarize count() by DeviceId, bin(Timestamp,5m)` |
| project | Select/rename columns (drops others) | `project DeviceId, Val=Value` |
| extend | Add computed column, keeps all others | `extend Celsius = (Value-32)*5/9` |

**Memory trick:** *project* = pick columns, throw rest away. *extend* = keep everything, add one more.

## Real-Time Dashboard vs Power BI Report

| | Real-Time Dashboard | Power BI Report |
|---|---|---|
| Query language | KQL | DAX (semantic model) or DirectQuery/KQL |
| Refresh | Near-instant, live | Scheduled (Import: 8/day Pro, 48/day Premium/Fabric) or DirectQuery |
| Best for | Operational monitoring, alerting | Polished, curated business reporting |
| Formatting/visuals | Limited compared to Power BI | Rich formatting, broad visual library |

## When to Choose Real-Time Intelligence vs Lakehouse Batch

| Scenario clue | Choose |
|---|---|
| Continuous stream, seconds-level latency, alerting | Eventstream + KQL DB + Real-Time dashboard |
| Large volume, scheduled/hourly-or-slower, historical analytics | Lakehouse + Data pipeline/Dataflow Gen2 |
| Need both real-time query AND Spark/SQL joins with historical data | KQL DB with **OneLake availability** enabled (mirrors to Delta in OneLake, no duplicate ETL) |

## Common Exam Traps
- Confusing **Real-Time hub** (discovery/catalog) with **Eventstream** (actual ingestion engine).
- Assuming Power BI DirectQuery is automatically 'real-time' — it still depends on refresh/query triggers, unlike native Real-Time dashboards.
- Using `project` when you meant to keep existing columns plus add one (should use `extend`).
- Forgetting `where` should immediately follow the table/pipe to filter before expensive aggregation for performance.
