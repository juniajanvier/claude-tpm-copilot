---
name: "life-audit"
description: "Run a recurring all-tracks life and career audit with a graded scorecard and dated action list when the owner says \"audit me\" or asks for a quarterly or half-year review."
---

# Life and career audit

Evidence over self-report. A graded, cross-track review that ends in dated actions.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Person being audited |
| `{{ACTIVE_TRACKS}}` | Tracks to grade, e.g. day job, job search, side business, study goal, newsletter, home project, personal foundation |
| `{{TRACKER_SHEET_ID}}` | Task tracker spreadsheet ID |
| `{{CAPACITY_CEILING_HRS}}` | Weekly hours ceiling for committed side work |
| `{{PERIOD_OUTCOMES}}` | The two to four stated outcomes for the period, e.g. "one external offer, one closed transaction, one exam sitting with a real score" |

Trigger: "audit me", "it's that time again", quarterly or half-year audit, life and career review.

## 1. Gather before judging
- Read memory for every active track: `{{ACTIVE_TRACKS}}`.
- Read the tracker (`{{TRACKER_SHEET_ID}}`): Dashboard (KPIs and wins), Capacity (committed hours versus the `{{CAPACITY_CEILING_HRS}}`-hour ceiling), Waiting On, Deadlines, and the Done On dates for what actually finished in the period.
- Read the Skill Payoff tab: runs, hours saved and verdict for each skill and scheduled task.
- Search recent chats for the last audit so grades can be compared.
- Check the calendar for the current week if a calendar tool is connected.
- Look for evidence (a practice-test score, a closing, a signed contract), not self-report. A row marked Done or a moved due date is not evidence by itself.

## 2. Output format
1. **Title line:** "[Quarter] audit, all tracks. [start date] to today."
2. **Headline:** two or three sentences naming the cross-cutting pattern (example: builds infrastructure, gap between building and shipping).
3. **Scorecard on the stated outcomes** (`{{PERIOD_OUTCOMES}}`). One bullet each: status plus the evidence.
4. **Track-by-track grades** (A to F with +/-), one short paragraph each: what moved, the gap, the next move. Include personal tracks alongside career ones.
5. **Capacity:** committed hours versus the ceiling for the next four weeks, and what to cut if over.
6. **Skills and automations:** total hours saved this period, the top two earners, and every Watch or Retire? row with a call: retire, merge into another skill, or fix its trigger. Flag any new build since the last audit that skipped the priority check.
7. **Action list:** five or six concrete actions with dates and tracker IDs. Flag anything deadline-locked first.
8. Close by naming which item is externally deadline-locked and what is functioning as avoidance.

## 3. Tone
- Direct and specific. Push back on self-reported progress when the evidence is missing; update a grade when real context arrives.
- Not legal or financial advice; say so in a few words where relevant.
- Writing rules: no em dashes, no sentence opening with "I", American dates (October 2).

## 4. After
Write the dated actions to the tracker as rows or updates if the owner says yes (follow the life-tracker-update skill), and offer to put them on the calendar.
