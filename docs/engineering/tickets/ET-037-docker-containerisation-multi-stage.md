---
ticket_id: ET-037
title: Build Multi-Stage Dockerfile and Container Packaging
publish: approval
priority: must
type: task
workstream: devops
owner_role: devops
---

# [ET-037] — Build Multi-Stage Dockerfile and Container Packaging

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-037 |
| **Title** | Build Multi-Stage Dockerfile and Container Packaging |
| **Project** | eTalent Search |
| **Workstream** | B. Infrastructure and DevOps |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | DevOps Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Architecture, Deployment |

---

## 2. Objective

Create optimized multi-stage Dockerfile packaging the Java 21 Spring Boot runtime and compiled Angular SPA into a secure container image.

---

## 3. Background and Context

Specification v1.0 Section 5: Spring Boot serves the built Angular bundle in Release 1 (one deployable). A production container image is required for deployment to cloud container instances.

---

## 4. User Story / Engineering Story

> As a DevOps engineer, we need a secure multi-stage Dockerfile, so that eTalent Search is packaged into an efficient, production-ready container image.

---

## 5. Scope

### In Scope
- Stage 1 (Frontend): Node 20 LTS building Angular SPA.
- Stage 2 (Backend): Eclipse Temurin Java 21 building Spring Boot jar with frontend assets.
- Stage 3 (Runtime): Minimal Eclipse Temurin Java 21 JRE Alpine/Distroless image running as non-root user.
- `docker-compose.yml` for local development spinning up application and PostgreSQL+pgvector.
- Container vulnerability scanning with Trivy.

### Out of Scope
- Kubernetes Helm chart development

### Constraints
- Container must run as non-root user.
- Image size target < 300MB.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Architecture, Deployment

### Technical Requirements
- TR-068-01: Write `Dockerfile` with 3-stage build (node -> gradle -> eclipse-temurin-jre).
- TR-068-02: Create `docker-compose.yml` including `pgvector/pgvector:pg16`.
- TR-068-03: Enforce `USER appuser` non-root execution in runtime container.

---

## 7. Implementation Flow

1. Node stage installs dependencies and compiles Angular SPA.
2. Gradle stage copies compiled SPA into static resources and builds fat jar.
3. Runtime stage copies jar, configures non-root user, and exposes port 8080.
4. Container starts with JVM container-aware memory flags (`-XX:+UseContainerSupport`).

---

## 8. Acceptance Criteria

- **AC-01:** Docker image builds cleanly and passes container vulnerability scan.
- **AC-02:** Container runs as unprivileged non-root user.
- **AC-03:** `docker-compose up` boots full working system (app + PostgreSQL/pgvector).

---

## 9. Testing Requirements

### Required Test Coverage
- Container smoke test verifying health endpoint `http://localhost:8080/actuator/health` returns UP.
- Vulnerability scan verifying zero CRITICAL CVEs in base image.

---

## 10. Deliverables

- Dockerfile
- docker-compose.yml
- .dockerignore

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-001, ET-026
- **Downstream Tickets:** ET-039
- **Technical Risks & Mitigations:** Large container image size; mitigated by multi-stage build and minimal JRE base image.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/37
- **Branch:** `feature/et-037-docker-containerisation-multi-stage`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
