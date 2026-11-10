---
ticket_id: ET-045
title: Implement Shortlist CSV Export Functionality
publish: auto
priority: nice
type: feature
workstream: qa
owner_role: developer
---

# [ET-045] — Implement Shortlist CSV Export Functionality

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-045 |
| **Title** | Implement Shortlist CSV Export Functionality |
| **Project** | eTalent Search |
| **Workstream** | H. Testing, Release & Optional |
| **Ticket Type** | Feature |
| **Priority** | Nice |
| **Publishing Mode** | auto |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-13 |

---

## 2. Objective

Build CSV export endpoint and UI download button allowing recruiters to export shortlisted candidates with scores and explanations.

---

## 3. Background and Context

Specification v1.0 FR-13: Export a shortlist as CSV. Classified as Nice priority (dropped first if time runs short).

---

## 4. User Story / Engineering Story

> As a recruiter, I want to export our candidate shortlist as a CSV file, so that I can share shortlist summaries with external hiring managers.

---

## 5. Scope

### In Scope
- Endpoint `GET /api/vacancies/{id}/shortlist/export.csv` generating formatted CSV.
- Columns: Rank, Full Name, Current Title, Total Score, Required Skills Match, Experience Score, Availability, Top Reason.
- UI 'Export CSV' button on Shortlist tab.
- Proper CSV quoting handling commas, newlines, and quotes in candidate descriptions.

### Out of Scope
- PDF report export
- Customizable column selection

### Constraints
- Export restricted to authenticated recruiters/admins.
- Clean RFC 4180 CSV formatting.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-13

### Technical Requirements
- TR-076-01: Implement `CsvExportService` using OpenCSV or Apache Commons CSV.
- TR-076-02: Add CSV download action in Angular `ShortlistTabComponent`.
- TR-076-03: Set HTTP response headers: `Content-Type: text/csv` and `Content-Disposition`.

---

## 7. Implementation Flow

1. Recruiter opens Shortlist tab on a vacancy.
2. Recruiter clicks 'Export Shortlist CSV'.
3. Browser downloads `shortlist-[vacancy-title]-[date].csv`.
4. File opens cleanly in Excel / Google Sheets with proper column formatting.

---

## 8. Acceptance Criteria

- **AC-01:** Clicking 'Export CSV' downloads valid CSV containing all shortlisted candidates.
- **AC-02:** CSV data includes rank, name, total score, factor breakdown, and explanation summary.
- **AC-03:** Special characters (commas, quotes) are properly escaped according to RFC 4180.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit test verifying CSV generator escaping and column alignment.
- Integration test downloading CSV for sample vacancy shortlist.

---

## 10. Deliverables

- CsvExportService
- Shortlist CSV export endpoint
- UI download trigger

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-023, ET-030
- **Downstream Tickets:** ET-047
- **Technical Risks & Mitigations:** CSV injection vulnerability (cells starting with `=`); mitigated by prepending `'` to formula triggers.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/45
- **Branch:** `feature/et-045-csv-export-shortlist`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
