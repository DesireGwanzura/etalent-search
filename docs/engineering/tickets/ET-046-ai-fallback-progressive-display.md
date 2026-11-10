# [ET-046] — Implement AI Fallback Strategy and Degraded Mode

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-046 |
| **Title** | Implement AI Fallback Strategy and Degraded Mode |
| **Project** | eTalent Search |
| **Workstream** | D. AI and Semantic Evaluation |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Consistency and Performance, FR-2, FR-3 |
| **GitHub Labels** | stream:backend, stream:ai, type:feature, priority:must, role:developer |

---

## 2. Objective

Build graceful degradation and fallback mechanism when AI evaluation times out or encounters rate limits.

---

## 3. Background and Context

Specification v1.0 mandates: AI timeout or rate limit must display the retrieval-based list flagged 'not fully evaluated', never an error screen. Progressive display delivers retrieval list immediately while scores stream in.

---

## 4. User Story / Engineering Story

> As a recruiter, I want to see retrieved candidates immediately with a clear 'not fully evaluated' notice if AI services fail, so that my recruitment workflow is never blocked by external service outages.

---

## 5. Scope

### In Scope
- Fallback handler catching AI provider exceptions (timeout, HTTP 429, HTTP 503).
- Marking candidate results as `partially_evaluated` or `retrieval_only`.
- Synthesizing baseline ordering using semantic similarity score when AI evaluation fails.
- Clear UI flag indicator: 'Ranking based on semantic retrieval; AI evaluation degraded'.
- Progressive ranking payload support returning initial retrieval list immediately.

### Out of Scope
- Permanent third-party AI provider failover

### Constraints
- The system must NEVER show an error page instead of a candidate list.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Consistency and Performance, FR-2, FR-3

### Technical Requirements
- TR-046-01: Implement `FallbackRankingProvider` transforming retrieval results into fallback ranking.
- TR-046-02: Add `evaluationStatus` enum (`FULL`, `PARTIAL`, `FALLBACK_RETRIEVAL_ONLY`) to ranking DTO.
- TR-046-03: Configure circuit breaker tripping to fallback after 3 consecutive provider failures.

---

## 7. Implementation Flow

1. AI orchestrator detects provider timeout or circuit breaker open.
2. Catch exception and route candidates to `FallbackRankingProvider`.
3. Generate fallback ranking using normalized vector similarity scores.
4. Attach explanation: 'AI evaluation unavailable; candidate ranked by profile semantic match'.
5. Return 200 OK with `evaluationStatus: FALLBACK_RETRIEVAL_ONLY`.

---

## 8. Acceptance Criteria

- **AC-01:** When AI provider throws 500 or times out, system returns 200 OK with ranked retrieval list.
- **AC-02:** Results carry explicit `evaluationStatus
- **AC-03:** No error page or unhandled exception is presented to the recruiter.

---

## 9. Testing Requirements

### Required Test Coverage
- Fault injection integration test simulating AI service HTTP 503 and verifying fallback response.
- Timeout test verifying slow AI responses trigger fallback after 5s per candidate.

---

## 10. Deliverables

- FallbackRankingProvider
- Circuit breaker configuration
- FallbackRankingResponse DTO

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-045
- **Downstream Tickets:** ET-047, ET-059
- **Technical Risks & Mitigations:** Recruiter misinterpreting fallback ranking as fully evaluated; mitigated by prominent UI warning badge.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/15
- **Branch:** `feature/et-046-ai-fallback-progressive-display`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
