## 03. REQUIREMENTS

**ANTIER Project Assignment – Hypothetical Client Engagement**
**Baseline Date:** 13 September 2026
**Document Status:** Working Draft v0.1

---

## 1. Business Requirements Document (BRD)

**Purpose:**
To define high-level business requirements traceable to discovered pain points and business needs, without prescribing technical implementation.

| **BR-ID** |      Business Requirement                                                                                                               | Linked Business Need   | Linked Pain Point                      |       Priority      |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -- | --------------------- | ----------- |
| **BR-01**                                                                  | The solution shall provide a unified view of downtime events across all production lines.                           | N1 | Fragmented logs       | Must Have   |
| **BR-02**                                                                  | The solution shall enable standardized tracking of changeover activities (start, end, duration, reason).            | N2 | Extended changeover   | Must Have   |
| **BR-03**                                                                  | The solution shall support early-warning alerts for emerging asset faults before failure occurs.                    | N3 | Unplanned downtime    | Should Have |
| **BR-04**                                                                  | The solution shall provide frontline staff with on-demand access to relevant SOPs and historical fault resolutions. | N4 | Tribal knowledge      | Should Have |
| **BR-05**                                                                  | The solution shall enforce a structured fault taxonomy to enable consistent root-cause tagging.                     | N5 | No root-cause tagging | Must Have   |
| **BR-06**                                                                  | The solution shall display real-time operational dashboards accessible to shift supervisors during handover.        | N6 | Shift handover gaps   | Could Have  |

**Assumptions:**

- All BRs are based on hypothetical discovery findings and require client validation.
- No BR implies autonomous action; all recommendations require human approval.

---

## 2. Functional Requirements

**Purpose:**
To specify what the system must do to satisfy business requirements, at a level appropriate for BA/PM positioning (not engineering specs).

| **FR-IDFunctional RequirementLinked BRLinked Business NeedValidation Approach** |                                                                                                        |              |        |                                             |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------ | ------ | ------------------------------------------- |
| **FR-01**                                                                       | System shall capture downtime events with timestamp, production line, asset ID, and fault code.        | BR-01        | N1     | Demo: Create downtime event; verify fields  |
| **FR-02**                                                                       | System shall record changeover start time, end time, line, and reason code.                            | BR-02        | N2     | Demo: Log changeover; verify duration calc  |
| **FR-03**                                                                       | System shall generate alerts when anomaly detection models identify emerging fault patterns.           | BR-03        | N3     | Simulation: Trigger anomaly; verify alert   |
| **FR-04**                                                                       | System shall retrieve and display relevant SOPs based on fault code or asset ID via RAG assistant.     | BR-04        | N4     | Demo: Query fault code; verify SOP display  |
| **FR-05**                                                                       | System shall enforce selection from a predefined fault taxonomy during downtime logging.               | BR-05        | N5     | Demo: Attempt free-text fault; verify block |
| **FR-06**                                                                       | System shall display real-time dashboards showing line status, active alerts, and changeover progress. | BR-06        | N6     | Demo: View dashboard; verify data freshness |
| **FR-07**                                                                       | System shall require human approval before generating work orders or notifications from alerts.        | BR-03, BR-04 | N3, N4 | Demo: Trigger alert; verify approval step   |

**Defensibility Note:**

- FR-03 and FR-04 explicitly separate **predictive AI** (anomaly detection) from **RAG** (knowledge retrieval), per prompt guidance.
- FR-07 enforces **Human-in-the-Loop** as a non-negotiable governance control.

---

## 3. Non-Functional Requirements (NFRs)

**Purpose:**
To define quality attributes, constraints, and operational expectations at a business/PM level (not engineering specs).

| **NFR-IDNon-Functional RequirementCategoryLinked BRRationale** |                                                                                               |                  |                     |                                                           |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | ---------------- | ------------------- | --------------------------------------------------------- |
| **NFR-01**                                                     | System shall be accessible via web browser on existing plant PCs and tablets.                 | Usability        | BR-01, BR-06        | Leverages existing hardware; reduces training             |
| **NFR-02**                                                     | System shall log all user actions (create, edit, approve) with timestamp and user ID.         | Auditability     | BR-01, BR-02, BR-05 | Supports traceability and compliance                      |
| **NFR-03**                                                     | System shall display dashboards with data latency ≤ 5 minutes under normal conditions.        | Performance      | BR-06               | Enables timely shift decisions                            |
| **NFR-04**                                                     | System shall integrate with existing IT security policies (SSO, role-based access).           | Security         | All BRs             | Aligns with C02 constraint (01. Project Initiation)       |
| **NFR-05**                                                     | System shall support export of downtime and changeover data to CSV/Excel for ad-hoc analysis. | Interoperability | BR-01, BR-02        | Enables interim reporting during transition               |
| **NFR-06**                                                     | System shall be deployable in phases (MVP → Scale) without full factory-wide cutover.         | Scalability      | All BRs             | Aligns with phased rollout principle (Prompt Section 21)  |

