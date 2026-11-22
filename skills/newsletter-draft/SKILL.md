---
name: "newsletter-draft"
description: "Draft an issue of a local community newsletter (personal brand plus a real estate practice) in a fixed 12-section, gamified format for Mailchimp."
---

# Local newsletter draft

Use when the owner asks to draft, outline, or brainstorm a newsletter issue ("draft Issue #3", "newsletter time", "start the next issue"). For a full paste-ready HTML build, use newsletter-html-build instead.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Newsletter author |
| `{{BRANDS}}` | Brands the single list serves, e.g. an education brand plus a brokerage practice |
| `{{BROKERAGE}}` | Brokerage name, if real estate is included |
| `{{REGION}}` | Region the newsletter covers, e.g. a state |
| `{{CITY}}` | Main city for the local events section |
| `{{AUDIENCE}}` | Who reads it (past clients, leads, agents, community, professional network) |
| `{{LICENSE_JURISDICTION}}` | Where the real estate license applies |
| `{{FEATURED_LISTING}}` | Listing to lead with while active, if any |
| `{{LANGUAGE_CORNER}}` | Language for the phrase-of-the-issue corner |
| `{{OWNER_TITLE}}` | Correct job title, if mentioned |

## What the newsletter is
- One Mailchimp list serving `{{BRANDS}}`.
- Promise: real estate updates, tech, local happenings, and community events for `{{REGION}}`.
- Audience: `{{AUDIENCE}}`.
- One central template (no brand variants), gamified and engaging.

## Before drafting
1. Ask for the issue number and send date if not given.
2. Ask what's new this cycle: listings (lead with `{{FEATURED_LISTING}}` while active), events attended or hosted, tech or education work, anything in the Content Bank. If a Newsletter Creation Guide is pasted, use its Content Bank.
3. Search the web for current `{{CITY}}` and `{{REGION}}` events in the two to three weeks after the send date, one strong local stat, and one relevant tech story. Cite sources; summarize in your own words.

## Fixed section order (every issue)
1. **Opening line**: one warm, specific sentence.
2. **One stat, one take**: a single number (local housing, tech, or education) plus a one-line take.
3. **The big story**: the lead item, 120 to 180 words.
4. **Tech Tea**: one tech or AI story explained plainly and why it matters to local readers.
5. **What I'm Up To**: recent and upcoming work, speaking, and events.
6. **On the market**: listings, leading with `{{FEATURED_LISTING}}` when active. Real estate stays inside `{{LICENSE_JURISDICTION}}`.
7. **Explore `{{CITY}}`**: two or three local events or spots with dates.
8. **Ear + Tongue**: one song recommendation (title and artist only, never lyrics) and one `{{LANGUAGE_CORNER}}` phrase with meaning and a pronunciation hint.
9. **Reply prompt**: default is asking readers what events or questions they want covered next.
10. **One rotating CTA**: exactly one per issue (book a call, join a club, share the newsletter, giveaway entry).
11. **Next-issue tease**: one line.
12. **Sources**: links for every stat, story, and event.

## Gamified elements
Work in one or two per issue, rotating: guess-the-number tap, true/false, progress bar, passport stamp for the local section, scoreboard, one-tap rating. Describe how each is built in Mailchimp (poll links, button blocks, emoji bars).

## Rules
- Under 900 words total.
- Subject line names the specific thing inside. Offer three options plus preview text.
- One CTA only.
- Writing rules: no em dashes; never begin a sentence with "I"; avoid "passionate about," "dedicated to," "spearheading," "at the intersection of"; use "equity-centered" or "community-centered," never "DEI"; American dates ("October 14"); title is `{{OWNER_TITLE}}` if mentioned.
- Never reproduce lyrics or long article text.

## Output
Deliver the issue as an editable document ready to paste into Mailchimp, with section headers matching the order above, then a short list: word count, the CTA used, and which gamified elements appear. Finish by suggesting two Content Bank items to save for the next issue.
