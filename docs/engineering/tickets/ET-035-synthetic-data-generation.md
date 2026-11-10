# [ET-035] — Implement Synthetic Candidate and Vacancy Dataset Generation

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-035 |
| **Title** | Implement Synthetic Candidate and Vacancy Dataset Generation |
| **Project** | eTalent Search |
| **Workstream** | A. Foundation & Architecture |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | QA Engineer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | Foundation, Privacy, FR-7 |
| **GitHub Labels** | stream:foundation, stream:qa, type:test, priority:must, role:tester |

---

## 2. Objective

Build automated generator for 100-200 synthetic candidate CV profiles and 5-10 benchmark vacancies with expected top-5 rankings.

---

## 3. Background and Context

Specification v1.0 mandates no real candidate data in the repository or tests. A synthetic dataset of 100-200 messy CVs, 5-10 benchmark vacancies, and a 1,000-candidate scale set is required before the AI spike and integration tests can run.

---

## 4. User Story / Engineering Story

> As an engineering team, we need a realistic synthetic dataset generator for CVs and vacancies, so that development, testing, and AI benchmarking proceed compliantly without real candidate data.

---

## 5. Scope

### In Scope
- Automated generator producing 100-200 diverse, messy synthetic candidate JSON profiles.
- 5-10 benchmark vacancies covering engineering, architecture, and management roles with expected top-5 candidates.
- Scale set generator for 1,000 synthetic CVs for the AI feasibility spike.
- Edge cases: missing dates, sparse profiles, equivalent skills (JS/JavaScript), non-standard titles.

### Out of Scope
- Ingestion into production database
- Real candidate data parsing

### Constraints
- Zero real personal information; all synthetic data generated using Faker/custom seed rules.
- Must conform to CV JSON schema.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation, Privacy, FR-7

### Technical Requirements
- TR-035-01: Create data generation script `generate_synthetic_data.py` or Java fixture generator.
- TR-035-02: Ensure generated CV JSON conforms strictly to Specification section 7 schema.
- TR-035-03: Seed 10 benchmark vacancies with curated expected top-5 candidate IDs.

---

## 7. Implementation Flow

1. Define synthetic persona generator with varied experience, skills, and locations.
2. Generate 100-200 base synthetic CV JSON files under `src/test/resources/fixtures/candidates/`.
3. Generate 10 benchmark vacancies with expected top-5 ranking lists.
4. Generate 1,000 candidate scale dataset for the AI feasibility spike.
5. Validate all generated JSON against schema.

---

## 8. Acceptance Criteria

- **AC-01:** At least 150 synthetic CV JSON files generated conforming to the CV JSON contract.
- **AC-02:** 10 benchmark vacancies generated with documented expected top-5 candidates.
- **AC-03:** Synthetic data contains zero real PII and includes deliberate missing data and equivalence cases.

---

## 9. Testing Requirements

### Required Test Coverage
- Schema validation test validating all generated files against the CV JSON schema.
- Automated PII scanner verifying absence of real South African ID numbers, actual phone numbers, and real emails.

---

## 10. Deliverables

- Synthetic data generator script
- 150+ synthetic candidate JSON fixtures
- 10 benchmark vacancy fixtures

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-032
- **Downstream Tickets:** ET-036, ET-042, ET-047, ET-071
- **Technical Risks & Mitigations:** Synthetic data not being messy enough to test parser resilience; mitigated by deliberate edge-case generation.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/4
- **Branch:** `feature/et-035-synthetic-data-generation`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
