# QA AI Standards Hub

Central hub for **AI usage standards in QA** across multiple projects.

This repository is intentionally lightweight.  
Detailed standards for specific areas are maintained in dedicated repositories:

- Postman testing standards: https://github.com/justynaSV/postman-testing
- Gherkin scenarios standards: https://github.com/justynaSV/gherkin-scenarios-tmp
- Playwright testing standards: https://github.com/justynaSV/playwright-testing (scaffold, conventions in progress)

---

## Purpose
This hub defines:
1. universal AI usage rules for QA,
2. minimum review and traceability requirements,
3. how to apply standards across different projects.

It does **not** replace project-specific testing strategy or domain-specific rules in individual project repositories.

---

## Repository contents
- `ai-usage-policy.md` — what is allowed/prohibited, risk approach, review responsibility, versioning/changelog
- `how-to-use-existing-repos.md` — integration model for Postman/Gherkin repos + project repos
- `glossary.md` — shared definitions of key terms used across this hub
- `templates/ai-output-review-checklist.md` — mandatory checklist before accepting AI-generated artifacts
- `templates/prompt-examples.md` — mini library of good/bad prompt examples for common QA tasks
- `skills/` — ready-to-use Claude Skills for common QA tasks (see [Skills](#skills) below)

---

## Skills

`skills/` contains ready-to-use Claude Skills for common QA tasks. Unlike `templates/prompt-examples.md`, these aren't copy-paste text — once saved, Claude applies them automatically when a task matches, without you having to open this repo and find the right prompt. They don't replace the standards above; every skill routes back to `ai-usage-policy.md` and `templates/ai-output-review-checklist.md` before its output is accepted.

- `skills/qa-boundary-case-generator` — generates boundary and negative test cases for a single field/parameter as a table (input, expected result, reasoning)
- `skills/qa-bug-report-rewriter` — restructures a bug report into Summary/Steps to Reproduce/Expected/Actual/Environment without adding unconfirmed claims
- `skills/qa-postman-assertion-reviewer` — reviews a Postman script against `postman-testing` conventions, flags missing checks without inventing endpoints or fields
- `skills/qa-ai-output-review-checklist-runner` — walks a specific AI-generated artifact through `templates/ai-output-review-checklist.md` item by item, leaving the final decision to the human reviewer

### Using a skill
1. Save it — open the skill's file and use "Save skill" (if your org allows skill creation), or place the `skills/<name>/` folder in a project's `.claude/skills/` directory if you're working in Claude Code.
2. Describe your task normally (e.g. "draft Gherkin scenarios for this AC: ...") — Claude checks the skill's description and applies it automatically when it matches. No skill-saving feature available? The `SKILL.md` is just markdown — paste its contents into your prompt directly.
3. Treat the output as a draft. It still needs `templates/ai-output-review-checklist.md` and the `AI-assisted: yes (scope: ...)` tag before it's accepted, per `ai-usage-policy.md`.

---

## How QA members should use this hub
For each QA task:

1. Follow rules from `ai-usage-policy.md`
2. Use the relevant specialized standard:
   - API/Postman work → `justynaSV/postman-testing`, or `skills/qa-postman-assertion-reviewer` for a quick script review
   - BDD/Gherkin work → `justynaSV/gherkin-scenarios-tmp` (or your project's copy of the `gherkin-scenarios` template) — use its built-in `gherkin-scenario-generator` skill / `/gherkin-scenarios` Copilot prompt to draft scenarios directly, no hub skill needed
   - Playwright test work → `justynaSV/playwright-testing`
3. Apply domain-specific constraints from the current project repository
4. Complete `templates/ai-output-review-checklist.md` before accepting AI-assisted output — or run `skills/qa-ai-output-review-checklist-runner` for an item-by-item pass

---

## Ownership
- Owner: QA team
- Suggested reviewers: QA Lead + designated QA standards maintainers
- Suggested review cadence: monthly (or when process/tooling changes)