---
name: antislop
description: Review developer-built or AI-generated websites against the actual product, audience, and repository, then identify generic AI design patterns, weak or synthetic copy, misleading product representation, UX problems, and implementation issues. Use when auditing a live URL, landing page, SaaS site, portfolio, generated frontend, or website repository for product-to-website fit, credibility, originality, conversion clarity, responsive behavior, accessibility, or "AI slop," and when producing prioritized design, copy, or code-level fixes.
---

# Antislop

Audit whether a website is the right website for its product before judging whether it is visually polished. Treat AI slop as an accumulation of unsupported, interchangeable, or unintentional decisions—not as a list of forbidden styles.

## Invocation Modes

The skill accepts one of two inputs:

- `$antislop <URL>`: review the supplied live or local URL. Treat the URL as
  the complete source of truth unless a repository is explicitly supplied too.
- `$antislop me`: review the current working repository's local frontend or
  landing page. Find the relevant app entrypoint, start or preview it when
  safe, and inspect the rendered result. Do not audit unrelated backend code.

For `me`, discover the frontend instead of assuming a filename or framework.
Inspect the current directory's project markers, package scripts, framework
configuration, route structure, static assets, and HTML entry points. Common
signals include a package manifest, a dev/build script, application route
files, templates, and public-page metadata. Prefer the rendered public landing
route or homepage identified by the app's routing and navigation. A static
`index.html` is one possible signal, not a requirement.

If the current working directory is itself a frontend directory, treat it as
the target. Do not search sibling directories or choose among examples unless
the user asks you to review the parent folder.

If `me` finds multiple plausible frontends in the current directory, identify
them and ask which one to review. If it finds no frontend or landing page, say
what was searched and ask for a URL or the frontend path.

Support a live URL, a local URL, a repository, or a URL plus repository. The
URL-only mode must remain useful because it is the normal public-site workflow.

If only a URL is supplied, perform the complete experience and copy review but
label implementation findings as inferred. If `me` or only a repository is
supplied, run or preview the frontend when safe; otherwise review the source
and clearly state that runtime behavior was not verified.

## Product Dossier First

Before judging the design, create an inferred product dossier from the visible
site or rendered frontend. Write it as part of the report, or save it as
`product.md` when the user asks for a durable artifact. Include evidence and
confidence for:

- Product category and actual job to be done
- Likely audience and buyer sophistication
- Business model and primary conversion motion
- Claimed capabilities and differentiators
- Likely business impact of the page
- Unknowns, contradictions, and unsupported claims

Do not treat inferred business impact as verified fact. Keep the original page
in view during the audit; the dossier is a working model, not a replacement
for the evidence.

## Presentation Scope

This is a presentation audit. Judge whether the visible site feels specific,
human, credible, usable, and appropriate for the inferred product and
audience. Assess copy, visual language, UI examples, navigation, responsive
behavior, accessibility, and the conversion path.

Do not penalize a URL-only site for an unverified backend, database, API,
authentication system, analytics setup, real customer data, or form endpoint.
Record those as unknowns when they matter. Only report implementation failure
when it is visible in the experience, such as a broken link, missing state,
overflow, inaccessible control, or a claim contradicted by available evidence.

Never create a finding solely because source HTML lacks a form `action`,
`method`, JavaScript handler, backend, confirmation message, loading state, or
error state. For static pages, those are not evidence of a presentation defect.
Assess the visible form's labels, hierarchy, affordance, and destination. Only
assess submission feedback when a reachable interaction visibly attempts to
submit and produces a broken or confusing state.

Do not include internal tool attempts, extraction status, API-key status, or
agent process notes in the user-facing report unless they directly limit what
was observed. Report the evidence limitation itself in plain language.

## Evaluation Contract

For every possible finding, classify the evidence as:

- Observed: directly visible in the page or a rendered interaction
- Inferred: a reasonable interpretation of visible evidence
- Unknown: cannot be established from the supplied material

Only report a finding when all three are true:

1. It is within the requested presentation scope.
2. It is supported by direct or clearly labeled inferred evidence.
3. It materially affects product understanding, trust, usability, personality,
   or the visitor's next decision.