**Out of Scope (Explicit):**

- Specific cloud provider or on-premise architecture
- Database technology or API protocols
- Network topology or OT security controls
  *(These are specialist-owned per Prompt Section 2)*

---

## 4. Data Requirements

**Purpose:**
To define what data is required, why, and at what quality level—without engineering-level schema design.

| **DR-IDData RequirementSource (Hypothetical)PurposeQuality Expectation** |                                                             |                             |                |                                         |
| ------------------------------------------------------------------------ | ----------------------------------------------------------- | --------------------------- | -------------- | --------------------------------------- |
| **DR-01**                                                                | Downtime event records (timestamp, line, asset, fault code) | Operator logs, CMMS export  | FR-01, BR-01   | Complete, consistent fault codes        |
| **DR-02**                                                                | Changeover logs (start, end, line, reason)                  | Shift supervisor records    | FR-02, BR-02   | Timely entry; standardized reason codes |
| **DR-03**                                                                | Asset master data (asset ID, line, type, location)          | Maintenance master list     | FR-01, FR-03   | Accurate, up-to-date                    |
| **DR-04**                                                                | Fault taxonomy (code, description, category)                | Maintenance lead input      | FR-05, BR-05   | Controlled vocabulary; no free text     |
| **DR-05**                                                                | SOP documents (PDF/text linked to fault code or asset)      | Quality/maintenance manuals | FR-04, BR-04   | Searchable, version-controlled          |
| **DR-06**                                                                | User master data (user ID, role, shift)                     | HR/IT system                | NFR-02, NFR-04 | Accurate role assignments               |

**Data Readiness Note:**

- Historical data is assumed fragmented (A01, 01. Project Initiation).
- Phase 1 focuses on **new data capture**; predictive models deferred until data readiness validated.

---

## 5. Integration Requirements

**Purpose:**
To define high-level integration needs without specifying protocols or architectures.

| **IR-IDIntegration RequirementSource System (Hypothetical)PurposeConstraint** |                                                                                         |                             |              |                                             |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------- | ------------ | ------------------------------------------- |
| **IR-01**                                                                     | System shall ingest downtime event data from existing CMMS via scheduled export or API. | CMMS                        | FR-01, BR-01 | Must comply with IT security policies (C02) |
| **IR-02**                                                                     | System shall allow manual entry of downtime/changeover data via web form.               | N/A (User Input)            | FR-01, FR-02 | Fallback if CMMS integration delayed        |
| **IR-03**                                                                     | System shall export dashboards and reports to CSV/Excel for management review.          | N/A (Output)                | NFR-05       | No live BI tool integration in MVP          |
| **IR-04**                                                                     | System shall authenticate users via existing corporate SSO (if available).              | Corporate Identity Provider | NFR-04       | Optional in MVP; manual login acceptable    |

**Specialist Ownership Note:**

- Detailed API design, data mapping, and security protocols are owned by IT/Data Engineering specialists.

---

## 6. User Stories

**Purpose:**
To express requirements from end-user perspectives, limited to 10 representative stories (per prompt’s “no artificial 50+ backlog” principle).

| **US-IDUser StoryLinked FRLinked BRPriority** |                                                                                                                                      |              |         |             |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ------- | ----------- |
| **US-01**                                     | As a Shift Supervisor, I want to log a downtime event with line, asset, and fault code so that I can track unplanned stops.          | FR-01        | BR-01   | Must Have   |
| **US-02**                                     | As a Maintenance Lead, I want to view all downtime events for my shift so that I can prioritize repairs.                             | FR-01, FR-06 | BR-01   | Must Have   |
| **US-03**                                     | As an Operator, I want to record changeover start and end times so that we can measure improvement.                                  | FR-02        | BR-02   | Must Have   |
| **US-04**                                     | As a Plant Manager, I want to see changeover duration trends by line so that I can identify bottlenecks.                             | FR-02, FR-06 | BR-02   | Should Have |
| **US-05**                                     | As a Maintenance Technician, I want to receive an alert when an asset shows anomalous behavior so that I can inspect before failure. | FR-03, FR-07 | BR-03   | Should Have |
| **US-06**                                     | As a Maintenance Lead, I want to approve or reject an alert before a work order is created so that I control maintenance workload.   | FR-07        | BR-03   | Must Have   |
| **US-07**                                     | As a Technician, I want to search for SOPs by fault code so that I can follow correct procedures.                                    | FR-04        | BR-04   | Should Have |
| **US-08**                                     | As a Quality Manager, I want to enforce a fault taxonomy so that root-cause analysis is consistent.                                  | FR-05        | BR-05   | Must Have   |
| **US-09**                                     | As a Shift Supervisor, I want to view a real-time dashboard during handover so that I don’t lose context.                            | FR-06        | BR-06   | Could Have  |
| **US-10**                                     | As an IT Manager, I want all user actions logged with timestamp and user ID so that we can audit system usage.                       | NFR-02       | All BRs | Must Have   |

