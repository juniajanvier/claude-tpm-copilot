---
name: "life-tracker-update"
description: "Read or update a single-source-of-truth task tracker in Google Sheets (tasks, statuses, check-ins, skill payoff) whenever the owner gives a status, adds a task, or asks what's on their plate."
---

# Life tracker update

The tracker is the owner's single source of truth for every task across work and life. Status lives in the sheet, never only in chat.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Person the tracker belongs to |
| `{{TRACKER_SHEET_ID}}` | Google Sheets ID of the tracker |
| `{{TRACKER_URL}}` | Link to the tracker, returned after every update |
| `{{TRACKS}}` | Track names with ID prefixes, e.g. `DAY JOB (JOB), REAL ESTATE (RE), BUSINESS + BRAND (BB), HOME + PERSONAL (HOME), SOMEDAY / ARCHIVE (SOM)` |
| `{{DAY_JOB_TRACK}}` | Track for the day job (kept high level, excluded from capacity) |
| `{{SKILL_PAYOFF_REVIEW_DATE}}` | Date the Skill Payoff verdicts start counting |
| `{{BUSINESS_EMAIL}}` | Address used on business-facing items |
| `{{OWNER_TITLE}}` | Owner's correct job title, for any row or reply that mentions it |

Always write to the sheet with the Google Sheets connector (get_values, update_values). Never keep status only in chat, a CSV, a doc checklist or an artifact. If the Sheets connector is missing, say so and suggest connecting it; don't fake an update.

## Commands

- **"Tracker check-in"**: read open rows (Status not Done/Dropped), group by This Week / overdue / waiting on, and show each task as an in-chat choice with options Done, In progress, Waiting on, Parked (plus Other for Blocked, Dropped, Confirm or a note). Write every answer straight to the sheet in the same turn.
- **"Update tracker: <ID> <status>"** (e.g. "Update tracker: RE-07 done"): write the status; for Done also set Done On to today.
- **"Add to tracker: <task>"**: pick the track, next free ID for that prefix, Type, Priority, Effort, Due; append it in the next empty row.
- **"What's on my plate this week"**: read the This Week view (or filter Tracker by Due within 7 days plus P0/P1 in progress) and summarize briefly.
- When an in-chat checklist or dropdown is shown for tasks, every selection gets written to the sheet. No exceptions.

## Tracker tab layout (the only tab that takes input)

Columns A to T are inputs: A ID, B Track, C Task, D Next Action, E Type, F Status, G Priority, H Effort (hrs), I Recurs, J Who / Waiting On, K Blocked By, L Start, M Due, N Link, O Notes, P Risk, Q Add To Calendar, R Cal Event ID (script-owned, don't edit), S Done On, T Claudify.
Columns U onward are formulas for rows 2 to 600. Never write to them.

All other tabs (Dashboard, Gantt, This Week, Claude Queue, Deadlines, Triage, Waiting On, Commitments, Capacity, By Track, Intake) rebuild themselves. Don't edit them. The exceptions are Network (log touches in Last Touch), Skill Payoff (Run Log rows and yellow input cells), Settings yellow cells, yellow filter cells on Gantt and By Track, and Change Log (add a line for structural changes).

## Rules for every new or changed row

- Dates: write as YYYY-MM-DD; in chat use American dates (October 25).
- Fill every applicable column so the row works everywhere: Track, Type, Status, Priority, Effort, Start and Due when known, Add To Calendar as Y or N (never TRUE, FALSE or blank), Claudify as Autonomous, In session, Prep only or No.
- A row with no Start or Due does not appear on the Gantt or in Capacity, so give every open non-standing row a date, even a proposed one, and say it is proposed.
- Statuses: Not started, In progress, Waiting on, Blocked, Confirm, Parked, Done, Dropped.
- Types: Project, Errand, Decision, Deadline, Standing. Standing rows need Recurs (Weekly, Biweekly, Monthly, Quarterly). For yearly items use an Errand with a due date and note "repeat yearly".
- Priorities: P0 to P4.
- Before writing, get_values the rows to find exact row numbers and the next empty row; never guess. Rows do not stay grouped by track, so find a row by its ID.
- Merges: set the old row to Dropped with a note "Merged into <ID> on <date>".
- Recurring rows are never Done. When one instance of a recurring row finishes, keep Status as In progress, update Next Action to the next occurrence and note the date. Set Done or Dropped only when the commitment itself has ended.
- Don't move a due date to clear Overdue unless the owner asks or a new date is known. If you do, note it, and don't describe it as progress.
- Blocked By: clear it when the blocker is Done.

## Tracks and ID prefixes

`{{TRACKS}}`
`{{DAY_JOB_TRACK}}` rows stay high level and don't count toward capacity. Side work (job search, business, study) does count, because that time comes from outside the day job.
To add a track: add it to the next empty Settings row with a prefix; the Capacity tab needs a matching row, and the Gantt needs a track filter option and a color rule.

Sensitive tracks (money, health) follow the same mechanics, but keep only task-level detail in rows. Figures and account details stay in the owner's own documents, never in skill text or chat summaries. Education only, never personalized financial advice.

## Automation (optional, if installed)

An Apps Script bound to the sheet can:
- Create a calendar event on the Due date when Add To Calendar = Y (daily sync); remove events for Done, Dropped or Parked rows.
- Send a weekly digest email.
- Feed a phone capture form into the Intake tab; move items into Tracker during check-ins.
- Fill blank IDs on edit.
Don't reinstall or edit the script unless the owner asks. Scheduled tasks that read the sheet (weekly Claude Queue run, morning briefing, monthly relationship follow-ups) must be kept in step if the layout changes.

## Skill Payoff tab

Tracks whether skills and scheduled tasks actually save time.
- Left table: one row per skill or task. Inputs: name, type, what it does, minutes saved per run, notes. Formula columns (runs, runs in window, last used, hours saved, verdict): never write to them.
- Run Log: Date (YYYY-MM-DD), skill or task (must match the left table exactly), minutes saved (optional override), note.
- **"Log skill: <name> [minutes]"**, and whenever a skill or scheduled task finishes a run in a session: append one row. One row per run, not per step.
- New skill: add it in the first empty row with a proposed minutes estimate and copy the formula columns from the row above.
- Retired skill: keep the row, set Notes to "Retired <date>"; never delete log rows.
- Verdicts read Collecting until `{{SKILL_PAYOFF_REVIEW_DATE}}`, then Keep, Watch (1 run in the window) or Retire? (0 runs).

## Sources to sweep when asked to find missing tasks

Task app, email (starred and important threads), calendar, recent chats, recent Drive files, and any pipeline sheets the owner keeps (speaking, funding, contracts). Add only real open items, skip duplicates, and note the source in Notes.

## Writing style for rows and replies

No em dashes. Don't start sentences with "I". American dates. Short, plain next actions starting with a verb. Business items use `{{BUSINESS_EMAIL}}`; never put a home address in business materials. Title, if mentioned: `{{OWNER_TITLE}}`.

## After every update

Re-read the changed rows with get_values to confirm, then reply in one or two sentences with the IDs changed and `{{TRACKER_URL}}`.
