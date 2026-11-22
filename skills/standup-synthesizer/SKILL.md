---
name: "standup-synthesizer"
description: "Read raw standup notes, chat threads or tracker exports and produce a leadership-grade async update: status by workstream, blockers with owners, decisions needed, and what changed since last time."
---

# Standup synthesizer

Turns noisy daily input into a short update a director can read in under a minute.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{PROGRAM_NAME}}` | Program or project the update covers |
| `{{WORKSTREAMS}}` | Workstream names to group by |
| `{{AUDIENCE}}` | Who reads the update (team, leads, leadership) |
| `{{CADENCE}}` | Daily or weekly |
| `{{PREVIOUS_UPDATE}}` | The last update, if available, to compute what changed |

## When to use
"Synthesize standup", "write the async update", "summarize these notes for leadership", or when raw notes, a thread export or a tracker dump is pasted with a request for a status update.

## Steps
1. Read all input. Identify each item's workstream (`{{WORKSTREAMS}}`), owner, and state: done, in progress, blocked, at risk, new.
2. Pull out blockers: what is blocked, by whom or what, since when, and what unblocks it. A blocker without an owner gets flagged, not invented.
3. Pull out decisions: anything that needs a call from someone outside the team.
4. Compare with `{{PREVIOUS_UPDATE}}` when given: new risks, resolved blockers, slipped dates.
5. Assign a status per workstream: On track, At risk, Off track. Give one reason for anything not On track.
6. Draft the update for `{{AUDIENCE}}`. Drop routine progress that does not change status.

## Output format

**`{{PROGRAM_NAME}}` update, <Month D>**
**Bottom line:** one sentence.

| Workstream | Status | Change since last | Note |
|---|---|---|---|

**Blockers** (owner, since, unblock path)
**Decisions needed** (question, who decides, by when)
**Next `{{CADENCE}}` focus** (3 bullets max)

*Gaps: anything the notes did not answer. What was assumed: listed explicitly.*

## Rules
- Never invent owners, dates or numbers. Mark them [TBD].
- Keep names to roles unless the audience needs names.
- Keep confidential or customer data out of the update.
- No em dashes, no sentences starting with "I", American dates.
