# [ET-054] — Implement Shortlist Management REST API

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-054 |
| **Title** | Implement Shortlist Management REST API |
| **Project** | eTalent Search |
| **Workstream** | F. Backend and Security |
| **Ticket Type** | Feature |
| **Priority** | Should |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-15 |
| **GitHub Labels** | stream:backend, type:feature, priority:should, role:developer |

---

## 2. Objective

Build REST API endpoints allowing recruiters to mark candidates as shortlisted on a vacancy and persist the shortlist with the vacancy snapshot.

---

## 3. Background and Context

Specification v1.0 FR-15: A recruiter marks candidates as shortlisted on a vacancy and the shortlist is saved with it. The system never rejects candidates automatically.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to mark candidates as shortlisted on a vacancy, so that our hiring team saves the agreed candidate shortlist for interviewing.

---

## 5. Scope

### In Scope
- Endpoint `POST /api/vacancies/{id}/shortlist` accepting list of candidate IDs to shortlist.
- Endpoint `DELETE /api/vacancies/{id}/shortlist/{candidateId}` to un-shortlist a candidate.
- Endpoint `GET /api/vacancies/{id}/shortlist` returning only shortlisted candidates.
- Shortlist status persisted in the vacancy ranking snapshot items.
- Strict policy: shortlisted or un-shortlisted candidates are NEVER marked as 'rejected'.

### Out of Scope
- Automated email notifications to candidates
- Interview scheduling

### Constraints
- Human-controlled decision only; system never automatically rejects.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-15

### Technical Requirements
- TR-054-01: Add `is_shortlisted` boolean column to `candidate_snapshot_item` table.
- TR-054-02: Implement `ShortlistController` with shortlist management operations.
- TR-054-03: Log shortlist modification events in audit trail.

---

## 7. Implementation Flow

1. Recruiter toggles shortlist flag for a candidate on vacancy ranking.
2. Send shortlist update request to API.
3. Update `is_shortlisted` flag in snapshot item.
4. Log shortlist event in audit log.
5. Return updated shortlist status.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter can add and remove candidates from vacancy shortlist.
- **AC-02:** Shortlist state persists across vacancy reopenings and re-rankings.
- **AC-03:** System contains zero automatic rejection rules or states.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test adding candidates to shortlist and reloading vacancy.
- Negative test verifying un-shortlisted candidates remain in candidate database.

---

## 10. Deliverables

- ShortlistController
- ShortlistService
- Shortlist DTOs

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-049, ET-052
- **Downstream Tickets:** ET-061, ET-076
- **Technical Risks & Mitigations:** Accidental deletion of shortlist; mitigated by soft-toggle and audit trail.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/23
- **Branch:** `feature/et-054-shortlist-management-rest-api`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
