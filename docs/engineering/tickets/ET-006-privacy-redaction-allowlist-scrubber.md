---
ticket_id: ET-006
title: Build Privacy Redaction and Allowlist Scrubber
publish: approval
priority: must
type: feature
workstream: data
owner_role: developer
---

# [ET-006] — Build Privacy Redaction and Allowlist Scrubber

## 1. Ticket Information

| Field | Value |
| :--- | :--- |
| **Ticket ID** | ET-006 |
| **Title** | Build Privacy Redaction and Allowlist Scrubber |
| **Project** | eTalent Search |
| **Workstream** | C. Candidate Data Ingestion |
| **Ticket Type** | Feature |
| **Priority** | Must |
| **Publishing Mode** | approval |
| **Status** | Ready |
| **Suggested Owner** | Software Developer |
| **Suggested Reviewer** | AI Engineer |
| **Requirements Traceability** | FR-7, Privacy Rules |

---

## 2. Objective

Implement the strict privacy allowlist and text scrubber to ensure no PII or protected characteristics are sent to external AI services.

---

## 3. Background and Context

Specification v1.0 mandates a strict default-deny privacy allowlist. Names, contacts, IDs, DOB, protected attributes, full addresses, company names, and education years must NEVER be sent to AI services.

---

## 4. User Story / Engineering Story

> As a compliance officer and engineering team, we need a default-deny privacy scrubber, so that personal identifiers are stripped before payloads reach AI services.

---

## 5. Scope

### In Scope
- Strict allowlist filter allowing only: headline, skills, certifications, summary, job titles, dates, descriptions, qualification, institution, city/region/country, work preference, availability, opaque ID.
- Regex scrubbing for emails, telephone numbers, national ID patterns, and URLs in free text.
- Replacement of candidate's actual name in text with `[CANDIDATE]` placeholder.
- Masking of company names in experience records prior to AI transmission.

### Out of Scope
- Legal POPIA documentation (handled in ET-072)
- Real-time recruiter UI masking

### Constraints
- Zero PII leakage to AI provider.
- Must run entirely in-process before any AI network call.

---

## 6. Functional and Technical Requirements

### Functional Requirements
- **Traceability:** FR-7, Privacy Rules

### Technical Requirements
- TR-037-01: Implement `PrivacyScrubber` component with compiled regex patterns for PII.
- TR-037-02: Implement `AiPayloadFilter` mapping raw candidate data to `SanitizedAiCandidateProfile`.
- TR-037-03: Implement payload interception audit test verifying zero forbidden fields.

---

## 7. Implementation Flow

1. Receive raw candidate profile.
2. Extract candidate first and last names for exact-match scrubbing.
3. Apply regex pattern replacements for emails, phone numbers, and IDs.
4. Map only allowlisted fields to `SanitizedAiCandidateProfile`.
5. Assign opaque surrogate UUID for AI interaction.

---

## 8. Acceptance Criteria

- **AC-01:** Candidate names, phone numbers, email addresses, and national IDs are scrubbed from text.
- **AC-02:** Company names and graduation years are excluded from outgoing AI payloads.
- **AC-03:** Opaque surrogate ID is used for AI calls; real candidate ID is never transmitted.

---

## 9. Testing Requirements

### Required Test Coverage
- Unit tests with 50+ adversarial text inputs containing emails, phone numbers, and hidden PII.
- Payload interception test verifying outgoing AI JSON conforms strictly to allowlist.

---

## 10. Deliverables

- PrivacyScrubber class
- SanitizedAiCandidateProfile DTO
- Regex rule definitions

---

## 11. Dependencies and Risks

- **Upstream Dependencies:** ET-005
- **Downstream Tickets:** ET-007, ET-012
- **Technical Risks & Mitigations:** Obfuscated PII slipping through regex; mitigated by multi-pass scrubbing and benchmark evaluation.

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

- **GitHub Issue:** https://github.com/DesireGwanzura/etalent-search/issues/6
- **Branch:** `feature/et-006-privacy-redaction-allowlist-scrubber`
- **Pull Request:** `[Link to PR]`
- **GitLab Pipeline:** `[Link to Pipeline]`
- **Test Results:** `[Pass / Fail summary]`

---

## 14. Completion Notes

*Record implementation decisions, deviations, and operational notes upon ticket closure.*
