# Attribution & Sources

This repository is a derivative *working library* — a tool, not a transcription. It owes its taxonomy and the names of most principles to a specific published book, and its prose, examples, and analyses to a much wider body of design and HCI research. This document is a complete and honest accounting of what is borrowed, what is original, and where the underlying ideas come from.

## The primary source

> **Lidwell, W., Holden, K., & Butler, J. (2003). *Universal Principles of Design: 100 Ways to Enhance Usability, Influence Perception, Increase Appeal, Make Better Design Decisions, and Teach through Design*. Rockport Publishers. ISBN 1-59253-007-9.**

The 2003 first edition is the primary inspiration for this repository. Specifically, what we have borrowed:

- **The principle names.** "Hick's Law," "Fitts's Law," "Forgiveness," "Affordance," "Mapping," "Closure," "Figure-Ground Relationship," "Wabi-Sabi," and the rest — these names (and their attribution to particular researchers) are the editorial contribution of Lidwell, Holden, and Butler. Some of the names are older terms of art that the authors collected; others are their preferred coinages for principles that didn't have a single canonical name. Either way, the *organization* of these principles into a single coherent taxonomy is theirs.
- **The principle taxonomy.** Grouping principles into thematic clusters (perception, cognition, interaction, aesthetics, process) reflects both the book's structure and our own organizational choices. The thematic logic was theirs first.
- **Selected one-line definitions.** A handful of definitions in this library closely echo phrasings found in the book because the principle is essentially defined by its name and brief gloss. Where this is the case, the definition is short, generic, and unavoidable (e.g., "Mapping is the relationship between controls and their effects" — there is no meaningful way to phrase that idea differently).

What we have *not* borrowed from the book:

- **No reproduced text.** No paragraphs, no extended explanations, no captions, no examples are copied from the book. Every sentence in this repository's `SKILL.md` files and `references/` files is original.
- **No reproduced illustrations or diagrams.** The book has many illustrations; none are included or recreated here.
- **No reproduced page layouts.** The book follows a one-page-per-principle layout; this repository follows a directory-per-principle layout that is unrelated to the book's design.

The book is a research reference — like a citation in an academic paper — not a substrate that we have copied or adapted. If you want the book itself (which is excellent, frequently updated, and worth owning), purchase it from your preferred bookseller. This repository is not a substitute.

### Edition notes

The 2003 first edition contains exactly 100 principles. Subsequent expanded editions (2010, 2015, etc.) added more — Anthropomorphic Form, Cathedral Effect, Contour Bias, Horror Vacui, Nudge, Wabi-Sabi, Veblen Effect, Uncanny Valley, and others. A few of those expanded principles are included in this repository because they are useful in modern UX work; this is noted in the relevant `references/lineage.md` files.

## Underlying research literature

Each principle in *Universal Principles of Design* points to a specific research lineage. We draw on those primary sources directly rather than relying on the book's summaries. The `references/lineage.md` file in each skill cites the relevant sources. The most-cited works across the repository:

### Foundational HCI

- Norman, D. A. (1988). *The Design of Everyday Things*. Basic Books. (Originally published as *The Psychology of Everyday Things*.)
- Norman, D. A. (2004). *Emotional Design: Why We Love (or Hate) Everyday Things*. Basic Books.
- Nielsen, J. (1993). *Usability Engineering*. Academic Press.
- Nielsen, J. (1994). *Heuristic evaluation*. (The Ten Usability Heuristics.)
- Krug, S. (2000). *Don't Make Me Think: A Common Sense Approach to Web Usability*. New Riders.
- Cooper, A. (1999). *The Inmates Are Running the Asylum*. Sams Publishing.
- Shneiderman, B. (1983). Direct manipulation: A step beyond programming languages. *IEEE Computer*, 16(8), 57–69.
- Card, S. K., Moran, T. P., & Newell, A. (1983). *The Psychology of Human-Computer Interaction*. Lawrence Erlbaum Associates.

### Visual perception

- Wertheimer, M. (1923). Untersuchungen zur Lehre von der Gestalt II. *Psychologische Forschung*, 4, 301–350.
- Koffka, K. (1935). *Principles of Gestalt Psychology*. Harcourt, Brace.
- Köhler, W. (1947). *Gestalt Psychology*. Liveright.
- Rubin, E. (1915). *Synsoplevede Figurer*. (Doctoral dissertation introducing figure-ground perception.)
- Kanizsa, G. (1976). Subjective contours. *Scientific American*, 234(4), 48–52.
- Palmer, S. E. (1999). *Vision Science: Photons to Phenomenology*. MIT Press.
- Ware, C. (2012). *Information Visualization: Perception for Design* (3rd ed.). Morgan Kaufmann.

### Choice and motor capacity

- Hick, W. E. (1952). On the rate of gain of information. *Quarterly Journal of Experimental Psychology*, 4(1), 11–26.
- Hyman, R. (1953). Stimulus information as a determinant of reaction time. *Journal of Experimental Psychology*, 45(3), 188–196.
- Fitts, P. M. (1954). The information capacity of the human motor system in controlling the amplitude of movement. *Journal of Experimental Psychology*, 47(6), 381–391.
- Fitts, P. M., & Seeger, C. M. (1953). S-R compatibility: Spatial characteristics of stimulus and response codes. *Journal of Experimental Psychology*, 46(3), 199–210.
- Miller, G. A. (1956). The magical number seven, plus or minus two: Some limits on our capacity for processing information. *Psychological Review*, 63(2), 81–97.

### Information design

- Tufte, E. R. (1983). *The Visual Display of Quantitative Information*. Graphics Press.
- Tufte, E. R. (1990). *Envisioning Information*. Graphics Press.
- Tufte, E. R. (1997). *Visual Explanations*. Graphics Press.
- Cleveland, W. S., & McGill, R. (1984). Graphical perception: Theory, experimentation, and application to the development of graphical methods. *Journal of the American Statistical Association*, 79(387), 531–554.

