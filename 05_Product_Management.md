## 05. PRODUCT MANAGEMENT

**ANTIER Project Assignment – Hypothetical Client Engagement**
**Baseline Date:** 13 September 2026
**Document Status:** Working Draft v0.1

---

## 1. Product Vision

**Vision Statement:**
*Empower DMS Manufacturing operations and maintenance teams with a unified, intelligent operational platform that transforms reactive firefighting into proactive, data-informed decision-making—enabling continuous improvement in production continuity, changeover efficiency, and maintenance planning.*

**Vision Characteristics:**

- **User-Centric:** Focused on frontline operators, maintenance technicians, and shift supervisors.
- **Phased:** Progresses from visibility → analytics → predictive → prescriptive.
- **Governed:** Human-in-the-loop for all operational actions; no autonomous control.
- **Scalable:** MVP on 1–2 lines → factory-wide rollout.
- **Defensible:** Business-value driven, not technology-led.

---

## 2. Product Objectives

**Purpose:**
To translate business objectives (01. Project Initiation) and business needs (02. Discovery) into product-level outcomes.

| **Objective ID** |   Product Objective                                                                                      |  Linked Business Objective (01)      |  Linked Business Need (02)  |   Success Metric (Directional)                                    |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | ------ | -- | ---------------------------------------------- |
| **PO-01**                                                                                                            | Deliver unified visibility into downtime events across production lines.                | O1, O2 | N1 | % downtime events logged with valid fault code |
| **PO-02**                                                                                                            | Enable standardized changeover tracking with start/end times and reason codes.          | O2     | N2 | Avg changeover duration by line (trend)        |
| **PO-03**                                                                                                            | Provide early-warning alerts for emerging asset faults (once data readiness validated). | O3     | N3 | % alerts approved within 15 min                |
| **PO-04**                                                                                                            | Surface relevant SOPs and historical context at point of decision.                      | O3, O4 | N4 | Avg time to find SOP                           |
| **PO-05**                                                                                                            | Enforce structured fault taxonomy for consistent root-cause tagging.                    | O2     | N5 | % faults tagged with valid taxonomy code       |
| **PO-06**                                                                                                            | Deliver real-time operational dashboards for shift handover and management review.      | O4, O5 | N6 | Shift handover time reduction (directional)    |

**Defensibility Note:**

- All product objectives trace to business needs and requirements—no feature exists without a linked business rationale.
- Predictive objectives (PO-03) explicitly gated by data readiness validation.

---

## 3. Product Capability Framework

**Purpose:**
To define high-level capabilities the product must deliver, mapped to business needs and requirements.

| **Capability ID** |        Capability              |     Description                                                                     | Linked Business Need   | Linked BR   |   Linked FR   |
| ---------------------------------------------------------------------------- | ---------------------------- | ------------------------------------------------------------------------------ | ------ | ------------ | -------------- |
| **CAP-01**                                                                   | Downtime Event Capture       | Log downtime events with timestamp, line, asset, fault code.                   | N1     | BR-01        | FR-01          |
| **CAP-02**                                                                   | Changeover Tracking          | Record changeover start/end times, line, reason code; auto-calculate duration. | N2     | BR-02        | FR-02          |
| **CAP-03**                                                                   | Anomaly Detection & Alerting | Identify emerging fault patterns; generate alerts with human approval.         | N3     | BR-03        | FR-03, FR-07   |
| **CAP-04**                                                                   | Knowledge Retrieval (RAG)    | Surface SOPs and historical resolutions by fault code or asset.                | N4     | BR-04        | FR-04          |
| **CAP-05**                                                                   | Fault Taxonomy Enforcement   | Require selection from predefined fault codes; block free-text.                | N5     | BR-05        | FR-05          |
| **CAP-06**                                                                   | Operational Dashboards       | Display real-time line status, alerts, changeover progress, trends.            | N6     | BR-06        | FR-06          |
| **CAP-07**                                                                   | Audit & Governance           | Log all user actions with timestamp and user ID; enforce role-based access.    | All    | All BRs      | NFR-02, NFR-04 |
| **CAP-08**                                                                   | Data Export & Reporting      | Export downtime/changeover data to CSV/Excel for ad-hoc analysis.              | N1, N2 | BR-01, BR-02 | NFR-05         |

**Capability Principles:**

- Each capability is **testable** (via acceptance criteria).
- Each capability is **traceable** (to business need → BR → FR).
- No capability implies specialist engineering ownership (e.g., “Anomaly Detection” = business use case, not ML model spec).

---

## 4. Feature Definition

