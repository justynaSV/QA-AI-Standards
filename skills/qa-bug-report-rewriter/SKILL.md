---
name: qa-bug-report-rewriter
description: Rewrite a rough or unclear bug report into a clear, structured format (Summary / Steps to Reproduce / Expected / Actual / Environment) while preserving all technical facts exactly as given, never inventing root cause or new claims. Use this whenever asked to clean up, rewrite, improve the wording of, or restructure a bug report, defect, or issue description.
---

# QA Bug Report Rewriter

Improve the clarity and structure of a bug report without changing what it claims. This is a wording pass, not an investigation — the moment a rewrite adds a claim the original text didn't make (a likely root cause, an assumption about scope, a severity judgment), it has stopped being a wording improvement and become new content that needs its own review.

## Why the fact/wording boundary matters

A bug report is evidence. If a rewrite quietly sharpens "seems to happen sometimes" into "occurs consistently," or turns "might be related to the cache" into "caused by stale cache," it has changed what the report asserts — and whoever reads it next will trust that assertion because it now reads confidently. That's a bigger problem than a rewrite that stays awkwardly worded but factually honest. When in doubt, keep the hedge.

## Step 1: Read for facts vs. speculation

Before rewriting, mentally separate what the reporter directly observed (what they did, what they saw) from what they're guessing at (why it happened, how often, whether it's related to something else). Both can appear in the final report, but speculation must stay clearly marked as speculation.

## Step 2: Rewrite into the standard structure

```markdown
## Summary
<one-line description of the defect>

## Steps to Reproduce
1. <step>
2. <step>
...

## Expected
<what should have happened>

## Actual
<what actually happened>

## Environment
<browser/OS/app version/environment — whatever was given; note "not specified" rather than guessing>
```

Rules while rewriting:
- Keep every technical fact (values, error messages, field names, timestamps) exactly as given — don't paraphrase specifics.
- If the original text speculates about cause, keep it, but phrase it visibly as speculation (e.g. "Reporter suspects this may be related to X — unconfirmed") rather than folding it into Actual as if observed.
- If steps are missing or ambiguous, say so explicitly in the output rather than inventing plausible-sounding steps to fill the gap.

## Step 3: Hand off for review

- Tag `AI-assisted: yes (scope: wording improvement)` per `ai-usage-policy.md` section 6 — but if you found yourself adding or sharpening any claim beyond wording, tell the requester directly and suggest the tag should instead reflect that (and get peer review, since that's no longer just formatting/rewording).
- This is typically **low risk** per the policy's risk tiers, since it's wording only — that classification stops applying the moment content changes, not just phrasing.
- Mask any real customer data, credentials, or production payloads that appear in the draft before including them in the rewritten version, per section 7.

## Example

**Weak input:** "Make this bug report better."

**Better input:** "Rewrite this bug report for clarity, keeping all technical facts unchanged (no new claims about root cause): [paste draft]. Structure as Summary / Steps to Reproduce / Expected / Actual / Environment."

If given the weak version, still apply the same discipline — ask for the raw draft and rewrite it under the same no-new-claims rule by default, and flag anything in the original that already blurs fact and speculation.
