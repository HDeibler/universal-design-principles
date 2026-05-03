# Architecture

This document explains how the marketplace, plugins, skills, and references compose. If you're going to contribute, this is the model to internalize.

## The four layers

```
┌──────────────────────────────────────────────────────────────────┐
│ 1. Marketplace                                                   │
│    .claude-plugin/marketplace.json                               │
│    Lists every plugin with name, source path, description, tags. │
└──────────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┴───────────────┐
              ▼                               ▼
┌──────────────────────────┐    ┌──────────────────────────┐
│ 2. Plugin                │    │ 2. Plugin                │
│    perception-and-       │    │    cognition-and-        │
│    hierarchy-principles/ │    │    learnability-         │
│                          │    │    principles/           │
│    plugin.json           │    │                          │
│    README.md             │    │    plugin.json           │
│    skills/               │    │    README.md             │
└──────────────────────────┘    │    skills/               │
              │                 └──────────────────────────┘
              ▼
   ┌────────────────────────────────────────────────────┐
   │ 3. Skill (one per principle, plus sub-aspects)     │
   │    skills/<principle>/SKILL.md                     │
   │    skills/<principle>-<aspect>/SKILL.md            │
   │                                                    │
   │    Each SKILL.md has YAML frontmatter:             │
   │      name + description                            │
   │    plus the body content the agent reads.          │
   └────────────────────────────────────────────────────┘
                              │
                              ▼
       ┌──────────────────────────────────────────┐
       │ 4. References (deep-dive material)       │
       │    skills/<...>/references/<topic>.md    │
       │                                          │
       │    Read after the parent skill when      │
       │    more depth is needed. No frontmatter. │
       └──────────────────────────────────────────┘
```

Each layer has a specific responsibility:

- **Marketplace** — discovery. The user (or their client) needs to know what plugins exist.
- **Plugin** — packaging. A coherent group of skills around a theme.
- **Skill** — capability. A single `SKILL.md` that the agent reads and applies.
- **References** — depth. Material the agent reads only when the parent skill points to it.

## How the agent uses each layer

1. **Marketplace** is consulted at install time, not at runtime. Once a plugin is installed, the marketplace manifest is no longer relevant.
2. **Plugin** is a packaging artifact. The agent doesn't usually distinguish "which plugin a skill came from" — it just sees a flat list of available skills.
3. **Skills** are the runtime unit. The agent loads available skills' frontmatter (name + description) into its context, then matches user requests to skills, then reads the body of matched skills.
4. **References** are read on demand. The parent skill body says "for more depth, see `references/foo.md`"; the agent reads the reference if the user's request needs that depth.

## Why this architecture

A few design choices worth understanding:

### Frontmatter as the routing surface

Every `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: hicks-law-menus
description: Apply Hick's Law specifically to menu design — calibrating menu length, grouping options, deciding when to split into sub-menus or use search instead. Use when designing top-level navigation, dropdown menus, command palettes, or any list of choices the user has to scan to find what they want.
---
```

The `description` is read by the agent's routing layer. It needs to be:

- **Specific** — generic descriptions don't trigger reliably.
- **Trigger-rich** — contain the words the agent would naturally see in a user request ("designing menu," "dropdown," "navigation," etc.).
- **Self-contained** — the agent should be able to choose between candidates based on description alone.

We aim for 2–4 sentences per description. This is the highest-leverage part of any skill.

### Sub-aspect skills (instead of one giant skill per principle)

A principle like Hick's Law has fundamentally different shapes when applied to menus, defaults, and pricing pages. We could have shipped a single 2,000-line `hicks-law/SKILL.md` covering all three. Instead, we ship four files:

- `hicks-law/SKILL.md` — the principle itself, ~450 lines.
- `hicks-law-menus/SKILL.md` — application to menus, ~280 lines.
- `hicks-law-defaults/SKILL.md` — application to defaults, ~280 lines.
- `hicks-law-pricing/SKILL.md` — application to pricing, ~280 lines.

This serves two goals:

1. **Routing.** The agent can pick the most-specific skill for the user's actual context. If you ask about a pricing page, it loads `hicks-law-pricing` rather than the whole principle.
2. **Cognitive economy.** The agent doesn't need to load 2,000 lines into context to answer a question about menus. It loads 280 lines plus, if needed, the parent skill's overview.

### References (instead of inlining everything)

Each skill has a sibling `references/` directory with deep-dive material:

- For parent skills, the reference is `lineage.md` — the principle's origins, research history, key sources, and citation list.
- For sub-aspect skills, the reference is a topic-specific deep-dive (e.g., `references/menu-design-patterns.md`).

The reference is read **on demand** when the parent skill's body points to it. This means the agent only loads the deep-dive material when the user's question warrants it. For most tasks, the parent skill is enough.