Do not turn unknowns into defects. The absence of a product screenshot may be
noted as an evidence limitation or opportunity, but is not inherently
misleading. Raise its severity only when strong capability, performance, or
enterprise claims cannot reasonably be evaluated without evidence.

Audit the authority conveyed by the interface, not just the literal wording.
Disclaimers do not fully resolve a misleading impression when visual
hierarchy, precision, labels, personas, or data presentation imply more
certainty than the evidence supports.

Recommendations must answer what this specific product should say, show,
change, or remove. Avoid generic advice such as "add a workflow visual" unless
the recommendation names the product-specific workflow or decision it should
explain.

## Personality Test

Assess personality separately from polish. A site has personality when its
voice, vocabulary, examples, product motifs, restraint, or unusual but coherent
choices express a recognizable point of view for a specific audience.

Do not require unusual colors, typography, layouts, or illustration. Common
patterns are acceptable when they perform a clear product-specific job.

Use the substitution test: if the product name were replaced with an unrelated
product, would the section still feel natural? If yes, identify the missing
audience, mechanism, workflow, constraint, proof, or point of view. Do not
report "feels generic" without naming what is missing.

Bound live retrieval attempts. If initial navigation or rendering fails twice through the available methods, stop retrying. Enter degraded mode: record the retrieval failure, waive downstream route requirements, mark unsupported scorecard dimensions `N/V`, and request one of the following: screenshots at desktop and mobile widths, an exported page, or repository access. Never turn inaccessible evidence into a negative product finding.

Ask for missing product context only when the site and repository do not establish what the product does, who it serves, or what conversion it wants. Ask at most three focused questions. Do not ask for information that can be discovered from the supplied materials.

## Compose Existing Capabilities

Act as the coordinating reviewer. Use narrower installed skills or tools when available instead of reproducing their mechanics:

- Use browser-control, Playwright, or equivalent tooling for navigation, interaction, responsive checks, console errors, and rendered-state inspection.
- Use screenshot tooling for visual evidence at representative desktop and mobile widths.
- Use accessibility tooling such as axe, Lighthouse, or an installed accessibility skill for mechanical checks.
- Use a writing or copy-editing skill for final rewrites after identifying the product, audience, claim, and desired tone.
- Use Figma tooling only when a design source or explicit design-comparison task is supplied.
- Use repository-aware code tools for tracing rendered content to components and proposing or applying fixes.

Do not make the audit depend on a particular named tool. When a specialist is unavailable, perform the reasoning directly and disclose any resulting limitation.

## Follow the Audit Workflow

### 1. Establish Product Truth

Inspect the URL, repository, README, product documentation, routes, visible interface, metadata, and real feature implementations. Establish:

- What the product is and is not
- Primary audience and buyer sophistication
- User problem and job to be done
- Main conversion action
- Actual product maturity
- Real differentiators and evidence
- Necessary level of trust, explanation, and restraint

Separate verified facts from reasonable inferences and unknowns. Never infer implemented capability from decorative UI alone.

### 2. Test Product–Website Fit First

Read `references/product-fit.md`. Determine whether the site represents the product accurately and helps the intended visitor make the next decision.

Test the hero before lower sections. A visitor should be able to determine what the product is, who it helps, why it matters, and what to do next without reconstructing the product from buzzwords.

Compare marketing claims against repository evidence where possible. Flag:

- Capabilities implied by mockups but absent from the product
- Positioning that describes a different or broader product
- Enterprise language for an early prototype without trust support
- Visual tone that conflicts with the buyer or risk level
- Calls to action that do not match the sales or onboarding motion
- Missing proof for high-stakes or unusually strong claims

Treat product mismatch as more severe than surface-level visual sameness.

### 3. Inspect the Live Experience

Review all high-value public routes rather than only the homepage. At minimum inspect the homepage, primary conversion path, pricing or equivalent decision page when present, and one representative product/detail page.

Apply this minimum only when the initial site is reachable. Do not continue probing downstream routes after the bounded retrieval failure described above.

At desktop and mobile widths, check:

- Information hierarchy and scan path
- Navigation and CTA clarity
- Responsive layout, overflow, and touch targets
- Interaction feedback and functional states
- Visible form labels, affordances, and destinations. Assess submission,
  loading, error, and success states only when they are actually reachable.
