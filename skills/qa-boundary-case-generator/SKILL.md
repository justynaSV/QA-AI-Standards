---
name: qa-boundary-case-generator
description: Generate boundary and negative test cases for a specific field, parameter, or input constraint (type, min/max, required/optional), returned as a table of input, expected result, and reasoning. Use this whenever asked for edge cases, boundary values, negative test cases, or "what could break this field/parameter" — even if the user just describes a field's constraints without using the word "boundary."
---

# QA Boundary Case Generator

Generate a table of boundary and negative test cases for one field or parameter at a time. This is a candidate list for a human QA to review and select from, not a final assertion set — treat completeness and precision as more important than brevity.

## Why one field at a time, systematically

Most missed edge cases follow a small number of predictable patterns: the value at the boundary, one step past the boundary, the wrong type, the absent value, and the "technically valid but operationally weird" value (empty string, whitespace-only, unicode). Generating cases ad hoc tends to catch the obvious ones and miss the boring-but-important ones like "field present but empty." Going through a fixed set of categories catches the boring ones on purpose.

## Step 1: Get the field definition

You need: field name, data type, constraints (min, max, required/optional, format/pattern), and ideally what the field means in the business context (helps judge whether e.g. negative numbers are meaningless or a valid edge case). If any of this is missing, ask rather than guessing — a boundary case for an unstated constraint is not useful and may mislead the reviewer into thinking it was already covered.

## Step 2: Generate cases by category

Work through these categories, skipping any that don't apply to the field's type and noting why:

- **Boundary — valid**: exactly at min, exactly at max.
- **Boundary — invalid**: one below min, one above max.
- **Absence**: missing field entirely, `null`, empty string (if string), empty array (if list).
- **Type mismatch**: string where a number is expected, decimal where an integer is expected, wrong format (e.g. malformed date/email).
- **Whitespace / encoding**: leading/trailing whitespace, whitespace-only value, unicode or special characters if the field is free text.
- **Scale extremes**: a very large value, a very long string, duplicate entries if the field is a list.
- **Business-rule specific**: anything implied by the field's meaning that isn't captured above (e.g. a "quantity" field where 0 is technically in-range but may be a meaningless order).

## Output format

Always use this table:

| Input | Expected Result | Reason |
|---|---|---|
| `<value>` | `<pass / specific error>` | `<why this case matters>` |

Follow the table with a one-line note on any category you skipped and why (e.g. "Unicode/whitespace skipped — field is a numeric type").

## Step 3: Hand off for review

Remind whoever uses this:

- These are candidate cases, not confirmed assertions — run acceptance through `templates/ai-output-review-checklist.md`.
- Tag accepted artifacts `AI-assisted: yes (scope: edge-case suggestion)` per `ai-usage-policy.md` section 6.
- Treat this as **low risk** (formatting/candidate generation) if used to inform test design, but re-classify as **medium risk** the moment these cases are turned directly into committed assertions — that shift needs peer review per the policy's risk tiers.
- Use masked/fictional example values only — never real customer IDs, emails, or payment data, per section 7.

## Example

**Weak input:** "Give me edge cases for this API field."

**Better input:** "Field: `quantity` (integer, min 1, max 100, required). Suggest boundary and negative test cases (e.g. 0, 101, negative, decimal, null, missing field, non-numeric string). Return as a table: input | expected result | reason."

If given the weak version, ask for the type and constraints before generating anything — a boundary case is only as good as the constraint it's testing against.
