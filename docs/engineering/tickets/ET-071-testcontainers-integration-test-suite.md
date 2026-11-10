# [ET-071] — Build Testcontainers Integration Test Harness

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-071 |
| **Title** | Build Testcontainers Integration Test Harness |
| **Project** | eTalent Search |
| **Workstream** | H. Testing and Release |
| **Ticket Type** | Testing |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | QA Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Foundation, Architecture |
| **GitHub Labels** | stream:qa, type:test, priority:must, role:tester |

---

## 2. Objective

Build comprehensive integration test harness using Testcontainers for PostgreSQL 16 + pgvector, validating database operations and migrations.

---

## 3. Background and Context

Specification v1.0 Section 5: Testing requires JUnit 5, Testcontainers against real PostgreSQL+pgvector (no in-memory stand-in). Flyway migrations and vector operations must run against real database containers in all tests.

---

## 4. User Story / Engineering Story

> As a QA engineer, we need a reusable Testcontainers test harness, so that all backend integration tests run against real PostgreSQL with pgvector.

---

## 5. Scope

### In Scope
- Abstract base class `BaseIntegrationTest` managing singleton `pgvector/pgvector:pg16` Testcontainer.
- DynamicPropertySource configuring Spring Boot datasource properties from running container.
- Test data seeding utilities loading synthetic candidate and vacancy JSON fixtures.
- Fast container reuse across test classes to minimize test execution time.

### Out of Scope
- End-to-end browser testing (handled in ET-077)

### Constraints
- No in-memory databases (H2 strictly prohibited).
- Container must reuse across test classes.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation, Architecture

### Technical Requirements
- TR-071-01: Implement `PostgreSqlVectorContainer` using Testcontainers Java API.
- TR-071-02: Annotate base test class with `@Testcontainers` and configure dynamic properties.
- TR-071-03: Implement `FixtureDataLoader` populating test fixtures.

---

## 7. Implementation Flow

1. Testcontainers initializes `pgvector/pgvector:pg16` Docker container.
2. Flyway executes all migrations on clean database.
3. Spring application context boots with container JDBC URL.
4. Integration tests execute against real pgvector instance.
5. Container is cleaned up or reused for subsequent test suites.

---

## 8. Acceptance Criteria

- **AC-01:** Integration tests run against real PostgreSQL+pgvector container without requiring pre-installed database.
- **AC-02:** Container initializes once and reuses across test classes, keeping total suite under 3 minutes.
- **AC-03:** Vector extension, Flyway migrations, and JPA repositories operate seamlessly.

---

## 9. Testing Requirements

### Required Test Coverage
- Test suite execution verifying container spin-up and clean execution.
- Test verifying clean database state between test methods.

---

## 10. Deliverables

- BaseIntegrationTest class
- PostgreSqlVectorContainer definition
- FixtureDataLoader utility

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-033, ET-035
- **Downstream Tickets:** ET-073, ET-074
- **Technical Risks & Mitigations:** Slow container startup times; mitigated by singleton container pattern and container reuse.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/40
- **Branch:** `feature/et-071-testcontainers-integration-test-suite`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
