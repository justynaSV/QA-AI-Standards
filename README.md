# QA AI Standards Hub

Central hub for **AI usage standards in QA** across multiple projects.

This repository is intentionally lightweight.  
Detailed standards for specific areas are maintained in dedicated repositories:

- Postman standards: https://github.com/justynaSV/postman-testing
- Gherkin scenarios standards: https://github.com/justynaSV/gherkin-scenarios-tmp

---

## Purpose
This hub defines:
1. universal AI usage rules for QA,
2. minimum review and traceability requirements,
3. how to apply standards across different projects.

It does **not** replace project-specific testing strategy or domain-specific rules in individual project repositories.

---

## Repository contents
- `ai-usage-policy.md` — what is allowed/prohibited, risk approach, review responsibility
- `how-to-use-existing-repos.md` — integration model for Postman/Gherkin repos + project repos
- `templates/ai-output-review-checklist.md` — mandatory checklist before accepting AI-generated artifacts
- `templates/project-onboarding-template.md` — quick template for adopting this hub in any QA project

---

## How QA members should use this hub
For each QA task:

1. Follow rules from `ai-usage-policy.md`
2. Use the relevant specialized standard:
   - API/Postman work → `justynaSV/postman-testing`
   - BDD/Gherkin work → `justynaSV/gherkin-scenarios-tmp`
3. Apply domain-specific constraints from the current project repository
4. Complete `templates/ai-output-review-checklist.md` before accepting AI-assisted output

---

## Ownership
- Owner: QA team
- Suggested reviewers: QA Lead + designated QA standards maintainers
- Suggested review cadence: monthly (or when process/tooling changes)