# eTalent Search — Team Ownership & Role Allocation

**Standard:** Team Engineering Ticket Standard (TETS) v1.0  
**Team Size:** 7 Engineering Professionals  
**Project:** eTalent Search (v1.0)  

---

## 1. Team Composition & RACI Matrix

The eTalent Search engineering delivery team consists of seven distinct cross-functional roles:

| Role Identifier | Role Title | Headcount | Primary Responsibilities |
| :--- | :--- | :---: | :--- |
| **DEV-1** | Software Developer (Backend Lead) | 1 | Spring Boot architecture, PostgreSQL + Flyway, domain models, candidate ingestion pipeline, mass deletion guards |
| **DEV-2** | Software Developer (AI/Backend Integration) | 1 | AI service client integration, vector search integration, deterministic scoring arithmetic, caching & ranking snapshots |
| **DEV-3** | Software Developer (Full-Stack / Security) | 1 | Spring Security (session cookies, CSRF, BCrypt, RBAC), User & Vacancy REST APIs, Admin management endpoints |
| **DEV-4** | Software Developer (Frontend Lead) | 1 | Angular 17+ SPA application, components (Vacancy, Ranking, Candidate Profile, Shortlist, Admin), state management |
| **DEVOPS** | DevOps Engineer | 1 | CI/CD pipelines (GitLab CI & GitHub Actions), Docker containerization, PostgreSQL/pgvector environment setup, repository mirroring, secrets management |
| **AI-ENG** | AI Engineer | 1 | Embedding model selection & benchmarking, LLM prompt engineering for factor evaluation, JSON schema enforcement, privacy allowlist scrubbers, AI feasibility spike |
| **QA-ENG** | QA / Test Automation Engineer | 1 | Synthetic CV & vacancy test dataset generation, Testcontainers integration testing, ranking consistency suites, negative & security testing, E2E validation |

---

## 2. Workstream Allocation Matrix

| Workstream | Primary Suggested Owner | Secondary / Reviewer Roles |
| :--- | :--- | :--- |
| **A. Foundation & Architecture** | Software Developer / DevOps | AI Engineer, QA Engineer |
| **B. Infrastructure & DevOps** | DevOps Engineer | Software Developer, QA Engineer |
| **C. Candidate Data Ingestion** | Software Developer (Backend) | AI Engineer, QA Engineer |
| **D. AI & Semantic Evaluation** | AI Engineer | Software Developer (Backend), QA Engineer |
| **E. Scoring & Ranking Engine** | Software Developer (Backend) | AI Engineer, QA Engineer |
| **F. Backend & Security** | Software Developer (Security/API) | Software Developer (Backend), QA Engineer |
| **G. Frontend (Angular SPA)** | Software Developer (Frontend) | Software Developer (Backend), QA Engineer |
| **H. Testing, Release & Optional** | QA Engineer / Software Developer | DevOps Engineer, All Developers |

---

## 3. Code Review & Governance Principles

1. **Dual Approval Rule:** Every Pull Request into the integration branch (`dev`) requires approvals from at least **two** engineers other than the author.
2. **Cross-Disciplinary Reviews:**
   - AI and prompt changes (`stream:ai`) must be reviewed by both the **AI Engineer** and a **Software Developer**.
   - Security and authentication code (`stream:backend`) must be reviewed by a **Software Developer** and the **DevOps Engineer**.
   - Infrastructure, Docker, and CI configurations (`stream:devops`) must be reviewed by the **DevOps Engineer** and a **Software Developer**.
   - Database migrations and scoring logic (`stream:data`, `stream:backend`) must be reviewed by a **Software Developer** and the **QA Engineer**.
3. **No Named Human Assignments in Backlog:** All tickets use role designations (`Suggested Owner: Software Developer`, `Suggested Reviewer: AI Engineer`) to ensure sustainable maintenance, team flexibility, and clean onboarding.
