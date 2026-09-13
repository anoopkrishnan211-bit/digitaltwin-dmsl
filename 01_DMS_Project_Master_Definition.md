# DMS Project Master Definition

**Working Document 1 of 16**
**Project:** DMS Dewas Factory-Wide Operational Intelligence Transformation Program
**Client:** Dewas Metal Sections Pvt. Ltd. (hypothetical client engagement — case study)
**Status:** Draft for sign-off

**Classification key used throughout:**
- **DMS FACT** — supported by publicly available DMS information
- **ASSUMPTION** — created for this case study because internal DMS information is unavailable
- **RECOMMENDATION** — our proposed solution, architecture, process or delivery decision
- **TO BE VALIDATED** — requires confirmation during a real client engagement

---

## 1. Project Definition

**Project Name:** DMS Dewas Factory-Wide Operational Intelligence Transformation Program

**Client:** Dewas Metal Sections Pvt. Ltd. (hypothetical client engagement for case-study purposes)

**Facility:** Dewas manufacturing plant only

**One-line definition:**

> A factory-wide operational transformation, enabled by a Digital Twin and predictive intelligence, that lets DMS see what is happening, understand why, predict what's likely to happen next, and act before it costs production, quality or time.

**What this is NOT:** This is not "a Digital Twin implementation." The Digital Twin and predictive AI are the enabling mechanism — the thing being delivered is earlier, better decisions across the factory.

---

## 2. Business Problem

| Level | Statement |
|---|---|
| **Business Problem** | DMS's Dewas operations run on fragmented, delayed information, so problems are discovered after they've already cost time, material or quality — not before. |
| **Operational Problems** | Unplanned downtime; reactive maintenance; changeover-driven losses; late-detected quality defects; schedule deviation; poor cross-line visibility; delayed management reporting |
| **Root Causes** | No unified real-time visibility across lines; maintenance driven by failure/calendar rather than condition; changeover knowledge held informally by operators, not the system; quality checked end-of-line rather than correlated to upstream conditions; no structured historical dataset linking cause to effect |
| **Impact** | Lost production time; higher scrap/rework; unpredictable delivery; maintenance cost concentrated in emergency repairs; decisions made on lagging, not leading, indicators |
| **Business Need** | A connected, factory-wide operational data foundation supporting early detection and prediction of the above |
| **Desired Outcome** | Reduced unplanned downtime, reduced changeover loss, improved on-time delivery, lower reactive maintenance cost, faster and more confident decisions |

*Classification: **RECOMMENDATION** (problem hierarchy) built on **ASSUMPTION** (specific operational pain points, since real DMS pain points are unknown) — labelled explicitly wherever this appears downstream.*

---

## 3. Transformation Objective

> **SEE → UNDERSTAND → PREDICT → ACT → LEARN**

Delivered through: **Digital Twin + Data Foundation + Analytics + Predictive AI + Prescriptive Intelligence**

**Hero business capability:** **Predictive Production Continuity** — the ability to see disruption coming, regardless of its source (machine, changeover, schedule, quality), and act before production is affected.

---

## 4. Business Objectives

1. Establish factory-wide real-time operational visibility (Dewas)
2. Reduce unplanned downtime through early detection and prediction
3. Reduce changeover-related time and quality loss
4. Shift maintenance from reactive → condition-based → predictive
5. Improve production schedule reliability and on-time delivery
6. Improve quality traceability, catching deviation earlier
7. Give leadership a single, trustworthy operational data source
8. Build a reusable, AI-ready data foundation for continuous improvement and future expansion

Each objective traces directly to a row in the Business Problem hierarchy (Section 2) — no objective exists without a stated originating problem.

---

## 5. Scope

**In Scope**
- Entire DMS Dewas facility (all assumed production lines and shared processes)
- Slitting, roll forming, cutting/pressing, tool room/die shop, quality/inspection, maintenance, production planning, material movement, dispatch
- Design and delivery planning for the full Digital Twin, analytics, and predictive/prescriptive intelligence capability, with implementation maturity progressing through the defined phases as data readiness allows
- Program governance, multi-workstream delivery, change management, training, hypercare, BAU handover

**Out of Scope (current program)**
- Pune facility — **RECOMMENDATION:** flagged as future expansion candidate
- Ranipet facility — same treatment
- Autonomous machine/control actions
- PLC/control system or ERP replacement
- Autonomous AI decision-making without human approval
- AI action-taking beyond approved notification/ticket-creation workflows
- Full 3D visualization (not required to prove the concept)
- Production-grade ML models, real IoT integration, real MES/ERP integration specs (this is a case-study assignment, not a real build)

