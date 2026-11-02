---
name: english-worksheet-teaching-material-builder
description: Build a matched student worksheet (HTML to PDF, 2 printed pages per lesson) and a teacher teaching-material document from senior-high English textbook lesson PDFs, following a fixed 5-part teaching-material template. Use when the teacher attaches textbook lesson PDFs and asks for 學習單 and/or 教學材料, or asks to extend an existing set to more lessons.
version: 1.0.0
---

# English worksheet + teaching-material builder

Portable version: works with any AI assistant that can read PDFs and write files. It needs no platform-specific tools.

## What it produces

For each batch of lessons:

1. **Student worksheet**: one HTML file with one `<div class="page">` per lesson, printed to PDF as exactly **2 A4 pages per lesson**.
2. **Teacher teaching-material document**: one document for the batch, 5 parts per lesson.

## Files in this skill

| File | Purpose |
|---|---|
| `SKILL.md` | The workflow and the exact specification (this file) |
| `worksheet-template.html` | The worksheet page: A4 print CSS and the lesson block with placeholders. Copy it as is and only fill the placeholders. |
| `teaching-material-template.md` | The teaching-material structure with placeholders. Keep its headings and tables. |

## Copyright rule (read first)

This skill and its templates contain **no textbook text**. Passages, word lists and example sentences come from the teacher's own textbook PDFs at run time. The generated files are for classroom use only. Never paste textbook content into a public repository.

## When to use

- The teacher attaches one or more textbook lesson PDFs. Each is a full chapter: reading passage, Words for Production / Recognition, Idioms and Phrases, Grammar Focus, Language in Use, Comprehension Practice.
- The teacher asks for student worksheets and/or teaching materials.
- The teacher asks to extend an existing worksheet and teaching-material set to more lessons and refers to the earlier format. In that case match the earlier files.

## Step 1. Extract per lesson

If your platform supports parallel sub-agents, use one per PDF (these run 20+ pages). Otherwise go through them one at a time. Use a PDF text extractor such as `pdftotext -layout`. Extract:

- the main **reading passage**, verbatim;
- **Words for Production** (part of speech and Chinese gloss);
- **Words for Recognition**;
- **Idioms and Phrases**, with the book's own example sentences;
- the lesson's **Grammar Focus** sentence pattern and the secondary **Language in Use** pattern, each with the book's own example sentences drawn from the passage.

Do not invent anything that is not in the PDF.

## Step 2. Build the student worksheet

Use `worksheet-template.html`. Repeat the `<div class="page">` block once per lesson. Each lesson contains, in this order:

