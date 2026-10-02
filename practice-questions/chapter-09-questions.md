## Chapter 9: Star-Schema Modeling & Copilot in Fabric for Data Prep — Practice Questions

**Q1.** A data engineer is designing a semantic model for sales data. The source system's Customer table uses CustomerID as a natural key that occasionally gets reused after 5 years due to archiving policies. Which design approach should the engineer use for the Customer dimension table?

A) Use CustomerID directly as the primary key in the dimension table
B) Create a surrogate key column and use it as the primary key, keeping CustomerID as a regular attribute
C) Concatenate CustomerID with the row's load date to create a unique key
D) Store customer data directly in the fact table to avoid the join

<details>
<summary>Answer</summary>

**Correct: B**

Surrogate keys are system-generated and independent of the source system, avoiding uniqueness violations when natural keys are reused, and supporting SCD Type 2 history.

**Why the others are wrong:**
- Reusing the natural key directly will eventually cause duplicate key/referential integrity errors when CustomerID is reused
- Concatenating with load date is a workaround that doesn't scale and breaks standard SCD Type 2 patterns
- Storing customer attributes directly in the fact table violates star schema design and causes massive data duplication

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A developer asks Copilot in a Fabric notebook to write PySpark code that calculates total revenue by region from a DataFrame named sales_df. Copilot generates code that groups by 'Region' and sums a column named 'Revenue'. Before running this code in production, what should the developer do first?

A) Deploy the code immediately since Copilot output is pre-validated against the workspace schema
B) Ask Copilot to rewrite the same logic in T-SQL for a second opinion
C) Discard the code and write it manually because Copilot cannot generate PySpark reliably
D) Verify that the columns 'Region' and 'Revenue' actually exist in sales_df and match the intended business definition of revenue

<details>
<summary>Answer</summary>

**Correct: D**

Copilot does not validate its suggestions against your live schema or business rules; the developer must confirm column names exist and that 'revenue' matches the correct business calculation before use.

**Why the others are wrong:**
- Copilot does not automatically validate output against your actual schema or logic
- Rewriting in another language does nothing to address the validation gap
- Copilot can generate correct PySpark; the issue is verification, not capability

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A team is modeling a data warehouse in Fabric for a Power BI report with strict sub-second query performance requirements. The Product dimension could be normalized into Product, Category, and Subcategory tables (snowflake) or flattened into a single Product dimension table (star). Which approach should the team choose and why?

A) Snowflake schema, because normalization always reduces storage and improves performance
B) Snowflake schema, because Power BI relationships require fully normalized tables
C) Either approach performs identically since VertiPaq compresses all tables equally
D) Star schema, because fewer joins and denormalized dimensions generally perform better with VertiPaq

<details>
<summary>Answer</summary>

**Correct: D**

Star schema denormalizes dimensions into a single flat table, reducing joins and generally improving VertiPaq query performance for BI workloads.

**Why the others are wrong:**
- Normalization can reduce storage but the tradeoff is more joins, which hurts query performance — 'always' is false
- Power BI has no requirement for normalized tables; star schema is the recommended pattern
- Join complexity differs between schemas, so performance is not identical

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A data engineer needs help generating a T-SQL query to transform data in a Fabric Warehouse. Which Fabric experience provides Copilot assistance directly in the query editor for this purpose?

A) Copilot in Power BI Desktop
B) Copilot in Dataflows Gen2 only
C) Copilot in the Fabric Data Warehouse SQL query editor
D) Copilot in Data Activator

<details>
<summary>Answer</summary>

**Correct: C**

Copilot in the Fabric Warehouse SQL query editor assists with generating and explaining T-SQL directly against warehouse tables.

**Why the others are wrong:**
- Power BI Desktop Copilot focuses on DAX, quick measures, and report narratives, not T-SQL
- Dataflows Gen2 Copilot generates Power Query M code, not T-SQL
- Data Activator's Copilot capabilities relate to reflex triggers/alerts, not SQL transformation code

</details>

---

**Q5.** An analyst wants Copilot to help write a DAX measure that calculates year-over-year sales growth in a Power BI semantic model. Which Copilot experience should the analyst use?

A) Copilot in Dataflows Gen2
B) Copilot in a Spark notebook
C) Copilot in Data Activator
D) Copilot in Power BI (semantic model/Desktop) for quick measures and DAX generation

<details>
<summary>Answer</summary>

**Correct: D**

Copilot in Power BI generates DAX measures and quick measures from natural language descriptions within the semantic model.

**Why the others are wrong:**
- Dataflows Gen2 Copilot produces M/Power Query code, not DAX
- Spark notebook Copilot produces PySpark/Scala/SQL code, not DAX
- Data Activator is unrelated to DAX measure generation

</details>

---

**Q6.** Which prompt to Copilot in a Fabric notebook is MOST likely to generate accurate, usable PySpark code on the first attempt?

A) "Fix my data"
B) "Make this better"
C) "Write code to remove rows in sales_df where 'OrderDate' is null and cast 'Quantity' to an integer type"
D) "Optimize performance"

<details>
<summary>Answer</summary>

**Correct: C**

Specific prompts referencing exact DataFrame and column names with a clearly stated operation produce accurate, targeted code from Copilot.

**Why the others are wrong:**
- Vague prompts with no column or operation context produce generic, likely incorrect output
- "Make this better" gives Copilot no concrete target to act on
- "Optimize performance" lacks specificity about what to optimize or which columns/operations are involved

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** In a Fabric semantic model following star schema design, what is the correct relationship cardinality and cross-filter direction between the Date dimension table and the Sales fact table?

A) One-to-many, single direction from Date to Sales
B) Many-to-many, bidirectional
C) Many-to-one, bidirectional
D) One-to-one, single direction from Sales to Date

<details>
<summary>Answer</summary>

**Correct: A**

The standard star schema pattern is one dimension row filtering many fact rows, with single-direction cross-filtering from dimension to fact.

**Why the others are wrong:**
- Many-to-many is not appropriate for a standard dimension-to-fact relationship and risks ambiguous filtering
- Bidirectional filtering between fact and dimension can create ambiguous filter propagation and hurt performance in larger models
- A one-to-one relationship is incorrect since a fact table has many rows per single dimension value

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement correctly differentiates a fact table from a dimension table in a star schema?

A) Fact tables contain descriptive text attributes while dimension tables contain only numeric measures
B) Dimension tables always have more rows than fact tables
C) Fact tables and dimension tables are interchangeable and the distinction only affects table naming
D) Fact tables store measurable, quantitative business events at a defined grain along with foreign keys, while dimension tables store descriptive attributes used to filter and group those events

<details>
<summary>Answer</summary>

**Correct: D**

This is the standard Kimball definition: fact tables hold measures and foreign keys at a specific grain, dimensions hold descriptive attributes for filtering/grouping.

**Why the others are wrong:**
- This reverses the actual roles of fact and dimension tables
- Fact tables typically have far more rows than dimension tables, not fewer
- The distinction is functional and structural, not merely naming

</details>

---

