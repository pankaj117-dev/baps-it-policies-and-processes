# Stage Gate Process — Volunteer Onboarding Guide

**Who this is for**: Anyone new to the BAPS IT team — whether you are a developer, BA, designer, QA analyst, or a business stakeholder.

**What you will learn**: What the stage gate process is, why it exists, how it affects your role, and what happens if gates are not followed.

---

## The 60-Second Version

Every IT project at BAPS goes through **9 stages**. Between each stage there is a **gate** — a formal review where a decision is made to either continue, pause, or stop the project.

You **cannot skip a gate**. You **cannot start the next stage** until the current gate passes.

This might feel slow at first. It isn't. It prevents the much more painful experience of building the wrong thing, discovering it in production, and spending 10× the effort fixing it.

---

## Why Does This Process Exist?

### The Cost of Defect

Imagine you're building a house. If the architect draws the rooms in the wrong place, catching that on the blueprint costs almost nothing — erase and redraw.

If you catch it after the walls are built, it costs thousands to tear them down.

If you catch it after the family has moved in, it costs tens of thousands, plus the disruption to their lives.

Software is the same:

| When the error is found | Approximate cost to fix |
|---|---|
| During requirements (on paper) | $1 |
| During development | $100 |
| After production launch | $1,000+ |

Stage gates force us to **fail on paper first**. Every gate is a chance to catch errors before they become expensive.

### The "Fully Baked" Philosophy

It is always better to delay a feature than to release it broken.

When stakeholders pressure the team to "just launch it and fix it later," they are accepting a hidden cost: emergency fixes, user frustration, data issues, and lost trust. The stage gate process gives the team a structured way to say "we're not ready yet" — backed by evidence, not opinion.

---

## The 9 Stages at a Glance

```
STAGE 1 → Project Proposal
  Who: Department lead + RGC + ITC
  What: Is this project worth doing? Approved?
  Gate: ITC/BOD decision (Approved / On Hold / Rejected)

STAGE 2 → Project Initiation
  Who: RGC, PM, named team
  What: Charter signed, team in place, kickoff held
  Gate: All roles named, kickoff meeting done, MS Teams + ALM set up

STAGE 3 → Requirements
  Who: BA, DES, BT (FPO + SMEs)
  What: BRD + LFD → (mid-gate) → FRD + HFD
  Gate: BRD+LFD signed off, then FRD+HFD signed off by Sanyojak + FPO

STAGE 4 → Technical Design
  Who: SA, TL, EAB
  What: Architecture, TDD, traceability matrix
  Gate: TDD signed off by EAB

STAGE 5 → Estimate & Planning
  Who: PM, SA, TL, Devs, QA
  What: Story estimates, release timeline, formal "Handshake" with BT
  Gate: BT sign-off on timeline + scope (firm commitment)

STAGE 6 → Development
  Who: TL, Devs, QA, SA
  What: Build per design. Code reviewed, tested (≥80% coverage), VAPT Round 1
  Gate: All QA tests pass, VAPT cleared, deployment checklist ready

STAGE 7 → UAT
  Who: BT (testers), FPO, BA, QA
  What: Business team tests in UAT environment, P0/P1 issues resolved
  Gate: FPO sign-off form completed, no P0/P1 open

STAGE 8 → Launch & Hypercare
  Who: Infra, TL, PM, Support team
  What: Deploy to production, verify, support for 2–4 weeks
  Gate: VAPT Certificate, go-live smoke test passed, hypercare exit criteria met

STAGE 9 → Project Closure
  Who: PM-Admin
  What: Archive docs, revoke access, lessons learned logged
  Gate: Closure Report signed, ITC/BOD notified
```

---

## Your Role in the Process

### If you are a Developer (DEV / TL)

- **Stage 5**: You will estimate user stories. Use increments: 2, 4, 8, 12, 16, 24, 32, or 40 hours.
- **Stage 6**: Follow code standards, git guidelines, and get your code peer-reviewed. Minimum 80% test coverage.
- **Every package you add** must be in the Approved Package Register. If it's not there, raise it with the TL/SA before adding.
- **Mid-feature**: SA will walk through your completed feature. Have FRD + design sections ready.

### If you are a Business Analyst (BA)

- **Stage 3**: You run requirement workshops (minimum 3 sessions, 90–180 mins each). You write the BRD and then — only after BT signs off — the FRD.
- **Important**: Do NOT start the FRD until the BRD + LFD sign-off is formally closed. Starting early creates rework risk.
- **Traceability**: Every BRD requirement must map to a FRD section. You own this matrix.

### If you are a Designer (DES)

- **Stage 3**: You build LFDs alongside the BRD. HFDs come after BRD+LFD are signed off.
- **Before showing HFDs to BT**: DES-Lead must review your designs against the BAPS Design System. Get this done within 3 business days.
- **Revision cycles**: Maximum 2 Revise & Resubmit cycles before the review escalates to PM.

