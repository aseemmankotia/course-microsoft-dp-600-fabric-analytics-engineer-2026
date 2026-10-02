## Chapter 1: Workspace & Item Governance in Microsoft Fabric — Practice Questions

**Q1.** A Contributor in a Fabric workspace needs to give an external analyst access to view a single Power BI report, without granting that analyst any other access to the workspace. What should the Contributor do?

A) Assign the analyst the Viewer workspace role
B) Assign the analyst the Contributor workspace role
C) Share the report item directly with the analyst using Read permission
D) Ask a tenant admin to add the analyst to the workspace

<details>
<summary>Answer</summary>

**Correct: C**

Sharing an individual item grants access scoped only to that item (e.g., Read), without exposing the rest of the workspace's content.

**Why the others are wrong:**
- Viewer role grants read access to ALL items in the workspace, not just the one report — over-provisioned access.
- Contributor role grants full edit/delete rights across the workspace, far exceeding the requirement.
- Adding to the workspace (any role) always exposes more than a single item; item sharing is the correct scope.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company wants only the Finance security group to see files under the /Finance folder of a shared Lakehouse, while other analysts keep their existing full-lakehouse Viewer access. Which feature should be configured?

A) Assign the Finance group the Viewer workspace role
B) Share the Lakehouse item with the Finance group using Read permission
C) Enable row-level security (RLS) on the semantic model built from the Lakehouse
D) Create a custom OneLake data access role scoped to the /Finance folder and assign the Finance security group to it

<details>
<summary>Answer</summary>

**Correct: D**

OneLake data access roles provide folder- and table-level granular security within a Lakehouse, independent of workspace-level roles, and can be assigned to specific security groups.

**Why the others are wrong:**
- Viewer is a workspace-wide role and cannot restrict access to a single folder.
- Sharing the Lakehouse item still grants access to the whole item, not a specific folder.
- RLS applies to rows in a semantic model, not files/folders in OneLake storage.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A user must be able to create, edit, and publish reports and datasets in a workspace, but must NOT be able to add other users or share items with people outside the workspace. Which workspace role satisfies this exactly?

A) Contributor
B) Viewer
C) Member
D) Admin

<details>
<summary>Answer</summary>

**Correct: A**

Contributor can create, edit, and delete content in the workspace but cannot manage workspace access or share items with others.

**Why the others are wrong:**
- Viewer is read-only and cannot create or edit items.
- Member can share items and manage access for lower roles — exceeds the requirement.
- Admin has full control including deleting the workspace and managing all roles.

</details>

---

**Q4.** Which workspace role should be assigned to a stakeholder who only needs to open and interact with published reports, with no ability to edit any item?

A) Viewer
B) Contributor
C) Member
D) Admin

<details>
<summary>Answer</summary>

**Correct: A**

Viewer grants read/consume access to workspace content without edit or management capability.

**Why the others are wrong:**
- Contributor can create and edit items, exceeding the read-only requirement.
- Member can also share and manage lower-level access, more than needed.
- Admin grants full workspace control, far beyond consumption needs.

</details>

---

**Q5.** A team needs to assign an existing Fabric workspace to a new capacity. What is required to perform this action?

A) The user must be a workspace Admin and have Contributor (or higher) permission on the target capacity
B) Any workspace Member role is sufficient
C) Only a tenant admin can assign workspaces to capacities
D) Any Fabric license holder can assign a workspace to any capacity

<details>
<summary>Answer</summary>

**Correct: A**

Assigning a workspace to a capacity requires being an Admin of that workspace and having Contributor-level (or higher) access on the target capacity.

**Why the others are wrong:**
- Member role alone does not grant permission to change the workspace's capacity assignment.
- Tenant admins can do it too, but it is not exclusive to them — a qualifying workspace Admin can also do this.
- Capacity access is not open to any license holder; capacity-level permission is required.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** Where must a tenant administrator go to disable the 'Export to Excel' feature for the entire organization?

A) Workspace settings within an individual workspace
B) Admin portal > Tenant settings
C) Item-level sharing permissions on each report
D) OneLake data access roles configuration

<details>
<summary>Answer</summary>

**Correct: B**

Organization-wide feature toggles like export controls are configured in the Admin portal under Tenant settings, and they can cascade down unless overridden at a lower scope where allowed.

**Why the others are wrong:**
- Workspace settings control workspace-specific behavior (e.g., OneDrive, Git integration), not org-wide export policy.
- Item permissions control who can access an item, not organization-wide feature availability.
- OneLake data access roles control folder/table-level data security, unrelated to export features.

</details>

---

**Q7.** When sharing a semantic model, which permission allows the recipient to create new reports on top of the model without editing the model itself?

A) Build
B) Read
C) Reshare
D) Row-level security bypass

<details>
<summary>Answer</summary>

**Correct: A**

Build permission specifically allows a user to create new content (reports) connected to the shared semantic model.

**Why the others are wrong:**
- Read alone lets the user view existing content but not build new reports against the model.
- Reshare only allows forwarding access to others, not building new content.
- The RLS-bypass option ('Read all data') controls row visibility, not report-building capability.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement correctly describes the relationship between workspace roles and item-level permissions in Microsoft Fabric?

A) Item-level permissions always override and replace the user's workspace role entirely
B) A workspace role grants access to all items in the workspace by default, while item-level sharing grants access to a single item without changing the user's overall workspace role
C) Item-level permissions can only be granted to users who already hold a workspace role
D) Workspace roles and item permissions are mutually exclusive and cannot both apply to the same user

<details>
<summary>Answer</summary>

**Correct: B**

Workspace roles apply broadly across all items in the workspace, whereas sharing grants scoped access to an individual item and does not require or change workspace membership.

**Why the others are wrong:**
- Item permissions supplement rather than replace a workspace role; both can apply simultaneously.
- Item sharing can be granted to users outside the workspace who hold no workspace role at all.
- Both can coexist — a user can have a workspace role plus additional/different item-level shares.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

