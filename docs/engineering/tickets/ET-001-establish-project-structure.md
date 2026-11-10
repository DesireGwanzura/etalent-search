---
ticket_id: ET-001
title: Establish Project Structure and Gradle Wrapper
publish: approval
priority: must
type: task
workstream: foundation
owner_role: developer
---

# [ET-001] — Establish Project Structure and Gradle Wrapper

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-001 |
| **Title** | Establish Project Structure and Gradle Wrapper |
| **Project** | eTalent Search |
| **Workstream** | A. Foundation & Architecture |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | DevOps Engineer |
| **Requirements Traceability** | Foundation (FR-1 to FR-8, FR-14) |

---

## 2. Objective

Scaffold the Java 21 / Spring Boot 4.1.2 project repository layout using Gradle Wrapper and domain-driven modular package architecture.

---

## 3. Background and Context

Project Specification v1.0 mandates Java 21, Spring Boot 4.1.2, Gradle wrapper (never Maven), and domain modular packaging with Spring Boot serving the compiled Angular SPA in Release 1. Aligned with eTalent Search Project Specification v1.0 (Java 21, Spring Boot 4.1.2, Gradle wrapper, and FR-1 through FR-8 fully valid with restored authentication).

---

## 4. User Story / Engineering Story

> As an engineering team, we need a standardized Spring Boot 4.1.2 Gradle multi-project repository structure, so that developers have a consistent, reproducible build baseline.

---

## 5. Scope

### In Scope
- Initialize Gradle wrapper with Gradle 8.8+ configured for Java 21 toolchain.
- Scaffold domain packages: `security`, `vacancy`, `candidate`, `ai`, `scoring`, `admin`, `common`.
- Configure root and subproject `build.gradle` with strict dependency management.
- Establish static analysis and formatting plugins (Spotless, Checkstyle).

### Out of Scope
- Application business logic implementation
- Frontend Angular components (handled in ET-057)

### Constraints
- Must use Gradle Wrapper; Maven is explicitly prohibited.
- Must target Java 21 LTS and Spring Boot 4.1.2.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation (FR-1 to FR-8, FR-14)

### Technical Requirements
- TR-032-01: Configure `gradle-wrapper.properties` with Gradle 8.8+ and SHA-256 verification.
- TR-032-02: Configure `java { toolchain { languageVersion = JavaLanguageVersion.of(21) } }` in `build.gradle`.
- TR-032-03: Setup Spotless Gradle plugin enforcing Google Java Format.
- TR-032-04: Define domain package boundaries avoiding circular package dependencies.

---

## 7. Implementation Flow

1. Initialize Gradle project with `gradle wrapper --gradle-version 8.8`.
2. Define root `build.gradle` with Spring Boot 4.1.2 plugin and dependency management.
3. Create domain directory structure under `src/main/java/com/etalent/search/`.
4. Configure code style and quality validation tasks (`spotlessCheck`, `checkstyleMain`).
5. Verify clean build execution via `./gradlew clean build`.

---

## 8. Acceptance Criteria

- **AC-01:** `./gradlew clean build` succeeds on a clean environment with Java 21.
- **AC-02:** Package structure contains all domain packages (`security`, `vacancy`, `candidate`, `ai`, `scoring`, `admin`, `common`).
- **AC-03:** Code formatting check `./gradlew spotlessCheck` passes and enforces Google Java Format.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit test verifying Spring Boot application context loads (`@SpringBootTest`).
- ArchUnit architecture test verifying modular package dependencies have no cycles.

---

## 10. Deliverables

- Gradle build configuration (`build.gradle`, `settings.gradle`, `gradle/`)
- Domain directory scaffolding
- Base Application class

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** None (Foundation ticket)
- **Downstream Tickets:** ET-002, ET-003, ET-020, ET-034
- **Technical Risks & Mitigations:** Java 21 toolchain mismatch across developer machines; mitigated by Gradle toolchain auto-provisioning.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/1
- **Branch:** `feature/et-001-establish-project-structure`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
