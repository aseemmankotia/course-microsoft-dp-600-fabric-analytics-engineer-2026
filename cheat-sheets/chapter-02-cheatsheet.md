## Chapter 2 Cheat Sheet: RLS, CLS, OLS, DDM

### Where Each Security Type Lives
| Security Type | Layer | Defined With | Hides Rows/Cols/Objects |
|---|---|---|---|
| RLS | Semantic model (Power BI) | Roles + DAX filter expr | Filters **rows** |
| CLS | Warehouse / Lakehouse SQL endpoint | T-SQL GRANT/DENY on column | Hides **columns** |
| OLS (warehouse) | Warehouse / Lakehouse SQL endpoint | T-SQL DENY on table/view | Hides entire **object** |
| OLS (semantic model) | Semantic model | Tabular Editor / TMDL | Hides tables/columns/measures from Explorer |
| DDM | Warehouse / Lakehouse SQL endpoint | T-SQL MASKED WITH (...) | Obscures **values**, rows still returned |

Key distinction: RLS/OLS(model) apply only to Power BI semantic models. CLS/OLS(warehouse)/DDM apply only where a SQL analytics endpoint exists (Warehouse and Lakehouse). Spark notebooks on a Lakehouse **bypass** SQL-endpoint security entirely.

### RLS Essentials
- Static RLS: `[Region] = "West"` — one role per fixed value
- Dynamic RLS: filter on `USERPRINCIPALNAME()` (email/UPN format) or `USERNAME()` (domain\user format) joined to a security table
- Test with **View As Roles** in Power BI Desktop (supports entering a UPN)
- Assign users to roles in Power BI Service → dataset Security settings

### T-SQL Security Syntax
```sql
-- Column-level security (CLS)
GRANT SELECT ON dbo.Employees(Name, Dept) TO FinanceRole;

-- Object-level security (OLS)
DENY SELECT ON dbo.Salaries TO InternsRole;

-- Dynamic Data Masking — add to existing column
ALTER TABLE Customers
ALTER COLUMN Email ADD MASKED WITH (FUNCTION = 'email()');

ALTER TABLE Customers
ALTER COLUMN SSN ADD MASKED WITH (FUNCTION = 'partial(1,"XXXXXXX",0)');

-- Grant ability to see unmasked data
GRANT UNMASK ON dbo.Customers TO AuditRole;
```

### DDM Masking Functions
| Function | Behavior | Example |
|---|---|---|
| default() | Full mask by data type | string→XXXX, int→0, date→1900-01-01 |
| email() | Partial email mask | aXX@XXXX.com |
| partial(p,mid,s) | Custom string mask | partial(1,"XXXXXXX",0) |
| random(lo,hi) | Random numeric substitute | random(1,100) |

### Precedence Rules
- **DENY always overrides GRANT**, even if GRANT comes from a different role the user belongs to
- **REVOKE** only removes a prior grant/deny — does not override other role memberships
- db_owner/admins see **unmasked** data by default unless explicitly denied `UNMASK`

### Exam Traps
1. Confusing USERNAME() vs USERPRINCIPALNAME() → causes RLS to silently return zero rows
2. Assuming DDM hides rows — it does not; only column values are obscured
3. Forgetting `ADD` keyword when applying DDM to an existing column
4. Assuming Lakehouse Spark access respects SQL-endpoint CLS/OLS/DDM — it does not
5. Assuming RLS can be configured via T-SQL — it's a semantic-model-only construct
