# Glossary

Shared definitions of terms used across this hub and its specialized standards repos.

| Term | Definition |
|---|---|
| **AI-assisted** | An artifact (test case, scenario, bug report, script, etc.) that was drafted or modified with help from an AI tool, then reviewed by a human QA. Marked with `AI-assisted: yes (scope: <short scope>)`. |
| **Scope (traceability)** | Short description of what part of the artifact AI contributed to, e.g. `scenario draft`, `assertion proposal`, `wording improvement`, `edge-case suggestion`. |
| **Risk tier** | Classification of an AI-assisted change by potential impact: **Low** (formatting/rewording), **Medium** (new test scenarios/assertions), **High** (release-signoff influencing content). Determines required review level. |
| **Human accountability** | Principle that a human QA remains responsible for any AI-assisted output, regardless of how it was generated. AI cannot approve its own output. |
| **Go/no-go decision** | The release sign-off decision. Must always be made by a human; AI must never make this decision autonomously. |
| **Sensitive data (prompt context)** | Credentials, tokens, API secrets, personal/customer data, or confidential production payloads. Must never be pasted into AI prompts; use masked/anonymized examples instead. |
| **Skill** | A reusable, saved set of instructions (a `SKILL.md`) that Claude applies automatically once a task matches its description, instead of someone re-writing a prompt from scratch each time. Still subject to the same review requirement as any other AI-assisted output — a skill standardizes the input, not the review obligation. Hub skills live in `skills/`; a craft repo may instead have its own project-embedded skill (or an equivalent Copilot prompt) with direct knowledge of that repo's structure — see `how-to-use-existing-repos.md` for which one applies. |
| **Specialized standards repo** | A repository maintaining craft-specific standards (e.g. `postman-testing`, `gherkin-scenarios-tmp`, `test-cases-generator`) that this hub links to instead of duplicating. |
| **Central hub** | This repository (`qa-ai-standards`) — holds universal, cross-project AI usage rules only. |
| **Peer QA review** | Review performed by another QA team member (not the author) before accepting a Medium-risk AI-assisted artifact. |
| **QA Lead review** | Review performed by the QA Lead (or designated standards maintainer) before accepting a High-risk AI-assisted artifact. |