**Purpose:**
To break capabilities into user-facing features, without over-specifying technical implementation.

| **Feature ID** |        Feature                 | Linked Capability       |    User Role                   |  Description                                                                  |
| ---------------------------------------------------------- | --------------------------- | ------ | ------------------------------ | ------------------------------------------------------------------ |
| **F-01**                                                   | Downtime Logging Form       | CAP-01 | Shift Supervisor               | Web form to log downtime with enforced fault taxonomy.             |
| **F-02**                                                   | Changeover Timer            | CAP-02 | Operator                       | Start/stop timer for changeover; auto-calculates duration.         |
| **F-03**                                                   | Anomaly Alert Dashboard     | CAP-03 | Maintenance Lead               | Shows active alerts; requires approval before work order.          |
| **F-04**                                                   | SOP Search Assistant        | CAP-04 | Technician                     | Search SOPs by fault code or asset; displays relevant docs.        |
| **F-05**                                                   | Fault Code Selector         | CAP-05 | All Users                      | Dropdown of predefined fault codes; blocks free-text entry.        |
| **F-06**                                                   | Real-Time Line Status Board | CAP-06 | Shift Supervisor               | Dashboard showing line status, active alerts, changeover progress. |
| **F-07**                                                   | Audit Log Viewer            | CAP-07 | IT Manager, Plant Manager      | View all user actions with timestamp, user ID, record ID.          |
| **F-08**                                                   | CSV Export Button           | CAP-08 | Plant Manager, Quality Manager | Export downtime/changeover data to CSV for analysis.               |

**Feature Boundaries:**

- Features are **user-story aligned** (see 03. Requirements).
- Features do **not** specify UI framework, database schema, or API design.

---

## 5. Feature Prioritization

**Purpose:**
To prioritize features using MoSCoW method, aligned with phased rollout and data readiness.

| **Feature ID** |    Feature                         |   Priority     |        Rationale                                                        |  Phase             |
| ------------------------------------------- | --------------------------- | ----------- | -------------------------------------------------------------- | ------------- |
| **F-01**                                    | Downtime Logging Form       | Must Have   | Foundational for visibility (N1); enables root-cause analysis. | Phase 1 (MVP) |
| **F-05**                                    | Fault Code Selector         | Must Have   | Enables standardized taxonomy (N5); required for analytics.    | Phase 1 (MVP) |
| **F-02**                                    | Changeover Timer            | Must Have   | Foundational for changeover tracking (N2); quick win.          | Phase 1 (MVP) |
| **F-07**                                    | Audit Log Viewer            | Must Have   | Compliance and governance (NFR-02); low effort.                | Phase 1 (MVP) |
| **F-08**                                    | CSV Export Button           | Should Have | Enables interim reporting; not critical for MVP.               | Phase 2       |
| **F-06**                                    | Real-Time Line Status Board | Should Have | Improves handover (N6); requires dashboard infrastructure.     | Phase 2       |
| **F-04**                                    | SOP Search Assistant        | Should Have | Decision support (N4); requires RAG integration.               | Phase 2       |
| **F-03**                                    | Anomaly Alert Dashboard     | Could Have  | Predictive capability (N3); gated by data readiness.           | Phase 3       |

**Prioritization Principles:**

- **Must Have:** Required for MVP to deliver core visibility and governance.
- **Should Have:** Adds significant value but can wait for Phase 2.
- **Could Have:** Predictive/optimization features deferred until data validated.

---

## 6. MVP Definition

**Purpose:**
To define the Minimum Viable Product that delivers core business value while validating assumptions.

**MVP Scope (Phase 1 – 12 weeks):**

**Included Features:**

- F-01: Downtime Logging Form
- F-02: Changeover Timer
- F-05: Fault Code Selector
- F-07: Audit Log Viewer

**MVP Outcomes:**

- Unified downtime logging with fault taxonomy (validates N1, N5).
- Standardized changeover timing (validates N2).
- Audit trail for governance (validates NFR-02).
- Data foundation for future analytics (validates data readiness).

**Excluded from MVP:**

- Anomaly detection alerts (F-03) – requires data readiness validation.
- RAG SOP assistant (F-04) – requires document integration.
- Real-time dashboards (F-06) – can use static reports initially.
- CSV export (F-08) – manual export acceptable for MVP.

**MVP Success Criteria:**

- 90% of downtime events logged with valid fault codes.
- 100% of changeovers timed with start/end records.
- Zero autonomous actions; all alerts/approvals manual in MVP.
- User adoption: 80% of target users actively logging data.

**Defensibility Note:**

