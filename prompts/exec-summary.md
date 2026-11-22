# Exec summary

Compresses a project, decision, or incident into a one-page readout for senior leadership. Bottom line first, decision asks explicit.

## Variables

| Variable | Meaning |
|---|---|
| `{{TOPIC}}` | What the readout covers |
| `{{AUDIENCE}}` | Who reads it and what they care about (e.g. "SVP, cares about risk and dates") |
| `{{PURPOSE}}` | Inform, decide, or escalate |
| `{{SOURCE_MATERIAL}}` | Pasted notes, docs, metrics, threads |

## Prompt

```
Write a one-page executive summary.

Topic: {{TOPIC}}
Audience: {{AUDIENCE}}
Purpose: {{PURPOSE}}
Source material:
{{SOURCE_MATERIAL}}

Format (keep under 350 words):
1. Bottom line (two sentences max: the status and what it means)
2. Status: one of On track / At risk / Off track, with the single reason
3. Decision needed (only if Purpose is decide or escalate): the question, options
   with tradeoffs in one line each, recommendation, and decide-by date
4. Key facts (3 to 5 bullets, each with a number or date)
5. Risks (top 2, each with mitigation and owner)
6. Next milestones (table: milestone, date, owner)

Rules:
- Lead with the conclusion, not the history.
- Use only facts present in the source material. If a needed fact is missing, write [TBD]
  and list it under "Gaps" at the end.
- Translate jargon for the audience. No acronyms without expansion on first use.
- No em dashes, no hedging filler, American dates (July 3).
End with a "What was assumed" footer.
```

## Output check
- A reader who stops after the first two lines knows the status and the ask.
- Every bullet under Key facts contains a number or a date.
