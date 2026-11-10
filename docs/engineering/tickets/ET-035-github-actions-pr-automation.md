---
ticket_id: ET-035
title: Configure GitHub Actions PR Automation and Reviewer Assignment
publish: approval
priority: must
type: task
workstream: devops
owner_role: devops
---

# [ET-035] — Configure GitHub Actions PR Automation and Reviewer Assignment

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-035 |
| **Title** | Configure GitHub Actions PR Automation and Reviewer Assignment |
| **Project** | eTalent Search |
| **Workstream** | B. Infrastructure and DevOps |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | DevOps Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Engineering Workflow |

---

## 2. Objective

Build GitHub Actions workflow to validate PR naming, enforce ticket references, and automatically request two reviewers.

---

## 3. Background and Context

Team Workflow requires: feature work goes into dev after CI passes and two reviewers approve it. PR titles must include `[ET-XXX]`, branch must match `feature/ET-XXX-*`, and two approvals are required.

---

## 4. User Story / Engineering Story

> As an engineering team, we need GitHub PR automation, so that branch naming, ticket traceability, and dual peer reviews are automatically enforced.

---

## 5. Scope

### In Scope
- Workflow `pr-validation.yml`: checks PR title format `[ET-XXX] Description` and branch name `feature/ET-XXX-*`.
- Workflow `reviewer-assignment.yml`: automatically requests 2 reviewers based on role/module.
- Enforce PR description template with test evidence and issue reference.
- Status check blocking merge if PR naming or ticket link is invalid.

### Out of Scope
- Auto-merging PRs without human approval

### Constraints
- Compatible with free-tier GitHub Actions.
- Requires 2 reviewer approvals.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Engineering Workflow

### Technical Requirements
- TR-066-01: Create `.github/workflows/pull-request-automation.yml`.
- TR-066-02: Create `.github/pull_request_template.md` requiring ticket link and test evidence.
- TR-066-03: Create `.github/workflows/reviewer-assignment.yml` requesting reviewers.

---

## 7. Implementation Flow

1. Developer opens PR against `dev`.
2. GitHub Actions validates title format `[ET-XXX]` and branch naming.
3. If valid, check passes; if invalid, bot posts guidance and fails check.
4. Automatically assign two eligible peer reviewers from codeowners/config.
5. Require 2 approvals before merge button is unlocked.

---

## 8. Acceptance Criteria

- **AC-01:** PRs with invalid titles (missing `[ET-XXX]`) fail automated validation check.
- **AC-02:** Opening a valid PR automatically requests two eligible reviewers.
- **AC-03:** Merge to `dev` is blocked until two independent approvals are recorded.

---

## 9. Testing Requirements

### Required Test Coverage
- Test PR with invalid title verifying check failure.
- Test PR with valid title verifying check pass and reviewer request.

---

## 10. Deliverables

- .github/workflows/pull-request-automation.yml
- .github/pull_request_template.md

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-001
- **Downstream Tickets:** ET-036, ET-039
- **Technical Risks & Mitigations:** Reviewer assignment pinging absent team members; mitigated by rotating team pool.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/35
- **Branch:** `feature/et-035-github-actions-pr-automation`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