- MVP is **not** the entire factory; it is a controlled validation on 1–2 lines.
- MVP explicitly avoids predictive AI until data readiness confirmed.

---

## 7. Product Roadmap

**Purpose:**
To show phased delivery from MVP to factory-wide scale, aligned with business value and data readiness.

| **Phase** |  Timeline           |     Focus                                                 |  Key Features                          |             Business Outcome                                          |
| -------------------------------------------------- | ----------- | ---------------------------------------------------- | -------------------------- | ----------------------------------------------------- |
| **Phase 0: Discovery & Validation**                | Weeks 1–4   | Validate assumptions, audit data, confirm MVP scope  | N/A (Planning)             | Confirmed business case; data readiness baseline      |
| **Phase 1: MVP (Visibility)**                      | Weeks 5–16  | Foundational data capture and governance             | F-01, F-02, F-05, F-07     | Unified downtime/changeover logging; audit trail      |
| **Phase 2: Scale & Support**                       | Weeks 17–32 | Expand to all lines; add decision support            | F-06, F-04, F-08           | Real-time dashboards; SOP access; exportable reports  |
| **Phase 3: Predictive Intelligence**               | Weeks 33+   | Anomaly detection and alerts (if data ready)         | F-03                       | Early-warning maintenance; reduced unplanned downtime |
| **Phase 4: Optimization**                          | Ongoing     | Continuous improvement, prescriptive recommendations | Enhancements to F-03, F-04 | Optimized changeover; predictive maintenance maturity |

**Roadmap Principles:**

- **Phased rollout** mitigates risk and validates value at each stage.
- **Predictive features** explicitly gated by data readiness (Phase 3).
- **No big-bang deployment**; factory-wide scale achieved through controlled waves.

---

## 8. KPI & Success Metrics

**Purpose:**
To define how product success will be measured, linked to business objectives and capabilities.

| **KPI ID** |   KPI                          |  Formula                                                        |  Linked Product Objective           |     Target (Directional)                     |    Data Source                       |
| --------------------------------------------------------------------------- | --------------------------- | -------------------------------------------------------- | ----------- | ------------------------ | ------------------------- |
| **KPI-01**                                                                  | Downtime Logging Compliance | (Events with valid fault code / Total events) × 100      | PO-01       | ≥ 90%                    | Downtime Logging Form     |
| **KPI-02**                                                                  | Avg Changeover Duration     | Total changeover time / Number of changeovers            | PO-02       | Trend downward over time | Changeover Timer          |
| **KPI-03**                                                                  | Alert Approval Timeliness   | (Alerts approved within 15 min / Total alerts) × 100     | PO-03       | ≥ 80% (Phase 3+)         | Anomaly Alert Dashboard   |
| **KPI-04**                                                                  | SOP Retrieval Time          | Avg time from fault log to SOP view                      | PO-04       | Trend downward           | SOP Search Assistant logs |
| **KPI-05**                                                                  | Fault Taxonomy Compliance   | (Faults with valid code / Total faults) × 100            | PO-05       | ≥ 95%                    | Fault Code Selector       |
| **KPI-06**                                                                  | Dashboard Adoption Rate     | (Active dashboard users / Target users) × 100            | PO-06       | ≥ 75%                    | Dashboard access logs     |
| **KPI-07**                                                                  | Audit Log Completeness      | (Actions with timestamp & user ID / Total actions) × 100 | PO-01–PO-06 | 100%                     | Audit Log Viewer          |

**KPI Governance:**

- All KPIs are **directional** in assignment context; no invented baselines or ROI percentages.
- In real engagement, baselines would be captured during Phase 0 Discovery.
- KPIs trace to product objectives → business needs → business requirements.

---

## AI Involvement Disclosure (Internal Control Note)

*This Product Management document was drafted with AI assistance for structuring, capability mapping, and roadmap phasing. All product vision, objectives, capabilities, features, prioritization logic, MVP scope, and KPI definitions were reviewed and finalized by the author. All features are framed at business capability level; no technical implementation specs were created.*

---

## Next Step Confirmation

**05. Product Management** is now complete at draft v0.1, fully traceable to 01–04 and explicitly positioned as supporting capability (not primary role identity).

Shall I proceed to **Step 6: 06. Data & Information** (Data Requirements → Dictionary → KPI Definitions → Data Flow → Information Model → Readiness Assessment → Reporting)?

Proceeding to **Step 6: 06. Data & Information**.

This consolidates all seven line items from the frozen **06. Data & Information** section into a controlled working document, maintaining business-oriented framing (no data engineering specs) and explicit data-readiness gating per the Master Working Prompt.

---
