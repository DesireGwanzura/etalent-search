# [ET-053] — Implement Candidate Profile and Ranking Query REST API

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-053 |
| **Title** | Implement Candidate Profile and Ranking Query REST API |
| **Project** | eTalent Search |
| **Workstream** | F. Backend and Security |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-3, FR-4, FR-5 |
| **GitHub Labels** | stream:backend, type:feature, priority:must, role:developer |

---

## 2. Objective

Build REST API endpoints to retrieve ranked candidates for a vacancy, inspect full candidate profiles, and view scoring factor explanations.

---

## 3. Background and Context

Specification v1.0 FR-3, FR-4, FR-5: Results display sorted by score: name, title, score, top reasons. Recruiter can open full candidate profile. Every result carries plain-language explanation per factor.

---

## 4. User Story / Engineering Story

> As a recruiter, I want REST endpoints to fetch candidate rankings and detailed profiles, so that I can evaluate candidate evidence and make informed shortlisting decisions.

---

## 5. Scope

### In Scope
- Endpoint `GET /api/vacancies/{id}/rankings` returning sorted candidates, scores, factor explanations, and shortfall indicator.
- Endpoint `GET /api/candidates/{id}` returning full candidate profile (headline, experience history, skills, education, location).
- Data protection: Candidate names rejoin results from source record; unscrubbed PII is never exposed to unauthorized callers.
- Audit logging: Every candidate profile view is logged with user identity.

### Out of Scope
- Editing candidate profile data (eTalent is read-only for candidate records)

### Constraints
- Authenticated access only.
- Plain-language factor explanations must be included.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-3, FR-4, FR-5

### Technical Requirements
- TR-053-01: Implement `RankingController` returning `VacancyRankingResponseDTO`.
- TR-053-02: Implement `CandidateController` returning sanitized full candidate profile.
- TR-053-03: Record access event in `audit_log` table on profile retrieval.

---

## 7. Implementation Flow

1. Recruiter requests ranking for vacancy ID.
2. Fetch latest ranking snapshot from database.
3. Rejoin candidate personal details (name) from source record.
4. Return candidate list sorted by score with factor breakdown.
5. When candidate profile is opened, log view event in audit log.

---

## 8. Acceptance Criteria

- **AC-01:** Ranking endpoint returns candidates sorted by score with plain-language explanations.
- **AC-02:** Candidate profile endpoint returns complete work history, skills, and education.
- **AC-03:** Candidate profile views generate an audit log entry containing recruiter user ID.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test verifying ranking response structure and sort order.
- Audit test verifying candidate profile view creates audit log entry.

---

## 10. Deliverables

- RankingController
- CandidateController
- Ranking and Candidate Profile DTOs

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-049, ET-051, ET-052
- **Downstream Tickets:** ET-059, ET-060
- **Technical Risks & Mitigations:** Slow response times on large candidate profiles; mitigated by projected DTO queries.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/22
- **Branch:** `feature/et-053-candidate-profile-ranking-rest-api`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
