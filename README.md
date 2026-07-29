# BAPS IT Stage Gate Process

A structured, stage-by-stage governance framework for software project delivery — from initial proposal through to project closure.

**Live viewer**: [baps-stage-gate-process](https://pankaj117-dev.github.io/baps-stage-gate-process) *(GitHub Pages — enabled after first push)*

---

## What is this?

The BAPS IT Stage Gate Process is an 8-stage software delivery lifecycle designed for a volunteer IT organization. It ensures that no project proceeds to the next phase without passing a formal gate — a deliberate decision point where evidence is reviewed and a Go / Kill / Hold / Recycle decision is made.

This repository contains:
- An **interactive HTML viewer** (`index.html`) — open in any browser, share by URL or email
- A **full gap analysis** of the current process with 32 findings and concrete fixes
- A **Jira setup guide** for configuring the MYS sandbox with gate-enforcing workflows
- A **team education guide** for onboarding new volunteers to the process
- A **glossary** of every acronym used

---

## The 8 Stages at a Glance

```
Stage 1 → Project Proposal       Gate: ITC/BOD Approval
Stage 2 → Project Initiation     Gate: Charter signed, kickoff held, roles named
Stage 3 → Requirements           Gate: BRD+LFD sign-off → FRD+HFD sign-off
Stage 4 → Technical Design       Gate: TDD signed off by EAB
Stage 5 → Estimate & Planning    Gate: BT sign-off on timeline + scope
Stage 6 → Development            Gate: Code quality, QA tests, VAPT Round 1
Stage 7 → UAT                    Gate: FPO sign-off, no P0/P1 open defects
Stage 8 → Launch & Hypercare     Gate: VAPT Certificate, go-live, hypercare exit
Stage 9 → Project Closure        Gate: Closure Report, team offboarded, lessons logged
```

---

## Gate Decision Outcomes

Every gate produces one of four formal decisions, documented in writing:

| Decision | Meaning |
|---|---|
| **Approved** | Proceed to next stage. Resources allocated. |
| **Conditionally Approved** | Proceed, but named conditions must be resolved by the next gate. |
| **On Hold** | Deferred. Re-consideration date is mandatory. Reason documented. |
| **Rejected / Killed** | Project will not proceed. Rationale documented. Proposer notified within 2 business days. |

---

## Exit Points

The process has three strategic exit points that give departments flexibility without bypassing governance:

| Exit | When | What Happens |
|---|---|---|
| **Exit A** | Before Stage 1 begins | Department self-manages with their own team. Central governance (security, architecture) still applies. |
| **Exit B** | After Stage 3 (Requirements done) | Department uses BAPS BAs for requirements, then issues an RFP to an external vendor for the build. |
| **Exit C** | After Stage 5 (Estimate done) | IT estimate exceeds budget/timeline. Department finds an external solution. IT is not pressured to rush. |

---

## Why Stage Gates?

**Cost of Defect principle**: A bug found during requirements costs ~$1 to fix (rewrite a sentence). The same bug found in production costs ~$1,000 (emergency fix, rollback, user impact, data risk). Stage gates force the team to "fail on paper first" — discovering issues early when they are cheap and easy to fix.

**Fully-baked philosophy**: It is always better to delay a feature than to release a broken one. The stage gate process ensures requirements are solid before design starts, design is solid before development starts, and development is tested before it reaches users.

---

## Repository Structure

```
stage-gate-process/
├── index.html                         ← Interactive stage-by-stage viewer
├── README.md                          ← This file
├── GLOSSARY.md                        ← All acronyms defined
├── gap-analysis/
│   └── gap-analysis.md                ← 32 gaps with severity and fixes
├── jira/
│   ├── jira-setup-guide.md            ← Step-by-step MYS sandbox setup
│   ├── workflow-states.md             ← Epic + Story workflow definitions
│   ├── automation-rules.md            ← Gate compliance automation
│   ├── dashboard-filters.md           ← JQL compliance queries
│   └── issue-templates.md             ← Pre-filled stage templates
└── education/
    └── stage-gate-onboarding.md       ← Plain-language guide for new volunteers
```

---

## Industry Context

This process is modeled on **Cooper's Stage-Gate® framework** (the industry gold standard for structured project delivery) and adapted for a volunteer nonprofit IT organization.

| Cooper 5-Stage | BAPS 8-Stage Equivalent |
|---|---|
| Discovery | Stage 1: Project Proposal |
| Scoping | Stage 2: Project Initiation |
| Build Business Case | Stage 3: Requirements |
| Development | Stages 4–6: Design, Estimate, Development |
| Testing & Launch | Stages 7–9: UAT, Launch & Hypercare, Closure |

The BAPS model adds important extensions not in the original Cooper model:
- BRD/FRD split (prevents design starting on incomplete requirements)
- Exit Points A/B/C (prevents IT burnout from unrealistic demands)
- Readiness overlap model (prerequisites for next stage begin while current stage runs)
- Volunteer-specific RACI (accounts for limited availability and rotating team members)

---

## Key Contacts

| Role | Responsibility | Contact |
|---|---|---|
| RGC | Process governance, proposal coordination | apps.rgc@na.baps.org |
| ITC | Project approval and prioritization | Via RGC |
| EAB | Architecture sign-offs | Via RGC |
| SEC | VAPT and cybersecurity | Via RGC |

---

## References & Links

- [GLOSSARY.md](./GLOSSARY.md) — All acronyms
- [Gap Analysis](./gap-analysis/gap-analysis.md) — 32 process gaps with fixes
- [Jira Setup Guide](./jira/jira-setup-guide.md) — Configure MYS sandbox
- [Education Guide](./education/stage-gate-onboarding.md) — For new volunteers
- [Interactive Viewer](./index.html) — Open locally or via GitHub Pages
