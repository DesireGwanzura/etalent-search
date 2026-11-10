---
ticket_id: ET-042
title: Build Ranking Consistency and Top-5 Overlap Test Suite
publish: approval
priority: must
type: test
workstream: qa
owner_role: tester
---

# [ET-042] — Build Ranking Consistency and Top-5 Overlap Test Suite

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-042 |
| **Title** | Build Ranking Consistency and Top-5 Overlap Test Suite |
| **Project** | eTalent Search |
| **Workstream** | H. Testing and Release |
| **Ticket Type** | Testing |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | QA Engineer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-6, Consistency and Performance |

---

## 2. Objective

Build automated test suite validating ranking consistency and top-5 overlap against benchmark vacancies across repeated runs.

---

## 3. Background and Context

Specification v1.0 Section 9: Target ranking quality is top 5 matching the recruiter-expected top 5 in at least 4 of 5 positions on most sample vacancies. Same inputs must always return identical stored snapshot.

---

## 4. User Story / Engineering Story

> As a QA engineer, I want automated ranking consistency tests, so that we verify scoring reproducibility and ensure top-5 overlap targets are continuously maintained.

---

## 5. Scope

### In Scope
- Test suite evaluating 5 benchmark vacancies against expected top-5 candidate lists.
- Automated overlap metric calculation: `overlap = count(top5_actual in top5_expected) / 5`.
- Target threshold enforcement: overlap >= 4/5 (80%) on benchmark vacancies.
- Idempotency test: verify 10 consecutive ranking calls for same vacancy yield identical snapshots.

### Out of Scope
- Live manual recruiter interviewing

### Constraints
- Automated execution in nightly or release CI.
- Synthetic benchmark data.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-6, Consistency and Performance

### Technical Requirements
- TR-073-01: Implement `RankingConsistencyTest` running benchmark vacancies.
- TR-073-02: Calculate Jaccard and rank-order overlap metrics.
- TR-073-03: Assert snapshot reproducibility across repeated runs.

---

## 7. Implementation Flow

1. Load benchmark vacancies and candidate pool into Testcontainers database.
2. Execute ranking engine for each vacancy.
3. Compare returned top 5 candidates against expected benchmark top 5.
4. Calculate overlap percentage; assert >= 80% on at least 4 vacancies.
5. Re-run ranking and verify returned snapshot is bit-for-bit identical.

---

## 8. Acceptance Criteria

- **AC-01:** Benchmark vacancies achieve at least 4-of-5 top-5 overlap against expected rankings.
- **AC-02:** Repeated ranking evaluations with same parameters produce identical candidate ordering.
- **AC-03:** Test results output structured JSON report for release review.

---

## 9. Testing Requirements

### Required Test Coverage
- Automated execution of `RankingConsistencyTest` asserting quality thresholds.
- Negative test verifying altered weights produce expected rank shifts.

---

## 10. Deliverables

- RankingConsistencyTest suite
- Benchmark dataset loader
- Consistency reporting utility

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-004, ET-016, ET-040
- **Downstream Tickets:** ET-047
- **Technical Risks & Mitigations:** Minor LLM evaluation variation altering edge scores; mitigated by caching and robust prompt grounding.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/42
- **Branch:** `feature/et-042-ranking-consistency-overlap-tests`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
