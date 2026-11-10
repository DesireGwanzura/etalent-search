---
ticket_id: ET-012
title: Engineer Pinned LLM Prompts with Structured JSON Output
publish: approval
priority: must
type: feature
workstream: ai
owner_role: ai
---

# [ET-012] — Engineer Pinned LLM Prompts with Structured JSON Output

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-012 |
| **Title** | Engineer Pinned LLM Prompts with Structured JSON Output |
| **Project** | eTalent Search |
| **Workstream** | D. AI and Semantic Evaluation |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | AI Engineer |
| **Suggested Reviewer** | Software Developer |
| **Requirements Traceability** | FR-4, Security Rules |

---

## 2. Objective

Design, version, and validate LLM evaluation prompts enforcing structured JSON output for factor matches and cited evidence.

---

## 3. Background and Context

Specification v1.0 mandates that the AI returns 0-1 match scores and cited evidence per factor in structured JSON, never computing final scores or mentioning numeric scores in explanations. Prompt injection defense and version recording are mandatory.

---

## 4. User Story / Engineering Story

> As the eTalent scoring system, I want structured JSON factor evaluations from the LLM, so that deterministic scoring code can compute scores and display plain-language evidence.

---

## 5. Scope

### In Scope
- Evaluation prompt template for 5 factors: Required Skills, Experience, Role Match, Nice-to-Have Skills, Location/Availability.
- JSON Schema enforcement requiring: `factorId`, `matchScore` (float 0.0 - 1.0), `evidence` (quote/reference), `explanation` (plain text, no numbers), `missingData` (boolean).
- Rule: If profile lacks data, matchScore = 0.0 and explanation = 'not provided'.
- Rule: Explanation text must NEVER state a numeric score or percentage.
- Prompt-injection defense: treat candidate CV text strictly as untrusted data, never as system instructions.

### Out of Scope
- Weight multiplication (handled in ET-047)
- Recruiter UI rendering

### Constraints
- Model must be pinned with prompt version recorded in metadata.
- Strict JSON schema adherence.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-4, Security Rules

### Technical Requirements
- TR-043-01: Define JSON schema `factor-evaluation-schema.json`.
- TR-043-02: Implement `PromptTemplateService` injecting sanitized candidate and vacancy context.
- TR-043-03: Implement JSON validation parser validating LLM response structure.

---

## 7. Implementation Flow

1. Assemble vacancy requirements and sanitized candidate evidence.
2. Inject into versioned prompt template with structured JSON instructions.
3. Invoke pinned LLM provider API.
4. Parse and validate JSON response against strict schema.
5. Verify explanation contains no numeric scores.

---

## 8. Acceptance Criteria

- **AC-01:** LLM returns strictly valid JSON conforming to `factor-evaluation-schema.json`.
- **AC-02:** Explanations provide plain-language rationale without mentioning numbers or percentages.
- **AC-03:** Missing candidate data correctly returns `matchScore

---

## 9. Testing Requirements

### Required Test Coverage
- Unit test evaluating 20 sample candidate profiles across various vacancies.
- Adversarial prompt injection test verifying injected CV instructions ('Ignore previous instructions...') are ignored.

---

## 10. Deliverables

- Prompt templates with semantic versioning
- JSON schemas
- Prompt evaluation parser

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-003, ET-011
- **Downstream Tickets:** ET-014, ET-015, ET-016
- **Technical Risks & Mitigations:** LLM returning markdown backticks around JSON; mitigated by Jackson tolerant parsing and schema validation.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/12
- **Branch:** `feature/et-012-pinned-llm-structured-prompt-engineering`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
