---
name: annotated-bilingual-reading-webpage-builder
description: Build a self-contained bilingual (English + Traditional Chinese) annotated reading webpage for a group of 3 lessons from a senior-high English textbook, with click-to-reveal highlights for grammar patterns, phrases, vocabulary and reading-comprehension insights. Use when the teacher asks for a "課文重點標註網頁" / annotated reading webpage for a set of lessons (e.g. B3 U1~3, B4 U7~9), with or without handwritten teacher notes.
version: 1.0.0
---

# Annotated bilingual reading webpage builder

Portable version: works with any AI assistant that can read PDFs/images and write files. It needs no platform-specific tools.

The deliverable is **one self-contained HTML page** per 3-lesson batch. It shows the textbook's English passage paragraph by paragraph, with a few highlighted spans whose notes appear on click, plus a fresh Traditional Chinese translation under each paragraph.

**Do not confuse it with a student worksheet / teaching-material builder.** If the teacher says "worksheet" (學習單), that is a different deliverable. This skill is for "課文重點標註網頁" / "annotated webpage".

## Files in this skill

| File | Purpose |
|---|---|
| `SKILL.md` | The workflow and the design rules (this file) |
| `template.html` | The fixed page template: CSS (light and dark mode), the click-to-toggle popover script, and placeholders. Copy it as is. Only fill in the placeholders. |

## Copyright rule (read first)

This skill and its template contain **no textbook text**. The English passages come from the teacher's own textbook files at run time, and the generated pages are for classroom and self-study use only. Never paste textbook passages into this repository, and keep the disclaimer footer in `template.html`.

## Inputs to collect before starting

| Item | Example |
|---|---|
| Book and lessons | `B3`, `U1~3` |
| Textbook name (for the footer) | 龍騰版英語文第三冊課本 |
| Author credit (for the footer) | Default: `國立新豐高中英文科何瑞雲老師`. Use it unless the user gives a different credit. |
| Textbook chapter PDFs for the 3 lessons | the teacher's own files |
| Optional: supplementary exam materials per lesson | workbook (習作簿), comprehensive review book, grammar study guide (四合一講義) |
| Optional: photos of handwritten teacher's-edition notes | |

If the textbook name is not given, ask once and do not invent it. The author credit has a default (above), so do not ask for it.

## Step 1. Gather source material (research before any HTML)

For each of the 3 lessons:

1. **Extract the Reading Selection verbatim** from the lesson's chapter PDF, paragraph by paragraph. Use a text extractor such as `pdftotext -layout file.pdf out.txt`. Ignore harmless CJK font warnings. Fall back to reading page images only if the extracted text is garbled. Never invent or paraphrase the English source text. The textbook's wording is authoritative.
2. **Find the lesson's supplementary materials**, usually three PDFs: the workbook, the comprehensive review book (often has an explicit exam-frequency table for vocabulary, idioms and patterns, so always look for it) and the grammar study guide (usually has a "句型開講" section naming the lesson's official 1–2 target patterns).
3. **Summarise each lesson** from those PDFs: tested vocabulary with frequency counts if available, tested grammar patterns (especially any named "句型"), tested idioms and phrases, and a bottom line naming the most important pattern(s) and highest-frequency vocabulary. If your platform supports parallel sub-agents, run one per lesson. Otherwise do the three lessons one at a time. Focus on the cloze (綜合測驗) and grammar multiple-choice (文法選擇) sections and any frequency table. Do not report anything that is not actually in the PDFs.
4. **Check for an existing student worksheet** for the same lessons. Its word bank, vocabulary questions, grammar pattern and sentence-pattern frame are a fast, vetted cross-check of what the teacher considers testable. Reuse it as grounding when it exists.
5. **If handwritten note photos are supplied**, transcribe the grammar formulas, vocabulary glosses and strategy / language-highlight / note-the-details Q&A. Treat them as a primary guide to tone and teaching priorities, but **reference only, never authoritative over the textbook**. First verify that the lesson title and content in the photos match the PDF you extracted. If they do not match (for example after a curriculum edition change), stop and ask the teacher which content she wants, showing exactly what each source says. Do not guess or silently pick one. If a lesson has no matching notes, rely on steps 1–4; that works fine on its own.
6. The textbook's own embedded boxes (**Language Highlight**, **Reading Strategy**, **Note the Details**) are a strong source for insight-type highlights, because they are the editors' own flagged points.

## Step 2. Design the highlights per paragraph

Choose **up to 5** highlighted spans per paragraph, across 4 categories:

