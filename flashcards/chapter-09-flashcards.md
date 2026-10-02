## Chapter 9: Star-Schema Modeling & Copilot in Fabric for Data Prep — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | What is a surrogate key? | A system-generated unique identifier (usually an integer) for a dimension row, independent of the source system's natural/business key. Exam tip: used to handle key reuse and SCD Type 2 history. |
| 2 | Fact table vs dimension table — which holds foreign keys and measures? | The fact table holds foreign keys to dimensions plus numeric measures at a defined grain. Exam tip: define the grain FIRST when designing a fact table. |
| 3 | Star schema vs snowflake schema — which is generally preferred in Fabric/Power BI semantic models? | Star schema (denormalized dimensions) — fewer joins and better VertiPaq compression/query performance. Snowflake normalizes dimensions, saving storage but adding join overhead. |
| 4 | Which Fabric experience's Copilot generates Power Query M code from natural language? | Copilot in Dataflows Gen2. Distinguish from notebook Copilot (PySpark) and Power BI Copilot (DAX). |
| 5 | Which Fabric experience's Copilot generates PySpark/Python code? | Copilot in Fabric (Spark) notebooks. It can also explain and help fix errors in existing code. |
| 6 | Which experience's Copilot helps write DAX measures? | Copilot in Power BI Desktop/semantic model — supports quick measures and natural-language measure generation. |
| 7 | What must you ALWAYS do after Copilot generates transformation code or DAX? | Validate the output against the actual schema (real table/column names) and business logic — Copilot can hallucinate column names or misapply aggregation rules. |
| 8 | Can Copilot replace domain/business judgment on the exam? | No. Copilot accelerates code generation but cannot determine correct business definitions (e.g., what counts as 'active customer' or correct grain) — human validation is required. |
| 9 | Recommended relationship cardinality between a dimension and fact table in a star schema? | One-to-many (1 dimension row : many fact rows), single-direction cross-filter from dimension to fact. Use bidirectional filtering sparingly due to ambiguity risk. |
| 10 | What makes a Copilot prompt for PySpark transformation effective? | Reference exact DataFrame/column names and describe the specific operation (filter, cast, join) instead of vague requests like 'clean my data'. Specific prompts yield accurate output. |
| 11 | What defines the 'grain' of a fact table? | The level of detail represented by a single row (e.g., one row per order line item). Grain must be defined before adding measures or foreign keys. |
| 12 | Storage/performance tradeoff of snowflake schema | Snowflake normalizes dimensions into multiple related tables — reduces redundant storage but increases join count, generally hurting BI query performance versus star schema. |
