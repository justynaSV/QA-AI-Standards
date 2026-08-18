---
name: qa-bug-report-rewriter
description: Rewrite a rough or unclear bug report into a clear, structured format (Summary / Environment / Steps to Reproduce / Actual Result / Expected Result / Notes) while preserving all technical facts exactly as given, never inventing root cause or new claims. Accepts either pasted text or a Jira bug URL/key. Use this whenever asked to clean up, rewrite, improve the wording of, or restructure a bug report, defect, or issue description.
---

# QA Bug Report Rewriter

Improve the clarity and structure of a bug report without changing what it claims. This is a wording pass, not an investigation — the moment a rewrite adds a claim the original text didn't make (a likely root cause, an assumption about scope, a severity judgment), it has stopped being a wording improvement and become new content that needs its own review.

## Why the fact/wording boundary matters

A bug report is evidence. If a rewrite quietly sharpens "seems to happen sometimes" into "occurs consistently," or turns "might be related to the cache" into "caused by stale cache," it has changed what the report asserts — and whoever reads it next will trust that assertion because it now reads confidently. That's a bigger problem than a rewrite that stays awkwardly worded but factually honest. When in doubt, keep the hedge.

## Step 1: Get the draft

- **Jira bug URL or bare issue key** (e.g. `https://<site>.atlassian.net/browse/PROJ-123` or `PROJ-123`): use the Atlassian MCP tools, if available, to fetch the issue's summary, description, and any comments describing the defect. Treat the fetched content as the raw draft — the same fact/speculation discipline in Step 2 applies to it, since a Jira description can blur observation and guesswork just as easily as a pasted draft can. If the Atlassian MCP tools are unavailable or the fetch fails, say so and ask the user to paste the draft instead.
- **Pasted text**: use it directly as the raw draft.

## Step 2: Read for facts vs. speculation

Before rewriting, mentally separate what the reporter directly observed (what they did, what they saw) from what they're guessing at (why it happened, how often, whether it's related to something else). Both can appear in the final report, but speculation must stay clearly marked as speculation.

## Step 3: Rewrite into the standard structure

```markdown
## Summary
<one-line description of the defect>

## Environment
<browser/OS/app version/environment — whatever was given; note "not specified" rather than guessing>

## Steps to Reproduce
1. <step>
2. <step>
...

## Actual Result
<what actually happened>

## Expected Result
<what should have happened>

## Notes
<speculation about cause, unconfirmed reporter suspicions, or anything else that doesn't belong in the sections above — clearly marked as unconfirmed. Write "-" if there's nothing to put here.>
```

Rules while rewriting:
- Keep every technical fact (values, error messages, field names, timestamps) exactly as given — don't paraphrase specifics.
- If the original text speculates about cause, keep it, but move it to Notes and phrase it visibly as speculation (e.g. "Reporter suspects this may be related to X — unconfirmed") rather than folding it into Actual Result as if observed. Notes exists specifically so speculation never has to be smuggled into a section that's supposed to be pure observation.
- If steps are missing or ambiguous, say so explicitly in the output rather than inventing plausible-sounding steps to fill the gap.

## Step 4: Hand off for review

- Tag `AI-assisted: yes (scope: wording improvement)` per `ai-usage-policy.md` section 6 — but if you found yourself adding or sharpening any claim beyond wording, tell the requester directly and suggest the tag should instead reflect that (and get peer review, since that's no longer just formatting/rewording).
- This is typically **low risk** per the policy's risk tiers, since it's wording only — that classification stops applying the moment content changes, not just phrasing.
- Mask any real customer data, credentials, or production payloads that appear in the draft before including them in the rewritten version, per section 7.
- If the draft came from a Jira issue, keep the issue key/link with the rewritten version — that satisfies the "linked to relevant task/ticket/PR context" part of `templates/ai-output-review-checklist.md` for free.

## Example

**Weak input:** "Make this bug report better."

**Better input:** "Rewrite this bug report for clarity, keeping all technical facts unchanged (no new claims about root cause): [paste draft]. Structure as Summary / Environment / Steps to Reproduce / Actual Result / Expected Result / Notes."

**Also valid:** "Rewrite the bug report at https://mycompany.atlassian.net/browse/QA-2201." — fetch it via Atlassian MCP tools instead of asking for a paste.

If given the weak version, still apply the same discipline — ask for the raw draft (or a Jira link) and rewrite it under the same no-new-claims rule by default, and flag anything in the original that already blurs fact and speculation.