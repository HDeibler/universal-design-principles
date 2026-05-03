# Getting started

This guide walks you through installing the marketplace, verifying it works, and using your first skill.

## Prerequisites

You need one of:

- **Claude Code** — the CLI tool. Install instructions: <https://docs.claude.com/en/docs/claude-code>.
- **Cowork** (or another Claude desktop client that supports plugins).
- **Claude Agent SDK** project — you can drop the `skills/` directories into `.claude/skills/` in any SDK project.

You don't need anything else — no Node, no Python, no build step. The repository is pure markdown plus a few JSON manifests.

## Install — three options

### Option 1: install the entire marketplace

Best for: users who want all five plugins available, or who want to browse/install plugins from a UI.

```bash
# Pick a stable location — the marketplace folder will live here for as long as you use it
mkdir -p ~/.claude/marketplaces

# Clone the repository
git clone https://github.com/hunterd107/design-principles.git \
  ~/.claude/marketplaces/design-principles

# In Claude (Code or Cowork), register the marketplace
/plugins add ~/.claude/marketplaces/design-principles
```

After registering, the five plugins will be visible in `/plugins`. Install whichever you want.

### Option 2: install a single plugin

Best for: users who only want one or two of the plugins (smaller install, faster Claude startup).

```bash
# Clone the repo to wherever
git clone https://github.com/hunterd107/design-principles.git ~/code/design-principles

# Install the plugin into Claude's plugins directory via symlink
ln -s ~/code/design-principles/perception-and-hierarchy-principles \
  ~/.claude/plugins/perception-and-hierarchy-principles
```

Restart Claude (or run `/plugins reload`) and the plugin's skills will be available.

### Option 3: drop the skills into a project

Best for: users on the Claude Agent SDK or working in a single project who want the skills scoped to that project only.

```bash
cd path/to/your/project
mkdir -p .claude/skills

# Drop in the skills from any plugin
cp -r ~/code/design-principles/perception-and-hierarchy-principles/skills/* \
  .claude/skills/
```

The skills are now scoped to that project. Other Claude sessions won't see them.

## Verify it works

After installing, ask Claude something that should trigger one of the skills. For each plugin, here's a test prompt that reliably activates it:

| Plugin | Test prompt |
|---|---|
| Perception & Hierarchy | "I'm laying out a product card with a title, three metadata fields, a price, and a CTA. How should I structure the visual hierarchy?" |
| Cognition & Learnability | "My settings page has 60 options. How do I structure it?" |
| Interaction & Control | "What's the right minimum size for tap targets on a mobile UI?" |
| Aesthetics & Emotion | "How do I think about brand archetype for a B2B product?" |
| Process & Robustness | "Walk me through doing an accessibility audit of a web app." |

If the relevant plugin is installed, Claude's response should reference the principle by name (for example: "Using Hick's Law and progressive disclosure, …") and apply the principle in the actual recommendation.

## Your first skill in action

Try this end-to-end. Install the **Perception & Hierarchy** plugin, then in Claude:

```
You: I'm designing a dashboard with 8 metric cards. Each card has a title,
     a primary number, a small trend indicator, and a chart. Right now they
     all look identical. How do I introduce hierarchy?
```

Claude should reach into the `hierarchy` and `hierarchy-typographic` skills, applying the principle's vocabulary directly:

> Reaching for the hierarchy principle: right now your cards have *no* hierarchy because every element is competing equally. The fastest fix is typographic — make the primary number much larger (24–32px), keep the title at 13–14px, and demote the trend indicator and chart caption to a muted color at 12px. That gives the user a clear reading order on each card: number → context → trend.
>
> A second move is to identify which of the 8 cards is the primary metric and treat *that one* differently — wider, larger primary number, possibly a subtle accent color. The other 7 act as supporting metrics. This is hierarchy at the dashboard level, not just within each card …

The skill is doing the heavy lifting. You didn't have to remember to mention hierarchy; the agent reached for it on its own.

## Troubleshooting

### Skills don't seem to fire

- **Check the plugin is registered.** Run `/plugins list` and confirm the plugin appears as installed and enabled.
- **Check the skill descriptions match your prompt.** Skills fire based on description matches; if your prompt is generic ("design something"), no specific skill will trigger. Be specific about what you're working on.
- **Restart Claude.** Some clients only load skills at startup.

### "Skill not found" errors

- **Check the path.** Skills must live at `<plugin>/skills/<skill-name>/SKILL.md` with valid YAML frontmatter.
- **Check the frontmatter.** The `name` field in frontmatter must match the folder name exactly.

### Claude isn't using the principle vocabulary

- **Check the skill loaded.** Add `Read the SKILL.md file you're using and quote the first paragraph` to your prompt to verify the skill content actually loaded.
- **Be more specific.** "Help me with this" won't trigger anything; "How do I structure visual hierarchy?" will.

### Permission errors

- On macOS, you may need to grant Claude file-system access if it's installing skills outside your home directory.
- On Linux/Windows, ensure the user running Claude has read access to the plugins directory.

### Stray files in the cloned repo

The `.gitignore` ignores macOS `.DS_Store` files, but a fresh clone won't have any. If you see them after using the repository on macOS, that's normal — they're already excluded from version control.

## Next steps

- Read the **[Architecture overview](architecture.md)** to understand how plugins, skills, and references compose.
- Read **[How skills trigger](how-skills-trigger.md)** to learn the routing mechanism in detail.
- Browse the **[Principle Index](principle-index.md)** to see every principle with direct links into the relevant `SKILL.md`.
- Browse a per-plugin README to see the principles in that plugin and the planned next builds.

## Updating

To pull in new principles or improvements:

```bash
cd ~/.claude/marketplaces/design-principles
git pull origin main
```

If you installed by symlink, the change is picked up immediately. If you installed by copy, you'll need to re-copy. If you installed via the marketplace, run `/plugins update <plugin-name>` from your client.

## Uninstalling

```bash
# Remove a single plugin
rm ~/.claude/plugins/perception-and-hierarchy-principles

# Or remove the whole marketplace
rm -rf ~/.claude/marketplaces/design-principles
/plugins remove design-principles
```
