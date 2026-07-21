---
name: plain-language-changelog
description: Create a concise, non-super-technical changelog that explains implemented work in plain language. Use when the user asks to explain what changed, summarize PR/worktree implementation, turn technical changes into customer/operator-friendly release notes, or use a format like "Changelog" with checkmarked sections, Before/Now framing, "Why this matters", tests, proof artifacts, not-completed items, recommendations, and next steps.
---

# Plain Language Changelog

## Goal

Turn implementation details, PRs, investigations, or completed work into a readable changelog for a non-specialist technical operator. Explain the original problem, what changed, why it matters, what was tested, what remains unfinished, and what to do next.

## Output Shape

Use this structure unless the user asks for something else:

```markdown
**Changelog**

✅ **Short change title**

Before, [plain-language old behavior/problem].

Now, [plain-language new behavior].

**Why this matters:** [user/customer/operator impact].

---

✅ **Another change title**

[Repeat as needed.]

---

⚠️ **Not completed: [short title]**

[Clearly state what is not done, blocked, out of scope, or still unproven.]

**Recommendation:** [direct recommendation].
```

## Writing Rules

- Lead with the original problem when the user asks "how does this solve it?" or when the changelog is for a fix.
- Prefer "Before / Now / Why this matters" over implementation jargon.
- Use concise checkmarked sections for completed changes.
- Use warning sections for not completed, blocked, risky, or frontend/backend paired work that still needs its other half.
- Include tests and proof in human terms, with exact result counts or commands only when they are useful.
- Mention artifacts, PRs, branches, deployment status, or local paths when they help the user act.
- End with recommendations and suggested next steps.
- Keep the tone direct, calm, and operator-friendly.
- Use emojis sparingly for status only, such as ✅ and ⚠️.
- Avoid deep code terms unless the user needs them. Translate them:
  - "provider send" -> "the final email send step"
  - "route lookup" -> "finding the right recipient list"
  - "API response contract" -> "the data the UI receives"
  - "telemetry" -> "diagnostic breadcrumbs"

## Content Checklist

Cover the relevant items from this checklist:

- Original problem
- User-visible or operator-visible behavior before
- User-visible or operator-visible behavior now
- Why the change matters
- Backend/service behavior
- Frontend/UI behavior or whether frontend is still pending
- Guardrails or failure handling
- Metadata, diagnostics, or audit trail
- Tests run and results
- Proof artifacts generated
- Not completed / out of scope
- Recommendation
- Suggested next steps

## Style Guidance

Use simple cause-and-effect language:

```text
Old invite still marked active
        |
        v
Reminder job checks invite status first
        |
   active   -> send reminder
   canceled -> skip + record why
```

Prefer concrete examples over abstractions. If a customer/project triggered the work, name the scenario unless privacy or safety requires anonymizing it.

Do not overclaim. Separate:

- implemented
- tested locally
- verified in CI
- deployed
- still pending
- still unproven

## Mini Example

```markdown
✅ **Canceled meetings stop sending reminders**

Before, a meeting canceled after scheduling could still email attendees a reminder at the original time.

Now, the reminder job checks the invite status right before sending and skips canceled meetings.

**Why this matters:** attendees no longer get pinged about meetings that are not happening.
```
