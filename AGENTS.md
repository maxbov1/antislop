# Agent guidance

## Repository Overview

This repository contains the Antislop website-audit skill and marketplace packages for
Claude Code and Codex/ChatGPT. The canonical instructions are in
`plugins/antislop/skills/antislop/SKILL.md`.

## High-Risk Areas

Changes to the canonical `SKILL.md` and `references/` alter how agents judge real
websites. Changes to
the evidence contract, severity definitions, or fixture labels can make benchmark results
look better without improving the skill.

## Required constraints

- Preserve the presentation-only audit boundary in the canonical `SKILL.md`.
- Do not turn one fixture’s taste or defect into a universal rule without broader evidence.
- Keep evidence labels and the authority-conveyed-by-interface rule intact.
- Keep `tests/` ignored; fixture labels and benchmark notes are evaluator-only.
- Use `apply_patch` for edits and run `git diff --check` before handoff.

## Preferred workflow

- Read only the reference needed for the change.
- Add or update a fixture when a behavioral change needs validation.
- Validate with the skill quick validator and the relevant Claude/Codex plugin validators.
- Do not include private URLs, credentials, or generated customer reports.
