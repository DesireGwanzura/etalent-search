---
ticket_id: ET-005
title: Implement External Candidate Source File Adapter
publish: approval
priority: must
type: feature
workstream: data
owner_role: developer
---

# [ET-005] — Implement External Candidate Source File Adapter

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-005 |
| **Title** | Implement External Candidate Source File Adapter |
| **Project** | eTalent Search |
| **Workstream** | C. Candidate Data Ingestion |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-7 |

---

## 2. Objective

Build the external candidate source file adapter to ingest candidate records and CV JSON files from an agreed filesystem storage location.

---

## 3. Background and Context

Specification v1.0 section 7 defines release 1 exchange format as JSON files exported by the source to an agreed storage location, read by a loader behind a source adapter interface.

---

## 4. User Story / Engineering Story

> As a system administrator, I want candidate records and CV JSON files ingested from a configured storage location, so that candidate data is reliably loaded into eTalent Search.

---

## 5. Scope

### In Scope
- `CandidateSourceAdapter` interface and file-based implementation `FileSystemCandidateSourceAdapter`.
- Parsing source metadata: `candidateId`, `firstName`, `lastName`, `availability`.
- Parsing CV JSON: `headline`, `summary`, `skills`, `experience`, `education`, `certifications`, `location`, `workPreference`, `updatedAt`.
- Rule: Source record fields take precedence over CV JSON fields in case of conflict.

### Out of Scope
- Direct database sync from external ATS
- Scanned PDF/Word document OCR

### Constraints
- Tolerant parser: requires `candidateId` and at least one of summary/skills/experience.
- English CVs only.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7

### Technical Requirements
- TR-036-01: Define `CandidateSourceAdapter` interface returning `Stream<CandidateRawRecord>`.
- TR-036-02: Implement `JsonFileCandidateSourceAdapter` reading configured directory path.
- TR-036-03: Implement conflict resolution giving source record authority over CV JSON.

---

## 7. Implementation Flow

1. Scan configured directory for candidate export JSON files.
2. Read and deserialize source metadata and CV JSON payloads.
3. Apply conflict resolution rules.
4. Return standardized `CandidateRawRecord` stream for pipeline processing.
5. Handle corrupted or invalid JSON files gracefully with detailed error logging.

---

## 8. Acceptance Criteria

- **AC-01:** Ingestion successfully parses valid candidate source JSON and CV JSON files.
- **AC-02:** Source fields (`availability`, names) override conflicting CV fields.
- **AC-03:** Malformed JSON files log structured errors without crashing the ingestion run.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit tests with valid, partial, and malformed candidate JSON files.
- Integration test reading directory of synthetic candidate files.

---

## 10. Deliverables

- Candidate source adapter classes
- CandidateRawRecord DTOs
- Directory reader configuration

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-001, ET-002, ET-004
- **Downstream Tickets:** ET-006, ET-007
- **Technical Risks & Mitigations:** Large files exhausting memory; mitigated by streaming JSON reader (Jackson streaming API).

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/5
- **Branch:** `feature/et-005-candidate-json-file-adapter`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
