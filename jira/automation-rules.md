# Jira Automation Rules — Stage Gate Compliance
**Path to configure**: Project Settings → Automation → Create Rule

Each rule below includes the exact trigger, condition, and action to configure in Jira.

---

## Rule 1 — Gate Blocker

**Name**: `SGP: Block gate transition if checklist incomplete`
**When to run**: Single project

### Configuration

**Trigger**: Issue transitioned
- Issue types: Epic, Story
- To status: *any "Under Review" status* (Proposal Under Review, Initiation Under Review, Requirements Under Review, Design Under Review, Planning Under Review)

**Condition**: Sub-tasks incomplete
- Add condition: "Sub-tasks" → "All sub-tasks are done" = FALSE

**Action (if condition NOT met)**:
1. Transition issue back to previous status
2. Add comment to issue:
   ```
   ⛔ Gate transition blocked.

   The following Gate Criteria items are not yet complete:
   {{issue.subtasks.filter(status != "Done").map(s => "• " + s.summary).join("\n")}}

   All Gate Criteria sub-tasks must be marked Done before this gate can pass.
   If you need to skip an item, mark it "Won't Do" — this will trigger a formal review by PM Admin.
   ```
3. Notify assignee + reporter

---

## Rule 2 — Skipped Item Flag

**Name**: `SGP: Flag skipped gate item and put project On Hold`
**When to run**: Single project

### Configuration

**Trigger**: Issue transitioned
- Issue types: Sub-task
- To status: Won't Do

**Actions** (run in sequence):

1. **Create Bug issue** linked to parent:
   - Summary: `⚠️ Skipped gate item: {{issue.summary}}`
   - Description:
     ```
     A gate checklist item was marked "Won't Do" without a formal waiver.

     Skipped item: {{issue.summary}}
     Stage: {{issue.customfield_stageNumber}}
     Parent issue: {{issue.parent.key}} — {{issue.parent.summary}}
     Skipped by: {{issue.assignee}}
     Date: {{now.format("dd MMM yyyy")}}

     REQUIRED ACTION: PM Admin must either:
     (a) Confirm the item has been completed via an alternative method, OR
     (b) Obtain written waiver approval from RGC and document it in this issue.

     Until resolved, the parent project Epic will be placed On Hold.
     ```
   - Label: `gate-skipped`
   - Assign to: PM Admin user
   - Priority: High

2. **Transition parent Epic** to "On Hold" status

3. **Add comment to parent Epic**:
   ```
   ⚠️ This project has been automatically placed On Hold.

   Reason: A gate checklist item was skipped without a formal waiver.
   Skipped item: {{issue.summary}}
   Review issue: [created Bug key]

   PM Admin must resolve before this project can proceed.
   ```

4. **Notify** PM Admin and Epic owner

---

## Rule 3 — ITC SLA Alert

**Name**: `SGP: Alert when proposal review exceeds 15 business days`
**When to run**: Scheduled

### Configuration

**Trigger**: Scheduled
- Frequency: Every weekday at 9:00 AM
- JQL to find issues: `issuetype = Epic AND status = "Proposal Under Review"`

**Condition**: For each issue found, check:
- `issue.statusCategoryChangedDate` is more than 21 calendar days ago
  *(21 calendar = ~15 business days; adjust for your team's working week)*

**Actions**:

1. **Add comment to Epic**:
   ```
   🕐 ITC Review SLA Reminder

   This proposal has been in "Proposal Under Review" for more than 15 business days.

   Per the Stage Gate process, ITC must respond within 15 business days of submission.

   Required action: RGC to follow up with ITC and, if still no decision after 30 business days total, escalate to BOD representative with a written memo.

   Submitted: {{issue.created.format("dd MMM yyyy")}}
   Days in review: {{now.diff(issue.statusCategoryChangedDate, "days")}} calendar days
   ```

2. **Send email notification** to PM Admin and RGC contacts

---

## Rule 4 — Change Request Trigger

**Name**: `SGP: Auto-create Change Request task when Story descoped`
**When to run**: Single project

### Configuration

**Trigger**: Issue transitioned
- Issue types: Story
- To status: Won't Do

**Condition**: Parent Epic status is NOT "New Proposal Submitted" or "Proposal Under Review" or "Initiation Active"
*(Only trigger CR if we're past Gate 3 — earlier descoping is fine without a CR)*

**Actions**:

1. **Create Task** linked to Story:
   - Summary: `CR Required: {{issue.summary}}`
   - Description:
     ```
     A Change Request is required for the following descoped story.

     Story: {{issue.key}} — {{issue.summary}}
     Parent Epic: {{issue.parent.key}}
     Descoped by: {{issue.assignee}}
     Date: {{now.format("dd MMM yyyy")}}

     The Change Request process (SG05CR-G) must be followed.
     This CR must be approved before the scope reduction is confirmed.

     Impact assessment required:
     - [ ] Does this affect other stories or dependencies?
     - [ ] Does this require BT notification?
     - [ ] Does this change the project timeline?
     - [ ] Does this require ITC re-approval?
     ```
   - Assign to: PM
   - Label: `change-request`
   - Priority: Medium

2. **Add comment to descoped Story**:
   ```
   📋 Change Request raised: [CR Task key]
   This story has been descoped. The linked Change Request must be approved before the descoping is confirmed.
   ```

---

## Rule 5 — Weekly Compliance Digest

**Name**: `SGP: Weekly gate compliance summary`
**When to run**: Scheduled

### Configuration

**Trigger**: Scheduled
- Frequency: Every Monday at 8:00 AM

**Actions** (run without conditions — always post):

1. **Create Task** in project as a weekly digest:
   - Summary: `Weekly Gate Compliance Digest — {{now.format("dd MMM yyyy")}}`
   - Description (uses JQL-populated smart values):
     ```
     📊 Weekly Stage Gate Compliance Summary
     Generated: {{now.format("dd MMM yyyy, HH:mm")}}

     ── SKIPPED GATE ITEMS (action required) ──
     Open gate-skipped bugs: [filter: issuetype = Bug AND labels = "gate-skipped" AND resolution = Unresolved]

     ── FAILED GATES ──
     Epics/Stories with Gate Status = Failed: [filter: "Gate Status" = Failed]

     ── PROJECTS ON HOLD ──
     Epics currently On Hold: [filter: issuetype = Epic AND status = "On Hold"]

     ── OVERDUE REVIEWS ──
     Stories in Code Review > 3 days: [filter: issuetype = Story AND status = "Code Review" AND updated <= "-3d"]
     Stories in UAT > 5 days: [filter: issuetype = Story AND status = "UAT In Progress" AND updated <= "-5d"]

     Review the Stage Gate Compliance dashboard for full details.
     ```
   - Assign to: PM Admin
   - Label: `compliance-digest`

> **Note**: For Slack notifications, if your Jira is connected to Slack, replace the "Create Task" action with "Send Slack message" to your team's project channel using the same message body.
