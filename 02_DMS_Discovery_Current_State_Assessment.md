# DMS Discovery & Current State Assessment

**Working Document 2 of 16**
**Status:** DRAFT for sign-off — revised per consulting review
**Traces to:** Master Definition (Document 1), Sections 2, 6, 7, 9

**Classification key used throughout:**
- **DMS FACT** — supported by publicly available DMS information
- **ASSUMPTION** — created for this case study because internal DMS information is unavailable
- **RECOMMENDATION** — our proposed solution, architecture, process or delivery decision
- **TO BE VALIDATED** — requires confirmation during a real client engagement

---

## 1. Purpose of This Document

This document simulates the Phase 0 Discovery output — the structured questions a BA would ask DMS, the assumption-based current-state answers used for this case study (since no real DMS discovery has occurred), and the resulting hypothesized process, pain points, and requirement seeds that everything downstream traces back to.

**Important distinction, preserved throughout:** Document 1 defines what we are proposing. This document demonstrates *how we would discover and validate* what is actually true — it does not claim to have found it. Every "response" below is an **ASSUMPTION** authored for narrative and analytical coherence, not a real DMS statement.

> **Everything in this document is a starting hypothesis, not a finding.**

This single sentence protects the entire assignment from the obvious challenge — "how do you know DMS has these problems?" The answer: we don't claim to. Public facts, case-study assumptions, recommendations, and validation items are explicitly separated throughout; these are the hypotheses we would carry into a real Phase 0.

---

## 2. Discovery Questions (by category)

### Business Questions
- Why does DMS want this transformation now?
- What operational problems are currently hardest to see coming?
- What decisions are being made too late, and what does that cost?
- Who would use this system day to day, and what would change in their job?

### Operations Questions
- What is the current production process across the Dewas lines?
- Which lines/products are most critical to revenue and customer commitments?
- Where do bottlenecks or delays typically occur?
- How is downtime currently recorded, if at all?

### Maintenance Questions
- Is maintenance scheduled, reactive, or a mix?
- Are failure events and root causes documented anywhere?
- How is a maintenance decision currently made — on what information?

### Quality Questions
- Where are defects typically caught — inline or end-of-line?
- Are defects linked back to machine condition, changeover, or operator in any way today?

### Changeover / Tooling Questions
- How long does a typical changeover take, and does it vary by line/product?
- Is tooling condition tracked, and by whom?
- Is changeover knowledge documented or held by individual operators?

### Technology Questions
- Do machines have PLCs? Is there any SCADA/MES layer?
- Is there an ERP system, and does it reach the shop floor?
- How is production, downtime, and quality data currently captured (manual/digital)?

### Data Questions
- How much historical data exists, and in what form?
- Are timestamps and machine/asset IDs consistent across sources?
- Are failure events labeled with cause, or just logged as "stopped"?

### Security Questions
- What OT/IT security policies currently exist?
- Can operational data leave the plant network, or must it stay on-premise?

### Financial / Value Questions *(added per consulting review)*
- What is the financial impact of unplanned downtime?
- What is the approximate cost of scrap/rework?
- What is the cost of emergency/reactive maintenance versus planned maintenance?
- How is production loss currently valued or estimated?
- Which KPIs does leadership currently use to assess plant performance?
- What baseline data exists for calculating transformation benefits?

*This category exists specifically to feed the ROI Model (Document 11) with real formula inputs rather than invented figures.*

### Success Questions
- What would "this program worked" look like to DMS leadership a year from now?
- What baseline metrics exist today to measure improvement against?

---

## 3. Simulated Discovery Responses → Requirement Seeds

*Format revised per consulting review: Question → Case-Study Assumption → Evidence Required → Requirement Seed. All assumption-column content is **ASSUMPTION** — reworded below to avoid DMS-specific certainty.*

| # | Discovery Question | Case-Study Assumption | Evidence Required (real Phase 0) | Requirement Seed |
|---|---|---|---|---|
| D1 | Why now? | Assumed business driver: increasing customer delivery pressure and rising cost of unplanned downtime/rework are creating demand for earlier operational warning | Customer SLA data, downtime cost records, leadership priorities | BR: System must provide early warning of conditions likely to disrupt production or delivery |
| D2 | Which lines are most critical? | Assumed to vary by current order book; no single line is fixed as "most important" | Order/sales data by line, product margin data | BR: Line prioritization must be evidence-based (scoring model), not fixed by assumption |
| D3 | How is maintenance decided today? | Assumed predominantly reactive; maintenance responds when a machine stops or an operator flags an issue; some equipment may loosely follow manufacturer service intervals | Maintenance logs, work order history, technician interviews | BR: System must support a transition from reactive to condition-based maintenance prioritization |
| D4 | Are failures documented? | Assumed inconsistent — logs may capture "machine down, restarted at X" without a documented root cause | Sample maintenance/failure logs, format review | BR: System must introduce structured failure/event capture going forward, since historical labels can't be retrofitted |
| D5 | Where are defects caught? | Assumed primarily end-of-line/centralized QA; inline checks, if any, likely informal and unrecorded | QA process documentation, inspection records | BR: System must correlate quality outcomes with upstream machine/changeover conditions where inline data exists |
| D6 | Changeover duration/knowledge? | Assumed to vary significantly by product and operator experience; no standard documented changeover procedure per line | Changeover time logs (if any), SOP documentation, operator interviews | BR: System must capture changeover start/end and tooling ID to enable changeover analytics |
| D7 | PLC/MES/ERP landscape? | Assumed mixed — some newer machines may have PLCs; no MES assumed; ERP assumed to exist for order/planning but not connected to shop floor | IT/OT systems inventory, network architecture review | FR: Integration layer must support mixed-maturity data sources without requiring MES as a prerequisite |
| D8 | Historical data quality? | Assumed production/dispatch records more reliable than downtime/maintenance records; asset ID scheme assumed inconsistent across systems | Data sample audit across all identified sources | NFR: Data model must include an asset ID normalization/mapping step before any analytics is built |
| D9 | OT security posture? | Assumed data must remain on approved infrastructure; shop-floor network assumed segmented from office IT | OT security policy documentation, IT/OT lead interview | NFR: Architecture must respect OT/IT segmentation; Edge layer handles local processing before any data leaves the OT boundary |
| D10 | Financial impact of downtime/scrap? | Not assumed — deliberately left open pending real data | Downtime cost records, scrap/rework cost accounting, maintenance spend | BR: ROI model must be built on validated baseline figures, never assumed financial values |
| D11 | Success definition? | Assumed proxies: fewer surprise stoppages, faster changeover, less scrap, a single place to see line-by-line status | Leadership interviews, existing KPI reports | BR: KPI framework must center on downtime, changeover time, scrap rate, and cross-line visibility, not vanity metrics |

