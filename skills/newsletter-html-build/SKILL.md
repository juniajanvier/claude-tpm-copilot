---
name: "newsletter-html-build"
description: "Draft and build the next issue of a monthly Mailchimp newsletter as paste-ready, accessible, dark-mode-safe HTML that matches an approved master design, plus a browser fact-check prompt."
---

# Newsletter HTML build

Use when the owner asks to draft, build, refresh, or fact-check a newsletter issue ("newsletter time", "draft Issue 2", "start the next issue").

## Placeholders

| Variable | Meaning |
|---|---|
| `{{NEWSLETTER_NAME}}` | Newsletter title (HTML-escape apostrophes, e.g. `&rsquo;`) |
| `{{TAGLINE}}` | Masthead tagline |
| `{{AUTHOR_NAME}}` | Byline and sign-off name |
| `{{SITE_URL}}` | Author's website |
| `{{REFERENCE_ISSUE_URL}}` | Archive link to the approved master issue |
| `{{SIGNUP_URL}}` | List signup link |
| `{{SOCIAL_LINKS}}` | Instagram, LinkedIn and similar |
| `{{BUSINESS_EMAIL}}` | Contact address shown in the footer |
| `{{LOGO_URL}}` | Hosted logo file |
| `{{HEADSHOT_URL}}` | Hosted square-cropped headshot |
| `{{MEDIA_HOST}}` | Where images are hosted, e.g. a WordPress media library path |
| `{{BROKERAGE}}` | Brokerage name, if real estate is included |
| `{{BROKERAGE_DISCLAIMER}}` | Required brokerage trademark and fair housing text |
| `{{LICENSE_LINE}}` | License line, e.g. "Licensed in <state>, <license no.>" |
| `{{BUSINESS_PHONE}}` | Business phone shown in the footer |
| `{{MAILING_ADDRESS}}` | Business mailing address required by CAN-SPAM (never a home address) |
| `{{FEATURED_LISTING}}` | Current listing: name, URL, logo, address, facts that are safe to state |
| `{{REGION}}` / `{{CITY}}` | Coverage area and spot-of-the-month city |
| `{{MARKET_DATA_SOURCE}}` | Primary source for the monthly market stat (cite it directly) |
| `{{LANGUAGE_CORNER}}` | Language for the phrase-of-the-month box |
| `{{SOP_DOC}}` | Internal SOP that mirrors the section order |

## Reference issue
The approved master design is `{{REFERENCE_ISSUE_URL}}`. Mailchimp archive pages often block automated readers, so build from HTML the owner pastes (campaign archive RSS or an HTML export). Match its structure, spacing, classes, and section styles exactly unless asked for a change.

## Identity (use exactly)
- Name: **`{{NEWSLETTER_NAME}}`**; masthead tagline `{{TAGLINE}}`
- Byline: From `{{AUTHOR_NAME}}` · `{{SITE_URL}}`
- Sign-off: "Until next time, `{{AUTHOR_NAME}}`" with the logo beside it
- Scope: a five-minute regional roundup of local happenings, real estate, and a little tech.
- Cadence: monthly. One list serving every brand the author runs.

## Section order (master design)
Masthead (dark: logo left; "Issue N · Month D, YYYY" and View in browser right; h1 title, italic tagline, byline) > "In this issue" band (one sentence listing 4 to 5 highlights) > white card:
1. **Welcome + intro with headshot** (headshot left, welcome line + 2 to 3 sentence intro right)
2. **One stat, one take** (big number, short rule, one-line take; cite `{{MARKET_DATA_SOURCE}}`)
3. **On the market** (countdown chip to the next open house when there is one; listing card with image/logo panel, name, address, 3 chips, short description, bold open house line, "See the listing" button)
4. **What I'm up to** (one personal or community update; may carry its own button pair)
5. **Tech Tea** (two "Sips": one legal-tech or socially relevant story, one regional tech story; end with a one-line reply poll)
6. **Things to do** (grouped under small uppercase subheads: seasonal, Move your body, After dark, Meet people)
7. **Explore `{{CITY}}`** (one "Spot of the month" with what to order, plus one hosted image or GIF at 520px)
8. **`{{LANGUAGE_CORNER}}` of the Month** (phrase, pronunciation, meaning, the reply, "Try it on someone this week")
9. **Heads up** (one timely civic or practical line, e.g. voting dates)
10. **Reply prompt**: "Hit reply and tell me: what events or questions should I cover next?"
11. **Share CTA** ("Know someone who'd love this?" + "Share the signup link" button to `{{SIGNUP_URL}}`)
12. **Next issue tease + sign-off**
13. **Sources this issue** (one linked line per source)
Footer.

