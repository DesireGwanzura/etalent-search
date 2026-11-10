---
ticket_id: ET-032
title: Build Admin Console for User Accounts, Sync, and Defaults
publish: approval
priority: must
type: feature
workstream: frontend
owner_role: developer
---

# [ET-032] — Build Admin Console for User Accounts, Sync, and Defaults

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-032 |
| **Title** | Build Admin Console for User Accounts, Sync, and Defaults |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-7, FR-8, FR-14, Admin Rules |

---

## 2. Objective

Build the Angular Admin Console providing user account management, candidate sync trigger and status view, and default weight configuration.

---

## 3. Background and Context

Specification v1.0 Section 3, 4: Admin role manages user accounts, triggers data load, changes default weights, and views load status and audit logs.

---

## 4. User Story / Engineering Story

> As an administrator, I want an admin console, so that I can provision user accounts, monitor candidate synchronization, and configure system default weights.

---

## 5. Scope

### In Scope
- User Management Tab: List users, create new recruiter/admin account, activate/deactivate accounts.
- Sync Management Tab: View last sync status, timestamp, record counts, error logs, and 'Trigger Sync Now' button.
- System Settings Tab: Configure system default factor weights with validation enforcing total = 100.
- Audit Log Viewer Tab: Search and filter audit log events.
- Route guard `AdminGuard` preventing non-admin access to admin routes.

### Out of Scope
- Billing or cloud infrastructure management

### Constraints
- Accessible only to users with `ROLE_ADMIN`.
- Responsive administration interface.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7, FR-8, FR-14, Admin Rules

### Technical Requirements
- TR-063-01: Create `AdminConsoleComponent` with child tabs for users, sync, settings, and audit.
- TR-063-02: Implement `AdminGuard` checking `authService.currentUser.role === 'ADMIN'`.
- TR-063-03: Connect components to admin REST API endpoints.

---

## 7. Implementation Flow

1. Admin user signs in and clicks 'Admin Console' in navigation bar.
2. AdminGuard verifies role; non-admins redirected with notification.
3. Admin creates new recruiter account or triggers manual data sync.
4. Sync status card updates in real time showing progress.
5. Admin adjusts default weights and saves changes.

---

## 8. Acceptance Criteria

- **AC-01:** Admin can create user accounts with RECRUITER or ADMIN roles.
- **AC-02:** Admin can trigger candidate sync and view last run metrics and errors.
- **AC-03:** Admin can update system default weights, validating sum == 100.
- **AC-04:** Non-admin users cannot access admin console routes.

---

## 9. Testing Requirements

### Required Test Coverage
- Angular route guard unit test verifying non-admin access blocked.
- Component unit tests for user creation form and sync trigger button.

---

## 10. Deliverables

- AdminConsoleComponent
- AdminGuard
- SyncStatusComponent
- Admin styles

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-009, ET-024, ET-025, ET-026
- **Downstream Tickets:** ET-033
- **Technical Risks & Mitigations:** Accidental double-clicking sync trigger; mitigated by disabling trigger button while sync is running.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/32
- **Branch:** `feature/et-032-angular-admin-console-sync-weights`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
