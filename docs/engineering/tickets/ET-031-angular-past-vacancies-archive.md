---
ticket_id: ET-031
title: Build Past Vacancies Archive and Reopen UI
publish: auto
priority: should
type: feature
workstream: frontend
owner_role: developer
---

# [ET-031] — Build Past Vacancies Archive and Reopen UI

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-031 |
| **Title** | Build Past Vacancies Archive and Reopen UI |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Should |
| **Publishing Mode** | auto |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-11 |

---

## 2. Objective

Build the past vacancies archive list and reopen functionality displaying historical ranking snapshots.

---

## 3. Background and Context

Specification v1.0 FR-11: Past vacancies are stored and can be reopened by any recruiter; reopening shows the stored ranking. Archive hides a vacancy from default list; nothing is deleted; edits create a new version.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to browse past vacancies, archive closed vacancies, and reopen past searches, so that past recruitment searches are easily revisited.

---

## 5. Scope

### In Scope
- Vacancies dashboard with 'Active Vacancies' and 'Archived Vacancies' tabs.
- Archive vacancy action button (available only to creator or admin).
- Reopen vacancy action: loads stored ranking snapshot and displays historical scores and weights.
- Read-only indicator when viewing an archived vacancy.
- Search and filter past vacancies by title, date, and creator.

### Out of Scope
- Permanent deletion of vacancies

### Constraints
- All recruiters can view all vacancies; only creator/admin can archive.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-11

### Technical Requirements
- TR-062-01: Implement `VacancyDashboardComponent` with active and archive tabs.
- TR-062-02: Connect archive action to `POST /api/vacancies/{id}/archive`.
- TR-062-03: Render historical snapshot view when reopening past vacancy.

---

## 7. Implementation Flow

1. Recruiter navigates to Vacancies dashboard.
2. Switch between 'Active' and 'Archived' views.
3. Click 'Archive' on a filled vacancy to hide it from active search.
4. Click on an archived vacancy to reopen and view historical stored ranking.
5. UI clearly indicates historical snapshot date and original weights.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter can view list of all active and archived vacancies.
- **AC-02:** Archiving a vacancy moves it to archive list without deleting data.
- **AC-03:** Reopening an archived vacancy displays the exact historical ranking snapshot.

---

## 9. Testing Requirements

### Required Test Coverage
- Component unit tests verifying tab switching and archive action permissions.
- Integration test verifying historical snapshot display.

---

## 10. Deliverables

- VacancyDashboardComponent
- ArchiveVacancyDialogComponent
- Dashboard styles

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-021, ET-026
- **Downstream Tickets:** ET-044
- **Technical Risks & Mitigations:** Accidental archiving; mitigated by confirmation dialog.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/31
- **Branch:** `feature/et-031-angular-past-vacancies-archive`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
