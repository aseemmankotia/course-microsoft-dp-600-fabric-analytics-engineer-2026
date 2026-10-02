## Workspace Roles Hierarchy

| Role | Create/Edit Items | Delete Workspace | Share Items | Manage Access (lower roles) | Manage Admins |
|---|---|---|---|---|---|
| Admin | Yes | Yes | Yes | Yes (all roles) | Yes |
| Member | Yes | No | Yes | Yes (Member/Contributor/Viewer) | No |
| Contributor | Yes | No | No | No | No |
| Viewer | No (read-only) | No | No | No | No |

**Exam rule:** Roles apply to ALL items in the workspace by default (inheritance). Item-level sharing overrides scope down to a single item.

## Item Sharing Permissions (Semantic Models / Reports)

| Permission | Effect |
|---|---|
| Read | View/consume the item |
| Build | Create new reports on top of a shared semantic model |
| Reshare | Forward access to other users |
| Read all data (RLS bypass) | Bypass row-level security rules on the model |

**Exam rule:** Sharing an item never changes the recipient's workspace role — it's additive, scoped access only.

## OneLake Data Access Roles

- Provide **folder- and table-level** security inside a Lakehouse, independent of workspace roles.
- Assign Microsoft Entra security groups to custom roles scoped to specific folders/tables.
- Default: Viewers/Members get full Lakehouse access unless a custom OneLake role restricts them.
- **Use case:** Finance-only folder visibility while other analysts keep full-Lakehouse Viewer access.

## Tenant vs Workspace Settings

| Scope | Location | Example |
|---|---|---|
| Tenant | Admin portal > Tenant settings | Disable export to Excel, external sharing, capacity creation rights |
| Workspace | Workspace settings pane | Git integration, workspace OneDrive, workspace-specific storage format |

**Exam rule:** Tenant settings can restrict what's available at workspace level; workspace settings cannot override a tenant-level restriction if the tenant admin disabled it.

## Capacity Assignment

- Requires: Workspace **Admin** role + **Contributor (or higher)** permission on the target capacity.
- Tenant admins can also assign capacities but it is not exclusive to them.

## Common Traps

1. Assuming sharing an item = adding user to workspace (FALSE — sharing is scoped only).
2. Assuming Contributor can share items (FALSE — only Member/Admin can share).
3. Assuming Viewer role can be used for folder-level restriction (FALSE — use OneLake data access roles).
4. Assuming any workspace role can assign capacity (FALSE — needs Admin + capacity Contributor).
