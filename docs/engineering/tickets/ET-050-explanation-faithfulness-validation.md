# [ET-050] — Build Explanation Faithfulness and Evidence Validation

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-050 |
| **Title** | Build Explanation Faithfulness and Evidence Validation |
| **Project** | eTalent Search |
| **Workstream** | E. Scoring and Ranking Engine |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-4, Security and Privacy Rules |
| **GitHub Labels** | stream:backend, stream:ai, type:feature, priority:must, role:developer |

---

## 2. Objective

Build automated validation step verifying that AI-generated explanation evidence statements trace directly to real candidate profile fields.

---

## 3. Background and Context

Specification v1.0 Section 8 & 9: Explanation evidence must trace to a real profile field; a validation step checks it. Explanation faithfulness target is >= 95% of spot-checked evidence statements tracing to the profile.

---

## 4. User Story / Engineering Story

> As a quality assurance engineer and recruiter, I want AI explanations verified against actual candidate profile text, so that recruiters are never misled by AI hallucinations.

---

## 5. Scope

### In Scope
- Implement `EvidenceValidator` checking cited evidence substrings or entities against raw candidate CV text.
- Fuzzy substring and token containment matching to verify cited skills, roles, and dates exist in profile.
- Flagging hallucinated or un-grounded statements: if verification fails, replace with generic factual summary.
- Metrics emission: calculate and log faithfulness score per ranking run.

### Out of Scope
- Manual human spot-checking UI

### Constraints
- Validation check must execute in < 10ms per candidate.
- Faithfulness threshold >= 95%.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-4, Security and Privacy Rules

### Technical Requirements
- TR-050-01: Implement `EvidenceValidator` using token-set ratio or string containment.
- TR-050-02: Log warning when cited evidence does not match candidate source text.
- TR-050-03: Sanitize explanation replacing ungrounded claims with 'Evidence from profile'.

---

## 7. Implementation Flow

1. Extract cited evidence phrases from LLM factor evaluation response.
2. Search candidate profile fields for evidence occurrence.
3. If match score >= threshold, mark evidence as VERIFIED.
4. If ungrounded, flag record and sanitize explanation text.
5. Emit faithfulness metric.

---

## 8. Acceptance Criteria

- **AC-01:** Evidence validator verifies >= 95% of accurate evidence statements in sample set.
- **AC-02:** Fabricated evidence (injected in test) is detected and flagged.
- **AC-03:** Explanations never contain unsupported claims or numbers.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit tests with 30 ground-truth candidate profiles and deliberate hallucination injections.
- Metric verification test confirming faithfulness metric calculation.

---

## 10. Deliverables

- EvidenceValidator class
- FaithfulnessMetricsCollector
- Validation test suite

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-043, ET-047
- **Downstream Tickets:** ET-049, ET-074
- **Technical Risks & Mitigations:** Minor wording variations flagged as hallucinations; mitigated by token-overlap and fuzzy substring matching.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/19
- **Branch:** `feature/et-050-explanation-faithfulness-validation`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
