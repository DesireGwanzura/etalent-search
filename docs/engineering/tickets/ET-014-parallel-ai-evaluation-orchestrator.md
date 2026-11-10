---
ticket_id: ET-014
title: Build Parallel AI Evaluation Orchestrator and Rate Limiting
publish: approval
priority: must
type: feature
workstream: ai
owner_role: developer
---

# [ET-014] — Build Parallel AI Evaluation Orchestrator and Rate Limiting

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-014 |
| **Title** | Build Parallel AI Evaluation Orchestrator and Rate Limiting |
| **Project** | eTalent Search |
| **Workstream** | D. AI and Semantic Evaluation |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-2, Consistency and Performance |

---

## 2. Objective

Implement the parallel evaluation orchestrator with bounded concurrency, rate limiting, and evaluation caching.

---

## 3. Background and Context

Specification v1.0 mandates evaluating up to 100 retrieved candidates in parallel within <= 60s, with caching by candidate+vacancy+prompt+model version, and concurrency caps to prevent rate limit exhaustion.

---

## 4. User Story / Engineering Story

> As an engineering team, we need a parallel evaluation orchestrator with concurrency limits and caching, so that candidates are evaluated rapidly without exceeding AI provider rate limits.

---

## 5. Scope

### In Scope
- Bounded worker pool (`CompletableFuture` or Virtual Threads with Semaphore concurrency limit, default 10).
- Rate limiter (token bucket or resilience4j) protecting AI provider quotas.
- Evaluation caching: cache key `hash(candidateId + vacancyId + promptVersion + modelVersion)`.
- Progress tracking allowing progressive score streaming.
- Timeout protection per candidate call (default 5s) and overall evaluation timeout (60s).

### Out of Scope
- Final score arithmetic (handled in ET-047)
- WebSocket UI streaming

### Constraints
- Concurrency must be configurable via `app.ai.concurrency.max-workers`.
- No thread starvation.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-2, Consistency and Performance

### Technical Requirements
- TR-045-01: Configure `CustomTaskExecutor` with bounded queue and semaphore.
- TR-045-02: Implement `EvaluationCacheService` using PostgreSQL or Redis cache.
- TR-045-03: Integrate Resilience4j RateLimiter and Retry with exponential backoff.

---

## 7. Implementation Flow

1. Receive list of up to 100 candidate IDs for a vacancy.
2. Check cache for existing evaluations matching current version hash.
3. Dispatch un-cached candidates to worker pool under semaphore permit.
4. Aggregate factor match records as evaluations complete.
5. Return complete evaluation set or partial set if timeout threshold is reached.

---

## 8. Acceptance Criteria

- **AC-01:** 100 candidates evaluated in parallel within 60s in standard test environment.
- **AC-02:** Cached evaluations return instantly without making outgoing AI calls.
- **AC-03:** Rate limiter throttles outgoing requests to comply with provider limits without dropping jobs.

---

## 9. Testing Requirements

### Required Test Coverage
- Concurrency test evaluating 100 mock candidates verifying concurrency cap.
- Cache hit test verifying zero AI calls for identical candidate and vacancy parameters.

---

## 10. Deliverables

- AiEvaluationOrchestrator
- EvaluationCacheService
- Resilience4j configuration

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-012, ET-013
- **Downstream Tickets:** ET-015, ET-016, ET-021
- **Technical Risks & Mitigations:** Worker pool thread exhaustion under high load; mitigated by virtual threads (Java 21) or strict semaphore.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/14
- **Branch:** `feature/et-014-parallel-ai-evaluation-orchestrator`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
