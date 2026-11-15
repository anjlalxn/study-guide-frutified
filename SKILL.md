---
name: study-guide
description: Builds a styled PDF study guide / reviewer on any topic or lesson (school subjects, class reports, exam prep, presentation or defense prep, uploaded notes or slides turned into a reviewer). Use whenever the user asks for a reviewer, study guide, study notes, lesson summary, exam prep, presentation prep, or "guide 1 of 3"-style document, even if they don't mention PDF or styling. If the lesson is about programming, it also adds code blocks, method tables, and code walkthroughs. Output is a two-column A4 PDF with a raspberry title banner, dark green part headers, Finlandica text and JetBrains Mono for code.
---

# Study Guide

Turns a topic, lesson, notes, slides, or a repo into a friendly, easy-to-review PDF. The reader is a student who must understand the material and explain it out loud or answer questions on it. Write simply, explain the *why*, and anticipate what a teacher or panel might ask.

## Workflow

1. **Gather the source.** Use what the user gave: uploaded notes, slides, readings, a repo, or just a topic. Stick to the source and the user's course material; do not invent facts, terms, or code. If something is unclear or missing, say so. If the topic is current or uncertain, verify it first.
2. **Plan the guide.** Pick the parts and sections. Large topics split into numbered guides (Guide 1 of 3...). Confirm scope only if truly unclear; otherwise propose a split and proceed.
3. **Write the content** using the structure below.
4. **Build HTML, render to PDF** with the design system below, then look at 2 to 3 rasterized pages before presenting.
5. Save to `/mnt/user-data/outputs/` and call `present_files`.

## Content structure

1. **Intro block** (no banner): a short, friendly opening saying what the guide covers, then a numbered list of what the reader will learn or be able to do.
2. **Part banners**: `PART 1`, `PART 2`... each with a short title.
3. **Concept first, details second.** Start with a plain explanation or analogy ("Think of it this way:"), then a card box, list, diagram-like flow, or table, then the details.
4. **Worked example** as a numbered step-by-step flow, a solved problem, or a short scenario.
5. **Numbered sections** `1.1`, `1.2`... one per concept. Each has: a plain definition, why it matters, an example, and a table when comparing things (term / meaning, type / use, before / after).
6. **Review helpers** near the end of each part or at the end of the guide:
   - Key terms (term + one-line meaning)
   - Likely questions a teacher or panel might ask, with short model answers
   - Quick recap bullets
   - If it's a presentation or defense: a sample explanation written in first person that the student can say aloud
7. Short sentences. Define jargon at first use. Bold key terms. Prepared by (names), Thank you slides, etc. should be left out.

### If the lesson is about programming

Add these on top of the structure above:
- Real code snippets in code blocks with a language pill, followed by a plain-language walkthrough of what each part does.
- Method / function / route / command tables (name / what it does).
- A flow list showing how pieces connect (request to response, input to output, UI to database).
- A concept card box for architectures (e.g. Model / Controller / View).
- Code must come from the user's source or the actual repo and match their course style (follow the lecturer's slides or reviewer if given). Never rewrite or invent code.
- Likely "explain this code" questions in the review section.

Skip all of this for non-programming topics: no code blocks, no method tables.

## Fonts

- **Body, headings, UI text: Finlandica** (400, 500, 600, 700)
- **Code, inline code, eyebrow labels, card labels: JetBrains Mono** (400, 500, 700)

Google Fonts domains are blocked, so use npm:

```bash
npm install @fontsource/finlandica @fontsource/jetbrains-mono
# files are in node_modules/@fontsource/<name>/files/
```

Embed with `@font-face` (latin subset is enough). Fallbacks: `Finlandica, "Segoe UI", sans-serif` and `"JetBrains Mono", Consolas, monospace`.

## Design system

Palette (approximate; replace with exact values if the user provides them):

| Token | Hex | Use |
|---|---|---|
| raspberry | `#D93868` | title banner, bullets, inline code text, pills, rules |
| raspberry-tint | `#FDEEF2` | inline code bg, card box bg, alternate table rows |
| forest | `#1F4D2B` | part banners, h2 text, table headers, bold terms, list numerals, code left bar |
| code-bg | `#F4F7F4` | code block background |
| ink | `#222222` | body text |
| muted | `#555555` | footer, captions |

Page: A4, margins about 14 mm, white. Body 10 pt, line-height 1.5. Body in **two columns** with a thin divider (`column-count: 2; column-gap: 8mm; column-rule: .5pt solid #E3C7D0`). Title banner and footer span full width.

Components:

- **Title banner** (page 1 of each guide): raspberry rounded rectangle with a thicker forest bottom border. Left: white circle with an emblem or simple icon for the subject. Right: mono caps eyebrow with wide letter-spacing in semi-transparent white (`SUBJECT · STUDY GUIDE · GUIDE 1 OF 3`), under it the title in white bold ~22 pt (`Topic – Reviewer`).
- **Part banner**: forest background, 4px raspberry left border, rounded. Mono caps eyebrow `PART 1` in pale pink, white bold title ~15 pt.
- **h2** (`1.1 Title`): forest bold ~14 pt with a 2px raspberry rule beneath. **h3**: forest bold. "Example:" headings: raspberry bold.
- **Bold terms**: forest green. **Bullets**: raspberry dots. **Numbered lists**: bold forest numerals.
- **Card box**: raspberry-tint background, 1px raspberry border, radius 6px, bold raspberry title. Inside, white cards with a forest left bar: mono caps label, bold title, one-line description. Use for definitions, categories, or parts of a whole.
- **Table**: forest header with white bold text, alternating white and raspberry-tint rows, thin bottom borders.
- **Inline code** (programming or technical terms): mono ~9 pt, raspberry text on raspberry-tint, small padding, 2px radius.
- **Code block** (programming only): code-bg, 1px light border, 5px forest left bar, radius 3px, mono 8.5 pt, `pre-wrap`, small raspberry pill in the top-left with the language in white caps.
- **Footer** (every page): raspberry 1.5px rule, left `Project or Subject · Study guide`, right `Page X of N`, tiny bold muted text.
- No page breaks inside tables, cards, or code blocks (`break-inside: avoid`). Banners and headings never alone at the bottom of a column (`break-after: avoid`).

## Build recipe (HTML to PDF)

Use WeasyPrint (`pip install weasyprint --break-system-packages`) or headless Chromium.

```css
@page { size: A4; margin: 14mm 14mm 16mm;
  @bottom-left  { content: "Subject · Study guide"; font: 700 7pt Finlandica; color:#555; border-top:1.5pt solid #D93868; padding-top:3pt; width:100% }
  @bottom-right { content: "Page " counter(page) " of " counter(pages); font: 700 7pt Finlandica; color:#555 } }
body { font: 400 10pt/1.5 Finlandica, sans-serif; color:#222 }
.cols { column-count: 2; column-gap: 8mm; column-rule: .5pt solid #E3C7D0 }
code, pre { font-family: "JetBrains Mono", monospace }
```

Banner and footer full width; everything else inside `.cols`. Replace the footer text with the real subject.

## Quality checklist

- Every fact, term, and example traces back to the source or is well established.
- Each concept has a plain explanation plus an example.
- Review section (key terms, likely questions, recap) is present.
- For programming lessons: code is real, matches course style, and is explained.
- Both fonts embedded (check with `pdffonts`).
- No orphaned banners, split code blocks, or table overflow; page numbers read `Page X of N`.
- Briefly tell the user what's covered and what the next guide will cover.
