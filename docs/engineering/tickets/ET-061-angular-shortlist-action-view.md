# [ET-061] — Build Shortlist Action and Dedicated Shortlist View

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-061 |
| **Title** | Build Shortlist Action and Dedicated Shortlist View |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Should |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-15 |
| **GitHub Labels** | stream:frontend, type:feature, priority:should, role:developer |

---

## 2. Objective

Build shortlist toggle actions on candidate cards and a dedicated shortlist view tab for each vacancy.

---

## 3. Background and Context

Specification v1.0 FR-15: A recruiter marks candidates as shortlisted on a vacancy and the shortlist is saved with it. The system never rejects candidates automatically.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to shortlist candidates and view a dedicated shortlist tab, so that our recruitment team can finalize and review our interview shortlist.

---

## 5. Scope

### In Scope
- Shortlist toggle button (bookmark/star icon) on candidate cards and profile drawer.
- Dedicated 'Shortlist' tab on vacancy view showing only shortlisted candidates.
- Shortlist count badge in tab header (e.g., 'Shortlist (4)').
- Option to re-order or remove candidates from shortlist.
- Visual confirmation toast on shortlisting action.

### Out of Scope
- Automated ATS export (handled in optional CSV export)

### Constraints
- Shortlist actions must never reject non-shortlisted candidates.
- Optimistic UI update.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-15

### Technical Requirements
- TR-061-01: Implement `ShortlistToggleComponent` with optimistic state update.
- TR-061-02: Implement `VacancyShortlistTabComponent` displaying shortlisted subset.
- TR-061-03: Integrate with `ShortlistService` API.

---

## 7. Implementation Flow

1. Recruiter clicks 'Shortlist' button on candidate card.
2. Button updates optimistically to 'Shortlisted' with checkmark.
3. API call updates backend shortlist state in background.
4. Shortlist tab count increments.
5. Recruiter clicks 'Shortlist' tab to review curated candidate list.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter can toggle shortlist status on any candidate card.
- **AC-02:** Dedicated shortlist tab displays all shortlisted candidates for the vacancy.
- **AC-03:** Shortlist state persists upon page refresh.

---

## 9. Testing Requirements

### Required Test Coverage
- Component unit tests for shortlist toggling and tab filtering.
- Integration test verifying API call on shortlist toggle.

---

## 10. Deliverables

- ShortlistToggleComponent
- VacancyShortlistTabComponent
- Shortlist styles

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-054, ET-059
- **Downstream Tickets:** ET-076
- **Technical Risks & Mitigations:** Network failure during optimistic toggle; mitigated by automatic rollback and error notification.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/30
- **Branch:** `feature/et-061-angular-shortlist-action-view`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
