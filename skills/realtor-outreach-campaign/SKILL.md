---
name: "realtor-outreach-campaign"
description: "Build a FSBO/FRBO or geographic farming outreach campaign: branded postcards from an existing Canva template plus a 30-day text/email cadence and a compliance check."
---

# Real estate outreach campaign

## Placeholders

| Variable | Meaning |
|---|---|
| `{{AGENT_NAME}}` | Agent's name as printed |
| `{{BROKERAGE}}` | Brokerage name, printed on every piece |
| `{{LICENSE_JURISDICTION}}` | State(s) where the agent is licensed |
| `{{BUSINESS_PHONE}}` / `{{BUSINESS_EMAIL}}` / `{{SOCIAL_HANDLE}}` / `{{SITE_URL}}` | Contact block for the postcard front |
| `{{FSBO_TEMPLATE_ID}}` / `{{FRBO_TEMPLATE_ID}}` | Canva design IDs of the approved mailer templates |
| `{{BRAND_COLORS}}` | Named hex colors (primary, accent, dark panel, light text) |
| `{{SCRIPTS_DOC}}` | Doc holding the campaign scripts |
| `{{CRM_TOOL}}` | CRM that sends texts and emails and holds campaign tags |
| `{{BROKER_OF_RECORD}}` | Person who signs off on marketing |

## Postcards (Canva)
- Start from the existing template designs (`{{FSBO_TEMPLATE_ID}}`, `{{FRBO_TEMPLATE_ID}}`), never a blank generation. Never mail an old base design that still carries a prior brokerage's content.
- Copy the closest design, then swap only the hook (front) and the back message.
- Front: headshot; `{{BROKERAGE}}` in small caps; name in serif; "REALTOR® · SALES & RENTALS"; `{{BUSINESS_PHONE}}`, `{{BUSINESS_EMAIL}}`, `{{SOCIAL_HANDLE}}`, `{{SITE_URL}}`; Equal Housing logo; disclaimer.
- Back: dark panel, script "Hello!" and signature in the accent color, body in a light color; address panel right.
- Brand colors: `{{BRAND_COLORS}}`.
- Required on every piece: brokerage name, "Licensed in `{{LICENSE_JURISDICTION}}`", Equal Housing Opportunity, and a not-a-solicitation-of-listed-properties line.
- Show the preview and get approval before committing edits.

## Scripts (shared doc)
Reference: `{{SCRIPTS_DOC}}`. Sequence: Day 0 postcard, Day 4 intro email, Day 7 call (text only if Text-OK), Day 14 market snapshot email, Day 21 check-in, Day 30 last touch plus newsletter invite. Merge fields `{FirstName}`, `{Address}`, `{Street}`. `{{CRM_TOOL}}` tags per campaign plus Text-OK; any reply pauses the campaign.

## Compliance checklist
`{{BROKER_OF_RECORD}}` sign-off; texts only with prior consent (TCPA); scrub calls against Do Not Call; emails carry the office address and an unsubscribe line; skip properties already listed with a broker; newsletter adds only after a yes. Not legal advice.

## Writing rules
No em dashes, no sentence opening with "I", American dates. Fair housing: describe the property and the offer, never who it suits.
