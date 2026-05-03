<div align="center">

# Universal Design Principles

**A Claude plugin marketplace of 42 framework-agnostic UX & product-design principles, drawn from *Universal Principles of Design* (Lidwell, Holden, Butler, 2003) and the broader design and HCI research literature.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Plugins: 5](https://img.shields.io/badge/plugins-5-success.svg)](#whats-inside)
[![Skills: 137](https://img.shields.io/badge/skills-137-informational.svg)](docs/principle-index.md)
[![Principles: 42](https://img.shields.io/badge/principles-42-informational.svg)](docs/principle-index.md)
[![Lines: ~35.7k](https://img.shields.io/badge/content-~35.7k%20lines-lightgrey.svg)](#repository-stats)

[Getting Started](docs/getting-started.md) · [Architecture](docs/architecture.md) · [Principle Index](docs/principle-index.md) · [How Skills Trigger](docs/how-skills-trigger.md) · [Attribution](ATTRIBUTION.md) · [Contributing](CONTRIBUTING.md)

</div>

---

## What this is

A **working library** of design principles, packaged as a Claude plugin marketplace. Install one or more plugins and your Claude agent gains access to a curated set of skills that fire automatically whenever you work on UX, UI, or product design — regardless of design system, SDK, framework, or platform.

Each principle is built as a **reference-grade entry**: a router-style `SKILL.md` (~350–500 lines), 2–4 sub-aspect skills for context-specific application (~200–300 lines each), and per-skill `references/` deep-dive files with origins, research lineage, and worked patterns. The result is a library Claude can apply with the same depth as a senior designer who has internalized the canon.

## Why a plugin marketplace?

Many products today are built and reviewed by AI agents. The quality of their design judgment depends heavily on what they've been taught to attend to. Without a working library of principles, an agent will produce designs that are competent on average but blind in specific ways — the typography will drift, hierarchy will collapse on the third screen, the error states will be afterthoughts, the interaction patterns will be inconsistent across surfaces.

This marketplace gives your agent the same canon that experienced designers have internalized over years. Instead of one giant prompt, the canon is split across **five composable plugins** so you can install only what you need:

| Plugin | What it teaches | Skills |
|---|---|---:|
| 🎨 **[Perception & Hierarchy](perception-and-hierarchy-principles/)** | How the eye groups elements, where it lands first, what makes a composition read as ordered | 34 |
| 🧠 **[Cognition & Learnability](cognition-and-learnability-principles/)** | Mental models, complexity reduction, memory load, how new users get oriented | 33 |
| 🖱️ **[Interaction & Control](interaction-and-control-principles/)** | Affordance, feedback, errors, user agency, Fitts's Law for touch targets | 29 |
| ✨ **[Aesthetics & Emotion](aesthetics-and-emotion-principles/)** | Beauty, perceived quality, brand voice, flow, persuasive form | 17 |
| 🛠️ **[Process & Robustness](process-and-robustness-principles/)** | Iteration, accessibility, reliability under stress, what to prune | 24 |

Each plugin contains a **router skill** (which triggers on the plugin's category and points the agent at the right principle), one main skill **per principle**, and **2–4 sub-aspect skills** for principles whose application varies meaningfully by context (e.g., Hick's Law has different shapes in menus vs. defaults vs. pricing).

## Installation

### Option 1: install the entire marketplace

If you use Claude Code, Cowork, or any client that supports Claude plugin marketplaces, point your client at this repository:

```bash
# Clone the marketplace
git clone https://github.com/hunterd107/design-principles.git ~/.claude/marketplaces/design-principles

# Then in Claude (Code or Cowork), add the marketplace
/plugins add ~/.claude/marketplaces/design-principles
```

Once added, install any of the five plugins from the `/plugins` UI.

### Option 2: install a single plugin directly

Each plugin folder is a self-contained Claude plugin. Symlink (or copy) the folder into your Claude plugins directory:

```bash
# Example: install just the perception plugin
ln -s "$(pwd)/perception-and-hierarchy-principles" ~/.claude/plugins/perception-and-hierarchy-principles
```

Or, in Claude Code, run:

```bash
/plugins install ./perception-and-hierarchy-principles
```

### Option 3: drop the skills folder into your project

If you don't want to manage plugins centrally, you can drop a plugin's `skills/` directory into your project under `.claude/skills/`:

```bash
cp -r perception-and-hierarchy-principles/skills/* .claude/skills/
```

Claude will discover the skills the next time it loads the project.

See **[docs/getting-started.md](docs/getting-started.md)** for a more detailed walkthrough including verification steps and troubleshooting.

## Quick example

After installing one of the plugins (say, **Cognition & Learnability**), you can use it like this in any Claude conversation:

```
You: I'm designing a settings page for a SaaS dashboard. The product has
     accumulated about 60 settings across 8 categories. Help me think
     through the structure.

Claude: [silently invokes the cognition-router → progressive-disclosure skill]
        Looking at this through the lens of progressive disclosure and
        the 80/20 rule: roughly 12 of those 60 settings probably account
        for 80% of actual changes. Surface those in a clear default view,
        and tuck the remaining ~50 behind clearly-labeled disclosure...
```

The skills fire automatically based on the conversation context. You don't have to remember to invoke them.

For more concrete usage examples, see [docs/getting-started.md](docs/getting-started.md).

## Anatomy of a principle

Take **Hick's Law** as an example. Inside `cognition-and-learnability-principles/skills/`, you'll find:

```
hicks-law/
├── SKILL.md                                  # the principle's main entry (~450 lines)
└── references/
    └── lineage.md                            # origins, Hick (1952), Hyman (1953), modern empirical work

hicks-law-menus/
├── SKILL.md                                  # how Hick's Law applies to menus specifically
└── references/
    └── menu-design-patterns.md               # patterns and anti-patterns

hicks-law-defaults/
├── SKILL.md                                  # how Hick's Law applies to defaults
└── references/
    └── defaults-recipes.md

hicks-law-pricing/
├── SKILL.md                                  # how Hick's Law applies to pricing pages
└── references/
    └── pricing-tier-strategies.md
```

Each main `SKILL.md` includes:

1. **Definition** — Plain-language definition in our own words.
2. **Origins and research lineage** — Where the principle comes from, who studied it, what evidence supports it.
3. **When to apply** — Surfaces and decisions where the principle is decisive.
4. **When NOT to apply** — Contexts where the principle backfires or doesn't transfer.
5. **Worked examples** — Multiple cross-domain examples with code or diagrams.
6. **Anti-patterns** — Common misapplications and how to recognize them.
7. **Heuristic checklist** — Concrete questions to ask before shipping.
8. **Related principles** — What to read next.
9. **See also** — Links to `references/` and to sub-aspect skills.

For the full architecture, see **[docs/architecture.md](docs/architecture.md)**.

## What's inside

```
design-principles/
├── .claude-plugin/
│   └── marketplace.json                    # marketplace manifest
├── docs/                                   # cross-plugin documentation
│   ├── getting-started.md
│   ├── architecture.md
│   ├── how-skills-trigger.md
│   └── principle-index.md
├── perception-and-hierarchy-principles/    # 34 skills
├── cognition-and-learnability-principles/  # 33 skills
├── interaction-and-control-principles/     # 29 skills
├── aesthetics-and-emotion-principles/      # 17 skills
├── process-and-robustness-principles/      # 24 skills
├── README.md
├── CONTRIBUTING.md
├── ATTRIBUTION.md
├── CHANGELOG.md
├── LICENSE
├── .gitignore
└── .gitattributes
```

Browse the **[Principle Index](docs/principle-index.md)** for the alphabetical list with direct links into the relevant `SKILL.md`.

## Repository stats

| Metric | Count |
|---|---:|
| Plugins | 5 |
| Principles built | 42 |
| Skills (`SKILL.md` files) | 137 |
| Reference deep-dives (`references/*.md` files) | 137 |
| Lines of original content | ~35,700 |

The 2003 first edition of *Universal Principles of Design* contains exactly **100 principles**. We have built 42 of them at reference-grade depth — the principles most relevant to modern product, web, and software UX. Each per-plugin `README.md` lists the next-priority builds; contributions are welcome.

## Source attribution

This repository owes its **principle names and taxonomy** to:

> Lidwell, W., Holden, K., & Butler, J. (2003). *Universal Principles of Design: 100 Ways to Enhance Usability, Influence Perception, Increase Appeal, Make Better Design Decisions, and Teach through Design*. Rockport Publishers. ISBN 1-59253-007-9.

Each principle entry's **definitions, prose, code examples, anti-patterns, and analyses are written in our own words**, drawing on the broader design and HCI research literature: Wertheimer's Gestalt psychology, Hick (1952) and Hyman (1953) on choice latency, Fitts (1954) on motor capacity, Norman's *Design of Everyday Things* and *Emotional Design*, Nielsen's usability work, Tufte on information design, Lynch's *Image of the City* on wayfinding, the W3C WCAG framework on accessibility, Lavie & Tractinsky on aesthetic-usability, Csikszentmihalyi on flow, Zajonc on the mere-exposure effect, and many others.

**The book is a starting point; this plugin set is a working tool.** It is not a substitute for the book. If you find this useful, please buy the book — it remains an essential reference and the source of the editorial taxonomy this repository builds on.

For a complete attribution breakdown — including how this repository used the source book, every key research source, and our content-originality commitments — see **[ATTRIBUTION.md](ATTRIBUTION.md)**.

## How this repository is intended to be used

- **By Claude agents:** install one or more plugins; the skills fire automatically when you work on design tasks; the agent applies the principle vocabulary in its reasoning and outputs.
- **By human designers:** the `SKILL.md` files are written as standalone documents you can read directly. Many designers use the repository as a personal reference even without an AI tool.
- **By teaching contexts:** the `references/lineage.md` files trace the research lineage of each principle and are useful as teaching material.
- **By contributors:** see [CONTRIBUTING.md](CONTRIBUTING.md) — the repository is designed to grow incrementally toward covering all 100 principles.

## Companion plugins

This repository is the **vendor-neutral** version of the design principle library. Examples are in plain HTML, CSS, and conceptual pseudocode, with cross-domain examples from web, mobile, print, physical product, and information design. You should be able to apply any of these principles whether you're working in shadcn/ui, Material, Carbon, Tamagui, Ant Design, Bootstrap, vanilla CSS, SwiftUI, Jetpack Compose, Figma, or whiteboard markers.

If a sibling repository ships that maps these principles to a specific design system (e.g., `universal-design-shadcn`), it will be linked here. The two are designed to compose: this one teaches the principle, the other shows how to apply it via specific primitives.

## Contributing

Contributions are welcome and held to a high prose-quality bar. See **[CONTRIBUTING.md](CONTRIBUTING.md)** for:

- Structural conventions for adding a new principle.
- The quality bar for prose, examples, and references.
- Attribution rules.
- The pull-request process.

For new-principle proposals, please open an issue first to discuss scope and audience.

## License

This repository is licensed under the [MIT License](LICENSE). The principle names and high-level taxonomy are drawn from *Universal Principles of Design* (Lidwell, Holden, Butler, 2003) under fair use as a research reference; all prose and examples are original work licensed under MIT. See [ATTRIBUTION.md](ATTRIBUTION.md) and [LICENSE](LICENSE) for details.

## Acknowledgments

To William Lidwell, Kritina Holden, and Jill Butler — for assembling the editorial taxonomy that makes a repository like this possible. To the researchers cited in the per-principle `references/lineage.md` files — whose primary work is the actual substance behind every entry. To Anthropic and the Claude team — for building the agentic infrastructure that makes a marketplace of design principles a useful artifact rather than just a library no one reads.

---

<div align="center">

**[Browse all 42 principles →](docs/principle-index.md)**

</div>
