# AI Output Review Checklist (QA)

Use this checklist before accepting AI-generated or AI-assisted QA artifacts.

## Requirement fit
- [ ] Output aligns with requirement/story/acceptance criteria
- [ ] Assumptions are explicit (none hidden)
- [ ] Nothing critical was omitted

## Quality of test design
- [ ] Includes relevant positive scenarios
- [ ] Includes relevant negative/boundary scenarios (where applicable)
- [ ] Expected results are specific and testable
- [ ] Steps are clear and executable

## Technical correctness
- [ ] Names/endpoints/fields/flows are correct for this project
- [ ] Proposed assertions/checks are valid
- [ ] No contradictions with project standards

## Risk and compliance
- [ ] No sensitive data is exposed in prompts/output
- [ ] Appropriate reviewer level was applied (peer/lead if needed)

## Traceability
- [ ] Artifact is marked: `AI-assisted: yes (scope: ...)`
- [ ] Linked to relevant task/ticket/PR context

---

Decision:
- [ ] Accepted
- [ ] Accepted with edits
- [ ] Rejected

Reviewer: __________  
Date: __________  
Notes: __________