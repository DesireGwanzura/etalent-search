# [ET-040] — Implement Sync Status Reporting and Audit Logging

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-040 |
| **Title** | Implement Sync Status Reporting and Audit Logging |
| **Project** | eTalent Search |
| **Workstream** | C. Candidate Data Ingestion |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-7, FR-8 |
| **GitHub Labels** | stream:data, type:feature, priority:must, role:developer |

---

## 2. Objective

Implement synchronization run status recording, metric reporting, and audit logging for admin monitoring.

---

## 3. Background and Context

Specification v1.0 mandates an admin screen displaying last run status, record counts, and execution metrics, backed by persistent audit logs recording user identity.

---

## 4. User Story / Engineering Story

> As an administrator, I want to review candidate ingestion sync history and metrics, so that I can verify data freshness and detect sync anomalies.

---

## 5. Scope

### In Scope
- Entity `SyncAuditRecord` tracking startTime, endTime, status (SUCCESS/FAILED/ABORTED), counts (total, added, updated, deleted, skipped), error messages, and triggeredBy.
- REST endpoint `GET /api/admin/sync/status` returning current and historical sync status.
- REST endpoint `POST /api/admin/sync/trigger` allowing admin-triggered synchronization.
- Audit event logging for all manual sync triggers.

### Out of Scope
- Frontend UI views (handled in ET-063)
- External metrics exporter (Prometheus)

### Constraints
- Only users with `ADMIN` role can trigger sync or view detailed sync logs.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7, FR-8

### Technical Requirements
- TR-040-01: Create `SyncAuditRecord` JPA entity and repository.
- TR-040-02: Implement `AdminSyncController` secured with `@PreAuthorize("hasRole('ADMIN')")`.
- TR-040-03: Emit `AuditEvent` on sync start, completion, and failure.

---

## 7. Implementation Flow

1. Admin triggers sync via REST endpoint.
2. Controller verifies `ADMIN` role and initiates async sync task.
3. Sync service updates `SyncAuditRecord` with progress and final status.
4. Audit log records admin user identity and timestamp.

---

## 8. Acceptance Criteria

- **AC-01:** `GET /api/admin/sync/status` returns latest sync summary and historical log entries.
- **AC-02:** Non-admin users receive HTTP 403 Forbidden when attempting to trigger or view sync.
- **AC-03:** Failed or aborted sync runs log detailed error reasons and trigger timestamps.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test verifying admin access allowed and recruiter access forbidden.
- Integration test verifying audit record creation on sync completion.

---

## 10. Deliverables

- SyncAuditRecord entity
- AdminSyncController
- Audit logging service

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-039, ET-051
- **Downstream Tickets:** ET-063
- **Technical Risks & Mitigations:** Database deadlock during sync log update; mitigated by independent transaction propagation (`REQUIRES_NEW`).

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/9
- **Branch:** `feature/et-040-sync-status-reporting-audit-log`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