| Class | Colour | What it marks |
|---|---|---|
| `hl-vocab` | amber | A single core, high-frequency tested word |
| `hl-phrase` | lavender, dashed underline | A tested idiom or phrasal verb |
| `hl-pattern` | mint | A grammar structure: sentence-pattern formulas, reduced or fronted participial clauses, inversion, appositive noun clauses, correlatives, etc. Prioritise the lesson's officially named "句型". Show each core pattern at least once, and call out recurrences explicitly in the note (for example "呼應段落五…"). |
| `hl-insight` | sky blue | Reading-comprehension payoff: foreshadowing, thematic irony, the Big-Idea or inference answer, a callback to Note-the-Details logic. This is what makes it an annotation and not a glossary. |

**Priority when a paragraph has more than 5 good candidates:** keep pattern and insight highlights first. Drop plain "word = Chinese meaning" glosses first. A short paragraph may have fewer than 5. Never pad.

Rules for every highlight:

- `data-note` must be a genuine explanation: grammar formula plus rule, or idiom meaning plus usage, or the comprehension point it supports. Never a bare one-word gloss.
- The highlighted span must wrap the **whole** word or phrase the note defines. If the note defines "destination", the span wraps "destination", not just a neighbouring modifier.
- **Never mention commercial supplementary-material brand names** in any visible page text or note. They are research inputs, not citable sources. Phrase provenance generically ("學測常考", "呼應 Q5 推論題答案").
- Notes are written in the teacher's own pedagogical register: short, concrete, explained for a senior-high student.

Also:

- Write a fresh, accurate Traditional Chinese translation for each paragraph. Do not copy it from any source, and make it read naturally.
- Write one `.grammar-note` box per lesson summarising its 1–2 core sentence patterns (with the formula) plus any other recurring structure worth flagging. Same no-brand-names rule.
- The 5-highlight cap and the drop-vocab-first rule are internal authoring rules. Never mention them in the reader-facing intro.

## Step 3. Build the HTML from `template.html`

Copy `template.html` and **change nothing except the placeholders**. The CSS, the dark-mode tokens and the popover script are settled; do not redesign them.

| Placeholder | Fill with | Example |
|---|---|---|
| `{{PAGE_TITLE}}` | `B{book}U{n}~{n+2}課文重點標註` | `B3U1~3課文重點標註` |
| `{{BOOK_LABEL}}` | `B{book}` | `B3` |
| `{{LESSON_NUMBER}}` | Lesson number inside the page | `1` |
| `{{LESSON_TITLE_ZH}}` | Chinese lesson title | |
| `{{LESSON_TITLE_EN}}` | English lesson title | |
| `{{GRAMMAR_NOTE_HTML}}` | The lesson's grammar-note content. Use `<b>` for the lead phrase. | |
| `{{PARAGRAPH_NUMBER}}` | Paragraph number, from 1 | |
| `{{EN_PARAGRAPH_HTML}}` | The verbatim paragraph with `<span>` highlights | see below |
| `{{ZH_TRANSLATION}}` | Your fresh Traditional Chinese translation | |
| `{{TEXTBOOK_NAME}}` | From the inputs | |
| `{{AUTHOR_CREDIT}}` | From the inputs | |

Repeat the `<section class="lesson">` block once per lesson (3 per page) and the `<div class="p-card">` block once per paragraph.

Highlight markup:

```html
<span class="hl hl-pattern" data-note="核心句型：S + find + it + adj. + to VR。it 是形式受詞。">found it tremendously rewarding to</span>
```

Settled design decisions (do not re-litigate unless the teacher asks):

- The popover is click / tap to toggle. A native `title` tooltip was rejected as too easy to miss.
- `.page-sub` has `max-width: none` so the intro wraps at the same width as the cards below it.
- The page footer is the single disclaimer paragraph in the template. It states classroom-use-only, non-commercial use, the textbook source and copyright, and who selected the highlights, with the textbook name and author credit in bold.
- Fonts: Source Serif 4 (English body) and Noto Sans TC (Chinese and UI), loaded through the `<link>` in the template.
- Do not put the 5-highlight cap or the drop-vocab-first rule in the intro.

## Step 4. Verify before delivering

1. If you can run a headless browser, open the file and take screenshots of the top of the page, a scrolled section and a clicked highlight. Confirm that the layout is correct and the popover opens and closes.
2. If you cannot render it, run these checks instead and report them:
   - no `{{` placeholder remains;
   - every paragraph has at most 5 `.hl` spans;
   - every `.hl` has a non-empty `data-note`;
   - all tags are closed;
   - the English text matches the extracted textbook text exactly.
3. Re-read the visible text once for brand names of supplementary materials. There must be none.

## Step 5. Deliver

- File name: `B{book}U{n}~{n+2}課文重點標註.html`, for example `B3U1~3課文重點標註.html`. Keep the naming consistent across the series.
- For a small fix (wording, a highlight boundary, spacing), make a targeted edit and redeliver the file. Do not rebuild the whole file for a small fix. Re-verify visually only if the change is structural.
- The workflow does not depend on anything specific to Book 3 or to lessons 1–9. Repeat it for any book and any 3-lesson batch.
