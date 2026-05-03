# How skills trigger

This document explains the routing mechanism — how the agent decides which skill (or skills) to apply to a given user request. Useful for understanding why your skill fires (or doesn't), and for writing skill descriptions that route reliably.

## The short version

Each skill has a YAML frontmatter description. The agent considers the user's request against all available skill descriptions and picks the most-relevant one(s). The skill's body is then loaded into context and applied.

You don't have to invoke skills explicitly. They fire automatically.

## The longer version

### What the agent sees

When you install a plugin, every `SKILL.md` in the plugin's `skills/` directory becomes available. The agent doesn't load all of them at the start of every conversation — that would explode the context. Instead, it loads only the **frontmatter** (name + description) into a routing table.

For a skill like `hicks-law-menus`, the routing table entry looks like:

```yaml
name: hicks-law-menus
description: Apply Hick's Law specifically to menu design — calibrating menu length, grouping options, deciding when to split into sub-menus or use search instead. Use when designing top-level navigation, dropdown menus, command palettes, or any list of choices the user has to scan to find what they want.
```

The agent sees this entry alongside entries for all other available skills.

### How the agent matches requests to skills

When you send a message, the agent:

1. **Reads your message** and identifies the topic, the kind of work you're asking for, and any specific terms (e.g., "menu," "dropdown," "navigation").
2. **Compares against skill descriptions** — looking for skills whose descriptions are most relevant to your message.
3. **Selects one or more skills** — usually one, sometimes two if your request spans topics.
4. **Loads the selected skill's body** into context.
5. **Generates a response** that draws on the skill's content.

The matching is fuzzy and judgment-based, not keyword exact-match. A description containing "navigation" will match a request about a "nav bar" or a "site map" or a "menu," not just the literal word "navigation."

### Why descriptions matter so much

The description is the **only** thing the agent sees in the routing decision. The skill body, the references, the examples — all of these only get loaded if the description wins the routing competition. A skill with a brilliant body but a mediocre description will never fire.

This is why we obsess over descriptions in the SKILL.md frontmatter. They are not summaries of the skill (the body does that). They are **routing prompts** — they're trying to win a competition with other skills for the agent's attention.

### Routing tradeoffs

The routing has tradeoffs that affect how you write descriptions:

**Specificity vs. coverage.** A very specific description ("Apply Hick's Law to *pricing pages*") fires reliably for pricing-page questions but misses generic ones. A very generic description ("Help with design") fires too often and crowds out more specific skills. Aim for descriptions that are specific enough to be unambiguous but general enough to catch related queries.

**Single skill vs. several.** If two skills have very similar descriptions, the agent may struggle to pick between them. Better to consolidate or to differentiate the descriptions sharply. The hicks-law sub-aspects (`hicks-law-menus`, `hicks-law-defaults`, `hicks-law-pricing`) avoid this by clearly naming their specific context.

**Trigger words vs. natural prose.** A description that lists every conceivable trigger word ("menus dropdowns navs sidebars hamburger fly-out command palette nav-drawer") reads as keyword stuffing and routes worse than natural prose with the most-likely trigger words embedded. Write naturally; the agent's matching is sophisticated enough to recognize related terms.

## What good descriptions look like

Some patterns we've found that work:

### Lead with the action and the context

> "Apply Hick's Law specifically to menu design — calibrating menu length, grouping options, deciding when to split into sub-menus or use search instead."

The skill's job ("Apply Hick's Law…") and the context ("…menu design") are stated up front.

### Continue with concrete trigger contexts

> "Use when designing top-level navigation, dropdown menus, command palettes, or any list of choices the user has to scan to find what they want."

Lists the kinds of user requests that should trigger the skill. Not exhaustive, but representative.

### Reach for the user's vocabulary, not the principle's

The user is more likely to say "menu" or "dropdown" than "branching choice latency." Use the user's vocabulary in the description even when the principle has its own technical name.

### Avoid generic verbs

"Help with menus" is too generic. "Apply Hick's Law to menu design" is specific. Specific verbs route better.

### Differentiate from sibling skills

The three hicks-law sub-aspects (`menus`, `defaults`, `pricing`) each name their specific context. The agent can pick between them based on whether the user is asking about a menu, a default value, or a pricing page.

## Common routing failures

### Skill doesn't fire for relevant queries

Diagnosis: the description is too generic, doesn't include the user's vocabulary, or competes with a sibling skill that's slightly better.

Fix: tighten the description, add concrete trigger contexts, or differentiate from siblings.

### Skill fires for irrelevant queries

Diagnosis: the description is too broad — claims the skill applies to more than it does.

Fix: narrow the description. Add "Use when…" and "Use only when…" qualifiers.

### Two skills compete and the wrong one wins

Diagnosis: descriptions overlap; the wrong one happens to match the user's vocabulary slightly better.

Fix: re-differentiate the descriptions. Make each one's distinctive context obvious in the first sentence.

### Multiple skills fire and confuse the response

Diagnosis: the user's request genuinely spans skills (this is sometimes correct).

Fix: usually fine; the agent will weave them together. Concerning only if the response becomes incoherent.

## Router skills

Each plugin has a "router skill" (e.g., `cognition-router`). These are higher-level skills whose job is to recognize that a user is doing some kind of cognition-related design work and point at the appropriate per-principle skill.

Router skills are useful for:

- **First-encounter routing** — when a user's request is vague and could go several places, the router can read the request more carefully and choose.
- **Cross-principle synthesis** — when a request spans principles, the router can sequence them.
- **Vocabulary normalization** — translating user vocabulary to principle vocabulary.

Router skills aren't strictly necessary — the per-principle skills can route directly — but they help with ambiguous requests.

## Testing your skill's routing

When you add a new skill, test the routing with several representative user prompts:

```
Prompt: "How long should my dropdown menu be?"
Expected skill to fire: hicks-law-menus
```

```
Prompt: "I have a checkbox with 7 options on a settings page. Should they be grouped?"
Expected skill to fire: chunking-form-grouping (or proximity-form-fields)
```

```
Prompt: "We removed our color labels and now users can't distinguish error states from success states."
Expected skill to fire: color-accessibility-and-mode (or similarity-grouping)
```

Run the prompt; check what fires. If it's wrong, adjust the description.

## Anti-patterns

### Description is a summary of the body

> "This skill discusses Hick's Law as it applies to menu design, including the trade-offs between long menus and split menus, the role of search, and the impact of menu organization on user task completion."

This describes the skill's contents but doesn't tell the agent when to fire. Better:

> "Apply Hick's Law specifically to menu design — calibrating menu length, grouping options, deciding when to split into sub-menus or use search instead. Use when designing top-level navigation, dropdown menus, command palettes, or any list of choices the user has to scan to find what they want."

### Description in title case / formal voice

> "Application of Hick's Law to Menu Design Decisions"

The agent doesn't read titles; it reads descriptions. Use natural sentences.

### Description that's too short

> "About menus."

Useless. The agent can't route on this.

### Description that's too long

> [400 words explaining everything about menus]

The agent's routing layer is fast but bounded; very long descriptions don't help and may hurt.

Aim for **2–4 sentences**, **40–100 words**.

### Description repeats the skill name

> "hicks-law-menus: Apply Hick's Law to menus."

The name is already in the routing table. Don't waste description characters re-stating it.

## When you want to invoke a skill explicitly

You can always invoke a skill by name:

```
You: Read the hicks-law-menus skill and apply it to my screen.
```

The agent will load that specific skill regardless of routing. Useful when:

- You know exactly which principle applies and don't want to rely on routing.
- The routing is firing the wrong skill.
- You want to verify a skill loaded correctly.

## Cross-reference

- [Architecture](architecture.md) — the four layers and how they compose.
- [Getting Started](getting-started.md) — installation and verification.
- [Principle Index](principle-index.md) — all 42 principles with links to their skills.
- [CONTRIBUTING.md](../CONTRIBUTING.md) — structural conventions for new skills.
