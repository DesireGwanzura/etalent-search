# [ET-038] — Implement CV AI Extraction and Embedding Generation

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-038 |
| **Title** | Implement CV AI Extraction and Embedding Generation |
| **Project** | eTalent Search |
| **Workstream** | C. Candidate Data Ingestion |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-7 |
| **GitHub Labels** | stream:data, stream:ai, type:feature, priority:must, role:developer |

---

## 2. Objective

Implement the extraction and embedding pipeline that computes total experience, generates profile embeddings, and upserts candidates into pgvector.

---

## 3. Background and Context

Specification v1.0 mandates computing total years of experience by code from job dates, generating candidate profile embeddings using the pinned model, and storing them in pgvector.

---

## 4. User Story / Engineering Story

> As the eTalent system, I want candidate CVs extracted and embedded into pgvector, so that candidates are searchable by semantic vector similarity.

---

## 5. Scope

### In Scope
- Deterministic calculation of total years of experience from normalized ISO job dates.
- Constructing canonical profile text representation for embedding generation.
- Batch embedding generation via `EmbeddingClient`.
- Upserting candidate entities and vector embeddings into PostgreSQL/pgvector.
- Skipping unchanged candidates based on `updatedAt` timestamp and SHA-256 content hash.

### Out of Scope
- Real-time vacancy matching (handled in ET-044)
- Recruiter profile display UI

### Constraints
- Embeddings must be generated using the pinned embedding model version.
- Content hashing to prevent duplicate AI API spend.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7

### Technical Requirements
- TR-038-01: Calculate total experience in months/years handling overlapping tenures.
- TR-038-02: Compute SHA-256 hash of sanitized CV content to detect changes.
- TR-038-03: Store 1536/768-dim vector in `candidate_embedding` table with HNSW index.

---

## 7. Implementation Flow

1. Calculate total experience from employment date ranges.
2. Compute content hash and compare against existing database record.
3. If changed, invoke `EmbeddingClient` with sanitized canonical text.
4. Upsert candidate profile and vector embedding in a single database transaction.
5. Record embedding model version in candidate record.

---

## 8. Acceptance Criteria

- **AC-01:** Total experience accurately calculated with overlapping jobs counted once.
- **AC-02:** Unchanged candidates are skipped based on content hash, making repeat runs idempotent.
- **AC-03:** Embeddings are successfully persisted to pgvector and indexed.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit test for experience calculator covering gaps, overlaps, and current jobs.
- Integration test verifying upsert logic and hash-based skipping of unchanged records.

---

## 10. Deliverables

- ExperienceCalculator class
- CandidateEmbeddingService
- Repository upsert methods

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-033, ET-034, ET-037
- **Downstream Tickets:** ET-039, ET-040, ET-044
- **Technical Risks & Mitigations:** Inaccurate date parsing causing negative or inflated experience; mitigated by strict ISO date normalization.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/7
- **Branch:** `feature/et-038-cv-extraction-embedding-pipeline`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
