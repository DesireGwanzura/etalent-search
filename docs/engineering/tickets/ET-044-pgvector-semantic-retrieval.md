# [ET-044] — Implement pgvector Semantic Retrieval and Hard Filtering

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-044 |
| **Title** | Implement pgvector Semantic Retrieval and Hard Filtering |
| **Project** | eTalent Search |
| **Workstream** | D. AI and Semantic Evaluation |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-2 |
| **GitHub Labels** | stream:backend, stream:ai, type:feature, priority:must, role:developer |

---

## 2. Objective

Build the semantic retrieval repository query in pgvector combining hard vacancy filters with vector similarity and candidate cap K=100.

---

## 3. Background and Context

Specification v1.0 FR-2 mandates evaluating every candidate passing hard filters up to a cap of 100. Beyond 100, the closest 100 by semantic similarity are evaluated and the UI states the shortfall.

---

## 4. User Story / Engineering Story

> As a recruiter, I want the system to retrieve candidates passing vacancy filters and select the top 100 by semantic similarity, so that only the most relevant candidates are deeply evaluated.

---

## 5. Scope

### In Scope
- Vacancy embedding generation using the pinned embedding model.
- Hard SQL filters: availability, minimum experience years, remote/location constraints.
- Cosine similarity ranking: `1 - (candidate_vector <=> vacancy_vector)`.
- Cap evaluation at K=100 candidates; calculate total eligible count and shortfall count.
- Return retrieval list flagged for subsequent deep evaluation.

### Out of Scope
- LLM factor evaluation (handled in ET-045)
- Frontend rendering (handled in ET-059)

### Constraints
- Query execution under 2 seconds for 1,000+ candidates.
- HNSW index optimization.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-2

### Technical Requirements
- TR-044-01: Write native JPA/Hibernate query with pgvector cosine distance operator `<=>`.
- TR-044-02: Implement `CandidateRetrievalRepository` with filter parameters and limit 100.
- TR-044-03: Create HNSW index `candidate_embedding_hnsw_idx` on vector column.

---

## 7. Implementation Flow

1. Generate embedding vector for vacancy description and requirements.
2. Count total candidates matching hard filters.
3. Query top 100 candidates ordered by cosine similarity distance.
4. Calculate shortfall: `max(0, totalEligible - 100)`.
5. Return `RetrievalResultSet` with candidates, similarity scores, and shortfall count.

---

## 8. Acceptance Criteria

- **AC-01:** Retrieval returns candidates matching hard filters, ordered by vector similarity.
- **AC-02:** Candidate cap of 100 is strictly enforced when eligible candidates exceed 100.
- **AC-03:** Response accurately reports total eligible count and shortfall count.

---

## 9. Testing Requirements

### Required Test Coverage
- Testcontainers integration test verifying cosine distance ordering against real pgvector.
- Performance test verifying query latency under 500ms on 1,000 candidate dataset.

---

## 10. Deliverables

- CandidateRetrievalRepository
- HNSW Flyway index migration
- RetrievalResultSet DTO

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-033, ET-038, ET-042
- **Downstream Tickets:** ET-045, ET-047, ET-052
- **Technical Risks & Mitigations:** Missing HNSW index causing full table scans; mitigated by Flyway index migration and EXPLAIN ANALYZE test.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/13
- **Branch:** `feature/et-044-pgvector-semantic-retrieval`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
