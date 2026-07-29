# Gap Analysis — BAPS IT Stage Gate Process
**Review date**: July 2026
**Reviewed by**: PM Admin team + independent process review
**Source documents**: Stage-Gate Process (Draft).docx, StageGate_1_to_8_Reviewed_by_PM_Admins.xlsx

This document catalogs **32 gaps** across all 9 stages of the BAPS IT Stage Gate process. Each gap includes:
- The problem (what's missing or broken)
- Severity rating
- A concrete fix
- The document or Jira artefact that implements the fix

**Severity legend**: `CRITICAL` = blocks correct process execution | `HIGH` = significant risk if unresolved | `MEDIUM` = reduces quality/consistency | `LOW` = minor improvement

---

## Summary Table

| # | Stage | Gap | Severity |
|---|---|---|---|
| 1 | Stage 1 | Circular prerequisite — proposal is both stage name and prereq | CRITICAL |
| 2 | Stage 1 | No ITC review SLA | HIGH |
| 3 | Stage 1 | Gate decision states undefined | CRITICAL |
| 4 | Stage 1 | Communication cadence vague | MEDIUM |
| 5 | Stage 2 | Roles by title only, no named individual confirmation | HIGH |
| 6 | Stage 2 | EAB never defined anywhere | HIGH |
| 7 | Stage 2 | No MS Teams naming convention | MEDIUM |
| 8 | Stage 2 | Executive Summary deck template missing | MEDIUM |
| 9 | Stage 3 | No workshop minimum count, duration, or quorum | HIGH |
| 10 | Stage 3 | FRD writing can start before BRD/LFD gate formally closes | CRITICAL |
| 11 | Stage 3 | No Risk Register template or tool specified | HIGH |
| 12 | Stage 3 | No BAPS UI/UX Design System reference | MEDIUM |
| 13 | Stage 3 | QA involvement is informal — no artefact or storage | MEDIUM |
| 14 | Stage 4 | POC Register template missing | MEDIUM |
| 15 | Stage 4 | Design review has no SLA or outcome states | HIGH |
| 16 | Stage 5 | Change Request trigger is ambiguous | MEDIUM |
| 17 | Stage 5 | No Dependent Systems Agreement template | MEDIUM |
| 18 | Stage 6 | Package approval has no mechanism | HIGH |
| 19 | Stage 6 | Mid-feature demo has no template | LOW |
| 20 | Stage 7 | No defect severity classification (P0–P3) | CRITICAL |
| 21 | Stage 7 | UAT Sign-off has no standard format | HIGH |
| 22 | Stage 7 | No UAT tester minimum or training standard | MEDIUM |
| 23 | Stage 7 | Pilot stage is empty (no activities or gate criteria) | HIGH |
| 24 | Stage 8 | Hypercare duration and exit criteria undefined | CRITICAL |
| 25 | Stage 8 | Cybersecurity team / VAPT contact undefined | HIGH |
| 26 | Stage 8 | Retrospective has no template or standard agenda | MEDIUM |
| 27 | Stage 9 | Closure stage has no activities or gate criteria | HIGH |
| 28 | Stage 9 | Lessons learned never loops back into the process | MEDIUM |
| 29 | Cross-cutting | No Glossary of acronyms | CRITICAL |
| 30 | Cross-cutting | No Gate Compliance Scorecard | CRITICAL |
| 31 | Cross-cutting | No escalation path when a gate is skipped | HIGH |
| 32 | Cross-cutting | RACI abbreviations undefined inline | MEDIUM |

**Totals**: 6 Critical · 12 High · 12 Medium · 1 Low · 1 Low

---

## Stage 1 — Project Proposal

### Gap 1 — Circular prerequisite `CRITICAL`
**Problem**: "Project Proposal" is listed as a prerequisite of Stage 1, but Stage 1 IS the act of creating the proposal. A team cannot complete a prerequisite that is also the output of the stage.

**Fix**: Rename the prerequisite to **"Business Need Identified."** The entry condition for Stage 1 is that a department lead has a documented business problem (even in email or verbal form). The formal Project Proposal document is the Stage 1 *output*, not its input.

**Owner**: RGC | **Document**: Update Stage 1 prerequisites in process doc (SG0101)

---

### Gap 2 — No ITC review SLA `HIGH`
**Problem**: ITC can sit on a proposal indefinitely with no defined response time and no escalation path if they fail to act.

**Fix**: Add formal SLA to the process doc:
> *"ITC must provide a formal response within **15 business days** of submission. If no decision is reached after 2 ITC cycles (~30 business days), RGC escalates in writing to the BOD representative with a summary memo."*

**Owner**: ITC / RGC | **Document**: Update Gate 1 Criteria in process doc; add Jira automation alert

---

### Gap 3 — Gate decision states undefined `CRITICAL`
**Problem**: The current text says "a decision and priority is given" without defining what outcomes are valid. Teams cannot track proposal status or understand what a decision means.

**Fix**: Define 4 formal gate outcomes. All decisions must be documented in the Proposal Form and in Jira:

| Decision | Meaning | Required Documentation |
|---|---|---|
| **Approved** | Proceed to Stage 2. Resources allocated. | Decision + resource allocation logged in proposal form. |
| **Conditionally Approved** | Proceed, but named conditions must be resolved by Gate 2. | Conditions listed explicitly; become Gate 2 criteria. |
| **On Hold** | Deferred. Mandatory re-consideration date set. | Reason + date documented. Proposer notified within 2 days. |
| **Rejected** | Project will not proceed. | Rationale documented. Proposer notified within 2 days. |

**Owner**: ITC / BOD | **Document**: Update Gate 1 Criteria; create Decision States reference card

---

### Gap 4 — Communication cadence vague `MEDIUM`
**Problem**: "RGC should keep stakeholders informed at regular intervals" is unenforceable. There is no frequency, channel, or format specified.

**Fix**: Define cadence in process doc:
> *"RGC provides a written status update within **2 business days** of each ITC session via the project's MS Teams channel. If ITC has not met in the intervening period, a holding update is sent every **10 business days**."*

**Owner**: RGC | **Document**: SG0101 Communications activity

---

## Stage 2 — Project Initiation

### Gap 5 — Roles by title only, no named individuals `HIGH`
**Problem**: "Identify Initial Roles" can be satisfied by writing job titles (e.g., "PM = TBD"). There is no gate check that confirms named, reachable individuals are in place before the project proceeds.

**Fix**: Gate 2 exit criterion: *"Role Assignment Register completed with named individuals (not titles) confirmed and signed by RGC before Gate 2 closes."* Jira sub-task requires a Document Link to the signed register before it can be marked Done.

**Owner**: RGC | **Document**: Update Gate 2 Criteria; create Role Assignment Register template

---

### Gap 6 — EAB never defined `HIGH`
**Problem**: "EAB" appears in multiple RACI rows but is never explained anywhere in the process documents or guidelines. New PMs and team members have no idea who to contact or when.

**Fix**: Add to Glossary (done) and to the Stage 2 process doc:
> *"EAB = Enterprise Architecture Board. Responsible for technical standards, system integration, and architecture sign-offs. Current contact: [name/email]. Engage via RGC at the start of Stage 2. EAB review is mandatory before Gate 4 (Design sign-off)."*

**Owner**: RGC | **Document**: GLOSSARY.md; Stage 2 prerequisites

---

### Gap 7 — No MS Teams naming convention `MEDIUM`
**Problem**: Teams channels and project spaces are created ad hoc, making it impossible to find or filter projects consistently.

**Fix**: Define standard naming convention in ALM Setup Guideline (SG0203G):
> Format: `[ORG]-[ProjectCode]-[Year]` — e.g., `BAPS-GMS-2026`

All MS Teams and ALM projects must follow this convention. PM Admin verifies during Stage 2 setup sub-task.

**Owner**: PM-Admin | **Document**: SG0203G ALM Setup Guideline

---

### Gap 8 — Executive Summary deck template missing `MEDIUM`
**Problem**: Each kickoff meeting uses a different deck format, varying widely in quality and completeness.

**Fix**: Create a standard 5-slide kickoff deck template (SG0204T):
1. Project overview and justification (from proposal)
2. Approved scope (what is in / what is out)
3. Stage timeline with key milestone dates
4. Team RACI (one slide, all roles named)
5. Time commitment ask from Business Team (hours/week by stage)

**Owner**: RGC | **Document**: Create SG0204T

---

## Stage 3 — Requirements

### Gap 9 — No workshop minimum or quorum `HIGH`
**Problem**: A single rushed workshop could technically satisfy "workshops held." There is no minimum session count, duration, or attendance requirement.

**Fix**: Define minimums in SG0303G:
- Minimum **3 workshops** before BRD draft begins
- Each session: **90–180 minutes** (not shorter, not longer than 3 hours)
- Quorum: **FPO or designated BT lead must be present**. If quorum is not met, the session is void and must be rescheduled.
- Minutes uploaded to MS Teams within **2 business days** of each session

**Owner**: PM / BA | **Document**: SG0303G Requirements Workshop Guideline

---

### Gap 10 — FRD starts before BRD/LFD gate closes `CRITICAL`
**Problem**: The process describes FRD writing as a parallel activity to BRD+LFD, but sign-off on BRD+LFD is listed as a Gate Criteria item later. In practice, BAs start the FRD before the BT has approved the BRD, leading to rework when BT requests changes.

**Fix**: Add explicit mid-stage dependency rule:
> *"FRD writing may only commence after BRD and LFD have received formal sign-off (Gate Criteria item: BRD and LFD Sign-off). PM records sign-off confirmation in ALM before BA proceeds."*

In Jira: the FRD sub-task is blocked until the BRD+LFD Sign-off sub-task is marked Done.

**Owner**: PM / BA | **Document**: Stage 3 Activities; Jira automation rule

---

### Gap 11 — No Risk Register template `HIGH`
**Problem**: Risk tracking is mentioned as an activity but there is no standard template, tool, or review cadence defined. Risks are tracked inconsistently across projects.

**Fix**: Create Risk Register template (SG0306T) with columns:
`ID | Description | Probability (H/M/L) | Impact (H/M/L) | Risk Score | Mitigation | Owner | Status | Date Raised | Date Resolved`

- Stored in HawkEye (ALM) per project
- Reviewed at every weekly stand-up
- Risks rated **High × High** escalated to RGC within **2 business days**

**Owner**: PM | **Document**: Create SG0306T

---

### Gap 12 — No UI/UX Design System reference `MEDIUM`
**Problem**: LFD and HFD compliance reviews reference design system standards, but no design system document is cited. Designers cannot be reviewed against a standard that doesn't exist.

**Fix**: Either:
1. Reference the existing BAPS Design System URL in SG0305G (LFD) and SG0308G (HFD), OR
2. Flag as organizational blocker: *"Design System v1.0 must be published before any project may proceed to HFD phase."*

Until published, the HFD review gate uses the DES-Lead's written approval as a proxy.

**Owner**: DES-Lead / EAB | **Document**: SG0305G, SG0308G

---

### Gap 13 — QA involvement is informal `MEDIUM`
**Problem**: "QA starts the first round of writing QA scenarios" during Stage 3, but there is no artefact, storage location, review step, or completion criteria defined for this activity.

**Fix**: Add QA sub-task to Stage 3 Gate Criteria:
> *"QA Test Scenarios — Draft complete: scenarios stored in ALM Test Management, mapped to FRD requirements section by section, reviewed and approved by QA-Lead before Gate 3 closes."*

This makes QA an active participant in Stage 3, not a passive observer.

**Owner**: QA-Lead | **Document**: Stage 3 Gate Criteria; ALM test management setup

---

## Stage 4 — Technical Design

### Gap 14 — POC Register missing `MEDIUM`
**Problem**: POCs are described as necessary for mitigating technical risk, but there is no register to track them. Time can be spent on poorly scoped POCs with no approval or output requirement.

**Fix**: Create POC Register template (SG04POC-T) with columns:
`POC ID | Objective | Owner | Start Date | End Date | Time Budget (days) | Success Criteria | Output | SA Approved | PM Approved`

Each POC entry must be approved by SA and PM before work begins.

**Owner**: SA / PM | **Document**: Create SG04POC-T

---

### Gap 15 — Design review has no SLA or outcome states `HIGH`
**Problem**: The HFD design review is described as a compliance check by the DES-Lead, but there is no time limit, no defined outcome, and no escalation if reviews drag on.

**Fix**:
- **SLA**: DES-Lead must complete design review within **3 business days** of submission
- **Outcome states**: Approved / Revise & Resubmit (max 2 revision cycles, then escalates to PM)
- DES-Lead documents outcome in ALM comment and updates the Gate Status field

**Owner**: DES-Lead / PM | **Document**: SG0309G HFD Review Guideline

---

## Stage 5 — Estimate & Planning

### Gap 16 — Change Request trigger is ambiguous `MEDIUM`
**Problem**: The process says CR process starts "after FRD sign-off" in one place and "after design is complete and signed off" in another. Teams are confused about when CRs are required.

**Fix**: Clarify with a single authoritative rule:
> *"The Change Request process activates at **Gate 3 close** (FRD + HFD signed off). From that point forward, any new requirement, scope addition, or design change — regardless of which stage the project is in — must follow the CR process. This applies from Stage 4 through go-live."*

**Owner**: PM | **Document**: Create SG05CR-G Change Request Guideline; reference in Stage 4 and 5 process docs

---

### Gap 17 — No Dependent Systems Agreement template `MEDIUM`
**Problem**: Getting sign-off from teams who own systems this project depends on is described as an activity, but there is no standard artefact. Sign-offs are made verbally or in ad hoc emails.

**Fix**: Create a lightweight Dependent Systems Agreement (SG05DEP-T):

| Field | Content |
|---|---|
| Dependent System Name | |
| System Owner / TPO | |
| Planned Change / Integration | |
| Impact on Dependent System | |
| Agreed UAT Integration Date | |
| Agreed Production Integration Date | |
| FPO Sign-off | |
| Date | |

**Owner**: SA / PM | **Document**: Create SG05DEP-T

---

## Stage 6 — Development

### Gap 18 — Package approval has no mechanism `HIGH`
**Problem**: The process states all package dependencies must be pre-approved, but there is no list, no approval process, and no enforcement mechanism. Any developer can add any package.

**Fix**:
- TL maintains an **Approved Package Register** in the repository root (e.g., `approved-packages.json`)
- Any new package requires a Pull Request to this file, reviewed and approved by SA before the dependency can be added to code
- CI/CD pipeline is configured to **fail the build** if a package not in the approved list is introduced
- Register includes: package name, version range, approved date, approved by, reason

**Owner**: TL / SA | **Document**: SG06xxG Code Standards Guideline; CI/CD pipeline config

---

### Gap 19 — Mid-feature demo has no template `LOW`
**Problem**: The SA walkthrough conducted after each feature is complete has no agenda, sign-off record, or storage location. Quality varies entirely by person.

**Fix**: Create a 10-minute SA Feature Demo Checklist (SG06DEMO-T):

| Field | |
|---|---|
| Feature name | |
| FRD section reference | |
| Design section reference | |
| Demo date | |
| SA attended (Y/N) | |
| Issues raised | |
| SA approval (Y/N) | |

Stored in ALM against the Story.

**Owner**: SA | **Document**: Create SG06DEMO-T

---

## Stage 7 — UAT

### Gap 20 — No defect severity classification `CRITICAL`
**Problem**: The process says "fix critical issues as hotfixes" but never defines what "critical" means. Different people have different interpretations, leading to disputes about what must be resolved before sign-off.

**Fix**: Define severity levels in the process doc and link from all UAT templates:

| Level | Name | Definition | Impact on UAT |
|---|---|---|---|
| **P0** | Critical | System crash, data loss, security breach, or core function completely unavailable | Blocks UAT. Must be fixed and retested before sign-off. |
| **P1** | High | Core business function broken, no acceptable workaround exists | Blocks sign-off unless FPO formally waives in writing. |
| **P2** | Medium | Non-core function broken or degraded, a workaround exists | Must be in the fix backlog with a committed release date before sign-off. |
| **P3** | Low | Cosmetic issue, minor UX improvement, text error | Logged. Scheduled for next release. Does not block sign-off. |

**Owner**: QA-Lead / PM | **Document**: Create SG07SEV-G Defect Severity Guideline; reference in UAT Gate Criteria

---

### Gap 21 — UAT Sign-off has no standard format `HIGH`
**Problem**: "A formal sign-off must be provided by the business team" but there is no template. Some teams accept a verbal yes; others send a one-line email.

**Fix**: Create UAT Sign-off Form (SG07UAT-T) including:
- Project name and release version
- Sign-off date
- FPO name and signature
- List of known open issues at sign-off (with P-level and planned fix release for each)
- Statement: *"The Business Team confirms this system is fit for production deployment subject to the open issues listed above."*

Stored in MS Teams project folder before Gate 7 can be marked closed.

**Owner**: FPO / PM | **Document**: Create SG07UAT-T

---

### Gap 22 — No UAT tester minimum or training standard `MEDIUM`
**Problem**: "Business team should identify all UAT testers" provides no minimum number, no persona coverage requirement, and no training step before testers begin.

**Fix**: Define in SG07xxG:
- Minimum **one tester per user persona** defined in the BRD
- All testers must attend the UAT kickoff meeting (mandatory; no-shows cannot contribute to sign-off)
- BA provides a **30-minute system walkthrough** before testing begins
- Testers who did not attend kickoff and walkthrough cannot sign off on UAT

**Owner**: PM / BT | **Document**: SG07xxG UAT Planning Guideline

---

### Gap 23 — Pilot stage is empty `HIGH`
**Problem**: The Pilot stage is listed as optional and has two prerequisites but zero activities or gate criteria. Teams choosing a pilot have no guidance whatsoever.

**Fix**: Define minimum Pilot structure:

**Prerequisites**: Production environment ready, smoke test passed, pilot user group identified (named list, minimum 1 centre or department, FPO confirmed).

**Activities**:
- Pilot kickoff meeting with pilot group
- Daily check-in for first week, then every 2 days
- Feedback collection and daily grooming by BT
- Issue triage: P0/P1 fixed immediately; P2/P3 backlogged

**Gate Criteria**:
- Pilot Sign-off from pilot group FPO
- All P0 and P1 issues resolved
- Pilot run for minimum **2 weeks** (4 weeks for high-risk projects)

**Owner**: PM / FPO | **Document**: Create SG08PILOT-G

---

## Stage 8 — Launch & Hypercare

### Gap 24 — Hypercare duration and exit criteria undefined `CRITICAL`
**Problem**: The process says hypercare ends when "all changes are taken in a future release" — which could mean day 1 or day 365. There is no minimum duration, no exit criteria, and no formal handover to steady-state support.

**Fix**: Define hypercare policy:
- **Standard projects**: minimum **2 weeks** post go-live
- **High-risk projects** (new systems, PII data, >500 users): minimum **4 weeks**
- **Exit criteria** (all three must be met):
  1. No P0 or P1 open issues for **5 consecutive business days**
  2. Support team has completed knowledge transfer and can handle escalations independently
  3. PM Admin formally closes hypercare in Jira (Epic moved to "Hypercare Complete")
- After hypercare: only P0 issues get immediate response; all others require ITC approval for next release

**Owner**: PM-Admin / Support | **Document**: SG08HYP-G Hypercare Policy

---

### Gap 25 — Cybersecurity team / VAPT contact undefined `HIGH`
**Problem**: "Cybersecurity team performs final VAPT checks" but who they are, how to engage them, their availability, and their turnaround time is not documented anywhere.

**Fix**: Add to Glossary and to Stage 6 + Stage 8 process docs:
> *"SEC = Cybersecurity / VAPT team. Contact: [name/email — to be populated by RGC]. VAPT request must be submitted at least **3 weeks** before planned go-live date. The SEC team issues a VAPT Certificate within **5 business days** of receiving the final build. All Critical findings must be resolved before the certificate is issued."*

**Owner**: RGC / SEC | **Document**: GLOSSARY.md; SG06 and SG08 stage docs

---

### Gap 26 — Retrospective has no template `MEDIUM`
**Problem**: Two retrospectives are listed (Delivery Team and Business Team) but there is no template, agenda, or format. Lessons learned will not be captured consistently and will not improve future projects.

**Fix**: Create Retrospective Template (SG08RETRO-T) with 5 sections:
1. What went well (keep doing this)
2. What didn't go well (stop or change)
3. Root cause of the top 3 issues
4. Action items with named owners and dates
5. Process improvement recommendations (fed back to RGC for Stage Gate process review)

Outcomes stored in a shared **Lessons Learned Log** accessible across all projects.

**Owner**: PM / PM-Admin | **Document**: Create SG08RETRO-T; create Lessons Learned Log

---

## Stage 9 — Project Closure

### Gap 27 — Closure stage has no activities or gate criteria `HIGH`
**Problem**: Stage 9 (Project Closure) contains only one line: "Common Activities across all stages / Weekly project status." There are no closure-specific activities, no archival steps, and no formal gate. Projects effectively never close.

**Fix**: Define Stage 9 activities and Gate Criteria:

**Activities**:
1. All project documentation finalized and stored in MS Teams project folder
2. ALM/Jira Epic moved to Done; all open issues triaged (P0/P1 handled, rest backlogged)
3. All team access revoked via offboarding checklist
4. Lessons Learned Log updated with retrospective outputs

**Gate Criteria** (all required before project is formally closed):
- Project Closure Report (SG09-T) completed and signed by PM Admin
- ITC and BOD notified with project summary
- All agreed CRs for the release are deployed and validated

**Owner**: PM-Admin | **Document**: Create SG09-T Project Closure Report template

---

### Gap 28 — Lessons learned never feeds back into the process `MEDIUM`
**Problem**: Retrospective outputs are captured (once Gap 26 is fixed) but there is no mechanism for them to improve future stage gate iterations. The process will become stale.

**Fix**: Add to process governance section:
> *"Lessons Learned from each project retrospective are reviewed by RGC **quarterly**. If 2 or more projects raise the same issue, it triggers a Stage Gate process review cycle. Process changes are versioned (e.g., v1.1, v1.2), communicated to all active PMs, and reflected in the process doc, HTML viewer, and Jira templates within 30 days of approval."*

**Owner**: RGC | **Document**: Process governance section; quarterly review calendar item

---

## Cross-cutting Gaps

### Gap 29 — No Glossary `CRITICAL`
**Problem**: Acronyms RGC, ITC, BOD, EAB, FPO, BT, SA, TL, BA, DES, QA, RACI, BRD, FRD, LFD, HFD, ALM, CR, VAPT, SDLC, POC, FRD-TM, TDD, SAD, MOM, SME, TPO, SLA, ROI, CI/CD, UAT, UAT are used throughout all documents without ever being defined in one place.

**Fix**: Created `GLOSSARY.md` in the repository root. All process documents and Jira issue templates link to it.

**Status**: ✅ Fixed — see `GLOSSARY.md`

---

### Gap 30 — No Gate Compliance Scorecard `CRITICAL`
**Problem**: There is currently no way to prove a gate was properly passed. Any team could mark a stage complete without completing the gate criteria, with no audit trail.

**Fix**: Gate Compliance Scorecard is a Jira dashboard view showing — per project, per gate — how many checklist items were: (a) Done, (b) Skipped (Won't Do), (c) Still open. Built from the `Stage Number` custom field + sub-task status. PM Admin must review this scorecard before approving any gate transition. Skipped items require RGC written waiver, logged in Jira.

**Owner**: PM-Admin | **Implementation**: Jira dashboard — see `jira/dashboard-filters.md`

---

### Gap 31 — No escalation path for skipped gates `HIGH`
**Problem**: If a team skips a gate item, there is no defined consequence, no escalation, and no formal waiver process. In practice, gate criteria are frequently skipped with no accountability.

**Fix**: Define skipped-gate policy:
1. Sub-task marked `Won't Do` → Jira automation creates a Bug flagged `gate-skipped`
2. Project Epic is automatically moved to **On Hold** until the PM Admin resolves the item
3. Resolution options: (a) complete the item, or (b) obtain a formal **written waiver from RGC** documented in the Jira issue
4. Waivers are logged in the Gate Compliance Scorecard for audit purposes

**Owner**: PM-Admin / RGC | **Implementation**: Jira automation rule — see `jira/automation-rules.md`

---

### Gap 32 — RACI abbreviations undefined inline `MEDIUM`
**Problem**: RACI rows throughout the process doc use abbreviations (R, A, C, I) that are not defined inline. Readers unfamiliar with RACI need to look it up externally.

**Fix**: Every RACI reference in the process doc and in Jira sub-task descriptions includes or links to the mini-legend:
> R = Responsible (does the work) · A = Accountable (signs off) · C = Consulted (input required) · I = Informed (FYI only)

This legend is also at the top of `GLOSSARY.md`.

**Status**: ✅ Fixed — see `GLOSSARY.md`
