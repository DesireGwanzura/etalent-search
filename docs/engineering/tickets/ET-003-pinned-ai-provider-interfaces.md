---
ticket_id: ET-003
title: Establish Pinned AI Provider and Embedding Interfaces
publish: approval
priority: must
type: task
workstream: foundation
owner_role: developer
---

# [ET-003] — Establish Pinned AI Provider and Embedding Interfaces

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-003 |
| **Title** | Establish Pinned AI Provider and Embedding Interfaces |
| **Project** | eTalent Search |
| **Workstream** | A. Foundation & Architecture |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | Foundation, FR-2, FR-4 |

---

## 2. Objective

Design and implement decoupled Java interfaces and adapter contracts for the pinned LLM and embedding model providers.

---

## 3. Background and Context

Specification v1.0 mandates one pinned embedding model and one pinned LLM with structured JSON output behind strict interfaces so provider implementations can be swapped without touching domain logic.

---

## 4. User Story / Engineering Story

> As an engineering team, we need decoupled AI service interfaces for embeddings and evaluation, so that provider implementations remain isolated from domain ranking logic.

---

## 5. Scope

### In Scope
- Define `EmbeddingClient` interface with batch and single embedding methods.
- Define `LlmEvaluationClient` interface requiring structured JSON response schema.
- Define metadata tracking contracts recording model version, prompt version, and latency.
- Implement mock client for local and offline testing.

### Out of Scope
- Live provider billing contracts
- Specific prompt templates (handled in ET-043)

### Constraints
- Interfaces must be decoupled from any specific SDK vendor (OpenAI, Gemini, Bedrock).
- Structured output must be strictly typed.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Foundation, FR-2, FR-4

### Technical Requirements
- TR-034-01: Define `EmbeddingClient` with method `List<float[]> generateEmbeddings(List<String> texts)`.
- TR-034-02: Define `LlmEvaluationClient` with method `EvaluationResult evaluateEvidence(EvaluationPrompt prompt)`.
- TR-034-03: Implement `MockAiClient` returning deterministic fixture outputs for test suites.

---

## 7. Implementation Flow

1. Create `com.etalent.search.ai.api` package with interface contracts.
2. Define DTOs: `EvaluationPrompt`, `EvaluationResult`, `FactorMatchRecord`.
3. Implement `MockEmbeddingClient` and `MockLlmEvaluationClient` activated under `@Profile("test")`.
4. Verify integration with Spring Dependency Injection.

---

## 8. Acceptance Criteria

- **AC-01:** `EmbeddingClient` and `LlmEvaluationClient` interfaces defined with complete contract docstrings.
- **AC-02:** Mock implementations provide deterministic responses when `test` profile is active.
- **AC-03:** Model version and configuration metadata captured in every client call response.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit tests verifying interface contracts and DTO serialization.
- Component test verifying Spring Boot selects Mock client under test profile.

---

## 10. Deliverables

- Interface definitions (`EmbeddingClient`, `LlmEvaluationClient`)
- DTO schemas
- Mock implementations

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-001
- **Downstream Tickets:** ET-011, ET-012, ET-013
- **Technical Risks & Mitigations:** Provider API breaking changes; mitigated by vendor-neutral internal domain DTOs.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/3
- **Branch:** `feature/et-003-pinned-ai-provider-interfaces`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
