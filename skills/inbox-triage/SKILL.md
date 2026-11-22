---
name: "inbox-triage"
description: "Triage one or more email inboxes into [DELETE], [REVIEW], and [REPLY] labels when the owner asks to organize, sort, triage, or clean up their email. Labels only; never deletes, archives or sends."
---

# Inbox triage

Sort every untriaged inbox thread into one of three existing labels. Label only: never archive, trash, delete, unsubscribe, reply, send, or mark read. The owner does the final deleting and replying.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Inbox owner |
| `{{PRIMARY_ACCOUNT}}` | Main mailbox reached through the Gmail connector |
| `{{SECONDARY_ACCOUNT}}` | Business mailbox reached through Gmail web in the browser |
| `{{SECONDARY_ACCOUNT_INDEX}}` | The `/mail/u/N` index for the secondary account |
| `{{OPTIONAL_ACCOUNTS}}` | Other mailboxes, triaged only if already signed in |
| `{{LABEL_IDS}}` | Connector label IDs for [DELETE], [REVIEW], [REPLY] (re-check with list_labels each run) |
| `{{REVIEW_CATEGORIES}}` | Owner-specific senders and programs that always count as REVIEW (government registrations, boards, contracts, fellowships) |

Trigger phrases: "clean up email", "clean up my inbox", "triage my inbox", "sort my email". Default scope is `{{PRIMARY_ACCOUNT}}` and `{{SECONDARY_ACCOUNT}}`, plus any other account the owner names.

## Accounts

| Account | How to reach it |
|---|---|
| `{{PRIMARY_ACCOUNT}}` | Gmail connector. Label IDs: `{{LABEL_IDS}}` (re-check with list_labels; output is large, so filter the saved file for names matching `^\[(DELETE|REVIEW|REPLY)\]$`). A large inbox (300+ threads) can go to a background subagent with these rules so browser work on the other inbox runs in parallel. |
| `{{SECONDARY_ACCOUNT}}` | Browser, Gmail web at `mail.google.com/mail/u/{{SECONDARY_ACCOUNT_INDEX}}` (confirm the page title shows this address) |
| `{{OPTIONAL_ACCOUNTS}}` | Only if already signed in (check `/mail/u/N` titles). If not, say so and ask the owner to sign in; never enter passwords |

## Finding untriaged mail

- Query: `in:inbox -label:[DELETE] -label:[REVIEW] -label:[REPLY]` (label names unquoted; the quoted form `-label:"[DELETE]"` silently matches everything). This catches threads that carry other labels too. Loop until it returns nothing, and finish with this query as the completeness check.
- Sanity-check the syntax once per run with `label:[REVIEW]` (should return threads). In personal accounts every inbox thread carries a system or category label, so `has:nouserlabels` returns nothing; do not use it as a fallback.
- Labels are per message: threads with an unsent draft or a newer message can keep matching the query after labeling. If the leftovers are threads just labeled, the run is complete.
- A thread whose new message arrived after it was labeled can lose the label on the new message; relabel the whole thread.
- Connector: label_thread one call per thread, fired in large parallel batches.

## Gmail web procedure (browser account)

1. Navigate to `mail.google.com/mail/u/{{SECONDARY_ACCOUNT_INDEX}}/#search/` plus the URL-encoded query. Wait 5+ seconds; an early read can still show the previous page.
2. Read rows with JS from the VISIBLE main pane only: `[...document.querySelectorAll('div[role=main]')].find(m=>m.offsetParent)`, rows `tr.zA`, sender `.yX`, subject `.bog`, thread id from `[data-thread-id]`. Store them in `window._rows` and print about 20 rows per call, stripping symbols with `.replace(/[^A-Za-z0-9 ,\/:'-]/g,'')` (tool output truncates near 1,500 characters, and some characters trigger a content block).
3. Put decisions in `window._L = {REPLY:[...], REVIEW:[...], DELETE:[...]}` by row index and verify every index is assigned exactly once.
4. Tick checkboxes (`div[role=checkbox]`) by thread id, not position, because the list re-sorts after each label is applied. Untick everything first.
5. Open the label menu by CLICKING the toolbar Labels icon (take a screenshot to locate it). Never type label names while the message list has focus: Gmail keyboard shortcuts (e, y, [, ], l) can archive or act on the selection.
6. In the menu, click the label's row. If other labels show as indeterminate, an Apply button appears; click it. Otherwise the click applies immediately. Confirm with the toast ("N conversations added to ...").
7. Re-run the query to confirm completeness.
8. Keep the Gmail tab in the foreground while working; if another agent drives a different tab in the same window, Gmail can freeze. One browser task at a time.

## Rules

**[REPLY]**: someone is waiting on the owner. Direct asks, meeting requests, "let us know your availability," endorsement or recommendation requests, a person whose latest message is unanswered and asks something. Threads with a Claude-drafted reply stay in [REPLY] until the owner sends.

**[REVIEW]**: needs eyes or an action, but not a written reply.
- Money problems: insufficient funds, failed or declined payments, late-fee warnings, low-balance only if no insufficient-funds alert already covers it
- Security: account recovery, password changes or reset requests, new sign-ins, security plugin "problems found" (newest only), admin risk notices, payment-account limits or a new address added
- Interviews, recruiter scheduling confirmations, job alerts that match target roles
- Appointments and bookings that are still upcoming
- Subscription renewals or trials ending soon, new paid plans, price changes, billing warnings
- `{{REVIEW_CATEGORIES}}`
- Newsletter replies that are friendly but need no reply, bounces and "no longer at" notices (list cleanup), campaign results
- Notes-to-self, insurance statements, records requests, community events worth attending

**[DELETE]**: everything else.
- Promotions and retail marketing
- Unsolicited program and school marketing and info sessions
- Routine receipts, payment confirmations, autopay notices, statements, ride receipts, mail digests, shipping and delivery updates
- Verification codes, one-time passwords, "verify your email," welcome emails, terms updates, plugin auto-update notices
- Past-dated reminders and calendar notices, out-of-office auto-replies, application-received and still-under-review notices, rejections, feedback surveys
- Newsletters the owner did not write, Slack/Meetup digests, contact-form spam

When unsure between DELETE and REVIEW, choose REVIEW. When the thread is mid-conversation, open it before deciding.

## Wrap-up

Report counts per account and label, then a short list of the [REPLY] items and the time-sensitive [REVIEW] items (deadlines, payment failures, security alerts, appointments in the next week). Name any account that could not be reached.
