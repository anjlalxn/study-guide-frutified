# Study Guide Skill

A Claude skill that turns any topic, lesson, notes, or slides into a clean, two-column PDF reviewer. If the lesson is about programming, it adds code blocks, method tables, and code walkthroughs.

## What it makes

- Fruit-themed title banner (default raspberry, or pick one, random, or let Claude decide) with a `GUIDE 1 OF 3`-style eyebrow
- Dark part banners (`PART 1`, `PART 2`...)
- Numbered sections (`1.1`, `1.2`...) with plain explanations, analogies, and examples
- Card boxes, color-coded tables, and step-by-step flows
- Review helpers: key terms, questions the professor might ask with answers, quick recap
- Programming lessons only: syntax-labeled code blocks, method tables, "explain this code" questions
- Footer with `Page X of N`

## Fonts

| Use | Font |
|---|---|
| Text and headings | [Finlandica Text](https://fonts.google.com/specimen/Finlandica+Text) |
| Text and headings (fallback) | [Bricolage Grotesque](https://fonts.google.com/specimen/Bricolage+Grotesque) |
| Code and labels | [JetBrains Mono](https://www.jetbrains.com/lp/mono/) |

Finlandica Text is used by default. If it can't be installed or embedded, the skill falls back to Bricolage Grotesque. The fonts used are embedded in the generated PDF.

## Install

1. Download `SKILL.md` from this repo.
2. In Claude, go to **Settings → Capabilities → Skills** and upload the file (or the zipped `study-guide` folder).
3. Make sure Code Execution and File Creation is on.

## Use

Just ask in chat, for example:

- "Make a reviewer for Chapter 3 of my Networking class" (attach your notes or slides)
- "Study guide for photosynthesis, guide 1 of 2"
- "Reviewer for my capstone defense based on this repo"


## Notes

- Colors are approximate. Edit the palette table in `SKILL.md` to match your own theme.
- **Sample PDF disclaimer:** The sample PDFs included in this repository were generated using this Study Guide Skill to demonstrate its output and formatting capabilities. They are actual examples of the skill in use, not fixed templates or guaranteed results. Generated PDFs may vary depending on the source material, topic complexity, prompts, and Claude's generation process. Differences in layout, pagination, formatting, and content are expected between generations.
