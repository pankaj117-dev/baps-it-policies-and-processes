# Glossary — BAPS IT Stage Gate Process

Every abbreviation used in the stage gate process, RACI matrices, and Jira templates is defined here.
All Jira issue templates link to this file.

---

## Roles & People

| Abbreviation | Full Name | Description |
|---|---|---|
| **RGC** | Regional Governance Committee | The central IT governance body responsible for reviewing proposals, coordinating resources, and overseeing project quality across the organization. |
| **ITC** | IT Committee | Senior committee that approves or defers project proposals and allocates IT resources. Reports to BOD. |
| **BOD** | Board of Directors | Executive governance authority. Escalation point when ITC cannot reach a decision within the defined SLA. |
| **EAB** | Enterprise Architecture Board | Technical standards body responsible for architecture sign-offs, integration decisions, and system-level risk. Contact via RGC. Must be engaged no later than Stage 2 (Initiation). |
| **FPO** | Functional Product Owner | The business-side owner of the product/system being built. Responsible for requirement sign-offs and UAT approval. Typically a department lead (Sanyojak). |
| **BT** | Business Team | The department stakeholders, SMEs, and end-users representing the business side of the project. |
| **PM** | Project Manager | Accountable for overall project delivery, timelines, communications, and gate progression. |
| **PM-Admin** | Project Manager Admin | PM Admin track — responsible for process administration, ALM setup, MS Teams setup, and compliance tracking. |
| **BA** | Business Analyst | Responsible for requirements elicitation, BRD, FRD, and traceability matrices. |
| **SA** | Solution Architect / Systems Architect | Designs the technical architecture, leads POCs, reviews technical design, and signs off implementation quality. |
| **TL** | Technical Lead | Leads the development team, enforces code standards, approves packages, and is accountable for code quality. |
| **DES** | Designer (UI/UX) | Creates Low Fidelity and High Fidelity designs. Must comply with the BAPS Design System. |
| **DEV** | Developer | Implements user stories. Follows coding standards, peer review, and testing guidelines. |
| **QA** | Quality Analyst | Writes and executes test scenarios, test cases, performance tests, and regression tests. |
| **QA-Lead** | Quality Analyst Lead | Reviews and approves QA test scenarios and signs off all testing before UAT. |
| **SEC** | Security / Cybersecurity Team | Conducts VAPT. Must be engaged at least 3 weeks before planned go-live. Issues a VAPT Certificate before production release. |
| **Infra / DevOps** | Infrastructure / DevOps Team | Manages environments (Dev, QA, UAT, Prod), CI/CD pipelines, and deployment execution. |
| **DataEng** | Data Engineering Lead | Responsible for data integration design, migration scripts, and DB refresh processes. |
| **NDC** | National Development Committee | National-level oversight body. Includes engineering leads (NDC Engg Leads) and other track leads. |
| **SME** | Subject Matter Expert | A domain expert from the business team who provides detailed knowledge during requirements workshops. |
| **TPO** | Third-Party Owner | Owner/contact for an external system that the project integrates with. Responsible for providing API credentials and integration agreements. |

---

## Documents & Artefacts

| Abbreviation | Full Name | Description |
|---|---|---|
| **BRD** | Business Requirements Document | High-level document capturing the "What, Why, and For Whom." Covers business goals, scope, and user personas. Must be signed off before FRD begins. |
| **FRD** | Functional Requirements Document | Detailed document capturing the "How." Covers business logic, data rules, edge cases, integrations, and system behaviour. Signed off after BRD+LFD. |
| **LFD** | Low Fidelity Design | Wireframes/mockups created alongside BRD to visualize screens at a conceptual level. Signed off together with BRD. |
| **HFD** | High Fidelity Design | Pixel-level UI/UX designs in Figma. Must comply with BAPS Design System. Signed off together with FRD. |
| **TDD** | Technical Design Document | Document covering the full technical architecture, component design, API contracts, data models, and integration design. |
| **SAD** | System Architecture Design | High-level system architecture diagram and document. Produced by Solution Architect during Stage 4. |
| **FRD-TM** | FRD Traceability Matrix | Maps every BRD requirement to its corresponding FRD section. Ensures no requirement is missed in the detailed spec. |
| **CR** | Change Request | Any change to approved scope, requirements, or timeline after Gate 3 close (FRD+HFD sign-off). Must be formally logged and approved. |
| **RACI** | Responsible, Accountable, Consulted, Informed | Role assignment framework. R = does the work, A = signs off, C = input required before action, I = notified of outcome. |
| **MOM** | Minutes of Meeting | Written record of a meeting including decisions made, action items, and owners. Must be stored in MS Teams project folder within 2 business days. |

---

## Processes & Methodology

| Abbreviation | Full Name | Description |
|---|---|---|
| **SDLC** | Software Development Life Cycle | The end-to-end process for planning, creating, testing, and deploying software. The stage gate process IS the BAPS SDLC. |
| **ALM** | Application Lifecycle Management | The tool (e.g., HawkEye) used to track user stories, tasks, sprints, test cases, and project artefacts. |
| **VAPT** | Vulnerability Assessment and Penetration Testing | Security testing performed by SEC team before each production release. Round 1 before UAT, final round before go-live. |
| **POC** | Proof of Concept | A time-boxed technical experiment to validate a high-risk design decision before committing to full development. |
| **UAT** | User Acceptance Testing | Business-team-led testing in a production-like environment to confirm the system meets requirements before go-live. |
| **CI/CD** | Continuous Integration / Continuous Deployment | Automated pipeline that builds, tests, and deploys code. Enforces code quality gates (≥Grade A / 90%). |
| **RFP** | Request for Proposal | A formal document issued to external vendors when a department chooses Exit Point B (post-requirements self-management). |
| **SLA** | Service Level Agreement | A defined time commitment or performance standard. Used for ITC review (15 business days), design reviews (3 business days), etc. |
| **ROI** | Return on Investment | The expected business value of a project relative to its cost and effort. Used in proposal evaluation. |
| **PII** | Personally Identifiable Information | Personal data about individuals. Projects storing PII must follow data security and compliance requirements. |
| **PHI** | Protected Health Information | Health-related personal data. Subject to additional regulatory requirements. |

---

## Gate Decision Outcomes

Every gate produces one of four formal outcomes, documented in Jira:

| Decision | Meaning | Required Action |
|---|---|---|
| **Approved** | Proceed to next stage. Resources allocated. | PM updates project plan; stage begins. |
| **Conditionally Approved** | Proceed, but named conditions must be met and reviewed at next gate. | PM logs conditions in Jira; they become Gate Criteria for the next gate. |
| **On Hold** | Deferred. Re-consideration date is mandatory. | RGC communicates reason to proposer within 2 business days. Date set in Jira. |
| **Rejected / Killed** | Project will not proceed. | Rationale documented. Proposer notified within 2 business days. Jira Epic moved to Killed status. |

---

## Exit Points

| Exit | When | What Happens |
|---|---|---|
| **Exit A** | Start of Stage 1 | Department has its own capable team. They self-manage the project but must still follow central governance (cyber-security, architecture standards). |
| **Exit B** | After Stage 3 (Post-Requirements) | Department uses BAPS BAs for requirements, then exits to issue an RFP to a vendor for the build. |
| **Exit C** | After Stage 5 (Post-Estimation) | IT estimate exceeds department's timeline/budget. Department finds an external solution. IT is not pressured to rush. |
