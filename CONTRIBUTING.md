# Contributing to Antislop

Thanks for helping improve Antislop. The goal is a sharper, more useful audit—not a
larger checklist.

## What makes a good change

- It improves a decision the skill makes in a realistic website review.
- It is grounded in repeated evidence or a clear failure mode, not one personal taste.
- It preserves the presentation-only boundary: unknown backend behavior is not a defect.
- It names what is missing or misleading and explains the visitor or business impact.
- It keeps recommendations specific to the product and audience inferred from the page.

## Repository layout

- `plugins/antislop/skills/antislop/SKILL.md` is the canonical skill instruction file.
- `plugins/antislop/skills/antislop/references/` contains focused guidance and the report template.
- `.claude-plugin/` and `.agents/plugins/` contain the Claude and Codex marketplace catalogs.
- `plugins/antislop/` contains the shared plugin package and its ecosystem manifests.

## Pull Request Process

Describe the observed failure and the rule or reference changed. Do not include private
customer sites, API keys, or generated reports containing sensitive content.
