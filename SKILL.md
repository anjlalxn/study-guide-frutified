---
name: study-guide
description: Builds a styled PDF study guide / reviewer on any topic or lesson (school subjects, class reports, exam prep, presentation or defense prep, uploaded notes or slides turned into a reviewer). Use whenever the user asks for a reviewer, study guide, study notes, lesson summary, exam prep, presentation prep, or "guide 1 of 3"-style document, even if they don't mention PDF or styling. If the lesson is about programming, it also adds code blocks, method tables, and code walkthroughs. Output is a two-column A4 PDF with a fruit-themed title banner (default raspberry), dark part headers, Bricolage Grotesque and JetBrains Mono for code.
---

# Study Guide

Turns a topic, lesson, notes, slides, or a repo into a friendly, easy-to-review PDF. The reader is a student who must understand the material and explain it out loud or answer questions on it. Write simply, explain the *why*, and anticipate what the professor might ask.

## Workflow

1. **Gather the source.** Use what the user gave: uploaded notes, slides, readings, a repo, or just a topic. Stick to the source and the user's course material; do not invent facts, terms, or code. If something is unclear or missing, say so. If the topic is current or uncertain, verify it first.
2. **Skip filler slides.** When the source is a slide deck or presentation, ignore non-content slides: title/cover slides with only names, "Thank you", "Questions?", "Prepared by [name]", "Presented by", "Reporters", "Group members", agenda or outline-only slides, references-only slides, and any slide that is just a logo, date, or contact info. Do not mention them in the guide. Use real content only.
3. **Choose a color theme** (see Color themes below).
4. **Plan the guide.** Pick the parts and sections. Large topics split into numbered guides (Guide 1 of 3...). Confirm scope only if truly unclear; otherwise propose a split and proceed.
5. **Write the content** using the structure below.
6. **Build HTML, render to PDF** with the design system below, then look at 2 to 3 rasterized pages before presenting.
7. Save to `/mnt/user-data/outputs/` and call `present_files`.

## Content structure

1. **Intro block** (no banner): a short, friendly opening saying what the guide covers, then a numbered list of what the reader will learn or be able to do.
2. **Part banners**: `PART 1`, `PART 2`... each with a short title.
3. **Concept first, details second.** Start with a plain explanation or analogy ("Think of it this way:"), then a card box, list, diagram-like flow, or table, then the details.
4. **Worked example** as a numbered step-by-step flow, a solved problem, or a short scenario.
5. **Numbered sections** `1.1`, `1.2`... one per concept. Each has: a plain definition, why it matters, an example, and a table when comparing things (term / meaning, type / use, before / after).
6. **Review helpers** near the end of each part or at the end of the guide:
   - Key terms (term + one-line meaning)
   - Questions the professor might ask, each with a short model answer
   - Quick recap bullets
   - For presentations (class reports, thesis, capstone, or any defense): a sample explanation written in first person that the student can say aloud
7. Short sentences. Define jargon at first use. Bold key terms.

### If the lesson is about programming

Add these on top of the structure above:
- Real code snippets in code blocks with a language pill, followed by a plain-language walkthrough of what each part does.
- Method / function / route / command tables (name / what it does).
- A flow list showing how pieces connect (request to response, input to output, UI to database).
- A concept card box for architectures (e.g. Model / Controller / View).
- Code must come from the user's source or the actual repo and match their course style (follow the lecturer's slides or reviewer if given). Never rewrite or invent code.
- "Explain this code" questions the professor might ask, in the review section.

Skip all of this for non-programming topics: no code blocks, no method tables.

## Fonts

- **Body, headings, UI text: Bricolage Grotesque** - https://fonts.google.com/specimen/Bricolage+Grotesque
- **Code, inline code, eyebrow labels, card labels: JetBrains Mono** (400, 500, 700) - https://www.jetbrains.com/lp/mono/

Google Fonts domains are blocked, so use npm:

```bash
npm install @fontsource/bricolage-grotesque @fontsource/jetbrains-mono
# files are in node_modules/@fontsource/<name>/files/
# if the static package is missing, use the variable one instead:
# npm install @fontsource-variable/bricolage-grotesque
```

Embed with `@font-face` (latin subset is enough).

Fallbacks: `"Bricolage Grotesque", "Segoe UI", sans-serif` and `"JetBrains Mono", Consolas, monospace`.

## Color themes

Every theme has three colors: **primary** (title banner, bullets, inline code text, pills, rules), **dark** (part banners, h2, table headers, bold terms, list numerals, code left bar), and **tint** (inline code bg, card box bg, alternate table rows). All text on primary and dark is white, so keep them dark enough to read.

| Theme | primary | dark | tint |
|---|---|---|---|
| Raspberry (default) | `#D93868` | `#1F4D2B` | `#FDEEF2` |
| Strawberry | `#E0334C` | `#2F5D2E` | `#FDECEE` |
| Blueberry | `#4A5BC4` | `#1E2A5A` | `#EEF0FC` |
| Orange | `#E8761A` | `#6B3A12` | `#FFF1E4` |
| Mango | `#D98A0B` | `#7A4A0A` | `#FFF5DD` |
| Lemon | `#B89A00` | `#4F5A12` | `#FBF7D9` |
| Lime | `#5E9E1F` | `#23441C` | `#EEF7DF` |
| Kiwi | `#6E9B2F` | `#3B2F1E` | `#F1F7E4` |
| Grape | `#8244B0` | `#2E1A4A` | `#F4ECFA` |
| Plum | `#9B2F5F` | `#3A1730` | `#F9EAF1` |
| Watermelon | `#E5445F` | `#1F5B3A` | `#FDECEF` |
| Peach | `#E8795A` | `#7A3B2B` | `#FEEEE8` |

