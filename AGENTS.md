# Agent guidance

## Repository Overview

This repository contains the Antislop website-audit skill and its Claude Code plugin
metadata. The canonical instructions are in `SKILL.md`.

## High-Risk Areas

Changes to `SKILL.md` and `references/` alter how agents judge real websites. Changes to
the evidence contract, severity definitions, or fixture labels can make benchmark results
look better without improving the skill.

## Required constraints

- Preserve the presentation-only audit boundary in `SKILL.md`.
- Do not turn one fixture’s taste or defect into a universal rule without broader evidence.
- Keep evidence labels and the authority-conveyed-by-interface rule intact.
- Keep `tests/` ignored; fixture labels and benchmark notes are evaluator-only.
- Use `apply_patch` for edits and run `git diff --check` before handoff.

## Preferred workflow

- Read only the reference needed for the change.
- Add or update a fixture when a behavioral change needs validation.
- Validate with the skill quick validator and, for Claude packaging changes, `claude
  plugin validate . --strict`.
- Do not include private URLs, credentials, or generated customer reports.
