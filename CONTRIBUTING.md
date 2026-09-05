# Contributing to Antislop

Thanks for helping improve Antislop. The goal is a sharper, more useful audit—not a
larger checklist.

## Development Setup

This is a dependency-free instruction package. Python 3 is used for the local fixture
server, and Claude Code is optional for plugin validation.

## What makes a good change

- It improves a decision the skill makes in a realistic website review.
- It is grounded in repeated evidence or a clear failure mode, not one personal taste.
- It preserves the presentation-only boundary: unknown backend behavior is not a defect.
- It names what is missing or misleading and explains the visitor or business impact.
- It keeps recommendations specific to the product and audience inferred from the page.

## Repository layout

- `SKILL.md` is the canonical skill instruction file.
- `references/` contains focused guidance and the report template.
- `examples/` contains public, URL-only HTML fixtures for manual evaluation.
- `tests/` is local-only and ignored; it may contain private labels and benchmark notes.
- `.claude-plugin/` contains Claude Code plugin metadata.
- `agents/` contains Codex UI metadata and is not required by Claude Code.

## Testing

```bash
python3 tests/run.py --list
python3 tests/run.py --case case-001
claude --plugin-dir .
```

Inside Claude Code, invoke the namespaced skill shown by `/help`. Run `/reload-plugins`
after editing plugin files during a development session.

Do not add tests that assert one exact generated paragraph. Prefer tests for fixture
coverage, route discoverability, and stable evaluation invariants.

## Pull Request Process

Describe the observed failure, the rule or reference changed, and how you evaluated it.
Include before/after reports when a behavioral change is intentional. Do not include
private customer sites, API keys, or generated reports containing sensitive content.
