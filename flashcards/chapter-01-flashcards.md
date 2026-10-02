## Chapter 1: Workspace & Item Governance in Microsoft Fabric — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Which workspace role can delete the workspace itself? | Only Admin. Member, Contributor, and Viewer cannot delete the workspace. Exam tip: 'delete workspace' = Admin-only action. |
| 2 | Which workspace role can share items and manage access for Members/Contributors/Viewers, but not add/remove Admins? | Member. Exam tip: Member manages lower-tier access; only Admin manages Admin membership. |
| 3 | Which workspace role can create, edit, and delete items but CANNOT share items or manage workspace access? | Contributor. Exam tip: Contributor = content creation only, no access management. |
| 4 | Which workspace role is read-only (view/consume content, no edit)? | Viewer. Exam tip: Viewer can interact with reports (filter/slice) but never edit or share. |
| 5 | Does sharing an item grant the recipient a workspace role? | No. Item sharing grants access scoped to that single item only; it does not add the user to the workspace or change their role. |
| 6 | What Build permission does when sharing a semantic model? | Allows the recipient to create new reports/content on top of the shared model, without granting edit rights to the model itself. |
| 7 | What are OneLake data access roles used for? | Granular, folder- and table-level access control within a Lakehouse, independent of workspace roles. Can be assigned to Entra security groups. Exam tip: use this when workspace role access is too broad. |
| 8 | Who can assign a workspace to a Fabric capacity? | A user who is Admin of the workspace AND has Contributor (or higher) permission on the target capacity. Exam tip: tenant admins can also do this, but it's not exclusive to them. |
| 9 | Where are org-wide feature toggles (e.g., disabling export, external sharing) configured? | Admin portal > Tenant settings — applies tenant-wide, may cascade to workspace/item level depending on setting. |
| 10 | Tenant setting vs Workspace setting — key difference? | Tenant settings (Admin portal) control org-wide policy for all workspaces; workspace settings control behavior scoped to a single workspace (e.g., Git integration, OneDrive integration). |
| 11 | Default OneLake access behavior for workspace Viewers on a Lakehouse? | Viewers get read access to the entire Lakehouse by default unless a custom OneLake data access role restricts them to specific folders/tables. |
| 12 | Item-level Reshare permission — what does it allow? | Lets the recipient forward/share the item's access with additional users, beyond just consuming it themselves. Exam tip: distinct from Read and Build permissions. |
