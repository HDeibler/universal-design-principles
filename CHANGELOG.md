# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

Nothing yet.

## [1.0.0] — 2026-05-02

First public release. The repository now ships as a Claude plugin marketplace with five composable plugins covering 42 principles across 137 skills and 137 reference files (~35,700 lines of original content).

### Added

- **Marketplace manifest** at `.claude-plugin/marketplace.json` listing all five plugins.
- **Repository documentation:** top-level `README.md`, `CONTRIBUTING.md`, `CHANGELOG.md`, `ATTRIBUTION.md`, `LICENSE` (MIT), `.gitignore`, `.gitattributes`.
- **Cross-plugin docs** under `docs/`: `getting-started.md`, `architecture.md`, `how-skills-trigger.md`, `principle-index.md`.
- **Per-plugin manifests** upgraded with version, license, repository, homepage, category, expanded keywords.
- **Per-plugin READMEs** rewritten with installation, usage, full principle index, and attribution.

### Plugins (state at 1.0.0)

#### Perception & Hierarchy (34 skills)

- Hierarchy + `typographic` + `spatial` + `color-and-tone`
- Proximity + `form-fields` + `data-tables` + `navigation`
- Signal-to-Noise Ratio + `densification` + `decoration-removal` + `emphasis-economy`
- Color + `semantic-systems` + `accessibility-and-mode`
- Alignment + `grid-systems` + `text-and-numerics`
- Legibility + `typeface-and-size` + `contrast-and-spacing`
- Readability + `line-length` + `rhythm-and-prose`
- Gestalt Similarity + `grouping` + `and-contrast`
- Closure + `implied-shapes` + `completion-cost`
- Figure-Ground Relationship + `cues` + `overlays-and-modals`

#### Cognition & Learnability (33 skills)

- Hick's Law + `menus` + `defaults` + `pricing`
- Wayfinding + `physical-spatial-metaphors` + `search-and-recovery` + `breadcrumbs-and-context`
- Progressive Disclosure + `defaults-and-tucking` + `disclosure-affordances`
- 80/20 Rule + `feature-prioritization` + `redesign-targeting`
- Chunking + `form-grouping` + `numeric-and-otp`
- Mental Model + `system-vs-interaction` + `mismatch-and-onboarding`
- Recognition Over Recall + `pickers-and-palettes` + `recents-and-suggestions`
- Consistency + `internal` + `external`
- Mimicry + `surface` + `behavioral`
- Iconic Representation + `resemblance` + `arbitrary-and-symbolic`

#### Interaction & Control (29 skills)

- Fitts's Law + `touch-targets` + `screen-edges` + `pointer-acceleration`
- Affordance + `signifiers` + `false-and-anti`
- Forgiveness + `undo-and-soft-delete` + `confirmation-and-prevention`
- Feedback Loop + `states-and-latency` + `positive-vs-negative`
- Errors + `slips` + `mistakes`
- Constraint + `physical` + `psychological`
- Mapping + `natural` + `cultural`
- Expectation Effect + `priming` + `design-cues`
- Control + `locus` + `power-vs-simplicity`

#### Aesthetics & Emotion (17 skills)

- Aesthetic-Usability Effect (reference-grade)
- Archetypes + `brand-voice` + `storytelling-arcs`
- Form Follows Function + `as-axiom` + `success-criteria`
- Wabi-Sabi + `imperfection` + `restraint`
- Exposure Effect + `onboarding` + `redesign-risk`
- Immersion + `flow` + `distraction-cost`

#### Process & Robustness (24 skills)

- Accessibility + `perceivable` + `operable` + `understandable` + `robust`
- Iteration + `design-vs-development` + `prototype-fidelity`
- Factor of Safety + `content-stress` + `failure-margin`
- Prototyping + `concept-throwaway-evolutionary` + `when-and-what`
- Weakest Link + `identification` + `treatment`
- Scaling Fallacy + `load-assumptions` + `interaction-assumptions`
- Ockham's Razor + `feature-pruning` + `equivalent-designs`

[Unreleased]: https://github.com/hunterd107/design-principles/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/hunterd107/design-principles/releases/tag/v1.0.0
