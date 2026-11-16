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


## Token usage and plan

Generating a study guide is heavier than a normal chat message. For each guide, Claude reads your source material, plans the parts, writes the full content, runs code to build the PDF, and checks the rendered pages before handing it over. Because of that, one guide can use a noticeable amount of your usage allowance.

- **Free plan:** Skills and file creation with code execution are available, so the skill works. Free usage limits are lower, so you may hit your limit partway through, especially with long slide decks or several guides in one sitting. If that happens, wait for the limit to reset and continue.
- **Paid plan (Pro or higher):** Recommended if you make guides often, upload large files, or split a big topic into several numbered guides (`GUIDE 1 OF 3`, etc.). You get a higher usage allowance, so a multi-guide set is much less likely to get cut off.
- **What uses the most:** large uploads (long PDFs, big slide decks, whole repos), long chats, and building many guides in the same conversation.
- **Ways to save usage:** upload only the pages or slides you need, make one guide per chat, and ask for one part at a time for very large topics.

Exact limits depend on your plan, the model you use, how long your chats are, and how large your files are, and they can change. Check Anthropic's [pricing page](https://claude.com/pricing) and [Help Center](https://support.claude.com) for the current numbers.

## Notes

- Colors are approximate. Edit the palette table in `SKILL.md` to match your own theme.
- **Sample PDF disclaimer:** The sample PDFs included in this repository were generated using this Study Guide Skill to demonstrate its output and formatting capabilities. They are actual examples of the skill in use, not fixed templates or guaranteed results. Generated PDFs may vary depending on the source material, topic complexity, prompts, and Claude's generation process. Differences in layout, pagination, formatting, and content are expected between generations.