Other tokens, same in every theme: code-bg `#F4F7F4`, ink `#222222`, muted `#555555`, divider `#E3E3E3`.

How to pick:
- **User names a theme** (e.g. "blueberry"): use it.
- **User says default, or says nothing about color**: use Raspberry.
- **User says "random", "surprise me", or "any"**: pick one from the table at random (for example `python3 -c "import random;print(random.choice(['Strawberry','Blueberry','Orange','Mango','Lemon','Lime','Kiwi','Grape','Plum','Watermelon','Peach']))"`) and tell them which one you got.
- **User says "you decide"**: choose the theme that fits the subject (Kiwi or Lime for biology/environment, Blueberry for networking/IT, Grape for literature/arts, Orange for chemistry, and so on) and say which you chose.
- **User gives their own colors**: use theirs in the same primary / dark / tint roles.

Use the chosen fruit as the emblem in the banner's white circle (a simple flat icon or the fruit emoji rendered as an image). Define the three colors as CSS variables (`--primary`, `--dark`, `--tint`) so the theme swaps in one place.

## Design system

Page: A4, margins about 14 mm, white. Body 10 pt, line-height 1.5. Body in **two columns** with a thin divider (`column-count: 2; column-gap: 8mm; column-rule: .5pt solid var(--divider)`). Title banner and footer span full width.

Components:

- **Title banner** (page 1 of each guide): primary rounded rectangle with a thicker dark bottom border. Left: white circle with the fruit emblem. Right: mono caps eyebrow with wide letter-spacing in semi-transparent white (`SUBJECT · STUDY GUIDE · GUIDE 1 OF 3`), under it the title in white bold ~22 pt (`Topic – Reviewer`).
- **Part banner**: dark background, 4px primary left border, rounded. Mono caps eyebrow `PART 1` in tint color, white bold title ~15 pt.
- **h2** (`1.1 Title`): dark bold ~14 pt with a 2px primary rule beneath. **h3**: dark bold. "Example:" headings: primary bold.
- **Bold terms**: dark. **Bullets**: primary dots. **Numbered lists**: bold dark numerals.
- **Card box**: tint background, 1px primary border, radius 6px, bold primary title. Inside, white cards with a dark left bar: mono caps label, bold title, one-line description. Use for definitions, categories, or parts of a whole.
- **Table**: dark header with white bold text, alternating white and tint rows, thin bottom borders.
- **Inline code** (programming or technical terms): mono ~9 pt, primary text on tint, small padding, 2px radius.
- **Code block** (programming only): code-bg, 1px light border, 5px dark left bar, radius 3px, mono 8.5 pt, `pre-wrap`, small primary pill in the top-left with the language in white caps.
- **Footer** (every page): primary 1.5px rule, left `Subject · Study guide`, right `Page X of N`, tiny bold muted text.
- No page breaks inside tables, cards, or code blocks (`break-inside: avoid`). Banners and headings never alone at the bottom of a column (`break-after: avoid`).

## Build recipe (HTML to PDF)

Use WeasyPrint (`pip install weasyprint --break-system-packages`) or headless Chromium.

```css
:root { --primary:#D93868; --dark:#1F4D2B; --tint:#FDEEF2; --divider:#E3E3E3; }
@page { size: A4; margin: 14mm 14mm 16mm;
  @bottom-left  { content: "Subject · Study guide"; font: 700 7pt "Bricolage Grotesque"; color:#555; border-top:1.5pt solid #D93868; padding-top:3pt; width:100% }
  @bottom-right { content: "Page " counter(page) " of " counter(pages); font: 700 7pt "Bricolage Grotesque"; color:#555 } }
body { font: 400 10pt/1.5 "Bricolage Grotesque", sans-serif; color:#222 }
.cols { column-count: 2; column-gap: 8mm; column-rule: .5pt solid var(--divider) }
code, pre { font-family: "JetBrains Mono", monospace }
```

`@page` margin boxes can't read CSS variables in some renderers, so write the primary hex directly there (generate the CSS from the chosen theme in Python). Banner and footer full width; everything else inside `.cols`. Replace the footer text with the real subject.

## Quality checklist

- Filler slides (thank you, prepared by, group members, etc.) are not in the guide.
- Every fact, term, and example traces back to the source or is well established.
- Each concept has a plain explanation plus an example.
- Review section (key terms, professor questions, recap) is present.
- For programming lessons: code is real, matches course style, and is explained.
- Theme colors are applied consistently, text on banners is readable, and the chosen theme is named to the user.
- Both fonts embedded (check with `pdffonts`).
- No orphaned banners, split code blocks, or table overflow; page numbers read `Page X of N`.
- Briefly tell the user what's covered and what the next guide will cover.
