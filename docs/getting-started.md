# Getting started

This guide walks through installing the Universal Design Principles skills in the major agent clients and verifying that the skills are visible.

## Prerequisites

You need at least one agent client:

- **Claude Code** for native `.claude-plugin` marketplace installs.
- **Codex** for native `.agents/plugins` marketplace installs or direct `.agents/skills` installs.
- **Cursor** for native Cursor plugins or `.cursor/rules` fallback guidance.
- **Gemini CLI** for direct Agent Skills installs.
- **Any AGENTS.md-compatible agent** for a lightweight fallback rule.

There is no build step. This repository is Markdown skill content plus JSON manifests.

## Clone once

Most local install paths start with a checkout:

```bash
git clone https://github.com/HDeibler/universal-design-principles.git ~/code/universal-design-principles
```

Use a stable path. Plugin and skill clients often cache or reference the path.

## Claude Code

For GitHub-hosted installs, add the marketplace directly:

```text
/plugin marketplace add HDeibler/universal-design-principles
/plugin install perception-and-hierarchy-principles@universal-design-principles
```

Repeat `/plugin install` for the plugins you want:

- `perception-and-hierarchy-principles`
- `cognition-and-learnability-principles`
- `interaction-and-control-principles`
- `aesthetics-and-emotion-principles`
- `process-and-robustness-principles`

For a local checkout:

```text
/plugin marketplace add ~/code/universal-design-principles
```

Then browse and install from `/plugin`.

## Codex

Add the repo as a plugin marketplace:

```bash
codex plugin marketplace add HDeibler/universal-design-principles
codex
```

Inside Codex, open:

```text
/plugins
```

Choose `Universal Design Principles`, install the plugins you want, then start a new thread.

For direct skill installs without plugin metadata:

```bash
mkdir -p ~/.agents/skills
cp -R ~/code/universal-design-principles/plugins/*-principles/skills/* ~/.agents/skills/
```

Restart Codex after copying. You can also use a project-scoped `.agents/skills/` directory if a repository should carry the skills with it.

## Cursor

This repository includes Cursor marketplace and plugin manifests:

- `.cursor-plugin/marketplace.json`
- `plugins/<plugin>/.cursor-plugin/plugin.json`

Install through Cursor's plugin flow from either the GitHub URL or your local checkout:

```text
https://github.com/HDeibler/universal-design-principles
~/code/universal-design-principles
```

If you are not using Cursor plugins, add a project rule instead:

```mdc
---
description: Use Universal Design Principles when working on UX, UI, product design, visual hierarchy, interaction design, accessibility, or design critique.
alwaysApply: false
---

When the task involves UX or product design, consult the Universal Design Principles skill repository and prefer the most specific principle skill before giving recommendations.
```

Save that as `.cursor/rules/universal-design-principles.mdc`.

## Gemini CLI

Link each plugin's skill directory:

```bash
for plugin in ~/code/universal-design-principles/plugins/*-principles; do
  gemini skills link "$plugin/skills" --scope user
done

gemini skills list
```

Use `--scope workspace` if you want the skills available only in the current project. Gemini also supports direct skill folders in `.gemini/skills/`, `.agents/skills/`, `~/.gemini/skills/`, or `~/.agents/skills/`.

## AGENTS.md fallback

For Copilot, Windsurf, and other rule-based agents, add a short instruction to the native rule file or `AGENTS.md`:

```md
# Design guidance

When working on UX, UI, product design, visual hierarchy, interaction design,
accessibility, or design critique, use the Universal Design Principles skills
from https://github.com/HDeibler/universal-design-principles. Prefer the most specific principle
skill for the task, and use the reference files only when the answer needs
research depth.
```

For GitHub Copilot, this can live in `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md`, or `AGENTS.md` depending on your editor surface. For Windsurf, use `.windsurf/rules/*.md` or `AGENTS.md`.

## Verify it works

After installing, ask a prompt that should clearly match one plugin:

| Plugin | Test prompt |
|---|---|
| Perception & Hierarchy | "I'm laying out a product card with a title, three metadata fields, a price, and a CTA. How should I structure the visual hierarchy?" |
| Cognition & Learnability | "My settings page has 60 options. How do I structure it?" |
| Interaction & Control | "What's the right minimum size for tap targets on a mobile UI?" |
| Aesthetics & Emotion | "How do I think about brand archetype for a B2B product?" |
| Process & Robustness | "Walk me through doing an accessibility audit of a web app." |

The response should name and apply a relevant principle, such as Hick's Law, progressive disclosure, hierarchy, Fitts's Law, or accessibility.

## Troubleshooting

### Skills do not appear

- Restart the agent client. Several clients only scan plugin or skill folders at startup.
- Confirm the manifest path exists for the client you are using.
- For direct skill installs, confirm every skill lives at `<skills-dir>/<skill-name>/SKILL.md`.
- Check that `SKILL.md` starts with valid YAML frontmatter containing `name:` and `description:`.

### Skills do not trigger

- Make the prompt specific. "Improve this UI" is weaker than "Review the visual hierarchy and interaction affordances in this settings page."
- Ask the agent what skills or plugins are available.
- Invoke the skill explicitly if the client supports slash or `@` invocation.

### Cursor or rule-based agents do not use the content

- Confirm the rule is active and not set to manual-only.
- Keep fallback rules short; point at the skill repository instead of pasting hundreds of lines.
- Use native plugins or direct Agent Skills when possible. Rules are useful fallback context, but they do not provide the same progressive disclosure as skills.

## Updating

For local checkouts:

```bash
cd ~/code/universal-design-principles
git pull --ff-only origin main
```

Then refresh or restart the client:

- Claude Code: `/reload-plugins` or restart.
- Codex: restart Codex, or update the marketplace from the plugin directory.
- Cursor: reload the window or update the plugin.
- Gemini CLI: run `/skills reload` or restart.

## Next steps

- Read the [Architecture overview](architecture.md) to understand how manifests, plugins, skills, and references compose.
- Read [How skills trigger](how-skills-trigger.md) to learn the routing mechanism in detail.
- Browse the [Principle Index](principle-index.md) to see every principle with direct links into the relevant `SKILL.md`.