---

## 4. Hypothesized AS-IS Operational Flow

*Renamed from "AS-IS Process" per consulting review — this is a hypothesis to be validated, not an observed process.*

```
Raw Material Coil (Yard)
      ↓
Slitting (SL-01 / SL-02) — shared upstream
      ↓
Roll Forming (RFL-01 to RFL-06)
      ↓
Cutting / Pressing (per line)
      ↓
Inline Inspection (per line, informal) → Centralized QA Lab (formal, end-of-line)
      ↓
Finished Goods → Dispatch
```

**Supporting/parallel functions (hypothesized):** Tool Room (die/roll servicing, changeover support) · Maintenance Workshop (reactive, ad hoc) · Production Planning (ERP-based, not shop-floor-connected)

**Hypothesized current information flow:** Shift-level manual logs → end-of-day/end-of-shift compilation → manual reporting to Production/Plant Manager → periodic (daily/weekly) leadership summary. No real-time cross-line view is assumed to exist.

*All elements of this flow are **ASSUMPTION**, pending Phase 0 validation.*

---

## 5. Pain Points (Hypothesized Operational Consequences, Traced to Root Causes)

| Pain Point | Root Cause | Business Consequence |
|---|---|---|
| Unplanned stoppages surprise the floor | No condition monitoring; maintenance is reactive | Lost production hours, rushed emergency repairs |
| Changeover takes longer / produces more early rejects on some lines than others | No documented procedure; tacit operator knowledge; tooling condition not tracked | Lower effective capacity, inconsistent quality at batch start |
| Defects discovered late (end-of-line) | Inline checks informal/unrecorded | Larger batches affected before detection, higher scrap |
| Management reporting is delayed and manually compiled | No unified real-time data source | Slower decisions, reactive leadership posture |
| Difficult to say which line needs attention right now | No cross-line visibility | Plant Manager relies on walking the floor / anecdote, not data |
| Maintenance prioritization is informal | No asset health scoring | Risk of prioritizing the loudest complaint over the highest-risk asset |

*All entries **ASSUMPTION** — hypothesized consequences pending validation.*

---

## 6. Current Operational Maturity Snapshot

| Dimension | Hypothesized Current State | Target State |
|---|---|---|
| Visibility | Manual, per-shift, delayed | Real-time, cross-line |
| Maintenance | Reactive | Condition-based → predictive (phased) |
| Quality | End-of-line detection | Correlated to upstream conditions |
| Changeover | Undocumented, operator-dependent | Tracked, analyzed, improved |
| Data | Fragmented, inconsistent IDs | Normalized, structured, historian-backed |
| Reporting | Manual compilation | Automated dashboards |
| Decision-making | Experience/anecdote-driven | Data and prediction-supported |
| Financial visibility *(added)* | Downtime/scrap cost not systematically tracked | Costed baseline feeding a transparent ROI model |

---

## 7. Validation Requirements (What Phase 0 Must Actually Confirm)

Everything in this document is a starting hypothesis, not a finding. The real Phase 0 discovery must validate, at minimum:

1. Actual line count, configuration, and product allocation per line
2. Actual PLC/SCADA/ERP footprint and integration feasibility
3. Actual historical data volume, structure, and quality (per data source)
4. Actual maintenance process and record-keeping maturity
5. Actual changeover procedures and tooling tracking practices (or absence thereof)
6. Actual OT security policy and data residency constraints
7. Real stakeholder list, decision rights, and success definitions from DMS leadership directly
8. Actual financial baseline for downtime, scrap, and maintenance cost *(added)*

*All eight items remain **TO BE VALIDATED** until a real discovery occurs — this document exists to demonstrate the discovery methodology, not to substitute for it.*

---

## 8. Traceability Forward

This document feeds directly into:
- **Document 3 (BRD)** — Section 3 requirement seeds become formal Business Requirements
- **Document 4 (RTM)** — pain points and requirement seeds anchor the traceability chain
- **Document 6 (Solution Architecture)** — Section 6 (D7–D9) shapes the integration and security architecture assumptions
- **Document 8 (Predictive Production Continuity Framework)** — Section 5 pain points map directly to the six predictive use cases
- **Document 11 (Business Value & ROI Model)** — Section 2 Financial/Value questions and D10 seed the ROI formula inputs, kept free of invented figures

---

*End of Document 2 — DMS Discovery & Current State Assessment*
