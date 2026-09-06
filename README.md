# Antislop

Antislop is a portable website-audit skill and Claude Code plugin for reviewing developer-built or AI-generated websites. It tests whether a website accurately represents its product and audience before assessing generic AI design patterns, synthetic copy, credibility, personality, UX, accessibility, and responsive behavior.

## What This Repository Does

Antislop reviews a live URL, a local frontend repository, or both. It first infers the
product and audience, then evaluates whether the presentation is specific, credible,
human, usable, and visually appropriate—without treating unknown backend behavior as a
frontend defect.

## Quick Start

Install this directory as `antislop` in the Codex skills directory:

```bash
cp -R /path/to/antislop-skill/plugins/antislop/skills/antislop ~/.codex/skills/antislop
```

Then invoke it with a URL or the current repository:

```text
$antislop https://example.com
$antislop me
```

## Common Commands

This repository is a marketplace containing one shared plugin. The canonical skill lives
at `plugins/antislop/skills/antislop/` and is packaged for both Claude Code and Codex.

Run the local fixture suite:

```bash
python3 tests/run.py --list
python3 tests/run.py --case case-001
```

Validate the skill and Claude plugin:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  plugins/antislop/skills/antislop
claude plugin validate .
claude plugin validate plugins/antislop
python3 ~/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py \
  plugins/antislop
```

`$antislop me` means: discover and review the frontend or landing page in the
current working directory. It uses project scripts, framework routes, package
metadata, templates, assets, and rendered navigation to find the target. It
does not require an `index.html`, and it does not mean review the Antislop
skill source itself.

To review one example, enter its directory first:

```bash
cd examples/case-001
```

Then invoke:

```text
$antislop me
```

For a URL, Antislop infers the product dossier from the site before judging
its copy, visual system, UI, UX, credibility, and conversion path.

For a repository, run or preview the frontend when safe and distinguish
verified implementation findings from URL-only inferences.

For a GitHub-hosted repository, give Codex the repository URL and ask it to install the
skill, or use the standalone copy command above.

With the built-in installer:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo maxbov1/antislop \
  --path plugins/antislop/skills/antislop
```

## Install in Claude Code

For local development or a checkout, load the plugin directly:

```bash
claude --plugin-dir /path/to/antislop-skill/plugins/antislop
```

Inside that Claude session, run `/help` and invoke the namespaced skill. For example:

```text
/antislop:antislop https://example.com
/antislop:antislop me
```

`$antislop` is the standalone Codex skill syntax. Run `/reload-plugins` after changing
the checkout during the same Claude session.

To install from a published marketplace, use the marketplace’s instructions. For the
Anthropic community marketplace, the eventual flow is:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install antislop@claude-community
```

The exact install command becomes available after marketplace review and publication.

This repository also contains marketplace catalogs at
`.claude-plugin/marketplace.json`. After publishing it to GitHub, users can add the
repository and install the plugin from its catalog:

```text
/plugin marketplace add maxbov1/antislop
/plugin install antislop@antislop
```

Codex/ChatGPT workspace users can add the repo marketplace with:

```text
codex plugin marketplace add maxbov1/antislop
```

The Codex marketplace catalog lives at `.agents/plugins/marketplace.json`. The plugin
package itself is under `plugins/antislop/` and contains the shared skill at
`plugins/antislop/skills/antislop/SKILL.md`.

For local testing of the catalog:

```text
/plugin marketplace add /path/to/antislop-skill
/plugin install antislop@antislop
```

## Example Prompts

```text
Use Antislop to review https://example.com and its repository. Start by checking whether the website accurately represents the product, then audit the copy, visual system, UX, credibility, responsiveness, and implementation. Do not edit anything.
```

```text
Use Antislop to review this landing page repository. Run it locally if safe, identify the five highest-impact problems, and map each recommendation to the relevant component or file.
```

```text
Use Antislop on this live URL only. Clearly distinguish observations from inferences and mark anything that cannot be verified.
```

```text
$antislop me
```

## Design Principle

Antislop does not treat gradients, cards, bento grids, animation, or other popular styles as automatic violations. It reports them when they make the website interchangeable, unsupported, misleading, or less useful for the actual product and audience.

## Development and release

The public `examples/` are multi-page HTML fixtures for behavioral evaluation. The
ignored `tests/` directory contains local runners and evaluator-only labels; it is
intentionally not part of releases. See [CONTRIBUTING.md](CONTRIBUTING.md) for the test
workflow and [CHANGELOG.md](CHANGELOG.md) for release notes.

Before publishing a Claude plugin, validate it with:

```bash
claude plugin validate .
```

Replace the placeholder GitHub URLs in `.claude-plugin/plugin.json` before release.

## Repository Layout

See [ARCHITECTURE.md](ARCHITECTURE.md) for the component and evidence flow. See
[CONTRIBUTING.md](CONTRIBUTING.md) for development and review conventions.

## License

MIT
