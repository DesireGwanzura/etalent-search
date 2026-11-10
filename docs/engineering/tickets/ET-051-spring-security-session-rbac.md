# [ET-051] — Configure Spring Security, Session Cookies, and RBAC

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-051 |
| **Title** | Configure Spring Security, Session Cookies, and RBAC |
| **Project** | eTalent Search |
| **Workstream** | F. Backend and Security |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | DevOps Engineer |
| **Requirements Traceability** | FR-8, Security Rules |
| **GitHub Labels** | stream:backend, type:security, priority:must, role:developer |

---

## 2. Objective

Configure Spring Security with session cookies, CSRF protection, BCrypt password hashing, and RECRUITER / ADMIN roles.

---

## 3. Background and Context

Specification v1.0 Section 3, 5, 8: Authentication is restored as Must. Uses Spring Security, session cookies (httpOnly, SameSite=Strict), CSRF protection enabled, BCrypt password hashes, roles RECRUITER and ADMIN, session timeout, and no self-registration.

---

## 4. User Story / Engineering Story

> As an administrator and recruiter, I want secure authentication with role-based access control, so that candidate data and management operations are protected from unauthorized access.

---

## 5. Scope

### In Scope
- Spring Security 6+ filter chain with session authentication.
- Session cookies: `httpOnly=true`, `SameSite=Strict`, `Secure=auto` (enforced in prod).
- CSRF protection enabled with `CookieCsrfTokenRepository.withHttpOnlyFalse()`.
- BCrypt password encoder (strength 12).
- Roles: `ROLE_RECRUITER` and `ROLE_ADMIN`.
- Session timeout: 30 minutes of inactivity.
- REST authentication endpoints: `POST /api/auth/login`, `POST /api/auth/logout`, `GET /api/auth/me`.

### Out of Scope
- OAuth2 / Company SSO (deferred post-Release 1)
- Public registration

### Constraints
- No self-registration; accounts created by admin only.
- All candidate endpoints require authentication.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-8, Security Rules

### Technical Requirements
- TR-051-01: Configure `SecurityFilterChain` with method security `@EnableMethodSecurity`.
- TR-051-02: Configure CSRF token repository and session cookie attributes.
- TR-051-03: Implement `CustomUserDetailsService` loading users from PostgreSQL.

---

## 7. Implementation Flow

1. User submits credentials to `/api/auth/login`.
2. AuthenticationManager validates credentials with BCrypt.
3. Establish SecurityContext in HttpSession and return session cookie + CSRF token.
4. Subsequent requests validate session cookie and CSRF header.
5. User signs out via `/api/auth/logout`, invalidating session.

---

## 8. Acceptance Criteria

- **AC-01:** Unauthenticated requests to `/api/*` (except auth) return HTTP 401 Unauthorized.
- **AC-02:** Session cookie is issued with `httpOnly=true` and `SameSite=Strict`.
- **AC-03:** CSRF token is required on state-mutating requests (POST, PUT, DELETE).
- **AC-04:** Recruiter cannot access admin endpoints (`/api/admin/**`); returns HTTP 403 Forbidden.

---

## 9. Testing Requirements

### Required Test Coverage
- Security integration tests testing login, logout, invalid credentials, and session timeout.
- Authorization tests verifying role restrictions on admin and recruiter routes.

---

## 10. Deliverables

- SecurityConfiguration class
- AuthController
- User entity and repository
- Flyway user migration

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-032, ET-033
- **Downstream Tickets:** ET-052, ET-053, ET-054, ET-055, ET-056
- **Technical Risks & Mitigations:** CSRF token mismatch with Angular SPA; mitigated by standard `XSRF-TOKEN` cookie convention.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/20
- **Branch:** `feature/et-051-spring-security-session-rbac`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
