# Contributing

Thank you for considering a contribution. This repository is a working library of design principles, and the bar is high: every principle entry is reference-grade, written in original prose, and grounded in publicly available research. Contributions that meet that bar are welcome and valued.

This document covers how to propose a change, the structural conventions every skill must follow, the quality bar for prose and examples, attribution rules, and the review process.

## Quick start

```bash
# 1. Fork and clone the repository
git clone https://github.com/<your-username>/design-principles.git
cd design-principles

# 2. Create a topic branch
git checkout -b add-<principle-name>

# 3. Make your changes (see the structural conventions below)
# 4. Verify locally
ls -d */                             # the five plugins should be present
find . -name "SKILL.md" | wc -l      # should grow by however many skills you added
find . -name "*.md" -path "*/references/*" | wc -l  # one reference file per skill

# 5. Commit and push
git commit -m "Add <Principle Name> to <plugin>"
git push origin add-<principle-name>

# 6. Open a pull request against main
```

## Ways to contribute

- **Add a new principle.** Pick from the "Planned" list in any per-plugin README, or propose a new one.
- **Add a new sub-aspect skill** to an existing principle (covering a context that isn't yet covered).
- **Improve an existing skill** with clearer prose, better examples, or tightened anti-patterns.
- **Fix typos, broken links, factual errors.**
- **Improve documentation** — anything in `docs/`, READMEs, or attribution.
- **Improve tooling** — `.gitignore`, manifests, validation scripts.

For anything beyond a typo, please open an issue first to discuss the proposal before investing time in the writing.

## Repository layout

```
design-principles/
├── .claude-plugin/
│   └── marketplace.json                    # marketplace manifest (lists every plugin)
├── docs/                                   # cross-plugin documentation
│   ├── getting-started.md
│   ├── architecture.md
│   ├── how-skills-trigger.md
│   └── principle-index.md
├── perception-and-hierarchy-principles/
│   ├── .claude-plugin/plugin.json          # per-plugin manifest
│   ├── README.md
│   └── skills/
│       ├── <router-skill>/SKILL.md         # router for the plugin's category
│       ├── <principle>/                    # one folder per principle
│       │   ├── SKILL.md                    # the principle's main entry
│       │   └── references/
│       │       └── lineage.md              # origins, research, sources
│       └── <principle>-<aspect>/           # one folder per sub-aspect
│           ├── SKILL.md
│           └── references/
│               └── <topic>.md
├── cognition-and-learnability-principles/  # same shape
├── interaction-and-control-principles/     # same shape
├── aesthetics-and-emotion-principles/      # same shape
├── process-and-robustness-principles/      # same shape
├── README.md                               # repository-level overview
├── CONTRIBUTING.md                         # this file
├── ATTRIBUTION.md
├── CHANGELOG.md
├── LICENSE
├── .gitignore
└── .gitattributes
```

## Structural conventions

Each principle is built as a small directory tree. Follow the conventions exactly so the marketplace can route to them reliably.

### Directory layout for a new principle

```
<plugin>/skills/<principle-name>/
├── SKILL.md                       # the principle's main entry
└── references/
    └── lineage.md                 # origins, research lineage, sources
```

Plus, for each sub-aspect skill that the principle splits into:

```
<plugin>/skills/<principle-name>-<aspect>/
├── SKILL.md
└── references/
    └── <topic>.md                 # context-specific deep-dive
```

### SKILL.md frontmatter

Every `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: <kebab-case-name-matching-folder>
description: One-paragraph description that explains when the skill triggers and what it does. Should be specific enough that a routing model can pick the right skill from a list of candidates. Aim for 2–4 sentences.
---
```

The `name` MUST match the folder name. The `description` should be specific and contain trigger words a model would naturally reach for (e.g., "Use when designing forms" or "Use when auditing typography").

### SKILL.md body sections

The body of a parent (router-style) `SKILL.md` should include, in roughly this order:

1. **Definition** — Plain-language definition in your own words. Lead with a blockquoted one-sentence summary.
2. **Why this matters** — Why a designer should care.
3. **When to apply** — Surfaces, decisions, and contexts where the principle is decisive.
4. **When NOT to apply** — Situations where the principle backfires or doesn't transfer.
5. **Sub-skills in this cluster** — Bulleted list naming each sub-aspect skill and what it covers.
6. **Worked examples** — At least 3 examples, ideally cross-domain (web, mobile, print, physical).
7. **Anti-patterns** — Common misapplications and how to recognize them.
8. **Heuristic checklist** — Concrete questions to ask before shipping.
9. **Related principles** — What to read next.
10. **See also** — A link to `references/lineage.md` and to each sub-aspect skill.

Sub-aspect `SKILL.md` files follow the same structure but are scoped to the specific application context.

### references/ files

Every `SKILL.md` has a sibling `references/` directory with at least one `.md` file. The reference file is a deep dive that supports the parent skill — it is read after the parent when more depth is needed.

Reference files should cover:

- Origins and research lineage (for parent skills, file is `lineage.md`).
- Specific patterns or recipes (for sub-aspect skills).
- Decision frameworks, checklists, or audit procedures.
- Source citations.

Reference files should NOT have the SKILL.md frontmatter — they are not skills, they are supporting documentation.

## Quality bar

### Prose

- **Original.** Every sentence in your own words. Do not paraphrase the source book; explain the principle in your own framing.
- **Concrete.** Use specific examples. Avoid vague claims like "improves usability" — say *how* and *for whom*.
- **Calibrated.** Claim only what the evidence supports. Distinguish well-established findings from intuitions.
- **Cross-domain.** Examples should span web, mobile, print, physical product, and information design where relevant.

### Examples

- At least 2–3 worked examples per `SKILL.md`.
- Mix of canonical (textbook) and contemporary (modern UI) examples.
- Show both correct application and a contrasting failure mode.
- Avoid over-reliance on a single design system or framework.

### Anti-patterns

- Real, recognizable mistakes — not strawmen.
- Explain *why* each anti-pattern is bad, not just that it's bad.
- Where applicable, suggest the fix.

### References

- Cite at least 3–5 sources in `references/lineage.md`.
- Prefer primary sources (original papers, foundational books) over secondary summaries.
- Use the existing citation style: `Author, A. (Year). *Title*. Publisher.`
- Always credit the contribution of *Universal Principles of Design* where applicable, but make clear what is from the book vs. what is added.

## Attribution rules

This repository takes attribution seriously. See `ATTRIBUTION.md` for the full attribution policy. Three rules to follow:

1. **Always credit *Universal Principles of Design* by name** when the principle appears in that book. Use the standard citation:

   > Lidwell, W., Holden, K., & Butler, J. (2003). *Universal Principles of Design*. Rockport Publishers.

2. **Cite specific research that supports the principle** — Hick (1952), Fitts (1954), Wertheimer (1923), Norman (1988), etc. Don't just attribute everything to the book.

3. **Be explicit about what is borrowed and what is original.** The principle name and taxonomy are borrowed from the source. The prose, examples, anti-patterns, and analyses must be original.

If you are introducing a principle that does not appear in the 2003 first edition (e.g., one from an expanded edition, or a related principle from another source), say so clearly in the `references/lineage.md`.

## Pull request process

1. **Open an issue first** for any non-trivial change, so the scope can be discussed.
2. **One principle per PR** is preferred. PRs that add several principles get hard to review.
3. **Verify the structural conventions** before submitting (frontmatter, references file, folder names).
4. **Update the per-plugin README** to add your new principle to the "Built" table, and remove it from "Planned" if applicable.
5. **Update `docs/principle-index.md`** to add your new principle alphabetically.
6. **Update `CHANGELOG.md`** under the `Unreleased` section.
7. **Submit the PR** with a clear description of what was added and why.

A reviewer will check structural conformance, prose quality, attribution, and that the principle fits the plugin's scope.

## Style conventions

- **Headings:** sentence case (`## Why this matters`), not title case.
- **Lists:** use `-` for bullets, not `*`.
- **Links:** prefer relative links within the repository (`../foo/SKILL.md`).
- **Code:** fenced blocks with language hints where applicable.
- **Citations:** parenthetical with author and year (Norman, 1988); full reference in `references/`.
- **Voice:** direct, second-person where instructional ("you should…"), third-person otherwise.
- **Tone:** measured, calibrated, anti-hype. Avoid superlatives unless the evidence is strong.

## Reporting issues

For bugs, factual errors, broken links, or quality concerns, open an issue with:

- **What's wrong** (with a link to the specific file/line if applicable).
- **Why it's wrong** (with a citation if it's a factual disagreement).
- **What you'd suggest instead.**

For new principle proposals, open an issue with:

- **Which plugin** the principle belongs to.
- **Why** it should be added (audience, use case, gap in the current coverage).
- **A proposed outline** (definition + 2–3 examples + sources).

## Code of conduct

Be kind, be specific, be honest about uncertainty. Disagreements about design are normal and welcomed; ad-hominem and dismissive responses are not. Reviewers will hold contributors to the prose-quality bar even when changes are well-intentioned — feedback is about the work, not the person.

## License

By contributing, you agree that your contributions will be licensed under the same MIT License as the rest of the repository (see `LICENSE`).
