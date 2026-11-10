# [ET-057] — Set Up Angular 17+ SPA and Spring Boot Bundle Integration

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-057 |
| **Title** | Set Up Angular 17+ SPA and Spring Boot Bundle Integration |
| **Project** | eTalent Search |
| **Workstream** | G. Frontend |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Foundation, Architecture |
| **GitHub Labels** | stream:frontend, type:infrastructure, priority:must, role:developer |

---

## 2. Objective

Scaffold the Angular 17+ standalone component single-page application and configure Gradle to bundle compiled static assets into Spring Boot.

---

## 3. Background and Context

Specification v1.0 Section 5: Angular SPA in its own folder, calling backend REST API. Spring Boot serves the built Angular bundle in Release 1 (one deployable); separate hosting remains possible.

---

## 4. User Story / Engineering Story

> As an engineering team, we need the Angular SPA project structure integrated with the Gradle build, so that a single executable Spring Boot jar serves the complete application.

---

## 5. Scope

### In Scope
- Angular 17+ project initialization in `frontend/` using standalone components.
- Configure Angular Router, HttpClient, and environment files (`environment.ts`).
- Configure Gradle task `processResources` to run `npm run build` and copy `dist/` into `src/main/resources/static`.
- Single deployable artifact verification (`./gradlew bootJar` contains Angular assets).

### Out of Scope
- Complex UI components (handled in subsequent tickets)
- SSR (Server-Side Rendering)

### Constraints
- Single deployable jar for Release 1.
- Standalone Angular components without NgModules.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation, Architecture

### Technical Requirements
- TR-057-01: Initialize Angular 17+ with CLI using standalone API and SCSS styling.
- TR-057-02: Add Gradle `com.github.node-gradle.node` plugin for Node/npm execution.
- TR-057-03: Configure Spring MVC resource handlers forwarding non-API routes to `index.html`.

---

## 7. Implementation Flow

1. Initialize Angular workspace under `frontend/`.
2. Configure Gradle build integration to trigger npm install and npm build.
3. Copy compiled static files to `build/resources/main/static/`.
4. Configure `SpaWebFilter` in Spring Boot to support HTML5 client-side routing.
5. Verify browsing to `http://localhost:8080/` serves the Angular app.

---

## 8. Acceptance Criteria

- **AC-01:** `./gradlew build` builds both backend and frontend, packaging Angular in the jar.
- **AC-02:** Spring Boot serves `index.html` on root and non-API routes.
- **AC-03:** Client-side routing operates without 404 errors on browser page refresh.

---

## 9. Testing Requirements

### Required Test Coverage
- Build test verifying compiled Angular files exist inside produced `bootJar`.
- E2E / mock test verifying `GET /` returns HTTP 200 with Angular root tag.

---

## 10. Deliverables

- Angular project structure in frontend/
- Gradle build integration
- SpaWebFilter class

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-032
- **Downstream Tickets:** ET-058, ET-059, ET-060, ET-061, ET-062, ET-063, ET-064
- **Technical Risks & Mitigations:** Node version discrepancies on developer machines; mitigated by Gradle node plugin auto-downloading Node 20 LTS.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/26
- **Branch:** `feature/et-057-angular-spa-project-setup`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
