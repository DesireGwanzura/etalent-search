# [ET-058] — Build Vacancy Creation and Configurable Weights UI

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-058 |
| **Title** | Build Vacancy Creation and Configurable Weights UI |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-1, FR-14 |
| **GitHub Labels** | stream:frontend, type:feature, priority:must, role:developer |

---

## 2. Objective

Build Angular vacancy creation and edit form with interactive weight sliders totaling 100% and validation.

---

## 3. Background and Context

Specification v1.0 FR-1, FR-14: Recruiter creates vacancy (title, required skills, optional skills, min experience, location, remote). Recruiter sets weight of each scoring factor per vacancy, starting from defaults.

---

## 4. User Story / Engineering Story

> As a recruiter, I want an intuitive vacancy creation form with interactive weight sliders, so that I can define vacancy requirements and tailor scoring factor weights.

---

## 5. Scope

### In Scope
- Vacancy form: Title, required skills tag input, optional skills tag input, minimum experience years, location, remote allowed checkbox.
- Five factor weight sliders/inputs: Required Skills (default 40), Experience (25), Role Match (15), Nice-to-have (10), Location/Availability (10).
- Real-time weight totalizer: visual indicator showing sum; blocks submission if total != 100.
- Reset to system defaults button.
- Client-side reactive form validation.

### Out of Scope
- AI prompt editing (recruiter cannot modify prompts)

### Constraints
- Weights must total 100 before submit button is enabled.
- Responsive design.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-1, FR-14

### Technical Requirements
- TR-058-01: Create `VacancyFormComponent` using Angular Reactive Forms.
- TR-058-02: Implement custom validator `totalWeightsValidator` enforcing sum == 100.
- TR-058-03: Integrate `VacancyService` calling `POST /api/vacancies`.

---

## 7. Implementation Flow

1. Recruiter opens 'Create Vacancy' screen.
2. Form pre-populates with system default weights (40/25/15/10/10).
3. Recruiter enters requirements and adjusts weight sliders.
4. Totalizer updates in real time; warns if sum != 100.
5. On submit, send payload to API and navigate to ranking results view.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter can input all vacancy fields and skill tags.
- **AC-02:** Weight sliders initialize with system defaults and validate sum == 100.
- **AC-03:** Successful submission redirects to ranking results page for the new vacancy.

---

## 9. Testing Requirements

### Required Test Coverage
- Angular component unit tests for form validation and weight totalizer.
- UI test verifying submit button disabled when weights total 95 or 105.

---

## 10. Deliverables

- VacancyFormComponent
- VacancyService
- Form SCSS styles and templates

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-052, ET-057
- **Downstream Tickets:** ET-059
- **Technical Risks & Mitigations:** Slider usability issues on mobile/tablet; mitigated by dual slider and direct numeric input controls.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/27
- **Branch:** `feature/et-058-angular-vacancy-creation-weights`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
