# [ET-075] — Implement Location and Availability Faceted Search Filters

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-075 |
| **Title** | Implement Location and Availability Faceted Search Filters |
| **Project** | eTalent Search |
| **Workstream** | H. Testing, Release & Optional |
| **Ticket Type** | Feature |
| **Priority** | Should |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-9 |
| **GitHub Labels** | stream:backend, stream:frontend, type:feature, priority:should, role:developer |

---

## 2. Objective

Build UI and backend faceted filters allowing recruiters to filter ranked candidate lists by location and immediate availability.

---

## 3. Background and Context

Specification v1.0 FR-9: Filter the ranked list by location and availability. Classified as Should priority (cut in reverse order if time runs short).

---

## 4. User Story / Engineering Story

> As a recruiter, I want to filter ranked results by location and availability, so that I can focus on candidates who can start immediately or reside in a specific city.

---

## 5. Scope

### In Scope
- Backend query parameters on ranking endpoint: `location`, `remoteOnly`, `maxAvailabilityDays`.
- Angular filter sidebar/chips on ranked results view allowing instant filtering.
- Candidate availability badges: 'Immediate', '2 Weeks', '1 Month', '3 Months'.
- Filter state saved in URL query parameters for shareable links.

### Out of Scope
- Geographical radius GPS distance mapping

### Constraints
- Filtering must not trigger re-evaluation; filters active ranking list in memory or cached query.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-9

### Technical Requirements
- TR-075-01: Add filter predicates to `RankingService`.
- TR-075-02: Implement `RankingFilterSidebarComponent` in Angular.
- TR-075-03: Update URL query parameters on filter change.

---

## 7. Implementation Flow

1. Recruiter views ranked candidate list.
2. Recruiter checks 'Immediate Availability' and selects 'Johannesburg'.
3. List instantly filters showing only matching candidates, preserving their relative scores.
4. Filter chip bar displays active filters with 'Clear All' option.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter can filter ranked candidate list by location and availability.
- **AC-02:** Filtering operates instantly without triggering new AI evaluation calls.
- **AC-03:** Clearing filters restores complete ranked list.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit tests for filter predicate matching.
- Angular component tests for filter sidebar interactions.

---

## 10. Deliverables

- RankingFilterSidebarComponent
- Backend filter query predicates
- Filter styles

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-053, ET-059
- **Downstream Tickets:** ET-078
- **Technical Risks & Mitigations:** Overly restrictive filters returning zero candidates; mitigated by clear empty state with 'Reset Filters' button.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/44
- **Branch:** `feature/et-075-location-availability-filters`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
