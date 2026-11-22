# PRD skeleton

Turns a one-line problem statement into a structured, reviewable product requirements document. Paste the prompt below into Claude, then fill the variables.

## Variables

| Variable | Meaning |
|---|---|
| `{{PROBLEM_STATEMENT}}` | One sentence: who has what problem, and why it matters now |
| `{{AUDIENCE}}` | Who will read and approve the PRD (e.g. engineering leads, risk partners, a VP) |
| `{{CONSTRAINTS}}` | Known limits: regulatory, budget, platform, dates |
| `{{CONTEXT}}` | Optional: links or pasted notes, research, prior decisions |

## Prompt

```
You are a senior product manager drafting a PRD. Write for this audience: {{AUDIENCE}}.

Problem statement: {{PROBLEM_STATEMENT}}
Constraints: {{CONSTRAINTS}}
Context: {{CONTEXT}}

Before drafting, list up to five clarifying questions whose answers would change scope.
If I say "draft anyway", proceed and mark each unanswered item as an assumption.

Produce the PRD with exactly these sections:
1. Summary (three sentences: problem, proposed solution, expected outcome)
2. Problem and evidence (who is affected, how often, cost of doing nothing; cite the evidence or say it is missing)
3. Goals and non-goals (bulleted; non-goals are as important as goals)
4. Users and key scenarios (2 to 4 scenarios written as "When..., the user needs..., so that...")
5. Requirements (table: ID, requirement, priority P0 to P2, acceptance criteria)
6. Success metrics (one primary metric with baseline and target, two guardrail metrics)
7. Data, privacy and compliance considerations (what data is used, retention, review needed)
8. Dependencies and stakeholders (team or role, what is needed, by when)
9. Risks and mitigations (table: risk, likelihood, impact, mitigation, owner)
10. Rollout plan (phases, gating criteria between phases, rollback trigger)
11. Open questions (each with an owner and a decide-by date)

Rules: plain language, no filler, no em dashes, American dates (March 4).
Never invent metrics, names, or numbers; use [TBD] and list it under Open questions.
End with a "What was assumed" footer listing every assumption made.
```

## Output check
- Every P0 requirement has testable acceptance criteria.
- The primary metric has a baseline, or the baseline is an open question.
- The footer lists assumptions explicitly.
