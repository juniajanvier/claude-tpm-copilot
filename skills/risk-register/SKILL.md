---
name: "risk-register"
description: "Maintain a living risk register from PR comments, chat threads, and meeting notes: extract new risks, update existing ones, score likelihood and impact, and flag stale or unowned risks."
---

# Risk register

Keeps one register current instead of rebuilding it before every review.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{PROGRAM_NAME}}` | Program the register covers |
| `{{REGISTER_LOCATION}}` | Where the register lives (a sheet ID, a doc, or a markdown table in the repo) |
| `{{SCORING_SCALE}}` | Likelihood and impact scale, default 1 to 5 each |
| `{{ESCALATION_THRESHOLD}}` | Score at or above which a risk is escalated, default 15 |
| `{{STALE_DAYS}}` | Days without an update before a risk is flagged stale, default 14 |

## Register columns
ID, Title, Description (cause, event, effect), Category (schedule, technical, data, compliance, vendor, people), Likelihood, Impact, Score (L x I), Trend (up, flat, down), Owner, Mitigation, Contingency, Trigger, Status (Open, Mitigating, Accepted, Closed), Source, Last Updated.

## Workflow
1. Read the current register at `{{REGISTER_LOCATION}}`. Never overwrite it blind; find rows by ID.
2. Read the new input (PR comments, threads, notes). Extract candidate risks: statements of uncertainty that could affect scope, schedule, quality, compliance or cost. Phrase each as "Because <cause>, <event> may happen, leading to <effect>."
3. Match each candidate against existing rows. Update an existing risk rather than creating a duplicate; note the new evidence and adjust the trend.
4. Score with `{{SCORING_SCALE}}`. Explain any score of 4 or 5 in one line.
5. Flag: risks with no owner, no mitigation, a score at or above `{{ESCALATION_THRESHOLD}}`, or no update in `{{STALE_DAYS}}` days.
6. Propose closing risks whose trigger date has passed or whose cause is gone, with the evidence.
7. Show the proposed changes as a diff (added, updated, proposed closed) and write only after approval.

## Output
- Change summary: counts added, updated, proposed closed.
- Top five risks by score, with owner and next mitigation step.
- Flags list (unowned, unmitigated, escalate, stale).
- The updated register table, or the rows written, with a link to `{{REGISTER_LOCATION}}`.

## Rules
- Every risk has one owner role. Unknown owners are flagged, never guessed.
- Quote the source line that justifies each new risk.
- Keep confidential data and customer information out of risk descriptions.
- No em dashes, American dates. End with a "What was assumed" footer.
