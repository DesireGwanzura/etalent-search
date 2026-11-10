# [ET-065] — Establish GitLab CI/CD Pipeline Configuration

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-065 |
| **Title** | Establish GitLab CI/CD Pipeline Configuration |
| **Project** | eTalent Search |
| **Workstream** | B. Infrastructure and DevOps |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | DevOps Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Foundation, Architecture |
| **GitHub Labels** | stream:devops, type:infrastructure, priority:must, role:devops |

---

## 2. Objective

Build `.gitlab-ci.yml` pipeline with stages for build, test (with Docker-in-Docker for Testcontainers), code quality, and artifact packaging.

---

## 3. Background and Context

Specification v1.0 Section 5: Testing and tooling requires JUnit 5, Testcontainers against real PostgreSQL+pgvector, and CI running `./gradlew build` and Angular build on every PR. The hybrid model uses GitLab for CI execution.

---

## 4. User Story / Engineering Story

> As an engineering team, we need a robust GitLab CI/CD pipeline, so that every commit is automatically validated with full builds and real Testcontainers tests.

---

## 5. Scope

### In Scope
- GitLab CI pipeline stages: `build`, `test`, `quality`, `package`.
- Gradle caching (`.gradle/caches`) and npm caching (`frontend/node_modules`).
- Docker-in-Docker (`dind`) service configuration enabling Testcontainers execution.
- Execution of `./gradlew check` and Angular test/build suites.
- Publishing JUnit test reports and pipeline status back to GitHub commit.

### Out of Scope
- Production Kubernetes deployment (deferred)

### Constraints
- Must support Testcontainers with real Docker daemon.
- Pipeline runtime under 10 minutes.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation, Architecture

### Technical Requirements
- TR-065-01: Create `.gitlab-ci.yml` with stages: `build`, `test`, `quality`, `package`.
- TR-065-02: Configure `services: [docker:dind]` and `DOCKER_HOST` for Testcontainers.
- TR-065-03: Configure GitHub commit status updater reporting pipeline results to GitHub.

---

## 7. Implementation Flow

1. Git commit pushed to GitHub; mirrored to GitLab.
2. GitLab CI pipeline triggers `build` stage compiling Java and TypeScript.
3. `test` stage executes JUnit tests with Testcontainers PostgreSQL+pgvector.
4. `quality` stage runs Spotless formatting and SonarQube checks.
5. Pipeline reports pass/fail status back to GitHub commit.

---

## 8. Acceptance Criteria

- **AC-01:** GitLab CI pipeline builds both backend and frontend successfully.
- **AC-02:** Testcontainers integration tests execute and pass within Docker-in-Docker.
- **AC-03:** Pipeline status is reported back to GitHub pull request.

---

## 9. Testing Requirements

### Required Test Coverage
- Pipeline validation run on test branch verifying all stages succeed.
- Deliberate test failure run verifying pipeline fails and reports failure to GitHub.

---

## 10. Deliverables

- .gitlab-ci.yml configuration
- GitLab CI documentation in docs/engineering/

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-032, ET-033, ET-057
- **Downstream Tickets:** ET-066, ET-067, ET-068, ET-069
- **Technical Risks & Mitigations:** Testcontainers failing to connect to Docker daemon in CI; mitigated by explicit DOCKER_TLS_CERTDIR configuration.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/34
- **Branch:** `feature/et-065-gitlab-ci-cd-pipeline-setup`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
