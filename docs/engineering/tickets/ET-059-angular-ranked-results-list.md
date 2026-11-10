# [ET-059] — Build Ranked Candidate Results List and Factor Explanations

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-059 |
| **Title** | Build Ranked Candidate Results List and Factor Explanations |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-2, FR-3, FR-4 |
| **GitHub Labels** | stream:frontend, type:feature, priority:must, role:developer |

---

## 2. Objective

Build the ranked candidate results list component displaying candidate score cards, factor breakdown badges, and plain-language explanations.

---

## 3. Background and Context

Specification v1.0 FR-2, FR-3, FR-4: Results display sorted by score: name, title, score, top reasons. Every result carries plain-language explanation per factor. Shortfall indicator displays when candidates exceed cap 100.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to view a ranked list of candidates with scores, factor breakdowns, and plain-language explanations, so that I understand exactly why each candidate received their score.

---

## 5. Scope

### In Scope
- Ranked candidate card list ordered by score DESC with rank position badge.
- Score display (0-100) and factor breakdown pill badges.
- Expandable factor explanation section showing plain-language AI explanation per factor.
- 'Not provided' indicator for factors with missing candidate data.
- Shortfall banner: 'Evaluating top 100 of X eligible candidates' if cap is exceeded.
- Degraded mode badge: 'Fallback ranking - AI evaluation unavailable' when applicable.

### Out of Scope
- Direct messaging or emailing candidate from UI

### Constraints
- Explanations must never contain raw numeric scores.
- Accessible contrast and typography.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-2, FR-3, FR-4

### Technical Requirements
- TR-059-01: Create `RankingListComponent` and child `CandidateCardComponent`.
- TR-059-02: Implement expandable accordions for factor explanations.
- TR-059-03: Bind shortfall banner to `response.shortfallCount`.

---

## 7. Implementation Flow

1. Fetch ranking data from `GET /api/vacancies/{id}/rankings`.
2. Render candidate cards sorted by score with rank numbers.
3. If `shortfallCount > 0`, display informative banner at top.
4. Recruiter clicks card to expand detailed factor explanations.
5. Recruiter clicks candidate name to open full profile modal/drawer.

---

## 8. Acceptance Criteria

- **AC-01:** Candidates are displayed sorted by score with name, current title, and total score.
- **AC-02:** Expanding a candidate reveals plain-language explanation per factor with missing data clearly labeled.
- **AC-03:** When candidates exceed 100, banner states how many candidates were not evaluated.

---

## 9. Testing Requirements

### Required Test Coverage
- Component unit tests verifying sorting order and accordion expansion.
- Visual check verifying 'not provided' styling on missing factor data.

---

## 10. Deliverables

- RankingListComponent
- CandidateCardComponent
- Component styles and templates

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-053, ET-057
- **Downstream Tickets:** ET-060, ET-061
- **Technical Risks & Mitigations:** Rendering performance lag on 100 candidate cards; mitigated by Angular `@for` with trackBy and virtual scrolling if needed.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/28
- **Branch:** `feature/et-059-angular-ranked-results-list`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
