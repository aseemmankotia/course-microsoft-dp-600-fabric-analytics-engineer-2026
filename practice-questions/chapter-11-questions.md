## Chapter 11: DAX, Calculation Groups, Performance Tuning & Model Security — Practice Questions

**Q1.** A model contains a measure Total Sales = SUM(Sales[Amount]). A report author writes a new measure: Avg Customer Sales = AVERAGEX(Customer, [Total Sales]). Inside the AVERAGEX iterator, why does [Total Sales] return a different value for each customer row even though CALCULATE is never explicitly written?

A) Referencing a measure inside an iterator triggers context transition, wrapping it in an implicit CALCULATE that converts the current row context into filter context
B) AVERAGEX automatically applies RLS filters per row
C) AVERAGEX only works on calculated columns, not measures, so the result is invalid
D) The Customer table has bidirectional relationships that force recalculation

<details>
<summary>Answer</summary>

**Correct: A**

Any measure reference evaluated in a row context (including inside iterators like AVERAGEX/SUMX) automatically undergoes context transition — DAX wraps it in CALCULATE, converting each row into an equivalent single-row filter.

**Why the others are wrong:**
- RLS is applied at query time regardless of iterator use, not the cause of per-row variation here
- Measures are fully valid inside iterators — this is a core exam concept, not an error
- Bidirectional relationships affect filter propagation direction but are not required for context transition to occur

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A finance team maintains 15 near-identical measures: Sales YTD, Sales QTD, Sales MTD, Sales PY, Sales PY YTD, and equivalents for Cost and Margin. Which approach BEST reduces this duplication while keeping the model maintainable?

A) Create a single disconnected slicer table and use SWITCH(TRUE(), ...) inside each of the 15 measures
B) Duplicate the base measures for each time variation and rename them for clarity
C) Build a calculation group with calculation items for YTD, QTD, MTD, and PY, applied to a small set of base measures (Sales, Cost, Margin)
D) Convert all base measures into calculated columns so time filters apply automatically

<details>
<summary>Answer</summary>

**Correct: C**

Calculation groups let you define time-intelligence calculation items once (YTD, QTD, MTD, PY) and apply them to any base measure, collapsing 15 measures into 3 base measures plus 4 reusable calculation items.

**Why the others are wrong:**
- SWITCH(TRUE()) still requires writing separate logic per measure and doesn't scale across Sales/Cost/Margin without repetition
- Duplicating measures is exactly the anti-pattern calculation groups are designed to eliminate
- Calculated columns are row-context values computed at refresh time and cannot dynamically respond to slicer-driven time filters like measures can

</details>

---

**Q3.** A DirectQuery semantic model over a 2-billion-row fact table shows report visuals timing out when users view a monthly sales summary by region. Detailed transaction-level drillthrough is rarely used. Which change BEST improves performance?

A) Switch the entire model to Import mode to cache all 2 billion rows in memory
B) Add more RLS roles to reduce the number of rows returned per user
C) Create an Import-mode aggregation table pre-summarized by month and region, and configure it to be used automatically via aggregation precedence over the DirectQuery detail table
D) Convert all measures to calculated columns to precompute values at refresh time

<details>
<summary>Answer</summary>

**Correct: C**

Aggregation tables let common summarized queries (month/region) hit a small, fast Import-mode table while detail queries fall back to DirectQuery — this is the core composite-model aggregation pattern tested on DP-600.

**Why the others are wrong:**
- Full Import of 2 billion rows may exceed capacity memory limits and isn't necessary when only summary-level queries are slow
- RLS controls data security, not query performance, and doesn't reduce scan size for aggregate queries
- Calculated columns don't aggregate across the fact table and won't help pre-summarized reporting scenarios

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which DAX function, when used to explicitly filter a table inside CALCULATE, does NOT itself cause context transition on the outer row context?

A) CALCULATE
B) ALLEXCEPT
C) FILTER
D) CALCULATETABLE

<details>
<summary>Answer</summary>

**Correct: C**

FILTER is a table function that iterates row-by-row using the existing context but does not itself invoke context transition — it's used as an argument passed into CALCULATE, which is the function that performs context transition.