### Wayfinding & mental models

- Lynch, K. (1960). *The Image of the City*. MIT Press.
- Johnson-Laird, P. N. (1983). *Mental Models*. Harvard University Press.
- Gentner, D., & Stevens, A. L. (Eds.). (1983). *Mental Models*. Lawrence Erlbaum.

### Aesthetics & emotion

- Lavie, T., & Tractinsky, N. (2004). Assessing dimensions of perceived visual aesthetics of web sites. *International Journal of Human-Computer Studies*, 60(3), 269–298.
- Csikszentmihalyi, M. (1990). *Flow: The Psychology of Optimal Experience*. Harper & Row.
- Zajonc, R. B. (1968). Attitudinal Effects of Mere Exposure. *Journal of Personality and Social Psychology Monograph Supplement*, 9(2, Pt. 2), 1–27.
- Bornstein, R. F. (1989). Exposure and affect: Overview and meta-analysis of research, 1968–1987. *Psychological Bulletin*, 106(2), 265–289.
- Beecher, H. K. (1955). The powerful placebo. *JAMA*, 159(17), 1602–1606.
- Koren, L. (1994). *Wabi-Sabi for Artists, Designers, Poets and Philosophers*. Stone Bridge Press.

### Brand & archetype

- Mark, M., & Pearson, C. S. (2001). *The Hero and the Outlaw: Building Extraordinary Brands Through the Power of Archetypes*. McGraw-Hill.
- Jung, C. G. (1959). *The Archetypes and the Collective Unconscious*. Princeton University Press.
- Aaker, J. L. (1997). Dimensions of brand personality. *Journal of Marketing Research*, 34(3), 347–356.

### Accessibility

- W3C Web Content Accessibility Guidelines (WCAG) 2.1 (2018) and 2.2 (2023).
- Microsoft Inclusive Design Toolkit.
- Atkinson, B., & Braille Institute. (2020). Atkinson Hyperlegible typeface and design rationale.

### Engineering & process

- Goldratt, E. M. (1984). *The Goal*. North River Press.
- Petroski, H. (1985). *To Engineer Is Human: The Role of Failure in Successful Design*. St. Martin's Press.
- Sheridan, T. B. (1992). *Telerobotics, Automation, and Human Supervisory Control*. MIT Press.
- Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779.
- Lee, J. D., & See, K. A. (2004). Trust in automation: Designing for appropriate reliance. *Human Factors*, 46(1), 50–80.
- *Site Reliability Engineering* (Beyer, Jones, Petoff, & Murphy, eds.; Google, 2016).

### Typography

- Bringhurst, R. (1992). *The Elements of Typographic Style*. Hartley & Marks.
- Tinker, M. A. (1963). *Legibility of Print*. Iowa State University Press.
- Lupton, E. (2010). *Thinking with Type* (2nd ed.). Princeton Architectural Press.

### Design philosophy & method

- Rams, D. (1976). Ten principles for good design.
- Maeda, J. (2006). *The Laws of Simplicity*. MIT Press.
- Carroll, J. M., Mack, R. L., & Kellogg, W. A. (1988). Interface metaphors and user interface design. In M. Helander (Ed.), *Handbook of Human-Computer Interaction*. North-Holland.

This is an incomplete list — individual `references/lineage.md` files cite additional sources specific to their principles.

## Style and content guarantees

The contributors to this repository have made the following commitments, which any contributor must also make:

1. **Original prose.** No `SKILL.md` or `references/` file copies, paraphrases, or closely mimics extended text from *Universal Principles of Design* or any other source.
2. **Honest paraphrasing of cited research.** When summarizing a paper or finding, the summary is in our own words and stays calibrated to what the source actually claims.
3. **Clear sourcing.** Where a finding is from a specific paper, we cite it (parenthetically in the body, fully in `references/`).
4. **Acknowledgment of limits.** Where evidence is contested, dated, or culturally specific, we say so.
5. **No appropriation as endorsement.** Citing a source does not imply that the source author endorses this repository.

## How we used the source book

To be specific about the working method: in writing this repository, we read the relevant entries from the 2003 first edition of *Universal Principles of Design*, used the principle names and high-level taxonomy as a starting point, then went to the primary research literature (Hick 1952, Fitts 1954, Wertheimer 1923, Norman 1988, etc.) to write our own definitions, examples, and analyses. The book functioned as an *index of principles worth covering*, not as a text to paraphrase. Each `references/lineage.md` records the actual sources we drew on for that principle.

If you find a passage in this repository that closely resembles passages from the source book or any other source beyond unavoidable phrasings, please open an issue. We will rewrite it.

## Plugins drawing on this work

This repository is the *vendor-neutral* version of the design principle library. A sibling repository (`universal-design-shadcn`) maps the same principles to specific shadcn/ui primitives; if it is published, it will be linked from the top-level `README.md`. Other sibling repositories may follow for Material, Carbon, Tamagui, etc. All such repositories follow the same attribution rules.

## How to cite this repository

If you use this repository in academic work, teaching, or other publications, please cite it as:

> Hunter D. (2026). *Design Principles Plugins: a working library of UX design principles*. Version 1.0.0. https://github.com/hunterd107/design-principles

And, separately, please cite the source book:

> Lidwell, W., Holden, K., & Butler, J. (2003). *Universal Principles of Design*. Rockport Publishers.

## Questions, concerns, corrections

If anything in this attribution feels incomplete, inaccurate, or unfair to a rightsholder, please open an issue or contact the maintainer at `hunterd107@gmail.com`. We take attribution seriously and will respond promptly.
