# [ET-070] — Configure GitHub Rulesets and Release Promotion Workflow

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-070 |
| **Title** | Configure GitHub Rulesets and Release Promotion Workflow |
| **Project** | eTalent Search |
| **Workstream** | B. Infrastructure and DevOps |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | DevOps Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Engineering Workflow |
| **GitHub Labels** | stream:devops, type:infrastructure, priority:must, role:devops |

---

## 2. Objective

Configure GitHub repository rulesets for dev and main branches, and establish the two-maintainer release promotion workflow.

---

## 3. Background and Context

Workflow Document Section 4, 5: dev is shared integration branch; main holds release code. Feature PRs merge into dev after 2 approvals. Release PR promotes dev to main after release CI, approved by maintainers with merge commits.

---

## 4. User Story / Engineering Story

> As a lead architect and release manager, we need strict GitHub branch rulesets, so that unauthorized merges are prevented and release promotions follow our governance standard.

---

## 5. Scope

### In Scope
- Branch ruleset for `dev`: require PR, require 2 approvals, require passing CI checks, require up-to-date branch, block force pushes.
- Branch ruleset for `main`: require PR from `dev` only, require passing release CI, restrict merge permissions to designated maintainers team.
- Release PR template `.github/PULL_REQUEST_TEMPLATE/release.md` listing included tickets with `Closes #XXX` references.
- Automation script verifying release PR conforms to promotion checklist.

### Out of Scope
- Automated semantic release version tagging

### Constraints
- Only two designated maintainers can merge to main.
- Merge commits mandated on main to preserve history.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Engineering Workflow

### Technical Requirements
- TR-070-01: Define GitHub ruleset configurations for `dev` and `main`.
- TR-070-02: Create `.github/PULL_REQUEST_TEMPLATE/release.md`.
- TR-070-03: Configure branch restriction ensuring only `dev` can be merged into `main`.

---

## 7. Implementation Flow

1. Feature branches merge into `dev` after 2 approvals and passing CI.
2. Release manager opens Release PR from `dev` into `main`.
3. Release PR lists all resolved tickets (`Closes #42`, etc.).
4. Release CI executes full integration and smoke test suite.
5. Designated maintainer executes merge commit; GitHub automatically closes linked issues to `Done`.

---

## 8. Acceptance Criteria

- **AC-01:** Direct pushes to `dev` and `main` are blocked by rulesets.
- **AC-02:** Merging to `main` is restricted to authorized maintainers team only.
- **AC-03:** Merging release PR to `main` automatically closes linked GitHub issues.

---

## 9. Testing Requirements

### Required Test Coverage
- Attempt direct push to `dev` verifying rejection.
- Attempt merge by non-maintainer to `main` verifying rejection.

---

## 10. Deliverables

- GitHub ruleset configuration export
- Release PR template
- Release promotion runbook

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-066, ET-067
- **Downstream Tickets:** ET-078
- **Technical Risks & Mitigations:** Accidental squash-merge to main destroying dev branch history; mitigated by ruleset requiring merge commits.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/39
- **Branch:** `feature/et-070-github-branch-rulesets-release-pr`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
