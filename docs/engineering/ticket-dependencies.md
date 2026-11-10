# eTalent Search — Ticket Dependency Graph & Execution Flow

**Standard:** Team Engineering Ticket Standard (TETS) v1.0  
**Project:** eTalent Search  
**Authoritative Specification:** eTalent Search Project Specification v1.0  
**Repository:** [DesireGwanzura/etalent-search](https://github.com/DesireGwanzura/etalent-search)  

---

## 1. Architectural Dependency Flowchart

The following dependency graph maps the critical path across all 47 engineering tickets:

```mermaid
flowchart TD
    subgraph Foundation ["Workstream A: Foundation & Architecture"]
        ET032["ET-032: Project Structure & Gradle"] --> ET033["ET-033: PostgreSQL + pgvector"]
        ET032 --> ET034["ET-034: AI Provider Interfaces"]
        ET032 --> ET035["ET-035: Synthetic Data Generator"]
    end

    subgraph DevOps ["Workstream B: DevOps & CI/CD"]
        ET032 --> ET065["ET-065: GitLab CI/CD Pipeline"]
        ET065 --> ET066["ET-066: GitHub PR Automation"]
        ET065 --> ET067["ET-067: GitHub-GitLab Mirror"]
        ET032 --> ET068["ET-068: Multi-Stage Dockerfile"]
        ET065 --> ET069["ET-069: Static Analysis & Scanners"]
        ET066 & ET067 & ET069 --> ET070["ET-070: GitHub Rulesets & Promotion"]
    end

    subgraph Ingestion ["Workstream C: Candidate Ingestion"]
        ET033 & ET035 --> ET036["ET-036: Candidate File Adapter"]
        ET036 --> ET037["ET-037: Privacy Scrubber & Allowlist"]
        ET034 & ET037 & ET033 --> ET038["ET-038: Extraction & Embeddings"]
        ET038 --> ET039["ET-039: Sync & Mass-Deletion Guard"]
        ET039 --> ET040["ET-040: Sync Status & Audit"]
        ET038 --> ET041["ET-041: Re-processing Trigger"]
    end

    subgraph AI ["Workstream D: AI & Semantic Evaluation"]
        ET034 & ET035 --> ET042["ET-042: AI Feasibility Spike (Early)"]
        ET042 --> ET043["ET-043: Structured JSON Prompts"]
        ET038 & ET042 --> ET044["ET-044: pgvector Semantic Retrieval"]
        ET043 & ET044 --> ET045["ET-045: Parallel Evaluation Orchestrator"]
        ET045 --> ET046["ET-046: AI Fallback & Degraded Mode"]
    end

    subgraph Scoring ["Workstream E: Scoring & Ranking Engine"]
        ET043 & ET045 --> ET047["ET-047: Deterministic Scoring Engine"]
        ET047 --> ET048["ET-048: Tie-Breaking & Instant Re-ranking"]
        ET033 & ET048 --> ET049["ET-049: Ranking Snapshots"]
        ET043 & ET047 --> ET050["ET-050: Faithfulness Validation"]
    end

    subgraph Backend ["Workstream F: Backend & Security"]
        ET032 & ET033 --> ET051["ET-051: Spring Security & RBAC"]
        ET051 & ET047 --> ET052["ET-052: Vacancy Management REST API"]
        ET049 & ET051 & ET052 --> ET053["ET-053: Ranking & Profile Query REST API"]
        ET049 & ET052 --> ET054["ET-054: Shortlist REST API"]
        ET051 --> ET055["ET-055: Admin User & Defaults API"]
        ET051 --> ET056["ET-056: Audit Logging Interceptor"]
    end

    subgraph Frontend ["Workstream G: Frontend Angular SPA"]
        ET032 --> ET057["ET-057: Angular 17+ SPA Setup"]
        ET051 & ET057 --> ET064["ET-064: Auth Login & App Shell"]
        ET052 & ET057 --> ET058["ET-058: Vacancy Creation & Weights UI"]
        ET053 & ET057 --> ET059["ET-059: Ranked Results List"]
        ET053 & ET059 --> ET060["ET-060: Candidate Profile Drawer"]
        ET054 & ET059 --> ET061["ET-061: Shortlist Action View"]
        ET052 & ET057 --> ET062["ET-062: Past Vacancies Archive"]
        ET040 & ET055 & ET056 & ET057 --> ET063["ET-063: Admin Console"]
    end

    subgraph TestingRelease ["Workstream H: Testing, Release & Optional"]
        ET033 & ET035 --> ET071["ET-071: Testcontainers Suite"]
        ET032 --> ET072["ET-072: POPIA Compliance Gate R1"]
        ET035 & ET047 & ET071 --> ET073["ET-073: Consistency & Overlap Tests"]
        ET037 & ET043 & ET051 --> ET074["ET-074: Adversarial & Security Tests"]
        ET053 & ET059 --> ET075["ET-075: Location & Availability Filters"]
        ET054 & ET061 --> ET076["ET-076: Shortlist CSV Export"]
        ET049 & ET059 --> ET077["ET-077: Mark Not Relevant"]
        ET070 & ET071 & ET072 & ET073 & ET074 --> ET078["ET-078: E2E Release 1 Readiness Gate"]
    end
```

---

## 2. Release Gates & Special Dependencies

### Gate 1: Early AI Feasibility Spike (`ET-042`)
- **Requirement:** Must execute early in Sprint 1 on the 1,000-candidate synthetic scale set.
- **Purpose:** Empirically measures top-5 overlap (target: 4 of 5), end-to-end latency (target: <= 60s), token costs, and regex scrubber residue.
- **Impact:** Informs candidate cap K, concurrency semaphore settings, and validates the 4-week delivery timeline before deep UI/scoring implementation.

### Gate 2: Legal POPIA Compliance Gate (`ET-072` / Gate R1)
- **External Dependency:** Formal legal review of candidate data reuse basis and AI provider terms (DPA, no model training, known geographical processing location).
- **Decoupled Architecture:** Gate R1 is a **launch gate for real candidate data**, NOT a development blocker. The entire development, testing, and CI pipeline executes against synthetic datasets (`APP_DATA_MODE=SYNTHETIC`) generated in `ET-035`.

### Gate 3: Release 1 Promotion Gate (`ET-070` & `ET-078`)
- **Ruleset Constraint:** Merging from integration branch `dev` into `main` requires passing Release CI (Testcontainers, quality gate, consistency tests) and approval from both designated maintainers.
- **Promotion Checklist:** 100% of Must functional requirements satisfied; <= 60s full ranking latency verified; >= 95% explanation faithfulness achieved.
