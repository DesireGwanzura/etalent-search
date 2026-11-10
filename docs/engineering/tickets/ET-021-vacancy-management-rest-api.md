---
ticket_id: ET-021
title: Implement Vacancy Management REST API
publish: approval
priority: must
type: feature
workstream: backend
owner_role: developer
---

# [ET-021] — Implement Vacancy Management REST API

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-021 |
| **Title** | Implement Vacancy Management REST API |
| **Project** | eTalent Search |
| **Workstream** | F. Backend and Security |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-1, FR-6, FR-10, FR-11, FR-14 |

---

## 2. Objective

Build RESTful API endpoints for creating, editing, viewing, archiving, and reopening vacancies with custom factor weights.

---

## 3. Background and Context

Specification v1.0 Section 3, 4: All recruiters see all vacancies. Only creator or admin edits a vacancy. Archiving hides a vacancy from default list without deleting. Edits create new versions.

---

## 4. User Story / Engineering Story

> As a recruiter, I want REST API endpoints to manage vacancies and configure factor weights, so that I can initiate candidate search rankings and collaborate with other recruiters.

---

## 5. Scope

### In Scope
- Endpoints: `POST /api/vacancies` (create), `GET /api/vacancies` (list active), `GET /api/vacancies/{id}` (detail), `PUT /api/vacancies/{id}` (edit), `POST /api/vacancies/{id}/archive` (archive), `POST /api/vacancies/{id}/reopen` (reopen).
- Fields: title, requiredSkills, optionalSkills, minExperienceYears, location, remoteAllowed, factorWeights.
- Access rule: All recruiters can view; only creator or admin can edit/archive.
- Archiving hides vacancy from default list; no hard deletion.

### Out of Scope
- Public job board postings
- Candidate application submission

### Constraints
- Weights must total 100.
- Only creator or admin can modify.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-1, FR-6, FR-10, FR-11, FR-14

### Technical Requirements
- TR-052-01: Create `Vacancy` JPA entity with audit fields (`createdBy`, `updatedAt`, `version`, `isArchived`).
- TR-052-02: Implement `VacancyController` with `@PreAuthorize` ownership checks.
- TR-052-03: Implement DTO validation (`@Valid`, custom weight total validator).

---

## 7. Implementation Flow

1. Recruiter submits vacancy creation payload.
2. Validate fields and verify weights total 100.
3. Save vacancy entity associated with current user identity.
4. Trigger initial candidate retrieval and ranking calculation.
5. Return created vacancy with initial ranking snapshot reference.

---

## 8. Acceptance Criteria

- **AC-01:** Recruiter creates vacancy with title, skills, experience, location, and weights.
- **AC-02:** All recruiters can view vacancies; non-creators are forbidden from editing (HTTP 403).
- **AC-03:** Archiving marks vacancy archived without deleting database records.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test covering vacancy CRUD lifecycle.
- Security test verifying non-creator edit rejection.

---

## 10. Deliverables

- Vacancy entity and repository
- VacancyController
- VacancyDTO schemas

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-020, ET-016
- **Downstream Tickets:** ET-022, ET-023, ET-027
- **Technical Risks & Mitigations:** Concurrent editing of same vacancy; mitigated by JPA `@Version` optimistic locking.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/21
- **Branch:** `feature/et-021-vacancy-management-rest-api`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
