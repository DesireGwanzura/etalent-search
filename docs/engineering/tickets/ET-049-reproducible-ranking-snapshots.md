# [ET-049] — Implement Reproducible Ranking Snapshot Persistence

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-049 |
| **Title** | Implement Reproducible Ranking Snapshot Persistence |
| **Project** | eTalent Search |
| **Workstream** | E. Scoring and Ranking Engine |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-6, FR-11 |
| **GitHub Labels** | stream:backend, type:feature, priority:must, role:developer |

---

## 2. Objective

Build the persistent ranking snapshot store to record weights, scores, model/prompt versions, explanations, and shortlists for full reproducibility.

---

## 3. Background and Context

Specification v1.0 FR-6 & section 9: The same vacancy, candidate data, weights, and configuration always return the same stored ranking. Reopening past vacancies returns the stored snapshot; recalculation occurs only on explicit request.

---

## 4. User Story / Engineering Story

> As a recruiter and audit manager, I want past vacancy rankings saved as immutable snapshots, so that past hiring decisions are fully reproducible and auditable over time.

---

## 5. Scope

### In Scope
- Entity `RankingSnapshot` storing: vacancyId, weights, candidate count, data version, model version, prompt version, createdAt, createdBy.
- Entity `CandidateSnapshotItem` storing: candidateId, rankPosition, totalScore, factorBreakdown JSON, explanations JSON, isShortlisted.
- Query API returning stored snapshot without re-running scoring or AI evaluation.
- Version tracking: editing a vacancy creates a new snapshot version, preserving historical snapshots.

### Out of Scope
- CSV export generation (handled in ET-076)

### Constraints
- Historical snapshots are immutable.
- Candidate redaction updates `status='REMOVED'` without deleting the snapshot row.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-6, FR-11

### Technical Requirements
- TR-049-01: Create `ranking_snapshot` and `candidate_snapshot_item` Flyway schema.
- TR-049-02: Implement `SnapshotService.saveSnapshot(rankingResult)`.
- TR-049-03: Implement `SnapshotService.getLatestSnapshot(vacancyId)`.

---

## 7. Implementation Flow

1. Ranking calculation completes.
2. Serialize weights, scores, factor match explanations, and version metadata.
3. Persist `RankingSnapshot` and child items in single transaction.
4. Return snapshot identifier with ranking response.
5. Reopening vacancy loads snapshot directly from database.

---

## 8. Acceptance Criteria

- **AC-01:** Reopening a vacancy returns the exact stored ranking snapshot without recalculation.
- **AC-02:** Snapshot captures model version, prompt version, and exact weights used.
- **AC-03:** Editing vacancy creates a new snapshot version without overwriting prior snapshots.

---

## 9. Testing Requirements

### Required Test Coverage
- Integration test saving and reloading snapshot verifying 100% field parity.
- Test verifying that subsequent candidate data changes do not alter existing snapshot scores.

---

## 10. Deliverables

- RankingSnapshot and CandidateSnapshotItem entities
- SnapshotService
- Flyway schema migration

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-033, ET-047, ET-048
- **Downstream Tickets:** ET-050, ET-053, ET-054
- **Technical Risks & Mitigations:** Large snapshot tables slowing down queries; mitigated by composite indexing on `(vacancy_id, version)`.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/18
- **Branch:** `feature/et-049-reproducible-ranking-snapshots`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
