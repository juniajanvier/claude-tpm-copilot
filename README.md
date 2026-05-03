# Claude TPM Copilot

> AI-powered workflows for technical program managers, built on Anthropic's Claude.

🚧 **Status:** Active development — v0.1 in progress.

---

## Why this exists

Technical program managers spend a huge portion of their time on the same handful of tasks: writing PRDs, summarizing status, tracking dependencies across teams, drafting stakeholder updates, and translating technical realities into executive context. These are exactly the kinds of tasks Claude is built to accelerate — but the tooling to do this well doesn't exist yet in a TPM-shaped form.

Claude TPM Copilot is a set of opinionated workflows and lightweight CLI tools that help TPMs operate at higher leverage without sacrificing rigor.

---

## What's coming in v0.1

A single CLI tool: **PRD generator**.

- Input: raw meeting notes (markdown or plain text)
- Output: a structured PRD with problem statement, goals, non-goals, requirements, risks, and open questions
- Uses Anthropic SDK with structured outputs
- Configurable model: Sonnet 4.6 default, Opus 4.7 for higher-stakes drafts

```bash
$ claude-tpm prd --input meeting-notes.md --output prd.md
```

## Roadmap

- [ ] v0.1 — PRD generator (in progress)
- [ ] v0.2 — Status synthesizer (pull from Jira/Linear/Notion exports → stakeholder summaries)
- [ ] v0.3 — Dependency mapper (surface cross-team blockers from project docs)
- [ ] v0.4 — Risk register builder
- [ ] v0.5 — Stakeholder voice tuner (rewrite same update for exec / eng / partner audiences)

## Stack

- Python 3.11+
- Anthropic Python SDK
- Claude Sonnet 4.6 / Opus 4.7
- Click for CLI
- Pydantic for structured outputs

## Why I'm building this in public

I'm a Senior TPM who uses Claude every day. The patterns I've stumbled into are too useful to keep to myself, and the AI tooling space for non-engineers in technical roles is still wildly underserved. Building in the open also keeps me honest about quality.

If you're a TPM, AI tools builder, or someone at Anthropic reading this — I'd love to hear from you.

## Author

Junia Janvier — [juniajanvier.com](https://juniajanvier.com) · [@juniajanvier](https://github.com/juniajanvier)
