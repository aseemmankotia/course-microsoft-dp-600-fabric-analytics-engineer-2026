## Chapter 8: Real-Time Intelligence: KQL for Streaming Data — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Power BI import-mode dataset scheduled refresh limits: Pro capacity vs Premium/Fabric capacity? | Pro: up to 8 refreshes/day. Premium/Fabric capacity: up to 48 refreshes/day. Exam tip: Real-Time dashboards on a KQL database bypass this limit entirely since they query live streaming data. |
| 2 | When does Real-Time Intelligence (Eventstream + KQL database) fit better than Lakehouse-based batch ingestion? | When data is high-velocity/continuous (IoT, logs, telemetry) and needs near-instant querying or alerting. Lakehouse batch fits scheduled, larger-volume, less time-sensitive data. Exam tip: 'seconds of latency' or 'continuous stream' points to Real-Time Intelligence. |
| 3 | Eventstream vs Data pipeline — which handles continuous streaming ingestion? | Eventstream. Data pipelines are for scheduled/batch orchestration (Copy, Dataflow, Notebook activities). Exam tip: 'streaming source' keyword = Eventstream. |
| 4 | Real-Time dashboard vs Power BI report on the same KQL database — which is best for sub-minute operational monitoring? | Real-Time dashboard — built directly on KQL queries with near-instant auto-refresh. Power BI report is better for polished, scheduled business reporting with richer formatting/visual options. |
| 5 | KQL: keep only specific columns, optionally renamed/computed? | project ColumnName, NewName=Expression — drops all other columns. Exam tip: project = SELECT-like; extend = ADD a column. |
| 6 | KQL: add a new computed column while keeping all existing columns? | extend NewCol = Expression. Unlike project, extend does not remove any existing columns. |
| 7 | KQL: aggregate rows into groups? | summarize count(), avg(Value) by DeviceId, bin(Timestamp, 5m). Exam tip: bin() is paired with summarize for time-window aggregation. |
| 8 | KQL: filter rows by condition? | where clause, e.g. where Timestamp > ago(1h). Exam tip: where should immediately follow the table name or a prior pipe operator for correct filtering order. |
| 9 | What is an Eventhouse in Fabric Real-Time Intelligence? | The workspace item/container that hosts one or more KQL databases, providing the compute for ingesting and querying event/time-series data. |
| 10 | Purpose of Real-Time hub in Fabric? | A centralized catalog to discover, preview, and connect to streaming data sources (Eventstreams, Fabric events, Azure sources) across the tenant — it is not itself a query or ingestion engine. |
| 11 | What destinations can a single Eventstream route data to? | KQL Database/Eventhouse, Lakehouse, Reflex (Data Activator), and custom endpoints. Exam tip: one Eventstream can fan-out to multiple destinations simultaneously. |
| 12 | How can KQL database data be queried from a Spark notebook or Lakehouse without duplicating storage? | Enable 'OneLake availability' on the KQL table — the data is automatically mirrored into OneLake in Delta Parquet format and accessed via a shortcut. Exam tip: this bridges Real-Time Intelligence and Lakehouse without building separate ETL. |
