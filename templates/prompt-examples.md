# Prompt Examples (QA)

Mini library of good/bad prompt patterns for common QA tasks. Pair with `ai-usage-policy.md` and `templates/ai-output-review-checklist.md`.

General rules for all prompts:
- Never include real credentials, tokens, or customer data — use masked/fictional values.
- State the acceptance criteria or requirement explicitly; don't let the AI guess it.
- Ask for assumptions to be listed separately from the output.

---

## 1. Gherkin scenarios

Superseded — don't prompt from scratch for this one. Use the `/gherkin-scenarios` Copilot prompt built into the `gherkin-scenarios` template repo and its project copies, including `gherkin-scenarios-tmp`. It already knows the project's real module folders, tagging, and traceability format, which a hand-written prompt here can't. See `how-to-use-existing-repos.md` for why this lives in the project repo instead of here.

---

## 2. Generating negative/boundary cases

**Weak prompt:**
> Give me edge cases for this API field.

**Better prompt:**
> Field: `quantity` (integer, min 1, max 100, required).
> Suggest boundary and negative test cases (e.g. 0, 101, negative, decimal, null, missing field, non-numeric string).
> Return as a table: input | expected result | reason.

---

## 3. Improving bug report wording

**Weak prompt:**
> Make this bug report better.

**Better prompt:**
> Rewrite this bug report for clarity, keeping all technical facts unchanged (no new claims about root cause):
> [paste draft]
> Structure as: Summary / Steps to Reproduce / Expected / Actual / Environment.

---

## 4. Reviewing/improving Postman assertions

**Weak prompt:**
> Check my Postman script.

**Better prompt:**
> Review this Postman test script against `postman-testing` conventions: [paste script].
> Flag missing status code checks, missing schema validation, and any hardcoded values that should be variables.
> Do not invent new endpoints or fields not present in the script.

---

## 5. What NOT to paste into a prompt

Avoid pasting:
- API keys, tokens, passwords, session cookies
- Real customer names, emails, addresses, payment data
- Full production payloads with real IDs — mask or use fixtures instead

If context is needed, anonymize first (e.g. `user@example.com`, `id: 12345` instead of real values).

---

## Traceability reminder
Any output used from these prompts must still go through `templates/ai-output-review-checklist.md` and be tagged `AI-assisted: yes (scope: ...)` per `ai-usage-policy.md`.