---
ticket_id: ET-038
title: Configure Static Analysis, SonarQube, and Secret Scanning
publish: approval
priority: must
type: task
workstream: devops
owner_role: devops
---

# [ET-038] — Configure Static Analysis, SonarQube, and Secret Scanning

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-038 |
| **Title** | Configure Static Analysis, SonarQube, and Secret Scanning |
| **Project** | eTalent Search |
| **Workstream** | B. Infrastructure and DevOps |
| **Ticket Type** | Technical Task |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | DevOps Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | Security Rules, Engineering Workflow |

---

## 2. Objective

Integrate automated static code analysis, Spotbugs, SonarQube quality gate, and secret scanning into the CI pipeline.

---

## 3. Background and Context

Specification v1.0 Section 5, 8: Secrets must never be committed. The delivery workflow enforces the SonarQube quality gate on every PR into dev or main.

---

## 4. User Story / Engineering Story

> As a security and DevOps engineer, we need automated security and quality scanners in CI, so that vulnerabilities, code smells, and secret leaks are detected before merge.

---

## 5. Scope

### In Scope
- GitGuardian / Gitleaks secret scanning on every commit and PR.
- OWASP Dependency-Check plugin in Gradle flagging known CVEs.
- SonarQube / SonarCloud scanner integration enforcing quality gate (0 new bugs, 0 vulnerabilities, >80% coverage).
- SpotBugs / Checkstyle static analysis plugins in Gradle build.

### Out of Scope
- Third-party penetration testing

### Constraints
- Pipeline must fail if any hardcoded secret is detected.
- Zero critical CVEs allowed.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** Security Rules, Engineering Workflow

### Technical Requirements
- TR-069-01: Add OWASP Dependency-Check Gradle plugin.
- TR-069-02: Add SonarQube Gradle plugin and quality gate profile.
- TR-069-03: Configure Gitleaks pre-commit and CI scanning step.

---

## 7. Implementation Flow

1. CI pipeline executes Gitleaks secret scanning on commit diff.
2. Execute OWASP dependency check against third-party libraries.
3. Run SonarQube analysis capturing test coverage and static metrics.
4. Block PR merge if SonarQube quality gate fails.

---

## 8. Acceptance Criteria

- **AC-01:** Gitleaks scan fails if committed code contains simulated secret token.
- **AC-02:** SonarQube analysis executes and reports quality gate status on PR.
- **AC-03:** Dependency check flags critical CVEs in application dependencies.

---

## 9. Testing Requirements

### Required Test Coverage
- Test secret commit verifying immediate detection and pipeline blockage.
- Clean pipeline run confirming scanner passes on valid codebase.

---

## 10. Deliverables

- .gitleaks.toml configuration
- SonarQube Gradle configuration
- Security scanning workflow

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-034
- **Downstream Tickets:** ET-039
- **Technical Risks & Mitigations:** False positive CVE alerts blocking urgent fixes; mitigated by suppression file with documented justifications.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/38
- **Branch:** `feature/et-038-security-scanning-dependency-checks`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
