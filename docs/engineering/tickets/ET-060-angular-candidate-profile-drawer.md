# [ET-060] — Build Candidate Profile Inspection View

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-060 |
| **Title** | Build Candidate Profile Inspection View |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-5 |
| **GitHub Labels** | stream:frontend, type:feature, priority:must, role:developer |

---

## 2. Objective

Build the full candidate profile modal/drawer component allowing recruiters to inspect complete candidate CV details and history.

---

## 3. Background and Context

Specification v1.0 FR-5: A recruiter opens a full candidate profile from the ranked list. Profile displays complete work history, skills, education, certifications, and availability.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to inspect a candidate's complete profile and work history, so that I can verify their experience and qualifications before shortlisting.

---

## 5. Scope

### In Scope
- Slide-out drawer or full-screen modal showing full candidate profile.
- Sections: Summary/Headline, Skills, Employment History (with roles, companies, dates, descriptions), Education, Certifications, Location & Availability.
- Highlights matching skills and required qualifications relevant to the current vacancy.
- Shortlist action button directly inside profile view.
- Responsive layout supporting desktop and tablet views.

### Out of Scope
- Editing candidate details
- Uploading new CV document

### Constraints
- Read-only candidate view.
- Close button and escape key dismiss support.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-5

### Technical Requirements
- TR-060-01: Create `CandidateProfileDrawerComponent`.
- TR-060-02: Connect to `CandidateService.getCandidateById(id)`.
- TR-060-03: Implement keyboard accessibility (Escape closes drawer).

---

## 7. Implementation Flow

1. Recruiter clicks candidate card in ranking list.
2. Drawer slides open loading candidate details from API.
3. Recruiter reviews complete CV timeline and skills.
4. Recruiter can toggle candidate shortlist status.
5. Drawer closes returning recruiter to exact scroll position in ranking list.

---

## 8. Acceptance Criteria

- **AC-01:** Profile drawer displays complete work history, education, skills, and availability.
- **AC-02:** Matching skills relevant to active vacancy are visually highlighted.
- **AC-03:** Recruiter can toggle shortlist status directly from the profile view.

---

## 9. Testing Requirements

### Required Test Coverage
- Component unit tests verifying data binding across all profile sections.
- Accessibility test verifying keyboard navigation and focus trapping.

---

## 10. Deliverables

- CandidateProfileDrawerComponent
- Profile templates and SCSS styles

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-053, ET-059
- **Downstream Tickets:** ET-061
- **Technical Risks & Mitigations:** Lengthy CVs causing poor scrolling experience; mitigated by sticky section navigation tabs.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/29
- **Branch:** `feature/et-060-angular-candidate-profile-drawer`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
