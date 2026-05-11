# claude-tpm-copilot

> TPM workflow tools and prompt scaffolds built atop Claude.

A working collection of reusable prompts, skill files, and small utilities that compress senior TPM workflows. Built and tested against real platform work at scale (16M+ accounts, 30M+ account migrations).

## What's here

| Module | Purpose |
|---|---|
| /prompts/prd-skeleton | Structured PRD generation from a one-line problem statement |
| /prompts/migration-runbook | Pre-flight, cut-over, and rollback runbooks for data migrations |
| /prompts/exec-summary | One-pager for senior leadership readouts |
| /skills/standup-synthesizer | Reads raw standup notes and produces a leadership-grade async update |
| /skills/risk-register | Maintains a living risk register from PR comments, Slack threads, and meeting notes |

## Why this exists

Senior TPM work is mostly compression. Turning unstructured input (Slack, calls, Jira, design docs) into structured output (PRDs, decisions, runbooks, exec briefs) under time pressure. These tools systematize that compression.

## Design principles

1. **No fluff** (output reads like a senior practitioner wrote it)
2. **Stakeholder-aware** (every prompt asks who the audience is before drafting)
3. **Defensible** (explicit assumptions, risks, and unknowns surfaced, never hidden)
4. **Auditable** (every output includes a "what was assumed" footer)

## Status

In active development. Public for transparency. No proprietary information from any employer included.

---

*Junia Janvier · [juniajanvier.com](https://juniajanvier.com)*
