# Team Engineering Ticket Standard (TETS) v1.0

**Project:** eTalent Search  
**Format:** GitHub + GitLab Issues & Version-Controlled Markdown  
**Detail Level:** Balanced (Engineering Audience)  
**Standard Version:** 1.0  
**Effective Date:** 10 November 2026  

---

## 1. Overview & Core Principles

The Team Engineering Ticket Standard (TETS) v1.0 establishes an authoritative, reproducible standard for defining, tracking, implementing, reviewing, and verifying engineering work across the eTalent Search project.

### Core Principles
1. **Clear Engineering Objective:** Every ticket defines a specific problem, technical or functional capability, and business or engineering rationale.
2. **Context & Traceability:** Functional features trace directly to Project Specification v1.0 requirements (`FR-1` to `FR-15`). Technical tasks trace to architecture decisions (`TR-xxx`).
3. **Appropriate Framing:** User-facing capabilities use formal User Stories (`US-xxx`). Internal backend, infrastructure, AI pipeline, and DevOps work use Engineering Objectives.
4. **Independently Verifiable Acceptance Criteria:** Criteria (`AC-xxx`) use concrete, testable conditions (Given/When/Then or testable assertions). Vague assertions like "works properly" or "is secure" are forbidden.
5. **Rigorous Quality Verification:** Every ticket defines explicit unit, integration, negative, security, or performance test cases (`TC-xxx`).
6. **Strict Definition of Done (DoD):** Implementation is complete only when code is reviewed by 2 engineers, automated CI passes, tests succeed, documentation is synchronized, and traceable PR links are provided.
7. **Privacy by Design:** Strict adherence to POPIA boundaries. Synthetic candidate data is mandated until legal approval (`R1`) is cleared. Personal identifiable information (PII) must never be sent in AI payloads or committed to Git.

---

## 2. Team Structure & Role Ownership

Work is distributed across a seven-member cross-functional engineering team:

| Role Title | Count | Core Responsibilities in eTalent Search |
| :--- | :---: | :--- |
| **Software Developer (Backend / Full-Stack)** | 4 | Spring Boot 4.1.2 REST APIs, domain services, security, Angular 17+ SPA components, data loaders, PostgreSQL/pgvector integration |
| **DevOps Engineer** | 1 | CI/CD pipelines (GitLab/GitHub Actions), containerisation (Docker, OCI), environment provisioning, mirror sync, automated quality gates |
| **AI Engineer** | 1 | Semantic retrieval, embedding models, LLM structured evaluation prompts, prompt-injection defense, privacy allowlist scrubbers, AI feasibility spike |
| **Tester / QA Engineer** | 1 | Test automation (Testcontainers, JUnit 5, Cypress/Playwright), ranking consistency checks, negative & boundary test suites, test datasets |

*Note:* Ownership is assigned by professional role (e.g., `Suggested Owner: Software Developer`, `Suggested Reviewer: AI Engineer`). Named employee credentials or GitHub usernames are not hardcoded.

---

## 3. Ticket Classification & Structure

Every ticket belongs to one of seven formal types:

| Ticket Type | Description | Story Format |
| :--- | :--- | :--- |
| **Feature** | User-facing functionality or product capability | User Story (`US-xxx`) |
| **Technical Task** | Architecture, data modeling, backend services, security, infrastructure | Engineering Objective |
| **Research / Spike** | Feasibility investigation, benchmarking, model evaluation | Research Questions (`RQ-xxx`) |
| **Testing** | Dedicated test harness, synthetic test datasets, consistency validation | Test Scope & Test Cases (`TC-xxx`) |
| **Documentation** | Architectural guides, runbooks, engineering standards | Documentation Scope |
| **Refactoring** | Internal architecture improvements preserving external behavior | Engineering Benefit |
| **Bug** | Correction of an observed defect or broken behavior | Defect & Reproduction Steps |

---

## 4. Priority Definitions

- **priority:must (Critical / High):** Core release 1 deliverables mandated by Specification v1.0 (`FR-1` to `FR-8`, `FR-14`). Required for system launch.
- **priority:should (Medium):** High-value capabilities (`FR-9` location/availability filters, `FR-10` edit & re-rank, `FR-11` reopen/archive past vacancies, `FR-15` save shortlist). Cut in reverse order if time runs short.
- **priority:nice (Low):** Optional enhancements (`FR-12` mark not relevant, `FR-13` CSV export). Dropped first if schedule tightens.

---

## 5. Delivery Workflow & Traceability

The team operates a hybrid GitHub/GitLab delivery model:
- **GitHub:** Single source of truth for issue tracking, specifications, PRs, code reviews, and status tracking.
- **GitLab:** CI/CD execution engine for automated builds, Testcontainers suites, security scanning, and container packaging.

### Branch & PR Conventions
- **Feature Branch:** `feature/ET-XXX-short-description`
- **Bugfix Branch:** `bugfix/ET-XXX-short-description`
- **Technical Task:** `task/ET-XXX-short-description`
- **Commit Message:** `ET-XXX: Concise description of change`
- **Pull Request Title:** `[ET-XXX] Concise description of change`
- **PR Description:** Must reference issue (e.g., `Refs #42` during dev; `Closes #42` on release promotion).
