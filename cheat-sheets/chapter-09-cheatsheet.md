## Star Schema & Copilot in Fabric — Cheat Sheet

### Fact vs Dimension Tables
| Aspect | Fact Table | Dimension Table |
|---|---|---|
| Contains | Measures + foreign keys | Descriptive attributes |
| Row count | Very high | Lower |
| Key type | Composite FK to dimensions | Surrogate key (PK) |
| Grain | Defined FIRST, one row = one event | N/A |
| Example | SalesFact (OrderID, ProductKey, DateKey, Amount) | DimProduct, DimCustomer, DimDate |

### Surrogate Keys — Why Use Them
- System-generated integer, independent of source natural key
- Solves: natural key reuse, NULL business keys, SCD Type 2 history tracking
- Never expose surrogate key as business-meaningful

### Star vs Snowflake
| Factor | Star Schema | Snowflake Schema |
|---|---|---|
| Dimension structure | Denormalized (flat) | Normalized (split into sub-tables) |
| Joins needed | Fewer | More |
| Storage | More redundancy | Less redundancy |
| Query performance (VertiPaq) | Generally better | Generally worse |
| Recommended in Fabric/Power BI | Yes (default best practice) | Only when strongly justified |

### Relationship Config Best Practice
- Cardinality: One (dimension) to Many (fact)
- Cross-filter direction: Single, dimension → fact
- Avoid bidirectional unless solving specific many-to-many/bridge table scenario

### Copilot in Fabric — Where to Use What
| Task | Copilot Location | Output Language |
|---|---|---|
| Data transformation logic in notebook | Fabric Notebook Copilot | PySpark / Python / SQL |
| Query building/transform steps | Dataflows Gen2 Copilot | Power Query M |
| Warehouse queries | Warehouse SQL editor Copilot | T-SQL |
| Measures/report logic | Power BI Desktop/semantic model Copilot | DAX |

### Effective Prompting Rules
- Reference EXACT table/column/DataFrame names
- State the specific operation (filter, join, cast, aggregate)
- Avoid vague asks: "fix my data", "optimize this", "make it better"
- Iterate: refine prompt if output references non-existent columns

### Validating Copilot Output — Checklist
1. Do referenced columns/tables actually exist in the schema?
2. Does the aggregation/logic match the actual business definition (not just a plausible guess)?
3. Does the DAX respect existing relationships and filter context correctly?
4. Re-run/test output against known sample data before trusting results

### Limits of Copilot (Exam Focus)
- Cannot know business rules not stated in the prompt (e.g., definition of "active customer")
- Cannot guarantee correct grain selection — that's a modeling decision
- Cannot validate itself against live schema — human review required
- Copilot accelerates code generation; it does NOT replace domain expertise or QA
