# Architecture

## System context

Antislop is an instruction package, not a runtime service. An agent loads `SKILL.md`,
selectively reads the focused references, and audits either a live URL or a frontend found
in the current repository.

## Components

- `SKILL.md`: canonical workflow, scope boundary, evidence contract, and report rules.
- `references/product-fit.md`: product dossier and fit guidance.
- `references/slop-patterns.md`: patterns to investigate without treating style as guilt.
- `references/report-template.md`: output structure.
- `.claude-plugin/plugin.json`: Claude Code plugin identity and release metadata.
- `agents/openai.yaml`: Codex display metadata and invocation policy.
- `examples/`: tracked multi-page fixtures for behavioral evaluation.
- `tests/`: ignored local runner and evaluator-only labels.

## Data flow

```text
URL or `me`
  -> discover routes/frontend
  -> infer product dossier from visible evidence
  -> inspect copy, visual system, UI, UX, credibility, responsive behavior
  -> classify observations as observed/inferred/unknown
  -> prioritize visitor/business impact
  -> produce the report template
```

The skill does not require a backend, database, API, or model-serving dependency. Browser
tooling is optional and only strengthens runtime evidence.

## Runtime and dependencies

The package has no application dependencies. Development uses Python 3 for the ignored
fixture server and Claude Code for plugin validation. Codex reads `agents/openai.yaml`;
Claude Code does not require that file.

## Operational concerns

Keep private audit reports and customer URLs out of the repository. Preserve the
presentation-only boundary: unknown backend behavior must remain unknown unless a visible
interaction demonstrates a problem. Update the changelog when the audit contract changes.
