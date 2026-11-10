---
ticket_id: ET-008
title: Implement Ingestion Synchronisation and Mass-Deletion Guard
publish: approval
priority: must
type: feature
workstream: data
owner_role: developer
---

# [ET-008] — Implement Ingestion Synchronisation and Mass-Deletion Guard

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-008 |
| **Title** | Implement Ingestion Synchronisation and Mass-Deletion Guard |
| **Project** | eTalent Search |
| **Workstream** | C. Candidate Data Ingestion |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-7, Consistency Rules |

---

## 2. Objective

Build the scheduled and on-demand synchronization engine with mass-deletion protection and historical snapshot redaction.

---

## 3. Background and Context

Specification v1.0 requires full sync where absence = deletion. Deletions above a configured threshold (e.g., 20%) must abort the run to prevent mass deletion. Deleted candidates are removed from vector search, while historical snapshots show 'candidate removed'.

---

## 4. User Story / Engineering Story

> As a system administrator, I want candidate sync to protect against mass deletion and clean up deleted profiles, so that database integrity and candidate privacy are preserved.

---

## 5. Scope

### In Scope
- Spring `@Scheduled` nightly execution (configurable cron) and programmatic admin trigger.
- Single-execution concurrency lock (`@SchedulerLock` or database lock) preventing concurrent runs.
- Mass-deletion threshold guard: abort run if deletions exceed configured percentage (default 20%).
- Deletion handling: delete candidate profile and vector from active search; update past snapshots to redact evidence and display 'candidate removed'.
- Staged build with atomic cut-over on successful completion.

### Out of Scope
- Admin UI screen (handled in ET-055)
- Real-time CDC pipeline

### Constraints
- Only one synchronization run at a time.
- Past rankings must remain reproducible without leaking deleted PII.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7, Consistency Rules

### Technical Requirements
- TR-039-01: Implement `CandidateSyncService` with synchronization lock.
- TR-039-02: Calculate `deletionCount / totalCandidates` and throw `MassDeletionAbortException` if > threshold.
- TR-039-03: Redact candidate snapshot rows setting `status = 'REMOVED'` and clearing evidence text.

---

## 7. Implementation Flow

1. Acquire sync execution lock; if locked, log and skip.
2. Read all candidate IDs from external source.
3. Identify additions, updates, and missing IDs (deletions).
4. Verify deletion percentage does not exceed threshold; abort if exceeded.
5. Apply additions and updates; purge deleted candidates from active search and redact in snapshots.
6. Record sync metrics (added, updated, deleted, duration) in `sync_log` table.

---

## 8. Acceptance Criteria

- **AC-01:** Nightly scheduler triggers sync, and concurrent triggers are safely rejected.
- **AC-02:** If deletion percentage exceeds threshold, sync aborts immediately without modifying existing records.
- **AC-03:** Deleted candidates are purged from pgvector and past snapshots display 'candidate removed'.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit test verifying mass deletion guard aborts when 25% of candidates are missing.
- Integration test verifying candidate removal from vector store and snapshot redaction.

---

## 10. Deliverables

- CandidateSyncService
- SyncLog entity and repository
- Mass deletion guard validator

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-007
- **Downstream Tickets:** ET-009, ET-024
- **Technical Risks & Mitigations:** Source feed failure triggering unintended deletion of all candidates; fully mitigated by mass-deletion guard.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/8
- **Branch:** `feature/et-008-sync-scheduler-mass-deletion-guard`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
