---
ticket_id: ET-036
title: Implement GitHub to GitLab Mirroring and Webhook Sync
publish: approval
priority: must
type: task
workstream: devops
owner_role: devops
---

# [ET-036] — Implement GitHub to GitLab Mirroring and Webhook Sync

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-036 |
| **Title** | Implement GitHub to GitLab Mirroring and Webhook Sync |
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

Configure automated repository mirroring and push event synchronization between GitHub (primary) and GitLab (CI execution).

---

## 3. Background and Context

The team delivery model uses GitHub as single source of truth for code and issues, with GitLab executing CI/CD. Push events on GitHub must instantly mirror to GitLab to trigger CI pipelines.

---

## 4. User Story / Engineering Story

> As a DevOps engineer, we need automated GitHub-to-GitLab mirror synchronization, so that commits pushed to GitHub immediately trigger GitLab CI pipelines.

---

## 5. Scope

### In Scope
- GitHub Actions workflow `.github/workflows/gitlab-mirror.yml` pushing branches and tags to GitLab mirror.
- Webhook / deploy key configuration between GitHub and GitLab.
- Mirror verification script `verify_mirror.py` checking commit hash synchronization.
- Documentation on mirror troubleshooting and manual sync procedures.

### Out of Scope
- Bidirectional mirror (GitLab commits are prohibited; GitHub is single source of truth)

### Constraints
- One-way mirror: GitHub -> GitLab only.
- Sync latency under 30 seconds.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Engineering Workflow

### Technical Requirements
- TR-067-01: Create `.github/workflows/gitlab-mirror.yml` triggered on `push`.
- TR-067-02: Configure `GITLAB_SSH_PRIVATE_KEY` secret in GitHub repository settings.
- TR-067-03: Implement mirror verification script in `scripts/repository-management/`.

---

## 7. Implementation Flow

1. Developer pushes commit to GitHub branch.
2. GitHub Actions mirror workflow executes `git push --mirror` to GitLab.
3. GitLab receives push event and immediately triggers CI/CD pipeline.
4. Pipeline results post back to GitHub commit status API.

---

## 8. Acceptance Criteria

- **AC-01:** Commits pushed to GitHub appear on GitLab mirror within 30 seconds.
- **AC-02:** New feature branches created on GitHub are automatically created on GitLab.
- **AC-03:** Mirror sync script verifies commit hash alignment between repositories.

---

## 9. Testing Requirements

### Required Test Coverage
- Push test commit to test branch and verify GitLab pipeline starts automatically.
- Verification script execution confirming branch and tag alignment.

---

## 10. Deliverables

- .github/workflows/gitlab-mirror.yml
- Mirror sync script
- Runbook documentation

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-034
- **Downstream Tickets:** ET-039
- **Technical Risks & Mitigations:** GitHub Actions secrets misconfiguration breaking mirror; mitigated by runbook and health check alert.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/36
- **Branch:** `feature/et-036-github-gitlab-mirror-sync`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
