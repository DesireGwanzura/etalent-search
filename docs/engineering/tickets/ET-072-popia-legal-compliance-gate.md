# [ET-072] — Establish POPIA Legal Compliance Gate and Synthetic Data Policy

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-072 |
| **Title** | Establish POPIA Legal Compliance Gate and Synthetic Data Policy |
| **Project** | eTalent Search |
| **Workstream** | H. Testing and Release |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | Security, Privacy and Fairness, Gate R1 |
| **GitHub Labels** | stream:foundation, type:documentation, type:security, priority:must, role:developer |

---

## 2. Objective

Document the POPIA compliance framework, AI processing terms, and enforce synthetic-data-only policy until Gate R1 legal clearance.

---

## 3. Background and Context

Specification v1.0 Section 8 & Gate R1: Legal confirms the basis for reusing stored candidate data and AI provider terms before real candidate data is loaded. Until then, the system runs on synthetic data only. R1 is a launch gate, not a development blocker.

---

## 4. User Story / Engineering Story

> As an engineering team and compliance officer, we need an enforced synthetic-data policy and POPIA gate definition, so that development proceeds without regulatory risk until legal clearance.

---

## 5. Scope

### In Scope
- Document `docs/compliance/popia-compliance-gate.md` defining legal Gate R1 requirements.
- Verification checklist for AI provider terms: Data Processing Agreement (DPA), zero model training on company data, known geographical processing location.
- Enforce environment variable flag `APP_DATA_MODE=SYNTHETIC` preventing ingestion of unverified external feeds.
- Audit trail verifying zero real candidate records exist in development or testing databases.

### Out of Scope
- Legal counsel sign-off (executed by external legal counsel)

### Constraints
- Real candidate data is strictly prohibited until Gate R1 is cleared in writing.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Security, Privacy and Fairness, Gate R1

### Technical Requirements
- TR-072-01: Implement `DataModeValidator` checking `APP_DATA_MODE` on ingestion startup.
- TR-072-02: Produce `docs/compliance/popia-compliance-gate.md` with audit criteria.
- TR-072-03: Configure pre-commit hook scanning for real South African ID patterns.

---

## 7. Implementation Flow

1. System initializes with `APP_DATA_MODE=SYNTHETIC` default.
2. Ingestion pipeline rejects non-synthetic sources if R1 gate is unverified.
3. Legal team reviews AI provider DPA and signs off Gate R1.
4. Authorized administrator enables production data mode with signed certificate reference.

---

## 8. Acceptance Criteria

- **AC-01:** Compliance document defines Gate R1 prerequisites and verification criteria.
- **AC-02:** System refuses to ingest unverified source feeds when `APP_DATA_MODE=SYNTHETIC`.
- **AC-03:** Development and CI pipelines operate 100% on synthetic data without blocking on legal.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit test verifying `DataModeValidator` blocks unverified feeds in synthetic mode.
- Automated repository scan verifying zero real PII committed in codebase.

---

## 10. Deliverables

- docs/compliance/popia-compliance-gate.md
- DataModeValidator class
- Compliance checklist

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-032
- **Downstream Tickets:** ET-078
- **Technical Risks & Mitigations:** Unintentional ingestion of real CV files; mitigated by strict environment variable enforcement.

---

## 12. Definition of Done

- [ ] Implementation complete and adheres to Specification v1.0.
- [ ] Acceptance criteria independently verified by QA.
- [ ] Automated unit and integration tests passing in CI.
- [ ] Dual peer code review approved.
- [ ] GitLab CI/CD pipeline successful on commit.
- [ ] Documentation updated and synchronized.
- [ ] Pull request linked to issue and merged to integration branch (`dev`).
- [ ] Verification evidence attached.

---

## 13. Implementation Evidence

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/41
- **Branch:** `feature/et-072-popia-legal-compliance-gate`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
