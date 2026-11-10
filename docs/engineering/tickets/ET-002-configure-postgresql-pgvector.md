---
ticket_id: ET-002
title: Configure PostgreSQL and pgvector Database Extension
publish: approval
priority: must
type: task
workstream: foundation
owner_role: developer
---

# [ET-002] — Configure PostgreSQL and pgvector Database Extension

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-002 |
| **Title** | Configure PostgreSQL and pgvector Database Extension |
| **Project** | eTalent Search |
| **Workstream** | A. Foundation & Architecture |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | DevOps Engineer |
| **Requirements Traceability** | Foundation, FR-2, FR-7 |

---

## 2. Objective

Configure PostgreSQL database with the pgvector extension and Flyway migrations for schema management and Testcontainers validation.

---

## 3. Background and Context

Specification v1.0 specifies PostgreSQL with pgvector inside the same database instance for candidate profiles, embeddings, and ranking snapshots. Real Testcontainers with pgvector are mandated (in-memory databases prohibited).

---

## 4. User Story / Engineering Story

> As an engineering team, we need PostgreSQL with pgvector initialized via Flyway, so that relational data and high-dimensional vector embeddings are stored transactionally.

---

## 5. Scope

### In Scope
- Flyway baseline migration script enabling `CREATE EXTENSION IF NOT EXISTS vector;`.
- Spring Data JPA configuration supporting pgvector column types.
- Testcontainers setup spinning up `pgvector/pgvector:pg16` for automated test execution.
- Base entity schema definitions for candidates, vacancies, and snapshots.

### Out of Scope
- Candidate parsing logic
- LLM evaluation calls

### Constraints
- PostgreSQL 16+ with pgvector 0.5.0+.
- In-memory database (H2/HSQLDB) strictly prohibited.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation, FR-2, FR-7

### Technical Requirements
- TR-033-01: Add Flyway migration `V1__init_pgvector.sql` enabling vector extension.
- TR-033-02: Integrate `com.pgvector:pgvector` Java library for JDBC vector type mapping.
- TR-033-03: Create base Testcontainers configuration class `@Container PostgreSQLContainer` using `pgvector/pgvector:pg16`.

---

## 7. Implementation Flow

1. Add Flyway and PostgreSQL dependencies to `build.gradle`.
2. Write Flyway migration `V1__init_schema.sql` enabling extension `vector`.
3. Configure `application.yml` for PostgreSQL datasource and Flyway lifecycle.
4. Implement abstract `BaseIntegrationTest` using Testcontainers.
5. Execute migration validation test verifying vector extension activation.

---

## 8. Acceptance Criteria

- **AC-01:** Flyway runs successfully on application startup, enabling `vector` extension.
- **AC-02:** Testcontainers initializes real `pgvector/pgvector
- **AC-03:** Vector table column with dimension 1536/768 can be created and queried using cosine distance (`<=>`).

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test verifying database connection and `vector` extension presence via `SELECT extname FROM pg_extension`.
- Integration test storing and retrieving test vector with cosine distance calculation.

---

## 10. Deliverables

- Flyway migration scripts
- Spring Data JPA configuration
- Testcontainers test base class

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-001
- **Downstream Tickets:** ET-005, ET-013, ET-016, ET-020
- **Technical Risks & Mitigations:** pgvector Docker container availability in restricted CI environments; mitigated by pinned image.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/2
- **Branch:** `feature/et-002-configure-postgresql-pgvector`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
