---
name: qa-ai-output-review-checklist-runner
description: Walk through the QA team's AI Output Review Checklist against a specific AI-generated artifact (test scenario, bug report, script, edge cases, etc.), producing an explicit pass/fail assessment per item rather than a vague "looks good." Use this whenever asked to review, validate, sign off on, or check an AI-assisted QA artifact before accepting it, or to "run the checklist" on something.
---

# QA AI Output Review Checklist Runner

Apply `templates/ai-output-review-checklist.md` to a specific artifact, item by item, with an explicit assessment for each one. The checklist only does its job if every item gets a real answer — this skill exists because a checklist that gets glanced at and mentally rubber-stamped catches nothing that a careful read wouldn't have caught anyway.

## What this skill is not

It does not make the accept/reject decision. That decision, the reviewer's name, and the date are a human's call per `ai-usage-policy.md`'s core principle that human QA is always accountable — never fill in Decision, Reviewer, or Date yourself, and never phrase your output in a way that implies the artifact has already been accepted.

## Step 1: Gather what you need

- The requirement, story, or acceptance criteria the artifact is supposed to satisfy.
- The AI-generated artifact itself.
- The declared scope of AI assistance (e.g. "scenario draft," "assertion proposal") if known — if not, ask, since it affects which risk tier applies.

## Step 2: Go through every item explicitly

For each item in the checklist's five sections (Requirement fit, Quality of test design, Technical correctness, Risk and compliance, Traceability), give one of: **Pass**, **Fail**, or **N/A**, with a one-sentence reason. Do not summarize a whole section at once — an item-by-item pass is what makes this useful instead of decorative.

```markdown
### Requirement fit
- [Pass/Fail/N/A] Output aligns with requirement/story/acceptance criteria — <reason>
- [Pass/Fail/N/A] Assumptions are explicit (none hidden) — <reason>
- [Pass/Fail/N/A] Nothing critical was omitted — <reason>

### Quality of test design
- ...

### Technical correctness
- ...

### Risk and compliance
- [Pass/Fail/N/A] No sensitive data is exposed in prompts/output — <reason>
- [Pass/Fail/N/A] Appropriate reviewer level was applied (peer/lead if needed) — <reason, referencing the risk tier from ai-usage-policy.md section 5>

### Traceability
- [Pass/Fail/N/A] Artifact is marked: `AI-assisted: yes (scope: ...)` — <reason>
- [Pass/Fail/N/A] Linked to relevant task/ticket/PR context — <reason>
```

## Step 3: Summarize blockers, then stop

```markdown
## Blockers (any Fail above)
- <item> — <what needs to change before this can be accepted>

## Decision
- [ ] Accepted
- [ ] Accepted with edits
- [ ] Rejected

Reviewer: __________
Date: __________
Notes: __________
```

Leave the Decision section blank for the human reviewer to complete — that's the whole point of keeping AI as an assistant rather than an approver, per the policy's core principle.

## Example

**Input:** "Run the checklist on this Gherkin scenario set against ticket QA-1042's acceptance criteria: [paste scenarios] [paste AC]."

**Output:** The item-by-item assessment above, ending in an unchecked Decision block ready for the actual reviewer to complete and sign.
