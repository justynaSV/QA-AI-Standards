# AI Usage Policy for QA Team

**Version:** 1.2
**Last updated:** 2026-08-17

## Changelog
| Version | Date | Change |
|---|---|---|
| 1.2 | 2026-08-17 | Cross-referenced `skills/`; clarified that the review requirement applies to skill-produced output the same as ad-hoc prompting |
| 1.1 | 2026-08-07 | Removed onboarding template reference; added glossary and prompt examples links |
| 1.0 | — | Initial policy: allowed/prohibited usage, review requirement, risk escalation, traceability, data handling |

## 1. Core principle
AI is an assistant, not an approver.  
**Human QA is always accountable** for final artifacts, decisions, and release impact.

## 2. Allowed usage
AI may be used for:
- drafting test scenarios (Gherkin),
- improving clarity of test cases,
- generating candidate negative/boundary cases,
- improving bug report wording,

## 3. Prohibited usage
AI must not be used to:
- make autonomous go/no-go release decisions,
- bypass required QA review,
- process secrets or sensitive production/customer data in prompts,
- fabricate test execution evidence.

## 4. Minimum review requirement (mandatory)
Before accepting AI-assisted output:
- verify factual correctness against requirements,
- verify expected results are testable,
- verify coverage includes happy path + negative/boundary where relevant,
- verify no ambiguous or non-actionable steps remain.

Use: `templates/ai-output-review-checklist.md`.

This requirement applies regardless of how the output was produced — a one-off prompt or a saved skill from `skills/`. A skill makes the *input* consistent; it does not change the review obligation.

## 5. Risk-based escalation
- Low impact (formatting/rewording): self-review may be enough.
- Medium impact (new test scenarios/assertions): peer QA review required.
- High impact (release-signoff influencing content): QA Lead review required.

## 6. Traceability requirement
For AI-assisted artifacts, add a note in ticket/PR/test documentation:

`AI-assisted: yes (scope: <short scope>)`

Examples of scope:
- scenario draft
- assertion proposal
- wording improvement
- edge-case suggestion

## 7. Data handling
Never include in prompts:
- credentials, tokens, API secrets,
- personal/customer-sensitive data,
- confidential production payloads.

Use masked/anonymized examples whenever context is needed.

## 8. Related resources
- Terminology used in this policy: `glossary.md`
- Example prompts for common QA tasks: `templates/prompt-examples.md`
- Ready-to-use Skills that apply this policy automatically for common QA tasks: `skills/` — see the root `README.md` for what each one does and how to use it. Skills for a craft area that has its own project-embedded AI mechanism (e.g. Gherkin's `gherkin-scenario-generator`) live in that project's repo instead — see `how-to-use-existing-repos.md`.