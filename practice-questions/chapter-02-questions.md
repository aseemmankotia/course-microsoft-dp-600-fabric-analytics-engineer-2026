## Chapter 2: Securing Data: RLS, CLS, OLS, and Dynamic Data Masking — Practice Questions

**Q1.** A company stores sales data in a Fabric Warehouse. Analysts from the EU region must never see the 'CreditCardNumber' column, but they still need to run SELECT * FROM Sales queries without modifying every query. Which approach requires the LEAST query rewriting?

A) Apply Row-Level Security with a DAX filter on the CreditCardNumber column
B) Create a view that excludes CreditCardNumber and force all analysts to query the view
C) Apply Dynamic Data Masking with the default() function on CreditCardNumber
D) DENY SELECT on the entire Sales table to the EU analysts role

<details>
<summary>Answer</summary>

**Correct: C**

Dynamic Data Masking obscures the column's contents in query results without changing table structure or requiring analysts to rewrite SELECT * statements; unauthorized users still see the column but masked.

**Why the others are wrong:**
- RLS uses DAX and only exists in semantic models (Power BI), not in the warehouse — it also filters rows, not columns
- Creating a view works but requires rewriting all existing queries to point at the new view
- DENY on the whole table blocks the analysts from seeing Sales data entirely, which is more restrictive than required

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** You need to prevent the 'Contractors' role from ever seeing that a 'Salaries' table exists in the semantic model, including in the Explorer pane. Which security technique should you use?

A) Row-level security with a DAX expression that returns FALSE()
B) Dynamic data masking on all columns in the table
C) Object-level security (OLS) hiding the table for that role
D) Column-level security via T-SQL DENY on the table

<details>
<summary>Answer</summary>

**Correct: C**

OLS in the semantic model completely hides tables, columns, or measures from specific roles, including from metadata browsing — RLS only filters rows, the table remains visible.

**Why the others are wrong:**
- RLS filtering to FALSE() hides rows but the table and column names are still visible and can appear in error messages
- Dynamic data masking obscures values but the table structure is still visible
- T-SQL DENY is a warehouse-level construct, not applicable to the semantic model object

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Which T-SQL statement correctly masks an existing email column so users without UNMASK permission see a partially obfuscated email address?

A) ALTER TABLE Customers ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()')
B) ALTER TABLE Customers ALTER COLUMN Email MASKED WITH (FUNCTION = 'email()')
C) GRANT MASK ON Customers.Email TO 'email()'
D) CREATE MASK ON Customers.Email USING (FUNCTION = 'email()')

<details>
<summary>Answer</summary>

**Correct: A**

Applying DDM to an existing column requires ALTER TABLE ... ALTER COLUMN ... ADD MASKED WITH (FUNCTION = 'email()'). The ADD keyword is required when adding masking to a column that already exists.

**Why the others are wrong:**
- Missing the ADD keyword — this is invalid syntax for adding masking to an existing column
- GRANT MASK is not valid T-SQL syntax; masking is not a permission grant
- CREATE MASK is not a valid T-SQL statement in Fabric Warehouse/SQL Server

</details>

---

**Q4.** A semantic model uses dynamic RLS where a security table maps USERPRINCIPALNAME() to allowed Region values. A user reports seeing NO data at all after the role is assigned, even though their email exists in the security table. What is the MOST likely cause?

A) Dynamic data masking is blocking all rows for this user
B) The role's DAX filter uses USERNAME() instead of USERPRINCIPALNAME(), and the security table stores email addresses not domain\username values
C) The user needs db_owner permission on the warehouse
D) Object-level security is hiding the Region table from this user

<details>
<summary>Answer</summary>

**Correct: B**

USERNAME() returns the domain\username format while USERPRINCIPALNAME() returns the email/UPN format used in Fabric/Power BI Service — mismatching the function to the stored format causes zero matching rows and an empty result.

