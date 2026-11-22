---
name: "priority-check"
description: "Before starting any new project, app, venture, product, tracker tab, skill or side project, check it against the owner's yearly priorities and weekly capacity and give a Go, Fold in or Park call."
---

# Priority check

A short gate that stops new things to maintain from quietly eating capacity. Not a lecture. The owner makes the final call.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Person the skill works for |
| `{{PRIORITY_YEAR}}` | Year the priority list covers (e.g. 2027) |
| `{{PRIORITY_RULE}}` | One-line rule for the year (e.g. "no new side projects; grow on existing foundations") |
| `{{PRIORITIES_FILE}}` | Memory or doc path holding the current priority list |
| `{{TRACKER_SHEET_ID}}` | ID of the task tracker spreadsheet |
| `{{CAPACITY_CEILING_HRS}}` | Weekly hours ceiling for committed work outside the day job (e.g. 30) |
| `{{EXISTING_PROJECTS}}` | Comma-separated list of existing brands, ventures and ideas to check for overlap |
| `{{PARK_TRACK_ID}}` | Tracker prefix for parked ideas (e.g. SOM) |

## When to run
- Before building anything that creates a new thing to maintain: an app, venture, product line, brand, course, club, newsletter, tracker tab, Claude skill, scheduled task, or a new tracker track. Cues: "let's start...", "I have an idea for...", "build me a...", "what if I made...".
- When the owner asks "should I take this on?" or "priority check".
- Skip it for work inside something that already exists (the next newsletter issue, a day-job deliverable, a client deliverable, study drills), for errands, and when the owner says "skip the check".

## Steps
1. Read `{{PRIORITIES_FILE}}` for the `{{PRIORITY_YEAR}}` priority list and the rule: `{{PRIORITY_RULE}}`.
2. Read the tracker (`{{TRACKER_SHEET_ID}}`): the Capacity tab for committed hours against the `{{CAPACITY_CEILING_HRS}}`-hour weekly ceiling over the next four weeks, and the `{{PARK_TRACK_ID}}` rows for parked ideas that match.
3. Check for overlap with something that already exists: an existing skill, sheet tab, brand or idea (`{{EXISTING_PROJECTS}}`). Overlap points to Fold in.
4. Answer four questions, one line each:
   - Priority served: which priority, or "none".
   - Money or time: does it bring clients or revenue within 90 days, or save at least an hour a week?
   - Cost: setup hours plus weekly upkeep hours, and capacity before and after.
   - Trade: what it replaces, or what gets parked to make room.
5. Make one call:
   - **Go**: serves a priority and fits capacity, or the owner names the trade. Proceed and add it to the tracker with Start and Due.
   - **Fold in**: overlaps something that exists. Say where it goes instead.
   - **Park**: serves no priority, or capacity is over the ceiling. Offer a parked row: Status Parked, Type Project, Priority P4, Start and Due set to the next quarterly audit as a revisit date, Notes "Parked by priority check on <date>: <one-line reason>".
6. If the owner says go anyway, go. No second argument. Note the override in the tracker row Notes.

## Output
A short card, under 120 words:

**Priority check: <idea>**
Priority served: ...
Money or time: ...
Cost: ... hrs setup, ... hrs a week; capacity goes from X to Y of `{{CAPACITY_CEILING_HRS}}`
Trade: ...
**Call: Go / Fold in / Park**, plus one sentence why.

Then ask "Go, fold in, or park?" (with an in-chat choice when available).

## After
- Follow the life-tracker-update skill for any tracker writes.
- Log the run on the tracker's Skill Payoff Run Log: date, "priority-check", minutes saved blank, note with the idea and the call.

## Style
No em dashes, no sentences starting with "I", American dates (January 5). Direct and warm, never preachy.
