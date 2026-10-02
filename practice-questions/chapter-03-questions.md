## Chapter 3: Lifecycle Management: Git, Deployment Pipelines, CI/CD & Capacity — Practice Questions

**Q1.** A workspace has a Fabric deployment pipeline with Dev, Test, and Prod stages. The team needs the Warehouse connection string in each notebook to automatically point to the correct environment's data source every time content is deployed, without manually editing the notebook after each deployment. What should they configure?

A) Manually update the connection string in each notebook after every deployment
B) A separate Git branch per environment with hardcoded connection strings
C) A deployment rule on the target stage that maps the connection string parameter
D) A dataflow gateway data source override applied only in production

<details>
<summary>Answer</summary>

**Correct: C**

Deployment rules are defined on the target stage and automatically apply configured values (like connection strings or parameters) every time new content is deployed into that stage, so manual edits are never needed again.

**Why the others are wrong:**
- Manual edits are not automated and must be repeated on every deployment, defeating the purpose.
- Git branches control source sync, not stage-specific runtime configuration; hardcoding also breaks portability.
- Gateway data source overrides are unrelated to deployment pipeline stage configuration.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Users on an F64 capacity report that Power BI reports load noticeably slower than usual during a busy morning, but the reports still return results correctly. No error messages appear. Which throttling stage is most likely occurring?

A) Background rejection
B) Interactive rejection
C) Autoscale activation
D) Interactive delay

<details>
<summary>Answer</summary>

**Correct: D**

Interactive delay is the first throttling stage: interactive operations (like report loads) are slowed down but still complete successfully when capacity utilization exceeds limits.

**Why the others are wrong:**
- Background rejection is the most severe stage and would cause scheduled jobs to fail outright, not slow report loads.
- Interactive rejection returns errors to users instead of just delaying results, which contradicts the scenario.
- Autoscale is a separate optional capacity feature, not a throttling stage, and isn't described here.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A capacity has been severely over-utilized for a sustained period. Users now receive explicit errors when opening reports, stating the capacity is overloaded, but nightly scheduled refreshes still complete successfully. Which throttling condition best describes this state?

A) Interactive delay only
B) Background rejection, with interactive operations unaffected
C) Both interactive and background rejection simultaneously
D) Interactive rejection, with background operations unaffected

<details>
<summary>Answer</summary>

**Correct: D**

Interactive rejection occurs after prolonged overuse and causes interactive requests to be rejected outright, while background operations (like scheduled refreshes) continue until the more severe background rejection stage is reached.

**Why the others are wrong:**
- Interactive delay only slows requests; it does not produce explicit rejection errors.
- Background rejection would cause the scheduled refresh to fail, contradicting the scenario.
- Both stages occurring together would mean scheduled refreshes also fail, which is not described.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team wants to automatically deploy Fabric items from the Dev stage to the Test stage as part of an Azure DevOps YAML pipeline, without any manual clicks in the Fabric portal. Which approach should they use?

A) Call the Fabric deployment pipeline REST APIs using a service principal
B) Manually trigger the deployment pipeline UI after each merge
C) Use Git branch-out to create a new workspace for every deployment
D) Schedule a Data pipeline within Fabric to copy workspace items

<details>
<summary>Answer</summary>

**Correct: A**

Fabric exposes deployment pipeline REST APIs that support service principal authentication, enabling full CI/CD automation from external orchestrators like Azure DevOps or GitHub Actions.

**Why the others are wrong:**
- Manual UI triggering defeats the purpose of an automated pipeline.
- Branching out creates a new workspace from a Git branch; it does not perform stage-to-stage deployment.
- Data pipelines move data, not Fabric item definitions between deployment stages.

</details>

---

**Q5.** An admin needs to see how much capacity unit (CU) consumption background operations like scheduled semantic model refreshes have used over the past several days, including any overage patterns. Which tool should they use?

A) The Fabric Monitoring hub
B) Git integration status pane
C) The deployment pipeline comparison view
D) The Capacity Metrics app

<details>
<summary>Answer</summary>

**Correct: D**

The Capacity Metrics app is built specifically to visualize CU consumption, interactive vs background usage, and throttling/overage trends for a capacity over time.

**Why the others are wrong:**
- The Monitoring hub shows job run status and history, not CU consumption trends.
- The Git integration status pane only shows sync/commit status of workspace items.
- The deployment pipeline comparison view shows content differences between stages, not capacity usage.

</details>

---

**Q6.** By default, how many stages does a newly created Fabric deployment pipeline contain?

A) 1
B) 2
C) 5
D) 3

<details>
<summary>Answer</summary>

**Correct: D**

A new deployment pipeline is created with 3 default stages: Development, Test, and Production, though the number of stages can be customized between 2 and 10.

**Why the others are wrong:**
- A single stage would not allow any promotion workflow, which defeats the pipeline's purpose.
- Two stages is a valid custom configuration but not the default.
- Five stages exceeds the default and requires manual configuration.

</details>

---

**Q7.** When a Fabric workspace is connected to Git, each item is synced to the repository as a folder containing content files plus one specific metadata file. What is that file called?

A) .gitignore
B) .platform
C) workspace.json
D) item.config

<details>
<summary>Answer</summary>

**Correct: B**

Fabric's Git integration serializes each item into a folder that includes a .platform file, storing metadata such as the item's display name and type alongside its content files.

**Why the others are wrong:**
- .gitignore is a standard Git file for excluding paths, not Fabric-specific item metadata.
- workspace.json is not a file Fabric generates for Git-synced items.
- item.config is not a real Fabric or Git integration artifact.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the primary purpose of a deployment rule in a Fabric deployment pipeline?

A) To restrict which users are allowed to trigger a deployment
B) To preserve stage-specific configuration values (like connection strings or parameters) so they are not overwritten on each deployment
C) To automatically schedule deployments on a recurring basis
D) To encrypt sensitive connection strings during transit between stages

<details>
<summary>Answer</summary>

**Correct: B**

Deployment rules let a target stage retain environment-specific values (such as a Test warehouse connection string) so that pushing new content from the previous stage doesn't overwrite those settings.

**Why the others are wrong:**
- User permissions are controlled by workspace roles and pipeline access settings, not deployment rules.
- Deployment pipelines do not include a native recurring scheduling mechanism triggered by rules.
- Deployment rules configure values, not encryption; encryption is handled at the platform/transport level.

</details>

---

