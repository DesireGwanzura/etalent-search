# [ET-055] — Implement Admin User Management and System Defaults API

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-055 |
| **Title** | Implement Admin User Management and System Defaults API |
| **Project** | eTalent Search |
| **Workstream** | F. Backend and Security |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-8, FR-14, Admin Rules |
| **GitHub Labels** | stream:backend, type:feature, priority:must, role:developer |

---

## 2. Objective

Build admin endpoints to manage user accounts, change system default factor weights, and view system health.

---

## 3. Background and Context

Specification v1.0 Section 3, 4: Admins manage user accounts (no self-registration), change system default factor weights, trigger data load, and view audit logs.

---

## 4. User Story / Engineering Story

> As an administrator, I want API endpoints to manage users and update default factor weights, so that system configuration and user access are securely administered.

---

## 5. Scope

### In Scope
- Endpoints: `GET /api/admin/users`, `POST /api/admin/users`, `PUT /api/admin/users/{id}/status` (activate/deactivate).
- Endpoints: `GET /api/admin/settings/weights` and `PUT /api/admin/settings/weights` (update system defaults).
- Validation: Default weights must sum to 100.
- Security: Restricted to `ROLE_ADMIN` using `@PreAuthorize("hasRole('ADMIN')")`.

### Out of Scope
- Self-service password reset (handled via admin reset)

### Constraints
- Admins cannot delete their own active admin account.
- Weights must sum to 100.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-8, FR-14, Admin Rules

### Technical Requirements
- TR-055-01: Implement `AdminUserController` for user provisioning.
- TR-055-02: Create `system_settings` table storing default weights.
- TR-055-03: Implement `AdminSettingsController` with weight validation.

---

## 7. Implementation Flow

1. Admin submits new user details (username, temporary password, role).
2. BCrypt hash password and save user account.
3. Admin updates default weights; validate total = 100.
4. Save new default weights in system settings.
5. Future vacancies initialize with new default weights.

---

## 8. Acceptance Criteria

- **AC-01:** Admin can create recruiter and admin accounts; self-registration is impossible.
- **AC-02:** Admin can update system default weights, and new vacancies inherit updated defaults.
- **AC-03:** Non-admin users are strictly denied access (HTTP 403 Forbidden).

---

## 9. Testing Requirements

### Required Test Coverage
- Security test verifying only admin can reach user management endpoints.
- Integration test verifying newly created vacancy inherits updated default weights.

---

## 10. Deliverables

- AdminUserController
- AdminSettingsController
- SystemSettings entity

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-051
- **Downstream Tickets:** ET-063
- **Technical Risks & Mitigations:** Locking out all admin users; mitigated by Flyway baseline seeding default admin account.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/24
- **Branch:** `feature/et-055-admin-user-management-system-settings`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