**Why the others are wrong:**
- DDM operates on the warehouse and masks values, it does not cause rows to disappear entirely from a semantic model
- Warehouse permissions are unrelated to Power BI semantic model RLS evaluation
- OLS hiding a table would cause a query error referencing that object, not silent zero rows across the whole model

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** You must give the 'Finance' role read access to the SalaryAmount column but explicitly block the 'Interns' role, which is a member of a broader 'AllStaff' role that already has SELECT on the whole table. Which statement should you run to guarantee interns cannot see the column regardless of other grants?

A) GRANT SELECT ON dbo.Employees(SalaryAmount) TO Finance
B) REVOKE SELECT ON dbo.Employees(SalaryAmount) FROM Interns
C) DENY SELECT ON dbo.Employees(SalaryAmount) TO Interns
D) ALTER TABLE dbo.Employees DROP COLUMN SalaryAmount FOR Interns

<details>
<summary>Answer</summary>

**Correct: C**

DENY always overrides any GRANT, including grants inherited from membership in another role — this guarantees the Interns role can never see SalaryAmount regardless of AllStaff's permissions.

**Why the others are wrong:**
- GRANT gives Finance access but does nothing to block Interns
- REVOKE only removes a previously granted permission — it does not override a GRANT the user inherits from another role membership
- There is no such T-SQL syntax; columns cannot be conditionally dropped per role

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Where can you enforce column-level and object-level security (CLS/OLS) using T-SQL GRANT/DENY statements in a Fabric workspace?

A) Only on Warehouse tables, not on Lakehouse tables
B) Only within the Power BI semantic model using Tabular Editor
C) Only on Lakehouse Spark notebooks using PySpark ACLs
D) On the SQL analytics endpoint of both Warehouses and Lakehouses

<details>
<summary>Answer</summary>

**Correct: D**

Both Warehouse and the Lakehouse SQL analytics endpoint support standard T-SQL GRANT/DENY for CLS and OLS, since both expose a SQL endpoint over the underlying Delta tables.

**Why the others are wrong:**
- Lakehouses also expose a SQL analytics endpoint that supports the same T-SQL security statements
- Tabular Editor is used for OLS in the semantic model, but that is a separate layer from warehouse/lakehouse T-SQL security
- Spark notebooks do not enforce SQL-style GRANT/DENY; Spark accesses the underlying files directly and bypasses SQL endpoint security

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A report developer wants to verify that the 'Regional Manager' RLS role correctly limits a specific test user to only their assigned region before publishing. What is the fastest way to validate this in Power BI Desktop?

A) Publish the report to the Service and ask the test user to check manually
B) Use 'View As Roles' and enter the test user's UPN along with the Regional Manager role
C) Open the DAX filter expression and manually trace the logic
D) Create a duplicate report with hardcoded filters matching the user's region

<details>
<summary>Answer</summary>

**Correct: B**

'View As Roles' in Power BI Desktop lets you simulate a specific role and optionally specify a UPN for dynamic RLS, showing exactly what that user would see without publishing or waiting on end users.

**Why the others are wrong:**
- Publishing first and relying on manual end-user testing is slow and doesn't catch errors before deployment
- Manually tracing DAX logic doesn't confirm the actual rendered result the way live testing does
- Hardcoding filters in a duplicate report doesn't test the actual RLS role logic and creates unnecessary maintenance overhead

</details>

---

**Q8.** Which statement correctly describes the difference between Row-Level Security (RLS) and Dynamic Data Masking (DDM)?

A) RLS masks specific column values while DDM filters entire rows from view
B) RLS and DDM are two names for the same Fabric feature
C) RLS applies only in the Warehouse; DDM applies only in the semantic model
D) RLS filters which rows a user can see; DDM obscures column values but still returns all rows

<details>
<summary>Answer</summary>

**Correct: D**

RLS restricts which rows are returned to a given user/role based on a filter expression, while DDM leaves all rows visible but obscures the actual values in specific columns for unauthorized users.

**Why the others are wrong:**
- This reverses the actual behavior of the two features
- They are distinct security mechanisms that operate at different layers (semantic model vs. SQL engine) and solve different problems
- RLS is a semantic model (Power BI) construct; DDM is a T-SQL/warehouse construct — the statement reverses their scope

</details>

---

