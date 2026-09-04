# How to Use Existing QA Standards Repositories

This hub integrates with existing specialized standards repositories.

## Sources of truth

## 1) Postman/API testing standards
Repository: https://github.com/justynaSV/postman-testing  
Description: Guideline and standards of creating test scripts in Postman.

Use when:
- creating/updating Postman test scripts,
- defining API assertions,
- reviewing API test quality patterns.

## 2) Gherkin/BDD standards
Repository: https://github.com/justynaSV/gherkin-scenarios-tmp

Use when:
- drafting/refining Gherkin scenarios,
- validating Given/When/Then quality,
- improving scenario readability and consistency.

## 3) Playwright testing standards
Repository: https://github.com/justynaSV/playwright-testing  
Description: Conventions for writing Playwright tests consistently across the team. Currently a scaffold — conventions/examples are being added incrementally.

Use when:
- writing/reviewing Playwright test specs,
- deciding on locator strategy, POM/fixtures structure, or tagging conventions.

## 4) Test case generation standards
Repository: https://github.com/justynaSV/test-cases-generator  
Description: Generates test case scenarios in an established style, directly as Azure DevOps-import-ready CSV. Ships its own AI mechanism — a `/generate-test-case` slash-command for both GitHub Copilot Chat and Claude Code — that interviews you for the missing details, generates against the repo's own style guide/examples, and validates the result.

Use when:
- drafting new test case scenarios for import into Azure DevOps,
- needing scenarios that match an established style guide and curated examples.

---

## Integration model (what lives where)

## Central hub (`qa-ai-standards`)
Contains:
- universal AI QA policy,
- review and traceability minimum,
- prompt examples and glossary for cross-project usage,
- `skills/` — reusable AI Skills for cross-cutting QA tasks and for craft repos that don't have their own AI mechanism yet.

## Specialized standards repos (`postman-testing`, `gherkin-scenarios-tmp`, `playwright-testing`, `test-cases-generator`)
Contain:
- craft-specific standards,
- examples and conventions for that testing style,
- where applicable, their own AI mechanism (Copilot prompt under `.github/prompts/` or equivalent) built with direct knowledge of that repo's real structure, scripts, and conventions. `gherkin-scenarios` (and its project copies) is the current example — see below.

## Project repositories (team/product-specific)
Contain:
- domain/business specifics,
- environment constraints,
- project-level test strategy and priorities.

---

## Where should an AI skill live?

Skills are executable, not just reference text — once saved, Claude applies them automatically instead of a person having to remember and paste a prompt. That makes *where* a skill lives matter more than where a static doc lives: a skill is only as good as its access to the actual project it's operating on.

1. **The project/craft repo already has its own AI mechanism** (a Claude Skill, a Copilot prompt, or equivalent) — use that, not a hub skill. It will always outperform a generic hub skill, because it has context a hub skill can't: real module folders, real npm scripts, real save paths. Example: `gherkin-scenarios` and its project copies (including `gherkin-scenarios-tmp`) ship `/gherkin-scenarios` (Copilot) — use that directly. Same for `test-cases-generator`, which ships `/generate-test-case` (Copilot and Claude Code).
2. **The craft repo has no AI mechanism of its own** — either the task doesn't need project-specific context (e.g. reviewing a standalone Postman script against `postman-testing` conventions), or the repo is still a scaffold (e.g. `playwright-testing`) — a hub skill in `skills/` is the right home, until the specialized repo builds its own.
3. **The task is cross-cutting QA process, not tied to any one craft repo** (rewriting a bug report, running the AI output review checklist) — this belongs in the hub permanently. There's no more-specific repo for it to move to.

When a specialized repo builds its own mechanism for something the hub currently covers, retire or narrow the hub skill's description rather than keeping both — two skills that could plausibly trigger for the same task just creates ambiguity about which one should.

---

## Working order for QA members (mandatory sequence)
For any QA task:

1. Read central AI policy (this hub)
2. Apply relevant specialized standard:
   - Postman/API → `justynaSV/postman-testing`
   - BDD/Gherkin → `justynaSV/gherkin-scenarios-tmp`
   - Playwright → `justynaSV/playwright-testing`
   - Test case generation → `justynaSV/test-cases-generator`
3. Apply the current project’s own constraints
4. Validate with AI output checklist before finalizing

---

## Change management recommendation
- Keep universal rules only in this hub.
- Keep technical standards in specialized repos.
- Avoid duplicating the same standards text in multiple places.
- In this hub, link to specialized repos instead of copying content.