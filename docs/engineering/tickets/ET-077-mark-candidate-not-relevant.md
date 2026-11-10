# [ET-077] — Implement Mark Candidate Not Relevant Action

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-077 |
| **Title** | Implement Mark Candidate Not Relevant Action |
| **Project** | eTalent Search |
| **Workstream** | H. Testing, Release & Optional |
| **Ticket Type** | Feature |
| **Priority** | Nice |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-12 |
| **GitHub Labels** | stream:backend, stream:frontend, type:feature, priority:nice, role:developer |

---

## 2. Objective

Build functionality allowing recruiters to mark a candidate as 'not relevant' for a specific vacancy (visible to all recruiters).

---

## 3. Background and Context

Specification v1.0 FR-12: Mark a candidate not relevant for a vacancy (per vacancy, visible to all). Classified as Nice priority (dropped first if time runs short). Note: This does NOT reject the candidate from the database or other vacancies.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to mark a candidate as not relevant for a specific vacancy, so that our team visually differentiates candidates who do not match this specific role.

---

## 5. Scope

### In Scope
- Endpoint `POST /api/vacancies/{id}/candidates/{candidateId}/not-relevant`.
- Flagging candidate in ranking snapshot item: `isNotRelevant: true`, `notRelevantMarkedBy: username`.
- UI visual treatment: candidate card appears dimmed with 'Not Relevant' badge and option to un-mark.
- Visible to all recruiters viewing that vacancy; candidate remains available for all other vacancies.

### Out of Scope
- Permanent deletion of candidate
- Automated rejection notification

### Constraints
- Per-vacancy flag only; candidate must never be globally rejected.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-12

### Technical Requirements
- TR-077-01: Add `is_not_relevant` boolean column to `candidate_snapshot_item`.
- TR-077-02: Implement toggle endpoint in `RankingController`.
- TR-077-03: Add dimmed visual card state in Angular `CandidateCardComponent`.

---

## 7. Implementation Flow

1. Recruiter reviews candidate and clicks 'Mark Not Relevant'.
2. Card updates to dimmed state with 'Marked Not Relevant' badge.
3. State is saved with the vacancy snapshot.
4. Other recruiters viewing the vacancy see the not-relevant badge.
5. Recruiter can un-mark candidate at any time.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter can mark candidate as not relevant for a specific vacancy.
- **AC-02:** Flagged candidates are visibly dimmed but remain in the list (never deleted).
- **AC-03:** Candidate remains completely unaffected in other vacancies and searches.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test marking candidate not relevant and verifying per-vacancy isolation.
- UI test verifying dimmed card rendering.

---

## 10. Deliverables

- Not-relevant toggle endpoint
- Snapshot schema migration
- UI card update

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-049, ET-059
- **Downstream Tickets:** ET-078
- **Technical Risks & Mitigations:** Recruiter misinterpreting flag as system rejection; mitigated by explicit tooltip explaining per-vacancy scope.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/46
- **Branch:** `feature/et-077-mark-candidate-not-relevant`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