---

## 6. Factory Assumptions

| Element | Classification | Statement |
|---|---|---|
| Facility | **DMS FACT** | Dewas is DMS's HQ and primary site; est. 1979; cold roll forming; products span Automobile, Railways, Solar Mounting, Air Pollution Control, ERW Tubes, General Engineering, Elevators |
| Historical footprint | **DMS FACT** (historical, SEBI filing) | Slitting, nine roll-forming mills, band saws, circular saws, power presses documented historically |
| Line count | **ASSUMPTION** (sizing placeholder only) | 6 roll-forming lines (RFL-01–06) assumed as a present-day consolidation of the historical footprint; explicitly not a claim about DMS's actual current configuration — to be replaced by verified inventory during Phase 0 |
| Slitting | **ASSUMPTION** | 2 shared slitting lines feeding all 6 RFLs |
| Tool Room | **ASSUMPTION** | 1 shared tool room / die shop |
| Quality | **ASSUMPTION** | 6 line-level inline inspection points + 1 centralized QA lab |
| Asset count | **ASSUMPTION** (sizing placeholder only) | ~26–28 monitored assets total, used for program sizing / effort estimation only |
| Line prioritization | **RECOMMENDATION** | Weighted scoring model (production volume, revenue criticality, downtime impact, failure history, data readiness, SLA criticality) determines rollout wave — not assumed by product type |
| Systems | **ASSUMPTION** | Mixed PLC maturity; no MES; partial ERP not integrated with shop floor |
| Historical data | **ASSUMPTION** (deliberately conservative) | Fragmented, partial — not a clean ML-ready dataset from day one |
| Maintenance model | **ASSUMPTION** | Predominantly reactive today |
| Shifts | **ASSUMPTION** | 2–3 shifts, 6-day operation |

*Full detail lives in the standalone Assumption Register (feeds Working Document 2 — Discovery & Current State Assessment). This section holds only the load-bearing assumptions that every other document depends on.*

**Sign-off required:** The line count (6) and asset count (~26–28) drive every downstream effort estimate, WBS line item and cost model. Confirm or adjust before these propagate further.

---

## 7. Stakeholders

| Persona | Primary Concern |
|---|---|
| Executive Sponsor / Business Leadership | ROI, risk, timeline, business outcomes |
| Plant Manager | Cross-line performance, capacity, escalations |
| Production Manager (per line) | Line-level output, downtime, schedule adherence |
| Maintenance Manager | Asset health, work order prioritization |
| Quality Manager | Defect trends, root cause, spec compliance |
| Tool Room / Changeover Lead | Changeover time, tooling availability |
| IT/OT Lead | Security, integration, infrastructure |

*All classified **ASSUMPTION** — real stakeholder map is a Phase 0 discovery output.*

---

## 8. Decision Model

The system is designed around decisions, not dashboards:

| Persona | Key Decision | Enabled By |
|---|---|---|
| Plant Manager | Which line needs attention right now? | Cross-line health ranking |
| Production Manager | Will today's target be met? | Shortfall prediction |
| Maintenance Manager | Which asset should be serviced next? | Failure risk ranking |
| Quality Manager | Is a defect trend emerging, and where? | Quality anomaly correlation |
| Tool Room Lead | Which tooling needs attention before next changeover? | Changeover risk prediction |
| Business Leadership | Is the program delivering value; where to invest next? | KPI / ROI trend reporting |

*This model is the traceability anchor: any dashboard element, alert, or prediction that doesn't map to a row here doesn't get built.*

---

## 9. Target Operating Model

**Current-State Hypothesis (ASSUMPTION):** Fragmented data across manual logs / spreadsheets / partial ERP; no cross-line real-time visibility; reactive maintenance; tacit changeover knowledge; end-of-line quality checks; manual, delayed management reporting.

**Target State:** Unified near-real-time Digital Twin across all Dewas lines; condition-based and progressively predictive maintenance; actively monitored and improving changeover performance; quality issues flagged before full-batch impact; leadership decisions supported by live, trustworthy data; continuous improvement loop driven by captured outcomes.

---

## 10. Digital Twin Definition

Explicit layer separation (load-bearing for the architecture document):

**Physical Layer** (factory) → **Data Platform** (ingestion/storage — plumbing, not the twin) → **Digital Twin Model** (structured state/hierarchy/relationships) → **Analytics Platform** (descriptive/diagnostic/predictive/prescriptive) → **Application Layer** (dashboards/alerts/AI Assistant) → **Action Layer** (human-approved workflows only)

