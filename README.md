# Antislop

Antislop reviews developer-built and AI-generated websites for product fit, credibility,
personality, UX, accessibility, responsive behavior, and generic AI design patterns.

## Install

Anthropic / Claude Code:

```bash
claude plugin install antislop@antislop
```

OpenAI / Codex:

```bash
codex plugin add antislop@antislop
```

Then invoke Antislop with a URL or the current repository, for example `$antislop
https://example.com` or `$antislop me`.

## Example prompts

```text
Use Antislop to review https://example.com for product fit, credibility, UX, and AI slop.
```

```text
Use Antislop to review this repository's frontend and identify the five highest-impact problems.
```

## Design principle

Antislop does not treat gradients, cards, bento grids, animation, or other popular styles as
automatic violations. It reports them when they make the website interchangeable,
unsupported, misleading, or less useful for the actual product and audience.

## Repository layout

The canonical skill lives at `plugins/antislop/skills/antislop/`. Marketplace metadata is
stored in `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`.