Skipping: any section can be skipped for one issue when there is nothing strong for it. It stays in the standard order and in the master file. Ask which sections to skip if it isn't clear.

Parked blocks (giveaway, big story, progress bars, reel card, scoreboard) are not used unless asked. Leave an HTML comment where a parked block would sit (e.g. `<!-- GIVEAWAY PARKED -->`); never delete them from the master.

## Footer (in this order)
`{{AUTHOR_NAME}}`; "REALTOR®, `{{BROKERAGE}}` · `{{BUSINESS_PHONE}}` · `{{LICENSE_LINE}}`"; one line on the author's other brand; links (`{{SOCIAL_LINKS}}`, `{{BUSINESS_EMAIL}}`); `{{BROKERAGE_DISCLAIMER}}`; "Equal Housing Opportunity. Market figures come from the sources listed above and are not a guarantee of value."; why the reader is getting this; `{{MAILING_ADDRESS}}`; update preferences / forward / unsubscribe; © year.
Never show a home address. Never imply licensed services outside the license jurisdiction.

## Design system
- Mailchimp "Code your own". Tables and inline styles only, 600px wrapper, light page background, white content card, 10px rounded corners on masthead top, cards, and footer bottom.
- Palette: define 8 to 9 named brand colors once in the top comment block (primary, dark, accents, page, card, muted) and reuse them.
- Fonts: one display serif and one body sans, each with a web-safe fallback, loaded from Google Fonts inside `<!--[if !mso]>`.
- Accessibility: light text only on the dark color; dark text on light surfaces; bright accents only as decoration, backgrounds with dark text, or display type 24px+. Body 16px, nothing under 12px, real h1/h2.
- Keep dark-mode guard classes (e.g. keep-dark, keep-white, ink, paper) and mobile classes (wrap, pad, stack, stack-gap, btn-link, masthead-title, stat-number).
- Section headers: 12px colored square + display h2 at 25px. Section padding 44px top (40px for the first two). Buttons rounded 24px.
- Keep the top-of-file comment block (issue number, date, subject, preview text, photo URLs, parked blocks, brand) updated each issue.
- Use Mailchimp merge tags, not hard-coded links: `*|ARCHIVE|*`, `*|UPDATE_PROFILE|*`, `*|FORWARD|*`, `*|UNSUB|*`, `*|CURRENT_YEAR|*`.
- Images: host at `{{MEDIA_HOST}}`. Email width 520 to 560px, upload at 2x, JPG under 200KB, GIF under 1MB (Outlook shows frame one). Gmail and Outlook ignore object-position, so upload square crops.

## Workflow
1. Ask for the issue number, send date, what's new (listings and open houses, personal update, a spot of the month with photos, the language phrase), and which sections to skip. Build from last issue's pasted HTML; otherwise ask for it.
2. Research for the 2 to 3 weeks after the send date: the latest market figure from `{{MARKET_DATA_SOURCE}}`, one legal-tech or socially relevant tech story, one regional tech story, and events across the Things to do subheads. Only include events confirmed on a real page. Never get around a paywall; use only what a public visitor sees and say so if a claim rests on a headline.
3. Write tight: about 600 words, skimmable. CTAs are clear buttons.
4. Build the full HTML file and send it, plus three subject lines naming specific things inside, preview text that complements (not repeats) the subject, and a reminder that subject and preview text are set in Mailchimp's fields, not in the code.
5. Give the owner one paste-ready prompt for Claude in their browser that (A) uploads new images to `{{MEDIA_HOST}}`, keeping file names and setting alt text, and returns the file URLs, and (B) fact-checks every item against its source with ✅ ⚠️ ❌ in one phone-friendly table, ❌ first. It must never edit, send, schedule, or test anything in Mailchimp.
6. After the owner reports back, apply fixes and resend.
7. `{{SOP_DOC}}` mirrors this section order; if the standard format changes, update both.

## Writing rules
No em dashes. Never begin a sentence with "I" (an approved "Hi! I'm <name>" intro is the one exception). Avoid "passionate about," "dedicated to," "spearheading," "at the intersection of." Say "equity-centered" or "community-centered," never "DEI." American dates ("October 18"). Never reproduce lyrics or long article text; paraphrase sources. Real estate copy follows fair housing: describe the property, not who it suits.
