# Jira Dashboard & JQL Filters — Stage Gate Compliance

These saved filters power the Stage Gate Compliance dashboard. Create each as a **Saved Filter** in Jira, then add them as gadgets to the dashboard.

**Path to create filters**: Issues → Search for Issues → [build query] → Save As
**Path to create dashboard**: Dashboards → Create Dashboard → Add Gadgets

---

## Saved Filters

### Filter 1 — Skipped Gate Items (Open)
```jql
project = MYS
AND issuetype = Bug
AND labels = "gate-skipped"
AND resolution = Unresolved
ORDER BY created DESC
```
**Purpose**: Shows all gate items that were skipped without a formal waiver. Every item here is an action required for PM Admin.
**Dashboard gadget**: Issue Statistics (by Assignee) or Issue List

---

### Filter 2 — Failed Gates
```jql
project = MYS
AND "Gate Status" = Failed
ORDER BY updated DESC
```
**Purpose**: All Epics and Stories where a gate was formally marked as Failed. Tracks which projects had gate failures and when.
**Dashboard gadget**: Issue Statistics (by Issue Type)

---

### Filter 3 — Active Projects with Open Gates
```jql
project = MYS
AND issuetype = Epic
AND status not in ("Project Closed", "Killed", "On Hold")
AND "Gate Status" not in ("Passed")
ORDER BY updated ASC
```
**Purpose**: Epics that are active but whose current gate has not been formally passed. Oldest-updated first (most stalled).
**Dashboard gadget**: Issue List (columns: Key, Summary, Status, Gate Status, Assignee, Updated)

---

### Filter 4 — Projects Currently On Hold
```jql
project = MYS
AND issuetype = Epic
AND status = "On Hold"
ORDER BY updated ASC
```
**Purpose**: All projects currently paused. Oldest hold date first — these need attention before they go stale.
**Dashboard gadget**: Issue List

---

### Filter 5 — Stories in Code Review > 3 Days
```jql
project = MYS
AND issuetype = Story
AND status = "Code Review"
AND updated <= "-3d"
ORDER BY updated ASC
```
**Purpose**: Stories sitting in code review longer than the 3-day SLA. Flag for TL/PM follow-up.
**Dashboard gadget**: Issue Statistics or Issue List

---

### Filter 6 — Stories in UAT > 5 Days
```jql
project = MYS
AND issuetype = Story
AND status = "UAT In Progress"
AND updated <= "-5d"
ORDER BY updated ASC
```
**Purpose**: UAT sessions that are running long. Possible FPO availability issue or undeclared defects.
**Dashboard gadget**: Issue List

---

### Filter 7 — Open Change Requests
```jql
project = MYS
AND issuetype = Task
AND labels = "change-request"
AND resolution = Unresolved
ORDER BY created DESC
```
**Purpose**: All open CRs across all projects. PM Admin tracks these for approval and scope tracking.
**Dashboard gadget**: Issue Statistics (by Priority)

---

### Filter 8 — Gate Compliance Scorecard (per Stage)
```jql
project = MYS
AND issuetype = Sub-task
AND "Stage Number" in (1, 2, 3, 4, 5, 6, 7, 8, 9)
ORDER BY "Stage Number" ASC, status ASC
```
**Purpose**: Full list of all gate checklist sub-tasks across all stages. Use the "Two Dimensional Filter Statistics" gadget with:
- X-axis: Stage Number
- Y-axis: Status (Done vs Won't Do vs In Progress vs To Do)

This is the **Gate Compliance Scorecard** — PM Admin reviews this before approving any gate transition.

---

### Filter 9 — Weekly Digest Issues
```jql
project = MYS
AND issuetype = Task
AND labels = "compliance-digest"
ORDER BY created DESC
```
**Purpose**: Archive of all weekly compliance digests. Useful for trend analysis.

---

## Dashboard Setup

**Path**: Dashboards → Create Dashboard → Name: `Stage Gate Compliance`

Recommended gadget layout (2-column):

| Left Column | Right Column |
|---|---|
| **Issue Statistics** — Filter 1 (Skipped Items) | **Issue Statistics** — Filter 2 (Failed Gates) |
| **Issue List** — Filter 3 (Active open gates) | **Issue List** — Filter 4 (On Hold projects) |
| **Issue List** — Filter 5 (Code Review overdue) | **Issue List** — Filter 6 (UAT overdue) |
| **Two Dimensional Filter Statistics** — Filter 8 (Scorecard) | **Issue Statistics** — Filter 7 (Open CRs) |

### How PM Admin uses this dashboard

1. **Monday morning**: Review Filter 1 (skipped items) and Filter 2 (failed gates) first. Resolve any outstanding items before the week's gate reviews begin.

2. **Before approving any gate transition**: Pull up Filter 8 (Gate Compliance Scorecard). Confirm:
   - All Gate Criteria sub-tasks for the current stage are Done
   - Zero `Won't Do` sub-tasks without a documented RGC waiver
   - Gate Status field on the parent is ready to be set to "Passed"

3. **Weekly**: Share the compliance digest (auto-created by Rule 5) with RGC.

4. **Monthly**: Export Filter 3 trends — which stages are most often blocked, which gates take longest. Feed this into the quarterly RGC process review.
