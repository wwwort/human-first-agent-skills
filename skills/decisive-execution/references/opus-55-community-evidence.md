# Community evidence used for `decisive-execution`

## Provenance

This note records the evidence summary preserved in the referenced ChatGPT conversation “生成果断执行技能”. The source conversation described a completed `decisive-execution` package and cited community discussions, independent practice reports, Hacker News comments, and Anthropic material. The links themselves were not included in the bounded handoff available to this installer, so the claims below are a behavioral rationale, not a fresh benchmark or an independently verified performance result.

## Repeated praise themes

The conversation grouped positive Opus 5.5 reports around:

- carrying more intermediate decisions without repeated user steering;
- building a broader working model of a codebase and noticing related issues;
- better judgment with less drift, less context switching, and less rework;
- smaller changes, more testing, self-checking, and long-running multi-step work;
- simplifying code and respecting existing responsibility boundaries.

The useful target for this skill is the interaction pattern behind those reports: choose a reasonable path, keep moving, inspect the relevant context, verify the result, and return only decisions that genuinely require the user.

## Counterevidence and limits

The same conversation recorded reports of overconfident investigations, account-takeover exposure, and agents trusting delegated summaries without reading the underlying diff. Therefore decisiveness must be paired with evidence, scope isolation, and explicit gates for irreversible external effects. The skill cannot change model routing, quotas, hidden system instructions, tool permissions, or underlying capability.
