---
name: "network-playbooks"
description: "Prep for an event, negotiate a rate or contract, or reconnect with a cold contact, and log follow-ups on a tiered Network tab in the tracker."
---

# Network playbooks (Event Strategy, Negotiation, Reconnect)

Use when the owner says things like "prep me for [event]", "help me negotiate [fee/contract/comp]", "reconnect script for [person]", or "who should I reach out to".

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Person the playbooks are for |
| `{{OWNER_TITLE}}` | Correct job title, if mentioned |
| `{{TRACKER_SHEET_ID}}` | Tracker spreadsheet holding the Network tab |
| `{{OUTREACH_PHONE}}` | Business phone used in outreach (never a personal line) |
| `{{LICENSE_JURISDICTION}}` | Where any professional license applies (e.g. one state) |
| `{{CRM_TOOL}}` | Tool that sends client texts, if any |
| `{{LEGAL_REVIEW_RESOURCE}}` | Where contracts can go for review (a clinic or a lawyer) |
| `{{EXISTING_RATE_CLIENTS}}` | Past or current low-rate engagements that must not become the anchor |

## Writing rules (always)
- No em dashes. Never open a sentence with "I". Avoid "passionate about", "dedicated to", "spearheading", "at the intersection of".
- Say "equity-centered" or "community-centered", never "DEI".
- Title, if mentioned: `{{OWNER_TITLE}}`. Dates are American style (October 14).
- Licensed work: stay inside `{{LICENSE_JURISDICTION}}`. Client texts go through `{{CRM_TOOL}}`. Phone for outreach: `{{OUTREACH_PHONE}}`.

## Where contacts live
Tracker (`{{TRACKER_SHEET_ID}}`), tab "Network". Columns: Name, Circle, Role / Org, Tier (A every 30 days, B 90, C 180; cadence cells are configurable), How We Met, Last Touch, Next Touch (calc), Days Left (calc), Status (calc), Next Move, Give First, Notes, Link. Never type in the calculated columns. A weekly standing row on the tracker is the habit.
Offer to add new people met or touched as rows, with Last Touch set to the date.

## Event Strategy
Ask only what is missing: event, date, goal, who will be there.
Output: one measurable goal (number of conversations and follow-ups), Before (target list, one-sentence intro, materials), During (opener about their work, three things to listen for, a specific closing ask, log on the Network tab), After (48-hour follow-up template). Tie to open tracker items when relevant (certifications, partnerships, speaking proposals).

## Negotiation Script
Covers speaking fees, consulting or training contracts, brand deals, and day-job compensation.
Always: anchor, target, walk-away numbers (the owner supplies them; never invent rates); package pricing over hourly; scripts for "what's your rate", "over budget", "can you do it free"; rules (say the number and stop, trade never discount, get it in writing). Keep `{{EXISTING_RATE_CLIENTS}}` rates from becoming the anchor. Close with a short note that this is not legal or financial advice and contracts can go to `{{LEGAL_REVIEW_RESOURCE}}`.
For day-job compensation: focus on outcomes and calibration evidence; do not give confident financial advice.

## Reconnect Script
Formula: real trigger, ask about them first, one line of the owner's news, one small ask, no apology for the gap. Give a short text version and an email version. Check the Network tab for context and Next Move first. For a real estate sphere, no hard sell and stay inside the licensed jurisdiction.

## Deliverable
Short playbooks go in chat. Several at once, or anything reusable, go in a shared doc.