### Vendor neutrality

The repository is **deliberately framework-agnostic**. Examples are in plain HTML, CSS, and conceptual pseudocode, with cross-domain examples from web, mobile, print, physical product, and information design. Sibling repositories may map the same principles to specific design systems (shadcn/ui, Material, Carbon, etc.); the two would compose.

## Anatomy of a single skill

Take `hicks-law/SKILL.md` as a reference. The structure:

```markdown
---
name: hicks-law
description: <2–4 sentences explaining when this skill triggers>
---

# Hick's Law

> **Definition.** <One-sentence blockquote summary.>

<2–4 paragraphs of plain-language definition and "why this matters">

## Why this matters

<2–3 paragraphs on the principle's importance>

## When to apply

<Bulleted list of decisions/surfaces where the principle is decisive>

## When NOT to apply

<Bulleted list of cases where the principle backfires>

## Sub-skills in this cluster

- **hicks-law-menus** — <description>
- **hicks-law-defaults** — <description>
- **hicks-law-pricing** — <description>

## Worked examples

### A bad case
<concrete example of the principle being violated, with explanation>

### A good case
<concrete example of the principle being applied, with explanation>

### A more nuanced case
<a third example that surfaces the principle's limits>

## Anti-patterns

<3–5 anti-patterns with names and explanations>

## Heuristic checklist

<5–10 concrete questions to ask before shipping>

## Related principles

- **<Principle 1>** — <how it relates>
- **<Principle 2>** — <how it relates>
...

## See also

- `references/lineage.md` — origins, research history, sources.
- `hicks-law-menus/` — application to menus.
- `hicks-law-defaults/` — application to defaults.
- `hicks-law-pricing/` — application to pricing.
```

A sub-aspect skill follows the same shape but is scoped to the specific application context. A reference file is freer-form prose without frontmatter; it serves the parent skill.

## Naming conventions

- **Plugins** — `<theme>-and-<theme>-principles/` (plural, hyphenated).
- **Router skills** — `<theme>-router` (e.g., `cognition-router`).
- **Principle skills** — `<principle-name>` in kebab-case (e.g., `hicks-law`, `figure-ground-relationship`).
- **Sub-aspect skills** — `<principle-name>-<aspect>` (e.g., `hicks-law-menus`).
- **Reference files** — descriptive names for the topic (e.g., `lineage.md`, `menu-design-patterns.md`).

The kebab-case folder name **must match** the `name:` in the SKILL.md frontmatter.

## File-count expectations

For a fully-built principle with N sub-aspects:

| Files | Count |
|---|---:|
| Parent `SKILL.md` | 1 |
| Parent `references/lineage.md` | 1 |
| Sub-aspect `SKILL.md` | N |
| Sub-aspect `references/<topic>.md` | N |
| **Total** | **2 + 2N** |

Most principles in this repository have 2 sub-aspects, so a typical principle is 6 files. A few have 3 sub-aspects (Hick's Law, Wayfinding, Fitts's Law) for 8 files. Accessibility has 4 sub-aspects (WCAG's four POUR pillars) for 10 files.

## Discovery and registration

When Claude starts (or `/plugins reload` is run), it:

1. Reads each plugin's `.claude-plugin/plugin.json` to learn the plugin's name, description, and metadata.
2. Walks the plugin's `skills/` directory looking for `SKILL.md` files.
3. Reads the YAML frontmatter from each `SKILL.md` to learn the skill name and description.
4. Registers each skill in its routing table.

At runtime, when the user sends a message, Claude:

1. Considers the user's message against the skill descriptions in the routing table.
2. Selects one or more skills whose descriptions match.
3. Loads the body of selected skills into context.
4. Generates a response that uses the skill's vocabulary and recommendations.
5. If the response would benefit from deeper material, follows links to `references/` files.

You don't have to do anything special to invoke a skill. The agent does it.

## How to tell if your skill is good

A few diagnostics:

- **The description triggers reliably for the relevant queries** — test with several user prompts and verify the right skill fires.
- **The body is structured** — definition, when-to-apply, anti-patterns, examples, checklist.
- **The examples are concrete and cross-domain** — not just web examples, not just abstract.
- **The references file is honest about sources** — citations to primary research, not just to the source book.
- **The sub-aspects don't overlap** — each one covers a context the others don't.
- **A reader could apply the principle after reading the skill alone** — without you to explain it.

If a skill fails any of these, it needs work.

## Cross-reference

- [Getting Started](getting-started.md) — installation and first use.
- [How Skills Trigger](how-skills-trigger.md) — the routing layer in detail.
- [Principle Index](principle-index.md) — all 42 built principles, alphabetical.
- [CONTRIBUTING.md](../CONTRIBUTING.md) — structural conventions for adding a new principle.
