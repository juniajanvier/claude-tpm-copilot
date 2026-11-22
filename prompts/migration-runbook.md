# Migration runbook

Generates pre-flight, cut-over, and rollback runbooks for a data or platform migration. Built for migrations where a bad cut-over is expensive and every step needs an owner and a go/no-go gate.

## Variables

| Variable | Meaning |
|---|---|
| `{{MIGRATION_NAME}}` | Short name of the migration |
| `{{SOURCE_SYSTEM}}` / `{{TARGET_SYSTEM}}` | Where data lives today and where it is going (generic descriptions are fine) |
| `{{SCOPE}}` | What moves: record counts, entities, tables, consumers |
| `{{CUTOVER_STRATEGY}}` | Big bang, phased by cohort, dual-write, or shadow read |
| `{{WINDOW}}` | Planned cut-over window and time zone |
| `{{ROLES}}` | Roles involved (e.g. migration lead, data engineer, QA, support, comms) |
| `{{CONSTRAINTS}}` | Regulatory, audit, downtime or SLA limits |

## Prompt

```
Act as a senior program manager writing a migration runbook that an on-call engineer
could execute at 2 AM without asking questions.

Migration: {{MIGRATION_NAME}}
Source: {{SOURCE_SYSTEM}}  Target: {{TARGET_SYSTEM}}
Scope: {{SCOPE}}
Strategy: {{CUTOVER_STRATEGY}}
Window: {{WINDOW}}
Roles: {{ROLES}}
Constraints: {{CONSTRAINTS}}

Produce three runbooks plus a summary.

A. Pre-flight (T-14 days to T-0)
   Numbered checklist. Each step: owner role, action, evidence of done, due (T-minus).
   Must include: data profiling and reconciliation baseline, mapping sign-off,
   dry run on production-like data with timing, rollback rehearsal, consumer inventory,
   comms plan, freeze scope, support readiness, final go/no-go meeting.

B. Cut-over (T-0)
   Timestamped steps relative to start (T+0:00). Each step: owner, command or action,
   expected result, verification query or check, and STOP condition.
   Insert explicit go/no-go gates after data load, after reconciliation, and before
   traffic switch. State who makes each call.

C. Rollback
   Trigger criteria (measurable thresholds), point of no return and why,
   ordered rollback steps with owners, data reconciliation after rollback,
   and the comms message template.

D. Summary table
   Phase, duration estimate, critical path step, top risk, mitigation.

Reconciliation must compare counts, checksums or sampled field-level diffs between
source and target, with an agreed tolerance. Never assume a tolerance; mark it [TBD].
No em dashes. American dates. End with a "What was assumed" footer.
```

## Output check
- Every step has a single owner role and a verification.
- Rollback triggers are numbers, not adjectives.
- The point of no return is named.
