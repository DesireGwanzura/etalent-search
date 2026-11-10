# eTalent Search — Complete Engineering Backlog Index

**Standard:** Team Engineering Ticket Standard (TETS) v1.0  
**Project:** eTalent Search  
**Authoritative Specification:** eTalent Search Project Specification v1.0  
**Repository:** [DesireGwanzura/etalent-search](https://github.com/DesireGwanzura/etalent-search)  
**Total Published Issues:** 47 (`ET-032` to `ET-078`)  

---

## 1. Executive Summary & Distribution

### Priority Distribution
- **priority:must (Must):** 39 tickets (Core Release 1 deliverables: FR-1 to FR-8, FR-14, Architecture, DevOps, Security, AI Spike)
- **priority:should (Should):** 6 tickets (FR-9 Filters, FR-10 Edit/Re-rank, FR-11 Past Vacancies/Archive, FR-15 Shortlist, Reprocessing trigger)
- **priority:nice (Nice):** 2 tickets (FR-12 Mark Not Relevant, FR-13 CSV Shortlist Export)
- **Total Backlog Tickets:** **47**

### Workstream Distribution
- **A. Foundation and Architecture:** 4 tickets (`ET-032` – `ET-035`)
- **B. Infrastructure and DevOps:** 6 tickets (`ET-065` – `ET-070`)
- **C. Candidate Data Ingestion:** 6 tickets (`ET-036` – `ET-041`)
- **D. AI and Semantic Evaluation:** 5 tickets (`ET-042` – `ET-046`)
- **E. Scoring and Ranking Engine:** 4 tickets (`ET-047` – `ET-050`)
- **F. Backend and Security:** 6 tickets (`ET-051` – `ET-056`)
- **G. Frontend (Angular SPA):** 8 tickets (`ET-057` – `ET-064`)
- **H. Testing, Release & Optional:** 8 tickets (`ET-071` – `ET-078`)

### Team Role Ownership Distribution (7-Person Engineering Team)
- **Software Developers (4 devs):** 36 tickets (Backend APIs, Domain Logic, Ingestion, Angular SPA, Security)
- **DevOps Engineer (1 devops):** 6 tickets (GitLab CI/CD, GitHub Actions, Docker, Rulesets, Scanners)
- **AI Engineer (1 ai):** 2 tickets (`ET-042` AI Spike, `ET-043` Structured Prompt Engineering) + Cross-cutting reviews
- **QA / Test Engineer (1 tester):** 3 tickets (`ET-035` Synthetic Datasets, `ET-071` Testcontainers, `ET-073` Consistency Tests, `ET-074` Adversarial Tests, `ET-078` E2E Readiness)

---

## 2. Complete Backlog Registry

| Ticket ID | Title | Workstream | Priority | Suggested Owner | Status | GitHub Issue Link |
| :--- | :--- | :--- | :---: | :--- | :---: | :--- |
| **ET-032** | Establish Project Structure and Gradle Wrapper | A. Foundation & Architecture | `Must` | Software Developer | `Ready` | [#1](https://github.com/DesireGwanzura/etalent-search/issues/1) |
| **ET-033** | Configure PostgreSQL and pgvector Database Extension | A. Foundation & Architecture | `Must` | Software Developer | `Ready` | [#2](https://github.com/DesireGwanzura/etalent-search/issues/2) |
| **ET-034** | Establish Pinned AI Provider and Embedding Interfaces | A. Foundation & Architecture | `Must` | Software Developer | `Ready` | [#3](https://github.com/DesireGwanzura/etalent-search/issues/3) |
| **ET-035** | Implement Synthetic Candidate and Vacancy Dataset Generation | A. Foundation & Architecture | `Must` | QA Engineer | `Ready` | [#4](https://github.com/DesireGwanzura/etalent-search/issues/4) |
| **ET-036** | Implement External Candidate Source File Adapter | C. Candidate Data Ingestion | `Must` | Software Developer | `Ready` | [#5](https://github.com/DesireGwanzura/etalent-search/issues/5) |
| **ET-037** | Build Privacy Redaction and Allowlist Scrubber | C. Candidate Data Ingestion | `Must` | Software Developer | `Ready` | [#6](https://github.com/DesireGwanzura/etalent-search/issues/6) |
| **ET-038** | Implement CV AI Extraction and Embedding Generation | C. Candidate Data Ingestion | `Must` | Software Developer | `Ready` | [#7](https://github.com/DesireGwanzura/etalent-search/issues/7) |
| **ET-039** | Implement Ingestion Synchronisation and Mass-Deletion Guard | C. Candidate Data Ingestion | `Must` | Software Developer | `Ready` | [#8](https://github.com/DesireGwanzura/etalent-search/issues/8) |
| **ET-040** | Implement Sync Status Reporting and Audit Logging | C. Candidate Data Ingestion | `Must` | Software Developer | `Ready` | [#9](https://github.com/DesireGwanzura/etalent-search/issues/9) |
| **ET-041** | Implement Model and Prompt Version Re-processing Trigger | C. Candidate Data Ingestion | `Should` | Software Developer | `Ready` | [#10](https://github.com/DesireGwanzura/etalent-search/issues/10) |
| **ET-042** | Execute AI Feasibility Spike and Latency/Cost Benchmark | D. AI and Semantic Evaluation | `Must` | AI Engineer | `Ready` | [#11](https://github.com/DesireGwanzura/etalent-search/issues/11) |
| **ET-043** | Engineer Pinned LLM Prompts with Structured JSON Output | D. AI and Semantic Evaluation | `Must` | AI Engineer | `Ready` | [#12](https://github.com/DesireGwanzura/etalent-search/issues/12) |
| **ET-044** | Implement pgvector Semantic Retrieval and Hard Filtering | D. AI and Semantic Evaluation | `Must` | Software Developer | `Ready` | [#13](https://github.com/DesireGwanzura/etalent-search/issues/13) |
| **ET-045** | Build Parallel AI Evaluation Orchestrator and Rate Limiting | D. AI and Semantic Evaluation | `Must` | Software Developer | `Ready` | [#14](https://github.com/DesireGwanzura/etalent-search/issues/14) |
| **ET-046** | Implement AI Fallback Strategy and Degraded Mode | D. AI and Semantic Evaluation | `Must` | Software Developer | `Ready` | [#15](https://github.com/DesireGwanzura/etalent-search/issues/15) |
| **ET-047** | Build Deterministic Factor Scoring Engine | E. Scoring and Ranking Engine | `Must` | Software Developer | `Ready` | [#16](https://github.com/DesireGwanzura/etalent-search/issues/16) |
| **ET-048** | Implement Tie-Breaking Logic and Instant Cached Re-ranking | E. Scoring and Ranking Engine | `Must` | Software Developer | `Ready` | [#17](https://github.com/DesireGwanzura/etalent-search/issues/17) |
| **ET-049** | Implement Reproducible Ranking Snapshot Persistence | E. Scoring and Ranking Engine | `Must` | Software Developer | `Ready` | [#18](https://github.com/DesireGwanzura/etalent-search/issues/18) |
| **ET-050** | Build Explanation Faithfulness and Evidence Validation | E. Scoring and Ranking Engine | `Must` | Software Developer | `Ready` | [#19](https://github.com/DesireGwanzura/etalent-search/issues/19) |
| **ET-051** | Configure Spring Security, Session Cookies, and RBAC | F. Backend and Security | `Must` | Software Developer | `Ready` | [#20](https://github.com/DesireGwanzura/etalent-search/issues/20) |
| **ET-052** | Implement Vacancy Management REST API | F. Backend and Security | `Must` | Software Developer | `Ready` | [#21](https://github.com/DesireGwanzura/etalent-search/issues/21) |
| **ET-053** | Implement Candidate Profile and Ranking Query REST API | F. Backend and Security | `Must` | Software Developer | `Ready` | [#22](https://github.com/DesireGwanzura/etalent-search/issues/22) |
| **ET-054** | Implement Shortlist Management REST API | F. Backend and Security | `Should` | Software Developer | `Ready` | [#23](https://github.com/DesireGwanzura/etalent-search/issues/23) |
| **ET-055** | Implement Admin User Management and System Defaults API | F. Backend and Security | `Must` | Software Developer | `Ready` | [#24](https://github.com/DesireGwanzura/etalent-search/issues/24) |
| **ET-056** | Implement Comprehensive Audit Logging Interceptor | F. Backend and Security | `Must` | Software Developer | `Ready` | [#25](https://github.com/DesireGwanzura/etalent-search/issues/25) |
| **ET-057** | Set Up Angular 17+ SPA and Spring Boot Bundle Integration | G. Frontend | `Must` | Software Developer | `Ready` | [#26](https://github.com/DesireGwanzura/etalent-search/issues/26) |
| **ET-058** | Build Vacancy Creation and Configurable Weights UI | G. Frontend | `Must` | Software Developer | `Ready` | [#27](https://github.com/DesireGwanzura/etalent-search/issues/27) |
| **ET-059** | Build Ranked Candidate Results List and Factor Explanations | G. Frontend | `Must` | Software Developer | `Ready` | [#28](https://github.com/DesireGwanzura/etalent-search/issues/28) |
| **ET-060** | Build Candidate Profile Inspection View | G. Frontend | `Must` | Software Developer | `Ready` | [#29](https://github.com/DesireGwanzura/etalent-search/issues/29) |
| **ET-061** | Build Shortlist Action and Dedicated Shortlist View | G. Frontend | `Should` | Software Developer | `Ready` | [#30](https://github.com/DesireGwanzura/etalent-search/issues/30) |
| **ET-062** | Build Past Vacancies Archive and Reopen UI | G. Frontend | `Should` | Software Developer | `Ready` | [#31](https://github.com/DesireGwanzura/etalent-search/issues/31) |
| **ET-063** | Build Admin Console for User Accounts, Sync, and Defaults | G. Frontend | `Must` | Software Developer | `Ready` | [#32](https://github.com/DesireGwanzura/etalent-search/issues/32) |
| **ET-064** | Build Authentication Login Screen and Application Shell | G. Frontend | `Must` | Software Developer | `Ready` | [#33](https://github.com/DesireGwanzura/etalent-search/issues/33) |
| **ET-065** | Establish GitLab CI/CD Pipeline Configuration | B. Infrastructure and DevOps | `Must` | DevOps Engineer | `Ready` | [#34](https://github.com/DesireGwanzura/etalent-search/issues/34) |
| **ET-066** | Configure GitHub Actions PR Automation and Reviewer Assignment | B. Infrastructure and DevOps | `Must` | DevOps Engineer | `Ready` | [#35](https://github.com/DesireGwanzura/etalent-search/issues/35) |
| **ET-067** | Implement GitHub to GitLab Mirroring and Webhook Sync | B. Infrastructure and DevOps | `Must` | DevOps Engineer | `Ready` | [#36](https://github.com/DesireGwanzura/etalent-search/issues/36) |
| **ET-068** | Build Multi-Stage Dockerfile and Container Packaging | B. Infrastructure and DevOps | `Must` | DevOps Engineer | `Ready` | [#37](https://github.com/DesireGwanzura/etalent-search/issues/37) |
| **ET-069** | Configure Static Analysis, SonarQube, and Secret Scanning | B. Infrastructure and DevOps | `Must` | DevOps Engineer | `Ready` | [#38](https://github.com/DesireGwanzura/etalent-search/issues/38) |
| **ET-070** | Configure GitHub Rulesets and Release Promotion Workflow | B. Infrastructure and DevOps | `Must` | DevOps Engineer | `Ready` | [#39](https://github.com/DesireGwanzura/etalent-search/issues/39) |
| **ET-071** | Build Testcontainers Integration Test Harness | H. Testing and Release | `Must` | QA Engineer | `Ready` | [#40](https://github.com/DesireGwanzura/etalent-search/issues/40) |
| **ET-072** | Establish POPIA Legal Compliance Gate and Synthetic Data Policy | H. Testing and Release | `Must` | Software Developer | `Ready` | [#41](https://github.com/DesireGwanzura/etalent-search/issues/41) |
| **ET-073** | Build Ranking Consistency and Top-5 Overlap Test Suite | H. Testing and Release | `Must` | QA Engineer | `Ready` | [#42](https://github.com/DesireGwanzura/etalent-search/issues/42) |
| **ET-074** | Build Security and Adversarial Prompt-Injection Test Suite | H. Testing and Release | `Must` | QA Engineer | `Ready` | [#43](https://github.com/DesireGwanzura/etalent-search/issues/43) |
| **ET-075** | Implement Location and Availability Faceted Search Filters | H. Testing, Release & Optional | `Should` | Software Developer | `Ready` | [#44](https://github.com/DesireGwanzura/etalent-search/issues/44) |
| **ET-076** | Implement Shortlist CSV Export Functionality | H. Testing, Release & Optional | `Nice` | Software Developer | `Ready` | [#45](https://github.com/DesireGwanzura/etalent-search/issues/45) |
| **ET-077** | Implement Mark Candidate Not Relevant Action | H. Testing, Release & Optional | `Nice` | Software Developer | `Ready` | [#46](https://github.com/DesireGwanzura/etalent-search/issues/46) |
| **ET-078** | Execute End-to-End System Testing and Release 1 Readiness Gate | H. Testing and Release | `Must` | QA Engineer | `Ready` | [#47](https://github.com/DesireGwanzura/etalent-search/issues/47) |

---

## 3. Specification Traceability Matrix (FR-1 to FR-15)

| Requirement ID | Specification Requirement | Priority | Implementing Ticket(s) |
| :--- | :--- | :---: | :--- |
| **FR-1** | Recruiter creates vacancy (title, skills, experience, location, remote) | Must | [`ET-052`](https://github.com/DesireGwanzura/etalent-search/issues/21), [`ET-058`](https://github.com/DesireGwanzura/etalent-search/issues/27) |
| **FR-2** | Semantic evaluation of candidates passing hard filters up to cap 100 | Must | [`ET-044`](https://github.com/DesireGwanzura/etalent-search/issues/13), [`ET-045`](https://github.com/DesireGwanzura/etalent-search/issues/14), [`ET-047`](https://github.com/DesireGwanzura/etalent-search/issues/16) |
| **FR-3** | Display sorted results by score with name, title, score, top reasons | Must | [`ET-048`](https://github.com/DesireGwanzura/etalent-search/issues/17), [`ET-053`](https://github.com/DesireGwanzura/etalent-search/issues/22), [`ET-059`](https://github.com/DesireGwanzura/etalent-search/issues/28) |
| **FR-4** | Plain-language AI factor explanations without numeric scores | Must | [`ET-043`](https://github.com/DesireGwanzura/etalent-search/issues/12), [`ET-047`](https://github.com/DesireGwanzura/etalent-search/issues/16), [`ET-050`](https://github.com/DesireGwanzura/etalent-search/issues/19) |
| **FR-5** | Recruiter opens full candidate profile from ranked list | Must | [`ET-053`](https://github.com/DesireGwanzura/etalent-search/issues/22), [`ET-060`](https://github.com/DesireGwanzura/etalent-search/issues/29) |
| **FR-6** | Reproducible ranking snapshots (same inputs = same stored ranking) | Must | [`ET-048`](https://github.com/DesireGwanzura/etalent-search/issues/17), [`ET-049`](https://github.com/DesireGwanzura/etalent-search/issues/18), [`ET-073`](https://github.com/DesireGwanzura/etalent-search/issues/42) |
| **FR-7** | Candidate ingestion pipeline (file adapter, scrub, embed, sync, guard) | Must | [`ET-036`](https://github.com/DesireGwanzura/etalent-search/issues/5), [`ET-037`](https://github.com/DesireGwanzura/etalent-search/issues/6), [`ET-038`](https://github.com/DesireGwanzura/etalent-search/issues/7), [`ET-039`](https://github.com/DesireGwanzura/etalent-search/issues/8) |
| **FR-8** | User authentication, RBAC (Recruiter/Admin), audit logging | Must | [`ET-051`](https://github.com/DesireGwanzura/etalent-search/issues/20), [`ET-055`](https://github.com/DesireGwanzura/etalent-search/issues/24), [`ET-056`](https://github.com/DesireGwanzura/etalent-search/issues/25), [`ET-064`](https://github.com/DesireGwanzura/etalent-search/issues/33) |
| **FR-9** | Filter ranked list by location and availability | Should | [`ET-075`](https://github.com/DesireGwanzura/etalent-search/issues/44) |
| **FR-10** | Edit vacancy and re-rank (instant weight re-rank from cache) | Should | [`ET-048`](https://github.com/DesireGwanzura/etalent-search/issues/17), [`ET-052`](https://github.com/DesireGwanzura/etalent-search/issues/21) |
| **FR-11** | Reopen past vacancies displaying stored snapshot; archive vacancy | Should | [`ET-049`](https://github.com/DesireGwanzura/etalent-search/issues/18), [`ET-062`](https://github.com/DesireGwanzura/etalent-search/issues/31) |
| **FR-12** | Mark candidate not relevant for a vacancy (per vacancy, visible to all) | Nice | [`ET-077`](https://github.com/DesireGwanzura/etalent-search/issues/46) |
| **FR-13** | Export shortlist as CSV | Nice | [`ET-076`](https://github.com/DesireGwanzura/etalent-search/issues/45) |
| **FR-14** | Recruiter sets weights per vacancy; admin changes defaults | Must | [`ET-047`](https://github.com/DesireGwanzura/etalent-search/issues/16), [`ET-055`](https://github.com/DesireGwanzura/etalent-search/issues/24), [`ET-058`](https://github.com/DesireGwanzura/etalent-search/issues/27) |
| **FR-15** | Recruiter marks candidates as shortlisted; saved with vacancy | Should | [`ET-054`](https://github.com/DesireGwanzura/etalent-search/issues/23), [`ET-061`](https://github.com/DesireGwanzura/etalent-search/issues/30) |