### If you are a QA Analyst

- **Stage 3**: You start writing test scenarios as FRD sections are completed. These are a mandatory Gate 3 exit item.
- **Stage 6**: You execute all test cases. All must pass — including API SLA performance tests — before the gate closes.
- **Stage 7 (UAT)**: You run the UAT environment smoke test before business testing begins. You support the BT during testing but you do not close the gate — that's the FPO.

### If you are a Business Team Member / Stakeholder (FPO / SME / Sanyojak)

- **Stages 3–5**: Your time is most important here. Requirements workshops require your presence (quorum = you or your delegate must attend). If you miss workshops, the project is delayed.
- **Sign-offs**: You will be asked to formally sign off on BRD, FRD, and the release timeline. Read these documents — they define exactly what will be built. Changes after sign-off require a Change Request.
- **UAT**: You lead the testing. You decide if the system is ready. Your sign-off (the UAT Sign-off Form) is the gate. Be honest about known issues — they are documented in the form, not hidden.

### If you are a Project Manager (PM)

- You are accountable for gate progression. You cannot mark a gate passed without the Gate Compliance Scorecard showing all sub-tasks Done.
- You run the Risk Register from Stage 3 onward. H×H risks escalated to RGC within 2 business days.
- Change Requests are your responsibility to log, track, and get approved.

---

## What Happens If Someone Skips a Gate?

This is not a hypothetical — it has happened. Here is what the process does:

1. **In Jira**: If a gate checklist item is marked "Won't Do" (skipped), Jira automatically:
   - Creates a Bug issue tagged `gate-skipped`
   - Places the project Epic "On Hold"
   - Notifies the PM Admin

2. **Resolution options** (PM Admin decides):
   - (a) The item is completed retroactively. Bug closed.
   - (b) RGC reviews and formally waives the item in writing. Waiver documented in Jira.

3. **There is no option (c)**: You cannot just ignore it and move on. Every skip has a paper trail.

This isn't punishment — it's protection. A skipped gate is a known risk. The process forces that risk to be acknowledged and accepted by the right people, not buried by the delivery team.

---

## The "Readiness Overlap" Model

You may have noticed that the process says things like "the TL should be onboarded before the FRD sign-off." This sounds strange — why involve the TL before Stage 3 is done?

This is intentional. The **Readiness Overlap Model** means:
- While working on Stage N, you prepare for Stage N+1
- You do not wait until Stage N is complete to start finding resources for Stage N+1

An analogy: you don't wait until you arrive at the airport to start packing your bags. You pack in advance so you're ready to go.

This prevents the most common cause of project stalls: finishing one stage and then spending weeks looking for the right person for the next one.

---

## Frequently Asked Questions

**Q: Can two stages run at the same time?**
A: No. Stages are sequential — each gate must pass before the next stage begins. However, prerequisites for the next stage can be prepared in parallel with the current stage (the Readiness Overlap Model).

**Q: What if the business changes their mind mid-project?**
A: Once Gate 3 is closed (FRD + HFD signed off), any change is a Change Request (CR). CRs are not blocked — but they must be logged, assessed for cost/timeline impact, and approved. This protects both the BT (their change is tracked) and the IT team (they have a record of scope changes).

**Q: The timeline seems long. Can we fast-track?**
A: Exit Points exist for this reason. Exit C (after Stage 5) lets a department find an external vendor if IT's timeline doesn't match their need. What you cannot do is ask IT to skip stages and rush — that's where the highest-risk systems come from.

**Q: What is "Conditionally Approved" at Gate 1?**
A: It means the ITC approves the project moving to Stage 2, but with named conditions that must be resolved (e.g., "budget must be confirmed by [date]", "security review required before Stage 3"). Those conditions become mandatory Gate 2 exit criteria.

**Q: Who is my first point of contact for process questions?**
A: RGC (apps.rgc@na.baps.org). They coordinate all governance questions and can connect you with the right person for technical or process queries.

---

## Glossary Quick Reference

All acronyms are defined in [GLOSSARY.md](../GLOSSARY.md).

**Most common ones**:

| Acronym | What it means |
|---|---|
| RGC | Regional Governance Committee — IT governance body |
| ITC | IT Committee — approves projects |
| FPO | Functional Product Owner — business-side sign-off authority |
| BT | Business Team — stakeholders and end-users |
| BA | Business Analyst — writes BRD and FRD |
| BRD | Business Requirements Document — the "what and why" |
| FRD | Functional Requirements Document — the "how" |
| LFD | Low Fidelity Design — wireframes |
| HFD | High Fidelity Design — Figma designs |
| RACI | Responsible · Accountable · Consulted · Informed |
| CR | Change Request — any scope change after Gate 3 |
| VAPT | Security testing before production |
| UAT | User Acceptance Testing — BT tests the system |
