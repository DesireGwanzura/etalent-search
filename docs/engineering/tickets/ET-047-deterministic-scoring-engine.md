# [ET-047] — Build Deterministic Factor Scoring Engine

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-047 |
| **Title** | Build Deterministic Factor Scoring Engine |
| **Project** | eTalent Search |
| **Workstream** | E. Scoring and Ranking Engine |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-2, FR-4, FR-14, Scoring Rules |
| **GitHub Labels** | stream:backend, type:feature, priority:must, role:developer |

---

## 2. Objective

Implement deterministic application logic to calculate candidate scores from AI factor match values and configurable factor weights.

---

## 3. Background and Context

Specification v1.0 Section 6: The AI returns a 0-1 match plus cited evidence per factor; deterministic code multiplies by weights, sums, sorts, and breaks ties by required skills. The AI NEVER computes a score.

---

## 4. User Story / Engineering Story

> As the eTalent system, I want deterministic code to calculate candidate scores from factor weights and AI evaluations, so that scoring is 100% reproducible and transparent.

---

## 5. Scope

### In Scope
- Five job-related scoring factors: Required Skills (default 40), Experience (25), Role Match (15), Nice-to-have Skills (10), Location/Availability (10).
- Deterministic formula: `CandidateScore = Sum(Weight_i * MatchScore_i) / Sum(Weights)` normalized to 100.
- Weight normalization: total weights must sum to 100; weight 0 switches a factor off.
- Blank factor rule: vacancy factor left blank spreads its weight proportionally across remaining factors.
- Missing candidate data rule: missing factor scores 0 and explanation states 'not provided'.
- Missing required skill: does NOT cap the total score in release 1 (show all, sorted).

### Out of Scope
- AI model invocation
- UI slider controls

### Constraints
- Scoring must be 100% deterministic (same inputs = exact same score).
- AI never computes score.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-2, FR-4, FR-14, Scoring Rules

### Technical Requirements
- TR-047-01: Implement `DeterministicScoringService` with exact floating-point / BigDecimal arithmetic.
- TR-047-02: Implement proportional weight redistribution for blank vacancy factors.
- TR-047-03: Validate that factor weights contain only the five approved factors.

---

## 7. Implementation Flow

1. Validate and normalize vacancy factor weights.
2. If a vacancy factor is blank, redistribute its weight proportionally.
3. For each candidate, multiply factor match scores (0.0 - 1.0) by normalized weights.
4. Sum weighted scores to compute total score (0 to 100 rounded to 1 decimal place).
5. Attach factor breakdown and explanations to candidate score record.

---

## 8. Acceptance Criteria

- **AC-01:** Deterministic calculation matches manual calculation across all test factor inputs.
- **AC-02:** Blank vacancy factor spreads weight proportionally across other factors.
- **AC-03:** Missing candidate data yields 0 for that factor with 'not provided' explanation.

---

## 9. Testing Requirements

### Required Test Coverage
- Parameterized unit tests verifying calculation across 100+ score/weight combinations.
- Test verifying weight redistribution when 1 or 2 vacancy factors are empty.

---

## 10. Deliverables

- DeterministicScoringService
- WeightNormalizer class
- ScoreCalculation DTOs

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-032, ET-043
- **Downstream Tickets:** ET-048, ET-049, ET-050
- **Technical Risks & Mitigations:** Floating-point precision rounding discrepancies; mitigated by standard `BigDecimal` rounding mode `HALF_UP`.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/16
- **Branch:** `feature/et-047-deterministic-scoring-engine`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
