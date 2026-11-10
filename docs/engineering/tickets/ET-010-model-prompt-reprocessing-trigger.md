---
ticket_id: ET-010
title: Implement Model and Prompt Version Re-processing Trigger
publish: auto
priority: should
type: task
workstream: data
owner_role: developer
---

# [ET-010] — Implement Model and Prompt Version Re-processing Trigger

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-010 |
| **Title** | Implement Model and Prompt Version Re-processing Trigger |
| **Project** | eTalent Search |
| **Workstream** | C. Candidate Data Ingestion |
| **Ticket Type** | Technical Task |
| **Priority** | Should |
| **Publishing Mode** | auto |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-7, Consistency Rules |

---

## 2. Objective

Build automated version detection and re-processing engine when the pinned embedding model or extraction prompt version changes.

---

## 3. Background and Context

Specification v1.0 mandates that embedding model or prompt version changes must trigger full re-processing of candidate vectors, while recording the exact versions that produced each stored artifact.

---

## 4. User Story / Engineering Story

> As an engineering team, we need automated re-indexing when the embedding model version changes, so that vector search space remains consistent across all candidate profiles.

---

## 5. Scope

### In Scope
- Version configuration: `app.ai.embedding.model-version` and `app.ai.evaluation.prompt-version`.
- Startup check: compare active configured version against database schema version registry.
- Admin maintenance task to trigger full re-embedding of active candidate corpus.
- Atomic vector table swap: build new embeddings in staging table before updating active search table.

### Out of Scope
- Automated migration of past historical ranking snapshots (snapshots preserve historical versions)

### Constraints
- Search remains available during re-indexing.
- Old vectors are preserved until new vectors are fully verified.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7, Consistency Rules

### Technical Requirements
- TR-041-01: Create `ai_version_registry` table storing active model and prompt hashes.
- TR-041-02: Implement `ReindexingService` executing batch re-embedding in background.
- TR-041-03: Atomic table or partition swap upon successful re-indexing.

---

## 7. Implementation Flow

1. Application detects difference between configured model version and registry.
2. Log warning and notify admin dashboard.
3. Admin triggers re-indexing task.
4. System embeds candidate profiles into staging table in batches.
5. On completion, swap active vector pointers and update registry.

---

## 8. Acceptance Criteria

- **AC-01:** Model version changes are detected on application startup and flagged.
- **AC-02:** Re-indexing completes without downtime for active recruiter searches.
- **AC-03:** Candidate vector records reflect new model version upon completion.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test verifying version registry update on re-indexing completion.
- Test verifying continuous search availability during staging re-index.

---

## 10. Deliverables

- AiVersionRegistry entity
- ReindexingService
- Admin re-indexing API endpoint

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-007, ET-009
- **Downstream Tickets:** ET-032
- **Technical Risks & Mitigations:** High AI API costs during full re-embedding; mitigated by explicit admin confirmation gate.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/10
- **Branch:** `feature/et-010-model-prompt-reprocessing-trigger`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