**Why the others are wrong:**
- CALCULATE always performs context transition, converting row context into filter context when a row context exists
- ALLEXCEPT is a filter modifier commonly used inside CALCULATE and depends on the context transition CALCULATE provides
- CALCULATETABLE behaves like CALCULATE but returns a table — it also performs context transition

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A star-schema table has a Transaction ID column with 40 million unique values and is not used in any relationship or visual. What is the BEST action to reduce Vertipaq storage size?

A) Change the column's data type from text to whole number to improve dictionary encoding
B) Enable bidirectional filtering on the column to allow better compression
C) Convert the column into a calculated column so Vertipaq compresses it separately
D) Remove the column from the model entirely, since high-cardinality columns unused in relationships or analysis inflate dictionary size with no analytical benefit

<details>
<summary>Answer</summary>

**Correct: D**

High-cardinality columns are the primary driver of Vertipaq dictionary size; if a column isn't used for relationships, RLS, or analysis, removing it is the most effective optimization — this is the #1 model-size gotcha tested in DP-600.

**Why the others are wrong:**
- Changing data type helps somewhat but a 40M-row unique-value column still compresses poorly regardless of type — removal is more effective
- Bidirectional filtering has no bearing on column compression and only affects filter propagation
- Calculated columns are stored the same way as regular columns in Vertipaq and don't improve compression by definition alone

</details>

---

**Q6.** An analyst configures incremental refresh on a fact table in Power BI Desktop with 'Store rows in the last 5 years' and 'Refresh rows in the last 10 days.' Which two parameters MUST exist in Power Query for this policy to work?

A) StartDate and EndDate as text parameters
B) RangeStart and RangeEnd as datetime parameters used in the table's filter step
C) MinDate and MaxDate as whole number parameters
D) RefreshStart and RefreshEnd as any/any type parameters

<details>
<summary>Answer</summary>

**Correct: B**

Incremental refresh strictly requires two parameters named exactly RangeStart and RangeEnd, of datetime type, referenced in a date filter step on the table — the Manage Incremental Refresh dialog only appears when this pattern exists.

**Why the others are wrong:**
- Custom names like StartDate/EndDate will not be recognized by the incremental refresh dialog regardless of type
- MinDate/MaxDate as whole numbers don't match the required naming or datetime type
- RefreshStart/RefreshEnd is not the required parameter naming convention

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A model requires that regional managers see only sales rows for their own region, determined dynamically from a Users table mapped to email via USERPRINCIPALNAME(). Which feature should be configured to enforce this?

A) Object-level security (OLS) hiding the Region column
B) A static RLS role manually listing every manager's region
C) Perspectives limiting visible tables per manager
D) A dynamic row-level security (RLS) role with a DAX filter expression referencing USERPRINCIPALNAME() against the Users table

<details>
<summary>Answer</summary>

**Correct: D**

Dynamic RLS uses USERPRINCIPALNAME() joined through a Users table to filter data per logged-in user automatically, avoiding one static role per manager — this is the standard DP-600 pattern for user-driven row filtering.

**Why the others are wrong:**
- OLS hides entire objects (tables/columns) for all users of a role; it doesn't filter rows dynamically per user
- Static roles require one hardcoded role per region/manager and don't scale or update automatically as staff change
- Perspectives are just curated views of model objects for authoring convenience and provide no security enforcement

</details>

---

**Q8.** A report author asks Copilot in Fabric to generate a year-over-year growth measure. What is the CORRECT expectation of this workflow per current Copilot capabilities?

A) Copilot will silently publish the measure directly to the production semantic model without review
B) Copilot generates a candidate DAX expression based on model metadata that the author must review, test, and validate before accepting into the model
C) Copilot bypasses DAX entirely and computes results using Python only
D) Copilot can only generate calculated columns, never measures

<details>
<summary>Answer</summary>

**Correct: B**

Copilot for DAX (in the DAX query view / Copilot pane) proposes DAX code based on table/column names and relationships, but the author must review, test against the model, and explicitly accept it — it does not auto-publish unreviewed logic.

**Why the others are wrong:**
- Copilot never auto-publishes changes without explicit user acceptance of suggested code
- Copilot generates DAX, not Python, for measure authoring in this context
- Copilot can generate both measures and DAX queries, not just calculated columns

</details>

---

