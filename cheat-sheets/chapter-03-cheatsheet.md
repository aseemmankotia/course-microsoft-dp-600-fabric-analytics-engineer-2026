## Chapter 3 Cheat Sheet — Lifecycle Management

### Git Integration
| Concept | Detail |
|---|---|
| Supported providers | Azure DevOps, GitHub |
| Prerequisite | Tenant-level Git integration setting enabled by Fabric admin |
| Mapping | One workspace ↔ one branch |
| Sync artifact | Each item → folder with content files + `.platform` metadata file |
| Key actions | Connect, Commit to Git, Update from workspace, Branch out (new workspace from a branch) |
| Exam trap | Git integration syncs one workspace to source control; it does NOT promote content between environments — that's deployment pipelines |

### Deployment Pipelines
| Concept | Detail |
|---|---|
| Default stages | 3 — Development, Test, Production |
| Configurable range | 2–10 stages |
| Deployment rules | Set on the TARGET stage; preserve connection strings/parameters across future deployments |
| Rule types | Connection string rules (data sources), Parameter rules (e.g., notebook/lakehouse defaults) |
| Exam trap | Rules apply forward on every future deploy — they don't retroactively fix already-deployed content |

### CI/CD Automation
| Concept | Detail |
|---|---|
| APIs available | Git integration APIs (Connect/Initialize/Commit/Update), Deployment Pipeline APIs, Item CRUD APIs |
| Auth for automation | Service principal (enables unattended pipelines in Azure DevOps/GitHub Actions) |
| Exam trap | Manual portal clicks ≠ CI/CD; look for "automate without manual steps" → REST API + service principal |

### Capacity Metrics App & Throttling
| Concept | Detail |
|---|---|
| Tool | Capacity Metrics app (installed from Microsoft) |
| Window | 24-hour rolling CU usage view |
| Distinguishes | Interactive vs background operation consumption |
| SKU naming | F64 = 64 CUs (number in SKU = CU count) |

**Throttling stage order (memorize this sequence):**
1. **Interactive delay** — requests succeed but slow down
2. **Interactive rejection** — interactive requests error out; background still runs
3. **Background rejection** — background/scheduled jobs start failing (most severe)

**Exam traps:**
- "Slow but works" = delay. "Error on open, refresh still works" = interactive rejection. "Refresh fails too" = background rejection.
- Monitoring hub = job run status/history. Capacity Metrics app = CU consumption/throttling trends. Don't mix them up.
- Deployment pipelines vs Git integration are complementary, not interchangeable.