**State Model** (per domain — what makes "the twin updates in real time" concrete):

| Domain | States |
|---|---|
| Machine | Running, Idle, Setup/Changeover, Fault, Maintenance, Planned Stop, Unplanned Stop |
| Production | Planned, In Production, Behind Schedule, At Risk, Completed |
| Quality | Normal, Warning, Deviation, Hold, Rejected |
| Maintenance | Healthy, Monitoring, Inspection Required, Maintenance Scheduled, Fault, Under Repair |

**Digital Thread:** Order → Product → Material → Production Line → Machine → Tooling → Process Parameters → Quality Result → Maintenance Event → Finished Product

---

## 11. AI Strategy

**Governing principle:** Use AI where learning from historical patterns creates measurable value beyond a deterministic rule. Use rules where rules are sufficient and cheaper to maintain.

**Six predictive use cases (priority order):**
1. Machine failure / unplanned downtime
2. Changeover-related downtime / quality risk
3. Production shortfall
4. Maintenance requirement
5. Quality anomaly
6. Bottleneck

**Model approach:** Selected empirically per use case based on observed data — not prescribed upfront. Candidates include anomaly detection, classification, regression, time-series forecasting, survival/time-to-event; bottleneck prediction explicitly favors rules/queueing logic over ML.

**Activation gate:** No use case/asset enters predictive maturity until it clears a **Data Readiness Score** (availability, completeness, quality, granularity, historical depth, labelling, consistency, context). No model ships on insufficient data.

**AI maturity path:** Descriptive → Diagnostic → Predictive → Prescriptive → Assisted/Agentic — gated by data readiness at each step, not calendar time.

**Human-in-the-loop (non-negotiable):** AI observes → alerts → predicts → recommends → **human approves** → system executes approved workflow only (ticket/notification — never machine control).

**Every prediction surfaces:** probability, prediction window, confidence, top contributing signals, recommended action, business impact if ignored — never a bare risk score.

**RAG vs. Predictive AI:** RAG answers "what does procedure say" (SOPs/manuals); Predictive AI answers "what's likely to happen" (operational data). AI Assistant blends both. AI Agent executes only approved workflows — no autonomous action.

---

## 12. Program Phases

| Phase | Objective |
|---|---|
| Phase 0 | Discovery & Assessment |
| Phase 1 | Foundation & Data Enablement |
| Phase 2 | Digital Twin & Real-Time Visibility (rolled out by prioritized wave, not all lines simultaneously) |
| Phase 3 | Advanced Analytics |
| Phase 4 | Predictive Intelligence (activated per use case/asset against readiness gates) |
| Phase 5 | Prescriptive Intelligence & AI Assistance |
| Phase 6 | Optimization & Continuous Improvement |

**Duration:** ~14–16 months, illustrative — factory-wide commitment, phased execution, not a pilot-then-decide model.

---

## 13. Golden Thread (Narrative Device)

**RFL-02 Bearing Degradation** is the single worked scenario carried through every document — BA chain, architecture, AI use case, PM/KPI tie-back — as the primary illustration. Changeover-risk and production-shortfall scenarios serve as lighter, one-paragraph parallel proof points showing the pattern generalizes beyond machine failure.

---

## 14. Success Criteria for the Assignment

The assignment succeeds if Nikhil concludes:

1. Discovery-style thinking visibly precedes solution design
2. Factory-wide ambition is real, but execution risk is honestly managed via phasing and data-readiness gates
3. Every requirement, dashboard element, and AI claim traces to a stated decision or business need
4. AI is applied with judgment (rules where sufficient, ML where it adds value) — not decoratively
5. The candidate is positioned as delivery owner, not architect/ML engineer
6. No invented numbers or unsupported ROI claims anywhere
7. AI-augmented delivery is disclosed transparently, with human ownership of decisions clearly retained

---

## 15. Final Deliverables

**Submitted to Nikhil:**
- Case Study PDF (22–28 pages)
- Executive Presentation PPTX (14–16 slides)
- PM Workbook XLSX
- *(Optional)* Technical Appendix PDF

**Built, not submitted (absorbed as source content into the three core deliverables above):**
Discovery Assessment, BRD, RTM, User Stories, Solution Architecture, Digital Twin/Digital Thread Design, Predictive Production Continuity Framework, AI Governance, ROI Model, Testing/UAT Strategy, Change Management Plan, Interview Defence Playbook

---

*End of Document 1 — DMS Project Master Definition*
