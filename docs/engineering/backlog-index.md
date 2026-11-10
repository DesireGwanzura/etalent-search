# eTalent Search — Complete Engineering Backlog Index

**Standard:** Team Engineering Ticket Standard (TETS) v1.0  
**Project:** eTalent Search  
**Authoritative Specification:** eTalent Search Project Specification v1.0  
**Repository:** [DesireGwanzura/etalent-search](https://github.com/DesireGwanzura/etalent-search)  
**Total Published Issues:** 47 (`ET-001` to `ET-047`, synchronized 1-to-1 with GitHub Issues #1 to #47)  

---

## 1. Executive Summary & Distribution

### Priority Distribution
- **priority:must (Must):** 39 tickets (Core Release 1 deliverables: FR-1 to FR-8, FR-14, Architecture, DevOps, Security, AI Spike)
- **priority:should (Should):** 6 tickets (FR-9 Filters, FR-10 Edit/Re-rank, FR-11 Past Vacancies/Archive, FR-15 Shortlist, Reprocessing trigger)
- **priority:nice (Nice):** 2 tickets (FR-12 Mark Not Relevant, FR-13 CSV Shortlist Export)
- **Total Backlog Tickets:** **47**

### Workstream Distribution
- **A. Foundation and Architecture:** 4 tickets (`ET-001` – `ET-004`)
- **C. Candidate Data Ingestion:** 6 tickets (`ET-005` – `ET-010`)
- **D. AI and Semantic Evaluation:** 5 tickets (`ET-011` – `ET-015`)
- **E. Scoring and Ranking Engine:** 4 tickets (`ET-016` – `ET-019`)
- **F. Backend and Security:** 6 tickets (`ET-020` – `ET-025`)
- **G. Frontend (Angular SPA):** 8 tickets (`ET-026` – `ET-033`)
- **B. Infrastructure and DevOps:** 6 tickets (`ET-034` – `ET-039`)
- **H. Testing, Release & Optional:** 8 tickets (`ET-040` – `ET-047`)

### Team Role Ownership Distribution (7-Person Engineering Team)
- **Software Developers (4 devs):** 36 tickets (Backend APIs, Domain Logic, Ingestion, Angular SPA, Security)
- **DevOps Engineer (1 devops):** 6 tickets (GitLab CI/CD, GitHub Actions, Docker, Rulesets, Scanners)
- **AI Engineer (1 ai):** 2 tickets (`ET-011` AI Spike, `ET-012` Structured Prompt Engineering) + Cross-cutting reviews
- **QA / Test Engineer (1 tester):** 5 tickets (`ET-004` Synthetic Datasets, `ET-040` Testcontainers, `ET-042` Consistency Tests, `ET-043` Adversarial Tests, `ET-047` E2E Readiness)

---

## 2. Complete Backlog Registry (Synchronized with GitHub Issues #1–#47)

| Ticket ID | Title | Workstream | Priority | Suggested Owner | Status | GitHub Issue Link |
| :--- | :--- | :--- | :---: | :--- | :---: | :--- |
| **ET-001** | Establish Project Structure and Gradle Wrapper | `Foundation` | `must` | `developer` | `Ready` | [#1](https://github.com/DesireGwanzura/etalent-search/issues/1) |
| **ET-002** | Configure PostgreSQL and pgvector Database Extension | `Foundation` | `must` | `developer` | `Ready` | [#2](https://github.com/DesireGwanzura/etalent-search/issues/2) |
| **ET-003** | Establish Pinned AI Provider and Embedding Interfaces | `Foundation` | `must` | `developer` | `Ready` | [#3](https://github.com/DesireGwanzura/etalent-search/issues/3) |
| **ET-004** | Implement Synthetic Candidate and Vacancy Dataset Generation | `Foundation` | `must` | `tester` | `Ready` | [#4](https://github.com/DesireGwanzura/etalent-search/issues/4) |
| **ET-005** | Implement External Candidate Source File Adapter | `Data` | `must` | `developer` | `Ready` | [#5](https://github.com/DesireGwanzura/etalent-search/issues/5) |
| **ET-006** | Build Privacy Redaction and Allowlist Scrubber | `Data` | `must` | `developer` | `Ready` | [#6](https://github.com/DesireGwanzura/etalent-search/issues/6) |
| **ET-007** | Implement CV AI Extraction and Embedding Generation | `Data` | `must` | `developer` | `Ready` | [#7](https://github.com/DesireGwanzura/etalent-search/issues/7) |
| **ET-008** | Implement Ingestion Synchronisation and Mass-Deletion Guard | `Data` | `must` | `developer` | `Ready` | [#8](https://github.com/DesireGwanzura/etalent-search/issues/8) |
| **ET-009** | Implement Sync Status Reporting and Audit Logging | `Data` | `must` | `developer` | `Ready` | [#9](https://github.com/DesireGwanzura/etalent-search/issues/9) |
| **ET-010** | Implement Model and Prompt Version Re-processing Trigger | `Data` | `should` | `developer` | `Ready` | [#10](https://github.com/DesireGwanzura/etalent-search/issues/10) |
| **ET-011** | Execute AI Feasibility Spike and Latency/Cost Benchmark | `Ai` | `must` | `ai` | `Ready` | [#11](https://github.com/DesireGwanzura/etalent-search/issues/11) |
| **ET-012** | Engineer Pinned LLM Prompts with Structured JSON Output | `Ai` | `must` | `ai` | `Ready` | [#12](https://github.com/DesireGwanzura/etalent-search/issues/12) |
| **ET-013** | Implement pgvector Semantic Retrieval and Hard Filtering | `Ai` | `must` | `developer` | `Ready` | [#13](https://github.com/DesireGwanzura/etalent-search/issues/13) |
| **ET-014** | Build Parallel AI Evaluation Orchestrator and Rate Limiting | `Ai` | `must` | `developer` | `Ready` | [#14](https://github.com/DesireGwanzura/etalent-search/issues/14) |
| **ET-015** | Implement AI Fallback Strategy and Degraded Mode | `Ai` | `must` | `developer` | `Ready` | [#15](https://github.com/DesireGwanzura/etalent-search/issues/15) |
| **ET-016** | Build Deterministic Factor Scoring Engine | `Scoring` | `must` | `developer` | `Ready` | [#16](https://github.com/DesireGwanzura/etalent-search/issues/16) |
| **ET-017** | Implement Tie-Breaking Logic and Instant Cached Re-ranking | `Scoring` | `must` | `developer` | `Ready` | [#17](https://github.com/DesireGwanzura/etalent-search/issues/17) |
| **ET-018** | Implement Reproducible Ranking Snapshot Persistence | `Scoring` | `must` | `developer` | `Ready` | [#18](https://github.com/DesireGwanzura/etalent-search/issues/18) |
| **ET-019** | Build Explanation Faithfulness and Evidence Validation | `Scoring` | `must` | `developer` | `Ready` | [#19](https://github.com/DesireGwanzura/etalent-search/issues/19) |
| **ET-020** | Configure Spring Security, Session Cookies, and RBAC | `Backend` | `must` | `developer` | `Ready` | [#20](https://github.com/DesireGwanzura/etalent-search/issues/20) |
| **ET-021** | Implement Vacancy Management REST API | `Backend` | `must` | `developer` | `Ready` | [#21](https://github.com/DesireGwanzura/etalent-search/issues/21) |
| **ET-022** | Implement Candidate Profile and Ranking Query REST API | `Backend` | `must` | `developer` | `Ready` | [#22](https://github.com/DesireGwanzura/etalent-search/issues/22) |
| **ET-023** | Implement Shortlist Management REST API | `Backend` | `should` | `developer` | `Ready` | [#23](https://github.com/DesireGwanzura/etalent-search/issues/23) |
| **ET-024** | Implement Admin User Management and System Defaults API | `Backend` | `must` | `developer` | `Ready` | [#24](https://github.com/DesireGwanzura/etalent-search/issues/24) |
| **ET-025** | Implement Comprehensive Audit Logging Interceptor | `Backend` | `must` | `developer` | `Ready` | [#25](https://github.com/DesireGwanzura/etalent-search/issues/25) |
| **ET-026** | Set Up Angular 17+ SPA and Spring Boot Bundle Integration | `Frontend` | `must` | `developer` | `Ready` | [#26](https://github.com/DesireGwanzura/etalent-search/issues/26) |
| **ET-027** | Build Vacancy Creation and Configurable Weights UI | `Frontend` | `must` | `developer` | `Ready` | [#27](https://github.com/DesireGwanzura/etalent-search/issues/27) |
| **ET-028** | Build Ranked Candidate Results List and Factor Explanations | `Frontend` | `must` | `developer` | `Ready` | [#28](https://github.com/DesireGwanzura/etalent-search/issues/28) |
| **ET-029** | Build Candidate Profile Inspection View | `Frontend` | `must` | `developer` | `Ready` | [#29](https://github.com/DesireGwanzura/etalent-search/issues/29) |
| **ET-030** | Build Shortlist Action and Dedicated Shortlist View | `Frontend` | `should` | `developer` | `Ready` | [#30](https://github.com/DesireGwanzura/etalent-search/issues/30) |
| **ET-031** | Build Past Vacancies Archive and Reopen UI | `Frontend` | `should` | `developer` | `Ready` | [#31](https://github.com/DesireGwanzura/etalent-search/issues/31) |
| **ET-032** | Build Admin Console for User Accounts, Sync, and Defaults | `Frontend` | `must` | `developer` | `Ready` | [#32](https://github.com/DesireGwanzura/etalent-search/issues/32) |
| **ET-033** | Build Authentication Login Screen and Application Shell | `Frontend` | `must` | `developer` | `Ready` | [#33](https://github.com/DesireGwanzura/etalent-search/issues/33) |
| **ET-034** | Establish GitLab CI/CD Pipeline Configuration | `Devops` | `must` | `devops` | `Ready` | [#34](https://github.com/DesireGwanzura/etalent-search/issues/34) |
| **ET-035** | Configure GitHub Actions PR Automation and Reviewer Assignment | `Devops` | `must` | `devops` | `Ready` | [#35](https://github.com/DesireGwanzura/etalent-search/issues/35) |
| **ET-036** | Implement GitHub to GitLab Mirroring and Webhook Sync | `Devops` | `must` | `devops` | `Ready` | [#36](https://github.com/DesireGwanzura/etalent-search/issues/36) |
| **ET-037** | Build Multi-Stage Dockerfile and Container Packaging | `Devops` | `must` | `devops` | `Ready` | [#37](https://github.com/DesireGwanzura/etalent-search/issues/37) |
| **ET-038** | Configure Static Analysis, SonarQube, and Secret Scanning | `Devops` | `must` | `devops` | `Ready` | [#38](https://github.com/DesireGwanzura/etalent-search/issues/38) |
| **ET-039** | Configure GitHub Rulesets and Release Promotion Workflow | `Devops` | `must` | `devops` | `Ready` | [#39](https://github.com/DesireGwanzura/etalent-search/issues/39) |
| **ET-040** | Build Testcontainers Integration Test Harness | `Qa` | `must` | `tester` | `Ready` | [#40](https://github.com/DesireGwanzura/etalent-search/issues/40) |
| **ET-041** | Establish POPIA Legal Compliance Gate and Synthetic Data Policy | `Qa` | `must` | `developer` | `Ready` | [#41](https://github.com/DesireGwanzura/etalent-search/issues/41) |
| **ET-042** | Build Ranking Consistency and Top-5 Overlap Test Suite | `Qa` | `must` | `tester` | `Ready` | [#42](https://github.com/DesireGwanzura/etalent-search/issues/42) |
| **ET-043** | Build Security and Adversarial Prompt-Injection Test Suite | `Qa` | `must` | `tester` | `Ready` | [#43](https://github.com/DesireGwanzura/etalent-search/issues/43) |
| **ET-044** | Implement Location and Availability Faceted Search Filters | `Qa` | `should` | `developer` | `Ready` | [#44](https://github.com/DesireGwanzura/etalent-search/issues/44) |
| **ET-045** | Implement Shortlist CSV Export Functionality | `Qa` | `nice` | `developer` | `Ready` | [#45](https://github.com/DesireGwanzura/etalent-search/issues/45) |
| **ET-046** | Implement Mark Candidate Not Relevant Action | `Qa` | `nice` | `developer` | `Ready` | [#46](https://github.com/DesireGwanzura/etalent-search/issues/46) |
| **ET-047** | Execute End-to-End System Testing and Release 1 Readiness Gate | `Qa` | `must` | `tester` | `Ready` | [#47](https://github.com/DesireGwanzura/etalent-search/issues/47) |

---

## 3. Specification Traceability Matrix (FR-1 to FR-15)

| Requirement ID | Specification Requirement | Priority | Implementing Ticket(s) |
| :--- | :--- | :---: | :--- |
| **FR-1** | Recruiter creates vacancy (title, skills, experience, location, remote) | Must | [`ET-021`](https://github.com/DesireGwanzura/etalent-search/issues/21), [`ET-027`](https://github.com/DesireGwanzura/etalent-search/issues/27) |
| **FR-2** | Semantic evaluation of candidates passing hard filters up to cap 100 | Must | [`ET-013`](https://github.com/DesireGwanzura/etalent-search/issues/13), [`ET-014`](https://github.com/DesireGwanzura/etalent-search/issues/14), [`ET-016`](https://github.com/DesireGwanzura/etalent-search/issues/16) |
| **FR-3** | Display sorted results by score with name, title, score, top reasons | Must | [`ET-017`](https://github.com/DesireGwanzura/etalent-search/issues/17), [`ET-022`](https://github.com/DesireGwanzura/etalent-search/issues/22), [`ET-028`](https://github.com/DesireGwanzura/etalent-search/issues/28) |
| **FR-4** | Plain-language AI factor explanations without numeric scores | Must | [`ET-012`](https://github.com/DesireGwanzura/etalent-search/issues/12), [`ET-016`](https://github.com/DesireGwanzura/etalent-search/issues/16), [`ET-019`](https://github.com/DesireGwanzura/etalent-search/issues/19) |
| **FR-5** | Recruiter opens full candidate profile from ranked list | Must | [`ET-022`](https://github.com/DesireGwanzura/etalent-search/issues/22), [`ET-029`](https://github.com/DesireGwanzura/etalent-search/issues/29) |
| **FR-6** | Reproducible ranking snapshots (same inputs = same stored ranking) | Must | [`ET-017`](https://github.com/DesireGwanzura/etalent-search/issues/17), [`ET-018`](https://github.com/DesireGwanzura/etalent-search/issues/18), [`ET-042`](https://github.com/DesireGwanzura/etalent-search/issues/42) |
| **FR-7** | Candidate ingestion pipeline (file adapter, scrub, embed, sync, guard) | Must | [`ET-005`](https://github.com/DesireGwanzura/etalent-search/issues/5), [`ET-006`](https://github.com/DesireGwanzura/etalent-search/issues/6), [`ET-007`](https://github.com/DesireGwanzura/etalent-search/issues/7), [`ET-008`](https://github.com/DesireGwanzura/etalent-search/issues/8) |
| **FR-8** | User authentication, RBAC (Recruiter/Admin), audit logging | Must | [`ET-020`](https://github.com/DesireGwanzura/etalent-search/issues/20), [`ET-024`](https://github.com/DesireGwanzura/etalent-search/issues/24), [`ET-025`](https://github.com/DesireGwanzura/etalent-search/issues/25), [`ET-033`](https://github.com/DesireGwanzura/etalent-search/issues/33) |
| **FR-9** | Filter ranked list by location and availability | Should | [`ET-044`](https://github.com/DesireGwanzura/etalent-search/issues/44) |
| **FR-10** | Edit vacancy and re-rank (instant weight re-rank from cache) | Should | [`ET-017`](https://github.com/DesireGwanzura/etalent-search/issues/17), [`ET-021`](https://github.com/DesireGwanzura/etalent-search/issues/21) |
| **FR-11** | Reopen past vacancies displaying stored snapshot; archive vacancy | Should | [`ET-018`](https://github.com/DesireGwanzura/etalent-search/issues/18), [`ET-031`](https://github.com/DesireGwanzura/etalent-search/issues/31) |
| **FR-12** | Mark candidate not relevant for a vacancy (per vacancy, visible to all) | Nice | [`ET-046`](https://github.com/DesireGwanzura/etalent-search/issues/46) |
| **FR-13** | Export shortlist as CSV | Nice | [`ET-045`](https://github.com/DesireGwanzura/etalent-search/issues/45) |
| **FR-14** | Recruiter sets weights per vacancy; admin changes defaults | Must | [`ET-016`](https://github.com/DesireGwanzura/etalent-search/issues/16), [`ET-024`](https://github.com/DesireGwanzura/etalent-search/issues/24), [`ET-027`](https://github.com/DesireGwanzura/etalent-search/issues/27) |
| **FR-15** | Recruiter marks candidates as shortlisted; saved with vacancy | Should | [`ET-023`](https://github.com/DesireGwanzura/etalent-search/issues/23), [`ET-030`](https://github.com/DesireGwanzura/etalent-search/issues/30) |
