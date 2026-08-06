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

---

## Integration model (what lives where)

## Central hub (`qa-ai-standards`)
Contains:
- universal AI QA policy,
- review and traceability minimum,
- onboarding template for cross-project usage.

## Specialized standards repos (`postman-testing`, `gherkin-scenarios-tmp`)
Contain:
- craft-specific standards,
- examples and conventions for that testing style.

## Project repositories (team/product-specific)
Contain:
- domain/business specifics,
- environment constraints,
- project-level test strategy and priorities.

---

## Working order for QA members (mandatory sequence)
For any QA task:

1. Read central AI policy (this hub)
2. Apply relevant specialized standard:
   - Postman/API → `justynaSV/postman-testing`
   - BDD/Gherkin → `justynaSV/gherkin-scenarios-tmp`
3. Apply the current project’s own constraints
4. Validate with AI output checklist before finalizing

---

## Change management recommendation
- Keep universal rules only in this hub.
- Keep technical standards in specialized repos.
- Avoid duplicating the same standards text in multiple places.
- In this hub, link to specialized repos instead of copying content.