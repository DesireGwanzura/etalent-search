# [ET-064] — Build Authentication Login Screen and Application Shell

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-064 |
| **Title** | Build Authentication Login Screen and Application Shell |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-8 |
| **GitHub Labels** | stream:frontend, type:security, priority:must, role:developer |

---

## 2. Objective

Build the Angular login screen, authentication interceptor, application navigation header, and session timeout management.

---

## 3. Background and Context

Specification v1.0 FR-8: Users sign in; only authenticated users see any candidate data; recruiters and admins have specified permissions; access is logged with user identity.

---

## 4. User Story / Engineering Story

> As a user, I want a secure login screen and navigation header, so that I can sign in, navigate features according to my role, and securely sign out.

---

## 5. Scope

### In Scope
- Login page component with username and password inputs and error display.
- HTTP Interceptor managing CSRF tokens and handling HTTP 401/403 responses.
- Navigation header with branding, active vacancy links, Admin link (admins only), user profile badge, and sign-out button.
- Session expiration handler redirecting to login upon session timeout.
- Auth guard protecting all candidate and vacancy routes.

### Out of Scope
- Social login or self-service password reset

### Constraints
- No candidate data displayed before successful authentication.
- Session cookie security.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-8

### Technical Requirements
- TR-064-01: Create `LoginComponent` and `AppHeaderComponent`.
- TR-064-02: Implement `AuthInterceptor` attaching `X-XSRF-TOKEN` and intercepting 401/403.
- TR-064-03: Implement `AuthGuard` redirecting unauthenticated users to `/login`.

---

## 7. Implementation Flow

1. Unauthenticated user visits app; AuthGuard redirects to `/login`.
2. User enters credentials; `AuthService` calls `POST /api/auth/login`.
3. Upon 200 OK, store user session state and redirect to dashboard.
4. AppHeader displays user name, role badge, and permitted navigation links.
5. User clicks 'Sign Out'; call `/api/auth/logout` and clear client state.

---

## 8. Acceptance Criteria

- **AC-01:** Login form validates credentials and authenticates with backend.
- **AC-02:** Navigation header adapts to user role, displaying admin links only to admins.
- **AC-03:** Session timeout or 401 response smoothly redirects to login with informative message.

---

## 9. Testing Requirements

### Required Test Coverage
- Auth guard and HTTP interceptor unit tests.
- Component unit tests verifying login form validation and error handling.

---

## 10. Deliverables

- LoginComponent
- AppHeaderComponent
- AuthInterceptor
- AuthGuard

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-051, ET-057
- **Downstream Tickets:** ET-058, ET-059, ET-063
- **Technical Risks & Mitigations:** Session expiration silently dropping unsaved recruiter work; mitigated by session warning modal.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/33
- **Branch:** `feature/et-064-angular-auth-navigation-shell`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
