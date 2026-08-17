---
name: qa-postman-assertion-reviewer
description: Review a Postman test script (pm.test blocks) against the QA team's postman-testing conventions, flagging missing status-code checks, missing schema validation, and hardcoded values that should be variables — without inventing endpoints, fields, or behavior not present in the script. Use this whenever asked to review, check, audit, or improve a Postman test script or API test assertions.
---

# QA Postman Assertion Reviewer

Review an existing Postman test script for coverage gaps and hygiene issues. This is a review of what's on the page — never propose assertions about endpoints, fields, or response shapes that aren't actually visible in the script or an attached response example, since that's indistinguishable from fabricating API behavior.

## Why staying strictly inside the given script matters

It's tempting for a review to "helpfully" suggest checking a field that's common for this kind of endpoint (e.g. "you should also check `updatedAt`") even when that field never appears in the script or sample response. That suggestion looks like domain expertise but is actually a guess about an API contract the reviewer has no evidence for. If the reviewer wants that checked, they need to confirm the field exists first — flag it as a question, not a finding.

## Step 1: Get the inputs

You need the Postman test script itself (the `pm.test(...)` blocks and any pre-request logic), and ideally the team's `postman-testing` conventions doc or an example of a compliant script for comparison. If conventions aren't available, review against general good practice (below) and say so.

## Step 2: Check for these categories

- **Status code assertion** — is response status explicitly checked (not just implied by absence of error)?
- **Schema / response shape validation** — are expected fields and types checked, not just presence of *a* response?
- **Hardcoded values** — IDs, tokens, base URLs, or environment-specific values that should be Postman variables (`{{variable}}`) instead of literals.
- **Response time / performance assertions** — present if the team's conventions require them.
- **Naming and tagging** — test names descriptive and consistent with convention; requests tagged/organized per convention if that's part of the standard.
- **Negative-path coverage** — are error responses (4xx/5xx) tested anywhere, or only the happy path?

## Output format

```markdown
## Findings
| Category | Issue | Suggested fix |
|---|---|---|

## Already compliant
- <what the script already does correctly — don't skip this, it tells the reviewer what NOT to change>

## Questions (not findings)
- <anything that looks like a gap but requires confirming API behavior you weren't given>
```

## Step 3: Hand off for review

- Tag `AI-assisted: yes (scope: assertion proposal)` per `ai-usage-policy.md` section 6 for any new assertions suggested.
- New assertions are **medium risk** per the policy's risk tiers — peer QA review required before merging, even if the suggestions look obviously correct.
- Never paste real tokens, API keys, or production payloads into the review request — mask them first, per section 7.

## Example

**Weak input:** "Check my Postman script."

**Better input:** "Review this Postman test script against `postman-testing` conventions: [paste script]. Flag missing status code checks, missing schema validation, and any hardcoded values that should be variables. Do not invent new endpoints or fields not present in the script."

If given the weak version, still apply the "don't invent endpoints or fields" rule by default — it's the single most important constraint for this skill, not an optional add-on the requester has to remember to ask for.