**Acceptance Criteria:** Defined per story in next section.

---

## 7. Acceptance Criteria

**Purpose:**
To define testable conditions for each user story, enabling validation without engineering-level test scripts.

| **US-IDAcceptance Criteria (Summary)** |                                                                                                                                                       |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **US-01**                              | Given I am a Shift Supervisor, when I log a downtime event, then the system saves timestamp, line, asset, and fault code; free-text fault is blocked. |
| **US-02**                              | Given I am a Maintenance Lead, when I open the downtime list, then I see events filtered by my shift with sortable columns.                           |
| **US-03**                              | Given I am an Operator, when I start/changeover, then I can record start/end times and reason; duration auto-calculated.                              |
| **US-04**                              | Given I am a Plant Manager, when I view changeover reports, then I see trend charts by line and can export to CSV.                                    |
| **US-05**                              | Given an anomaly is detected, when the system generates an alert, then I receive a notification with asset ID and anomaly type.                       |
| **US-06**                              | Given an alert exists, when I review it, then I can approve (creates work order) or reject (logs reason); no auto-action.                             |
| **US-07**                              | Given I enter a fault code, when I search SOPs, then I see linked documents with titles and preview snippets.                                         |
| **US-08**                              | Given I log a fault, when I select from taxonomy, then free-text entry is disabled; invalid codes are rejected.                                       |
| **US-09**                              | Given I open the dashboard, when I view during handover, then I see line status, active alerts, and changeover progress updated within 5 min.         |
| **US-10**                              | Given any user action, when I check the audit log, then I see timestamp, user ID, action type, and record ID.                                         |

---

## 8. Requirements Traceability Matrix (RTM)

**Purpose:**
To demonstrate end-to-end traceability from business objective to test case and KPI, per prompt’s traceability principle.

| **Business ObjectiveBusiness NeedBR-IDFR-IDSolution ComponentPredictive Use CaseTest Case (Summary)KPI** |                          |       |              |                              |                        |                                                 |                                             |
| -------------------------------------------------------------------------------------------------------- | ------------------------ | ----- | ------------ | ---------------------------- | ---------------------- | ----------------------------------------------- | ------------------------------------------- |
| **O1** (Discovery)                                                                                       | N1 (Unified view)        | BR-01 | FR-01        | Downtime Logging Module      | N/A                    | TC-01: Log event; verify fields                 | % downtime events logged with fault code    |
| **O2** (Requirements)                                                                                    | N2 (Changeover tracking) | BR-02 | FR-02        | Changeover Tracker           | N/A                    | TC-02: Log changeover; verify duration          | Avg changeover duration by line             |
| **O3** (Solution)                                                                                        | N3 (Early warning)       | BR-03 | FR-03, FR-07 | Anomaly Detection + Alerting | Predictive Maintenance | TC-05: Trigger anomaly; verify alert + approval | % alerts approved within 15 min             |
| **O3** (Solution)                                                                                        | N4 (Decision support)    | BR-04 | FR-04        | RAG Knowledge Assistant      | N/A (RAG)              | TC-07: Search SOP by fault code                 | Avg time to find SOP                        |
| **O2** (Requirements)                                                                                    | N5 (Root-cause)          | BR-05 | FR-05        | Fault Taxonomy Engine        | N/A                    | TC-08: Enforce taxonomy; block free-text        | % faults tagged with valid code             |
| **O4** (Delivery)                                                                                        | N6 (Handover)            | BR-06 | FR-06        | Operational Dashboard        | N/A                    | TC-09: View dashboard; verify latency           | Shift handover time reduction (directional) |

**Traceability Rules:**

- Every BR maps to a business need (no orphan BRs).
- Every FR maps to a BR (no gold-plating).
- Every NFR is justified by a constraint or quality need.
- Every requirement has acceptance/test logic.
- No requirement exists solely because technology suggested it.

---

## AI Involvement Disclosure (Internal Control Note)

*This Requirements document was drafted with AI assistance for structuring, terminology consistency, and traceability validation. All business requirements, functional logic, NFRs, data needs, user stories, and acceptance criteria were reviewed and finalized by the author. All integration sources and data examples are hypothetical assumptions requiring client validation. No technical architecture or engineering specs were created.*

---

## Next Step Confirmation

**03. Requirements** is now complete at draft v0.1, with full traceability to 01. Project Initiation and 02. Discovery.

Shall I proceed to **Step 4: 04. Process & Solution Analysis** (As-Is → To-Be → Gap → Options → Evaluation → Proposed Solution)?

Proceeding to **Step 4: 04. Process & Solution Analysis**.

This consolidates all six line items from the frozen **04. Process & Solution Analysis** section into a controlled working document, strengthening the analytical chain (AS-IS → Pain → Gap → Options → Evaluation → Recommendation) while maintaining business-level framing and specialist boundary clarity.

---