- Typography, spacing, contrast, motion, and consistency
- Console or network failures when tooling exposes them

Do not claim exhaustive coverage. State routes and states actually inspected.

### 4. Detect AI-Generated Design Slop

Read `references/slop-patterns.md`. Require evidence of interchangeability, repetition, contradiction, or lack of product meaning. Do not flag a gradient, bento grid, rounded card, stock illustration, or animation merely because it is common.

Use the substitution test: if a section could be moved unchanged to several unrelated AI/SaaS websites, it is probably not doing enough product-specific work.

Look for pattern clusters such as:

- Generic visual systems with no product-derived motif
- Repeated cards that flatten hierarchy
- Decorative product mockups or invented data
- Excessive effects competing with the task
- Arbitrary iconography and illustration
- Repetitive section rhythms
- Inconsistent components or unexplained style shifts
- Animation that adds latency or spectacle without comprehension

### 5. Audit Website Copy

Evaluate copy against the verified product truth, not against generic conversion formulas. Inspect:

- Specificity: could the statement identify this product?
- Information value: does each sentence add a claim, proof, distinction, or instruction?
- Claim support: can strong language be substantiated?
- Audience fit: does the vocabulary match the buyer?
- Terminology consistency: are the product and features named consistently?
- Human rhythm: is the copy excessively symmetrical, fragmented, inflated, or repetitive?
- CTA precision: does the label describe the actual next step?
- Product honesty: does copy imply capabilities, customers, scale, or certainty not established by evidence?

Flag symptoms, not authorship. Do not claim text was written by AI. Say that it reads as generic, overproduced, repetitive, unsupported, or interchangeable, and explain why.

When proposing a rewrite, preserve the intended meaning, avoid inventing proof, and show the original and replacement together.

### 6. Inspect Frontend Evidence

When a repository is available, map important presentation findings to their
likely frontend source files and components. Review the design system, shared
layout, content source, routes, responsive styles, semantic HTML, asset use,
and obvious accessibility implementation. Do not audit backend completeness
unless the user explicitly asks for it.

Prefer targeted changes to a redesign. Identify whether each issue is:

- Content-only
- Component-local
- Design-system-wide
- Information-architecture-level
- Product-positioning-level

Do not edit the repository unless the user explicitly requests implementation.

### 7. Prioritize Findings

Assign severity based on user and product impact:

- **Critical:** materially misleads, creates serious accessibility or trust risk,
  or blocks the primary visible action
- **High:** obscures product meaning, audience, trust, or a major decision
- **Medium:** weakens specificity, personality, hierarchy, or confidence
- **Low:** polish issue with limited visitor impact

Rank issues using impact, confidence, and effort. Put product mismatch, misleading claims, and broken paths ahead of aesthetic preferences.

## Score Without False Precision

Score each dimension from 1–5 and justify it with evidence:

1. Product–website fit
2. Message and copy specificity
3. UX and conversion clarity
4. Credibility and product honesty
5. Visual intentionality and distinctiveness
6. Personality and point of view
7. Responsive and accessibility quality
Use `N/V` for not verified. Do not calculate a weighted percentage or claim scientific precision. The scorecard is a compact summary, not the conclusion.

## Produce the Report

Use `references/report-template.md`. Lead with the verdict and highest-impact mismatch. Include:

- Scope and inspected evidence
- Product truth summary
- Scorecard
- Prioritized findings with exact evidence
- Product-fit analysis
- Copy findings and paired rewrites
- Visual and UX findings
- Repository locations when available
- A Keep / Change / Remove summary
- The five highest-impact next actions

Every material finding must include:

- What was observed
- Where it was observed
- Why it matters for this product and audience
- A concrete recommendation
- Confidence level when evidence is incomplete

Distinguish direct observations from interpretations. Avoid vague feedback such as “make it pop,” “improve hierarchy,” or “feels AI-generated” without locating the problem and describing a fix.

## Preserve Useful Design

Identify what already works. Do not recommend wholesale replacement when editing positioning, reducing decorative patterns, or tightening a component system will solve the problem. The goal is a more truthful, intentional, product-specific website—not a particular aesthetic.
