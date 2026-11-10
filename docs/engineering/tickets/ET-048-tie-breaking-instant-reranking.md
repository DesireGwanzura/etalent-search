# [ET-048] — Implement Tie-Breaking Logic and Instant Cached Re-ranking

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-048 |
| **Title** | Implement Tie-Breaking Logic and Instant Cached Re-ranking |
| **Project** | eTalent Search |
| **Workstream** | E. Scoring and Ranking Engine |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-3, FR-6, FR-10, Scoring Rules |
| **GitHub Labels** | stream:backend, type:feature, priority:must, role:developer |

---

## 2. Objective

Implement deterministic tie-breaking rules and sub-second re-ranking from cached factor evaluations when weights change.

---

## 3. Background and Context

Specification v1.0: Ties are broken by Required Skills match. A weight-only change re-ranks instantly from cached factor matches without new AI calls. A requirement change re-evaluates.

---

## 4. User Story / Engineering Story

> As a recruiter, I want candidate ties broken by required skills and instant re-ranking when I adjust weights, so that I can explore weight scenarios without waiting for AI re-evaluations.

---

## 5. Scope

### In Scope
- Tie-breaking rule: Primary sort by total score DESC; secondary sort by Required Skills match score DESC; tertiary sort by Experience match score DESC; final sort by candidate ID ASC.
- Instant re-ranking service: re-calculate scores from stored factor match cache when weights change.
- Zero AI calls triggered during weight-only adjustments.
- Latency requirement: weight-change re-ranking response in < 500ms.

### Out of Scope
- Requirement changes (which trigger re-evaluation)

### Constraints
- Tie-breaking order must be strictly deterministic.
- Cache must be invalidated if vacancy requirements change.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-3, FR-6, FR-10, Scoring Rules

### Technical Requirements
- TR-048-01: Implement `CandidateComparator` with multi-tier tie-breaking logic.
- TR-048-02: Implement `rerankWithWeights(vacancyId, newWeights)` reading factor match cache.
- TR-048-03: Invalidate cached evaluation records on vacancy requirement updates.

---

## 7. Implementation Flow

1. Recruiter submits updated weights for existing vacancy.
2. Fetch cached factor evaluations for vacancy candidates.
3. Recalculate candidate scores with new weights.
4. Sort candidates using multi-tier tie-breaker.
5. Return updated ranking list in < 500ms.

---

## 8. Acceptance Criteria

- **AC-01:** Identical total scores are broken deterministically by Required Skills match score.
- **AC-02:** Updating weights produces a re-ranked list in < 500ms with zero AI calls.
- **AC-03:** Requirement changes properly invalidate cache and trigger re-evaluation.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit tests with tied candidate scores verifying tie-breaker sorting order.
- Performance test verifying 100 candidates re-ranked from cache in under 100ms.

---

## 10. Deliverables

- CandidateComparator class
- CachedRerankingService
- Tie-breaking test suite

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-047
- **Downstream Tickets:** ET-049, ET-052
- **Technical Risks & Mitigations:** Stale cache returned after vacancy requirements change; mitigated by cache key binding to requirements hash.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/17
- **Branch:** `feature/et-048-tie-breaking-instant-reranking`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
