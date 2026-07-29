# Jira Setup Guide — BAPS Stage Gate Process
**Sandbox**: `baps-sandbox.atlassian.net`
**Project**: `MYS` (existing Scrum Software project)
**Jira plan required**: Standard or above (needed for per-issue-type workflows and automation)

Follow these steps in order. Each step links to the exact Jira settings screen.

---

## Overview

The stage gate process uses two separate Jira workflows:

| Issue Type | Workflow | Covers |
|---|---|---|
| **Epic** | Early Stage Workflow | Gates 1–5: Proposal → Initiation → Requirements → Design → Planning |
| **Story** | Dev Stage Workflow | Gates 6–8: Development → UAT → Launch |
| **Sub-task** | Default (To Do / In Progress / Done / Won't Do) | Individual gate checklist items |
| **Task** | Default | Gate Review decisions — one per gate |

---

## Step 1 — Add Custom Issue Type

**Path**: Project Settings → Issue Types → Add Issue Type

Add one new issue type:

| Name | Description | Icon suggestion |
|---|---|---|
| `Gate Review` | Records the formal gate decision (Go / Kill / Hold / Recycle) for each stage transition | 🔑 |

Keep existing: Epic, Story, Sub-task, Bug, Task.

---

## Step 2 — Add Custom Fields

**Path**: Project Settings → Fields → Add Field (or go to Jira Settings → Issues → Custom Fields for global fields)

Add these fields. They will be added to screens in Step 3.

| Field Name | Type | Options / Notes |
|---|---|---|
| `Gate Status` | Dropdown (single select) | Not Reached, In Review, Passed, Failed, Skipped |
| `Gate Decision` | Dropdown (single select) | Approved, Conditionally Approved, On Hold, Rejected, Killed |
| `Stage Number` | Number | 1 through 9. Used in JQL filters and compliance reports. |
| `Responsible` | User Picker (single user) | Maps to R in RACI |
| `Accountable` | User Picker (single user) | Maps to A in RACI |
| `Document Link` | URL | Link to signed-off document in SharePoint/MS Teams |
| `Exit Type` | Dropdown (single select) | None, Exit A, Exit B, Exit C — add to Epic only |

---

## Step 3 — Create Screens

**Path**: Project Settings → Screens → Add Screen

Create two screens and add the appropriate fields:

### Screen 1: `SGP Early Stage Screen` (for Epics)
Fields to include (in addition to defaults):
- Summary, Description, Assignee, Reporter, Priority (keep defaults)
- Gate Status
- Gate Decision
- Stage Number
- Exit Type
- Document Link
- Responsible
- Accountable

### Screen 2: `SGP Dev Stage Screen` (for Stories)
Fields to include:
- Summary, Description, Assignee, Reporter, Story Points (keep defaults)
- Gate Status
- Document Link
- Responsible
- Accountable
- Stage Number

### Screen 3: `SGP Gate Review Screen` (for Gate Review issue type)
Fields to include:
- Summary, Description
- Gate Decision
- Gate Status
- Document Link
- Linked Issues (to link back to parent Epic/Story)

### Map Screens to Issue Types
**Path**: Project Settings → Screen Schemes → Edit

| Issue Type | Screen (Create) | Screen (Edit) | Screen (View) |
|---|---|---|---|
| Epic | SGP Early Stage Screen | SGP Early Stage Screen | SGP Early Stage Screen |
| Story | SGP Dev Stage Screen | SGP Dev Stage Screen | SGP Dev Stage Screen |
| Gate Review | SGP Gate Review Screen | SGP Gate Review Screen | SGP Gate Review Screen |
| Sub-task | Default | Default | Default |

---

## Step 4 — Create Workflows

**Path**: Project Settings → Workflows → Add Workflow

### Workflow 1: `SGP Early Stage Workflow` → Assign to **Epic**

Create the following statuses and transitions:

**Statuses** (create each as a new status):
```
New Proposal Submitted      (category: To Do)
Proposal Under Review       (category: In Progress)
Initiation Active           (category: In Progress)
Initiation Under Review     (category: In Progress)
Requirements Active         (category: In Progress)
Requirements Under Review   (category: In Progress)
Technical Design Active     (category: In Progress)
Design Under Review         (category: In Progress)
Estimate & Planning Active  (category: In Progress)
Planning Under Review       (category: In Progress)
Development Ready           (category: In Progress)
Project Closed              (category: Done)
On Hold                     (category: To Do)
Killed                      (category: Done)
```

**Transitions** (connect statuses):
```
New Proposal Submitted → Proposal Under Review         [name: "Submit for Gate 1 Review"]
Proposal Under Review → Initiation Active              [name: "Gate 1 Passed"]
Proposal Under Review → On Hold                        [name: "Put On Hold"]
Proposal Under Review → Killed                         [name: "Reject / Kill"]
Initiation Active → Initiation Under Review            [name: "Submit for Gate 2 Review"]
Initiation Under Review → Requirements Active          [name: "Gate 2 Passed"]
Requirements Active → Requirements Under Review        [name: "Submit for Gate 3 Review"]
Requirements Under Review → Technical Design Active    [name: "Gate 3 Passed"]
Technical Design Active → Design Under Review          [name: "Submit for Gate 4 Review"]
Design Under Review → Estimate & Planning Active       [name: "Gate 4 Passed"]
Estimate & Planning Active → Planning Under Review     [name: "Submit for Gate 5 Review"]
Planning Under Review → Development Ready              [name: "Gate 5 Passed — Start Dev"]
Development Ready → Project Closed                     [name: "Close Project"]
Any status → On Hold                                   [name: "Put On Hold"]
Any status → Killed                                    [name: "Kill Project"]
```

### Workflow 2: `SGP Dev Stage Workflow` → Assign to **Story**

**Statuses**:
```
To Do               (category: To Do)
In Development      (category: In Progress)
Code Review         (category: In Progress)
QA Testing          (category: In Progress)
QA Passed           (category: In Progress)
UAT In Progress     (category: In Progress)
UAT Passed          (category: In Progress)
Release Ready       (category: In Progress)
Done                (category: Done)
Blocked             (category: To Do)
Won't Do            (category: Done)
```

**Transitions**:
```
To Do → In Development           [name: "Start Development"]
In Development → Code Review     [name: "Submit for Code Review"]
Code Review → QA Testing         [name: "Code Review Passed"]
QA Testing → QA Passed           [name: "QA Gate Passed"]
QA Passed → UAT In Progress      [name: "Deploy to UAT"]
UAT In Progress → UAT Passed     [name: "UAT Sign-off Received"]
UAT Passed → Release Ready       [name: "Launch Readiness Review"]
Release Ready → Done             [name: "Released to Production"]
Any status → Blocked             [name: "Mark as Blocked"]
Blocked → In Development         [name: "Unblock"]
Any status → Won't Do            [name: "Descope / Won't Do"]
```

### Assign Workflows to Issue Types
**Path**: Project Settings → Workflows → Edit Workflow Scheme

| Issue Type | Workflow |
|---|---|
| Epic | SGP Early Stage Workflow |
| Story | SGP Dev Stage Workflow |
| Sub-task | Default (keep existing) |
| Bug | Default (keep existing) |
| Task | Default (keep existing) |
| Gate Review | Default (keep existing) |

---

## Step 5 — Set Up Automation Rules

**Path**: Project Settings → Automation → Create Rule

See `automation-rules.md` for the full rule configurations. Summary of 5 rules to create:

1. **Gate blocker** — blocks Epic/Story from moving to "Under Review" status if any Gate Criteria sub-tasks are incomplete
2. **Skipped item flag** — when sub-task set to Won't Do, auto-creates a Bug tagged `gate-skipped`
3. **ITC SLA alert** — when Epic in "Proposal Under Review" for >15 business days, notifies PM Admin
4. **CR trigger** — when Story set to Won't Do, auto-creates a Task: "Change Request required for [story name]"
5. **Weekly compliance digest** — Monday morning summary of any skipped or failed gates

---

## Step 6 — Create Dashboard

**Path**: Jira main navigation → Dashboards → Create Dashboard

Name: `Stage Gate Compliance`

Add these gadgets using the JQL filters from `dashboard-filters.md`:

| Gadget | Filter | Purpose |
|---|---|---|
| Issue Statistics | `issuetype = Bug AND labels = "gate-skipped"` | Skipped gate items count |
| Issue Statistics | `"Gate Status" = Failed` | Failed gates |
| Assigned to Me | Active epics with open gates | Your projects needing attention |
| Two Dimensional Filter Statistics | Stories by status | Dev pipeline health |
| Activity Stream | Project = MYS | Recent project activity |

---

## Step 7 — Create Test Project (Issue Templates)

To verify the setup works, create one test Epic with 9 child Stories:

1. **Create Epic**: "TEST — [Your Project Name]"
   - Set: Gate Status = Not Reached, Stage Number = 1

2. **Create 9 Stories** under the Epic (one per stage):
   - "Stage 1: Project Proposal — TEST"
   - "Stage 2: Project Initiation — TEST"
   - etc.
   - See `issue-templates.md` for the full pre-filled sub-task lists for each stage

3. **Test Gate 1 transition**:
   - Create a Sub-task under Stage 1 Story
   - Try to move Story to "Proposal Under Review" — automation should block it
   - Mark Sub-task Done, retry — should succeed

---

## Ongoing Maintenance

- **New project**: Create a new Epic, link 9 Stories (copy from templates), add Gate Criteria sub-tasks
- **Gate passing**: PM Admin reviews Gate Compliance Scorecard dashboard before approving any "Gate X Passed" transition
- **Skipped items**: Any `gate-skipped` Bug must be resolved or formally waived (RGC written approval) before the Epic can proceed
- **Process updates**: When RGC approves process changes, update the corresponding Jira issue templates and the `index.html` viewer