**Header** (matches the teacher's finished B3 L1–3 worksheet)
- A black banner bar with letter-spaced white text: `LESSON n ・ ENGLISH TITLE IN CAPITALS`. No Chinese title in the banner.
- The italic subtitle line: `Structure Map • Reading Practice • Sentence Building`.
- A three-cell score bar: `MISSION 1 (Structure Map) ＿＿＿／40`, `MISSION 2 (Reading Practice) ＿＿＿／60`, `TOTAL SCORE ＿＿＿／100`.

**Mission 1: Structure Map** (4 cells × 10 points)
- The section title carries the emoji 📘 and the small note `每格10分，共40分`.
- A dashed word-bank box (`📄 WORD BANK`) with **5 words** in italics separated by `｜`: 4 are used as blanks and 1 is an unused distractor. Do not add a "5選4" note.
- A 2×2 grid of rounded cells that summarises the passage in order. Each cell has a numbered capital-letter title (for example `① THE CLOWN'S JOB`) and 1–2 **bullet points**; the 4 blanks are written `(1) ______` and so on.
- A small grey answer line under the grid: `答案：(1) … (2) … (3) … (4) …　｜　干擾項：word（未使用）`. If the distractor itself appears in a cell's text, say so in this line (for example `未使用，已直接出現在①的文字中`).

**Mission 2: Reading Practice** (6 questions × 10 points)
- The section title carries the emoji 🔍 and the note `每題10分，共60分`. Each question is a rounded box with `( )` and a black pill label (`Q1 Vocabulary`), then a bold serif stem and the options. Q1 and Q2 show the options in two columns (A, B on the left; C, D on the right); Q3–Q6 use one column.
- **Q1, Q2 Vocabulary:** target words in **new context sentences**, not copied from the passage.
- **Q3 Big Idea.**
- **Q4 Detail:** this question has `page-break-before` (class `pb`), so it starts a fresh printed page.
- **Q5 Inference.**
- **Q6 Grammar:** tests the lesson's **primary** Grammar Focus pattern.
- A small grey answer line listing all six answers: `答案：Q1 (A)　Q2 (B) …`.

**Mission 3: Sentence Building** (not graded; emoji 🖊️ and a black `不計分` pill in the title)
- A dashed frame with a sentence frame built on the lesson's **secondary** Language in Use pattern, for example `I find it ____ to ____.`
- `範例（盡量使用課本單字片語）：` followed by a demo sentence that uses passage vocabulary.
- Two labelled writing areas with two ruled lines each: `① 我的仿寫句（先自己寫，不用AI）` and `② AI 修正後的正確句`.
- The closing note, exactly as in the teacher's worksheet: `先人後機：先寫①，再請免費版AI檢查潤飾成②。請用不同顏色的筆，把②和①不一樣的地方標示出來，看看AI幫你修正了什麼。` If the teacher has a rule about which AI tools students may use, add it to this note only when she states it.

Worksheet rules:
- Every question must be written for this passage. Q6 and the Mission 3 frame must correspond to the grammar patterns actually shown in the lesson's Grammar Focus / Language in Use boxes. Never use a pattern the book does not teach.
- Answers appear in the answer notes so the teacher can check. The teacher removes or separates them before handing the sheet to students.

## Step 3. Build the teaching-material document

Use `teaching-material-template.md` (or the same structure in the document format the teacher asks for). Match the headings and tables of earlier lessons in the set. Five parts per lesson:

1. **六組單字片語分工表.** Split the vocabulary and idioms/phrases into **6 groups of about 4–5 items**, balanced by part of speech and difficulty. Put one idiom or phrase in each group when the count allows. When it does not, add a footnote that explains the shortfall. Give every word and phrase the **textbook's own example sentence** (taken from the lesson's Words and Idioms/Phrases sections). Do not write new ones.
2. **認讀字彙.** Recognition-only proper nouns and glosses, listed after the table.
3. **課文重點導讀.** A paragraph-by-paragraph Chinese summary, with the target English vocabulary inline in parentheses.
4. **簡化版 WSQ.**
   - W = the book's existing pre-reading task.
   - S = a bilingual event-ordering list and a bilingual 4-choice big-idea question with the answer marked.
   - Q = the grammar Practice reference, the Comprehension Practice self-check, and the Mission 3 sentence frame.
5. **句型教學規劃.** The primary pattern with the book's examples, then a 3-item practice table; the secondary pattern likewise; and a note that Listening Strategy is moved out of class as self-study material.

Then add a **節次規劃** (5-period schedule) that matches the number of paragraphs.

## Step 4. Render and verify

1. Print each worksheet to PDF (the template already has a page break after every lesson and before Q4) with a headless browser (for example Playwright with Chromium, `format: 'A4'`, `preferCSSPageSize: true`, `printBackground: true`).
2. Check the page count: `pdfinfo file.pdf | grep Pages` must equal **2 × the number of lessons** in that file. If one lesson is off, look at that lesson. Mission 1 cell text running long is the usual cause. Trim wording; do not change the page-break rule.
3. Check programmatically that each lesson's 6 vocabulary groups have 4–5 items each (for example scan the `rowspan` values or the group rows in the table).
4. Confirm that Q6 and the Mission 3 frame correspond to grammar patterns actually in the lesson's Grammar Focus / Language in Use boxes.
5. Confirm that no `{{ }}` placeholder remains.

## Step 5. Deliver

Deliver the worksheet (HTML and PDF) and the teaching-material document. Name the files consistently across the series, for example `學習單_B{book}U{n}~{n+2}.pdf` and `教學材料_B{book}U{n}~{n+2}`. For a small fix, edit the affected lesson only and re-verify the page count.
