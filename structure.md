# Content Generation Ecosystem — v5.0
> Multi-Platform Content Processor · 4 Stages · 2 Active Formats · 1 Source of Truth

---

## What Changed from v4.0

| Change | Rationale |
|---|---|
| Stage 0 PP restructured for volume → part → slides hierarchy | Supports series-length courses, not just flat 5-part courses |
| PP input simplified to 5 fields | Removed POSITIONING_ANGLE and ROUGH_IDEAS — both belong in the human's head, not the prompt |
| PP output now emits a Handoff Block | Eliminates manual copy-paste between stages; copy one block, paste once |
| P0 input updated to consume Handoff Block directly | No retyping of audience, series name, or volume context |
| Short-form path clarified for volume-aware use | A short-form part still knows which volume it belongs to |
| Revision Loop expanded with volume-level entries | Covers new failure modes introduced by multi-volume structure |
| What did not change | The Golden Rule, Cross-Format Consistency Gate, and format prompts PA/PB/PE |

---

## Process Flow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  STAGE 0            STAGE 1          STAGE 2          STAGE 3               │
│                                                                              │
│  Course          →  Master Draft  →  Format Outputs                         │
│  Planner (PP)       (P0)             PA · PB · PE                           │
│                     ↑                                                        │
│  Run once.          Consumes the      PA  → DOCX handout                    │
│  Produces a         PP Handoff        PB  → MARP → PDF                      │
│  Handoff Block.     Block directly.   PE  → Title pack                      │
│  Review before                                                               │
│  proceeding.        Run once per      SHORT-FORM PATH:                       │
│                     part.             PP → PE-only (skip P0, PA, PB)         │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Core Design Principle:** Each course is scoped once at Stage 0. Each part is
> drafted once at Stage 1. Every format is a transformation of the same source —
> not a rewrite. You never think the same thought twice.

---

## Format Selection Guide

Run this check before starting any part:

| Part type | Run | Skip |
|---|---|---|
| Full teaching unit — handout + slides | P0 → PA · PB · PE | — |
| Full teaching unit — handout only | P0 → PA · PE | PB |
| Full teaching unit — slides only | P0 → PB · PE | PA |
| Short explainer / newsletter part | PE only (short-form path) | P0 · PA · PB |
| Blog / Substack only | PE only (short-form path) | P0 · PA · PB |

> **Always run PE** regardless of path. Consistent naming across channels
> protects discoverability.
>
> **Short-form path:** Use when the part is a standalone explainer or Substack
> essay that does not require slides or a handout. Go directly from the PP
> Handoff Block to PE. No P0 required.

---

## Stage 0 — Course Planner (PP)

**Run once per course. Review and edit the output before proceeding to Stage 1.**

The PP produces two things: a readable Course Structure for human review, and
a Handoff Block at the end that feeds directly into P0. Do not skip the review
step — the Handoff Block carries every downstream assumption.

---

### PP Input

```
## COURSE PLANNER INPUT

# ── REQUIRED ──────────────────────────────────────────────────────────

TOPIC_OR_WORKING_TITLE:
  {{ e.g. "Prompt Engineering 101" }}

TARGET_OUTCOME:
  {{ What should someone be able to DO after completing this course? }}
  {{ e.g. "Write prompts that consistently produce usable AI outputs" }}

TARGET_AUDIENCE:
  {{ Who is this for? Leave blank → planner will suggest }}

ASSUMED_KNOWLEDGE:
  {{ What do they already know? Leave blank → planner will suggest }}

THINGS_TO_AVOID:
  {{ Tone, words, framings to exclude — leave blank if none }}
```

---

### PP Prompt

```
## ROLE
You are a curriculum architect. Your job is to produce a structured course
plan from a rough input — ready for human review before any content is
produced.

## INPUT
{{ PASTE COMPLETED COURSE PLANNER INPUT }}

## OUTPUT FORMAT

### COURSE IDENTITY
TITLE:        [Benefit-led title — not topic-labelled]
SUBTITLE:     [One sentence — what it delivers for the learner]
POSITIONING:  [1–2 sentences — what makes this different from a generic
               course on this topic]

### AUDIENCE PROFILE
WHO:      [Specific — who this is for]
KNOWS:    [What they know coming in]
PROBLEM:  [The specific frustration this course solves — their words,
           not yours]

### COURSE STRUCTURE

VOLUME [N]: [Title]
ONE-LINER:  [What this volume covers — one sentence]

  PART [N.N]: [Title — outcome-framed, not topic-labelled]
  ONE-LINER:  [What this part teaches — one sentence]

    SLIDES:
    - [Slide title]: [One sentence — what this slide establishes]
    - ...

  Repeat for all parts in this volume.

Repeat for all volumes.

### FLOW RATIONALE
2–3 sentences on why the volumes are ordered this way. What must the
learner understand from Volume 1 before Volume 2 makes sense? What does
the final volume resolve or complete?

### REVIEW NOTES
Flag: volumes merged, topics cut, assumptions made about audience or
positioning that the human should confirm before proceeding.

---

### HANDOFF BLOCK
[Emit this block verbatim at the end. The human copies it into P0 input.]

SERIES_TITLE:      [Course title]
TARGET_AUDIENCE:   [From Audience Profile → WHO]
ASSUMED_KNOWLEDGE: [From Audience Profile → KNOWS]
CORE_PROBLEM:      [From Audience Profile → PROBLEM]
TONE:              [Your suggested default tone for this series — one phrase,
                   e.g. "direct, practical, zero fluff"]

## RULES
- Volumes: 2–5. Hard limit.
- Parts per volume: 3–8.
- Slides per part: 6–10.
- All titles must be outcome-framed.
  BAD:  "Introduction to Prompts"
  GOOD: "Why Your Prompts Keep Failing"
- Slide entries: title + one sentence only. No sub-bullets.
- If optional fields were blank, make a suggestion and flag it in
  Review Notes so the human can confirm or override.
- Stop at the plan. Do not produce Master Drafts or any content.

## SELF-CHECK (append verbatim)
□ 2–5 volumes, each with 3–8 parts, each with 6–10 slides
□ All titles are outcome-framed
□ Slide entries are title + one sentence only
□ Flow Rationale explains volume order
□ Handoff Block present and complete
□ No content produced — plan only
```

---

## Stage 1 — Master Draft (P0)

**One prompt per part. Do not run PA, PB, or PE without a completed,
reviewed Master Draft.**

The P0 input now has two sections: the Handoff Block (copied once from PP,
unchanged for every part in the series) and the Per-Part Fields (filled fresh
for each part).

---

### P0 Input

```
## MASTER DRAFT INPUT

# ── HANDOFF BLOCK — copy from PP output, do not rewrite ──────────────

SERIES_TITLE:      {{ From PP Handoff Block }}
TARGET_AUDIENCE:   {{ From PP Handoff Block }}
ASSUMED_KNOWLEDGE: {{ From PP Handoff Block }}
CORE_PROBLEM:      {{ From PP Handoff Block }}
TONE:              {{ From PP Handoff Block — override here if this part
                      needs a different register }}

# ── PER-PART FIELDS — fill for this part ──────────────────────────────

VOLUME_NUMBER:  {{ e.g. "Volume 2" }}
VOLUME_TITLE:   {{ Volume title from planner }}
PART_NUMBER:    {{ e.g. "Part 2.3" }}
PART_TITLE:     {{ Part title from planner }}

SLIDES_FROM_OUTLINE:
  {{ Slide titles and one-liners for this part, copied from PP output }}

PRIMARY_TAKEAWAY:
  {{ The single most important thing the learner walks away knowing }}

CTA:
  {{ The specific action for this part — one sentence }}

# ── OPTIONAL ──────────────────────────────────────────────────────────

EXAMPLES_OR_ANALOGIES:
  {{ Any examples you already have — leave blank otherwise }}

THINGS_TO_AVOID:
  {{ Additional exclusions for this part beyond the series defaults }}
```

---

### P0 Prompt

```
## ROLE
You are an expert instructional content writer and curriculum architect.
Your job is to produce a definitive Master Content Draft from the input above.
This draft is the single source of truth for all downstream formats.
Write it with that responsibility in mind.
Maintain TONE exactly throughout — no academic drift.

## INPUT
{{ PASTE COMPLETED MASTER DRAFT INPUT }}

## OUTPUT FORMAT

### 1. CORE CONCEPT (2–3 sentences)
The central idea of this part, stated plainly.
No jargon unless immediately defined.
Write it as if explaining to a smart 16-year-old.

### 2. WHY THIS MATTERS (2–3 sentences)
The stakes. What stays broken if the audience never learns this.

### 3. SLIDE-BY-SLIDE BREAKDOWN
For each item in SLIDES_FROM_OUTLINE:

  SLIDE TITLE:
  MAIN POINT:        [1 sentence — the single idea this slide teaches]
  TALKING POINTS:    [3–5 bullets, conversational not academic]
  VISUAL SUGGESTION: [What should appear on screen — diagram, code, photo]

### 4. ANCHOR ANALOGY
One strong real-world analogy that makes the core concept click.
Name it clearly (e.g. "THE RECIPE ANALOGY") so downstream prompts
can reference it by name.

### 5. WORKED EXAMPLE
A concrete before/after or step-by-step example.
Must match ASSUMED_KNOWLEDGE — no unexplained jargon.

### 6. INSIGHT BLOCK (exactly 5 entries)
Format each entry as:

  TAKEAWAY: "I now know that [statement]."
  WATCH OUT: [The most common way people get this wrong — one sentence]

### 7. CALL TO ACTION
The CTA from the input, expanded into 2–3 sentences of motivation.
Must feel earned, not bolted on.

## RULES
- Do not invent information not implied by the input.
- Match TONE exactly throughout — no academic drift.
- If EXAMPLES_OR_ANALOGIES were provided, use them. Do not replace them.
- Every section must be present. Do not skip or merge.
- THINGS_TO_AVOID words must not appear anywhere in the draft.

## SELF-CHECK (append verbatim)
□ All 7 sections present and non-empty
□ Core Concept ≤ 3 sentences
□ Exactly 5 entries in Insight Block
□ Anchor Analogy is named and labelled
□ Worked Example requires no knowledge beyond ASSUMED_KNOWLEDGE
□ Tone matches input — zero academic drift
□ THINGS_TO_AVOID words do not appear
```

---

## Stage 2 — Format Prompts

**Run any format independently after P0 is approved.**

---

### PA — DOCX Handout Generator

**Output:** A structured Word document (.docx) used as a course handout,
converted to PDF for distribution.

**Two-part process:** PA produces a Document Spec first, then a rendering
script. This decouples content from rendering — swap renderers without
rewriting the spec.

---

#### PA Input

```
## DOCX HANDOUT INPUT

MASTER_DRAFT:
  {{ PASTE COMPLETED MASTER DRAFT }}

PAGE_SIZE:
  {{ "A4" or "US Letter" — default: A4 }}

BRAND_ACCENT_COLOR:
  {{ Hex code — e.g. "#2563eb" — leave blank for default dark grey }}
```

---

#### PA Prompt

```
## ROLE
You are a professional instructional designer producing a Word document
(.docx) course handout using docx-js (Node.js).

This document will be used as a course handout and converted to PDF
for distribution. It must be clean, readable, and print-friendly.

Structure content into broad chapters — group related slides together
into coherent sections rather than making each slide a separate heading.
Aim for 3–5 chapters maximum per part, regardless of slide count.

## INPUT
{{ PASTE DOCX HANDOUT INPUT }}

## STEP 1 — DOCUMENT SPEC
Before writing any code, output a Document Spec in this format:

CHAPTER LIST:
  [List 3–5 chapter names and the slides each groups]

CONTENT MAP:
  For each chapter:
  - Chapter name
  - Intro paragraph source (which slide Main Points to synthesise)
  - Body content type (prose / procedural steps / mix)
  - Callout boxes needed (tip / warning / visual placeholder)
  - Whether Worked Example appears in this chapter

SPECIAL PAGES:
  - What You'll Learn page: yes/no
  - Key Takeaways page: yes/no
  - CTA page: yes/no

Output the spec, then pause with:
  "Spec complete. Proceeding to script."

## STEP 2 — NODE.JS SCRIPT
Produce a complete, runnable Node.js script using the docx npm package.
The script must generate a file named:
  [SERIES_TITLE]-[VOLUME_NUMBER]-Part[N]-Handout.docx

## DOCUMENT STRUCTURE

COVER PAGE:
  - Series title (Heading 1 style)
  - Volume number + title (Heading 2 style)
  - Part number + part title (Heading 2 style)
  - One-line descriptor (from Core Concept, first sentence)
  - Page break after cover

WHAT YOU'LL LEARN:
  - Short intro paragraph (from Why This Matters)
  - Bulleted list of the 5 Takeaways (from Insight Block)
  - Page break after section

MAIN BODY — one chapter per logical grouping of slides:
  For each chapter:
  - Chapter heading (Heading 1)
  - Intro paragraph (synthesise the slide Main Points into a
    readable paragraph — do not list them as bullets)
  - Body paragraphs expanding the Talking Points into prose
  - [VISUAL PLACEHOLDER] as a styled callout box where
    Visual Suggestion exists
  - Numbered steps where content is procedural
  - Warning callout box for each Watch Out from the Insight Block

WORKED EXAMPLE CHAPTER:
  - Heading: "In Practice: [short label]"
  - Before block (shaded table cell, labelled "Before")
  - After block (shaded table cell, labelled "After")
  - 1–2 sentence explanation of what changed and why

KEY TAKEAWAYS PAGE:
  - Heading: "What You Now Know"
  - The 5 Takeaways as a numbered list
  - Anchor Analogy in a bordered callout box, labelled with its name
  - Page break after

CTA PAGE:
  - Heading: "Your Next Step"
  - CTA text (from Section 7 of master draft, full 2–3 sentences)
  - Series title, volume number, and part number as footer line

## DOCX-JS RULES
- Install: npm install docx
- Use Arial as default body font, size 24 (12pt)
- Heading 1: Arial, size 32, bold — use for chapter headings
- Heading 2: Arial, size 28, bold — use for sub-sections only
- Never use \n inside TextRun — use separate Paragraph elements
- Never use unicode bullet characters — use LevelFormat.BULLET
  with a numbering config
- Page size: A4 = { width: 11906, height: 16838 }
            US Letter = { width: 12240, height: 15840 }
  Margins: top/right/bottom/left = 1440 (1 inch)
- Tables: always set width with WidthType.DXA, never PERCENTAGE
  Tables need dual widths: columnWidths array AND width on each cell
  Use ShadingType.CLEAR (never SOLID) for shading
  Add cell margins: { top: 80, bottom: 80, left: 120, right: 120 }
- Callout boxes: use a single-cell table with a left border accent
  and light background shading (ShadingType.CLEAR)
- BRAND_ACCENT_COLOR (if provided): apply to Heading 1 colour
  and callout box left border. Strip the # before passing to docx-js.
- Validate after generation:
  python scripts/office/validate.py [filename].docx

## OUTPUT RULES
- Output the Document Spec first, then the complete Node.js script.
- Every section from the master draft must appear in the document.
- Do not invent content not in the master draft.
- Write body sections in full prose — bullet lists only for
  Takeaways, procedural steps, and explicit list content.

## SELF-CHECK (append verbatim)
□ Document Spec produced before script
□ Script runs without error — docx file is generated
□ Cover page has series title, volume, part number, and part title
□ Content grouped into 3–5 broad chapters (not one section per slide)
□ All 5 Takeaways appear on the summary page
□ Worked Example has visible Before/After blocks
□ Warning callout boxes present for all Watch Out items
□ CTA page is the final page
□ Document reads cleanly with no video context needed
```

---

### PB — MARP Slides Generator

**Output:** A `.md` MARP file exported to PDF for sharing.
No speaker notes. Clean static slides optimised for readability as a PDF.

---

#### PB Input

```
## MARP SLIDES INPUT

MASTER_DRAFT:
  {{ PASTE COMPLETED MASTER DRAFT }}

MARP_THEME:
  {{ Paste your theme name or theme config exactly as it appears in your setup }}
  {{ e.g. "theme: my-theme" or paste the full @theme block }}

SLIDE_RATIO:
  {{ "16:9" (default) or "4:3" }}
```

---

#### PB Prompt

```
## ROLE
You are a presentation designer producing a clean MARP markdown slide deck.
This deck will be exported directly to PDF — no live presentation,
no speaker notes. Every design decision should serve readability in PDF form.

## INPUT
{{ PASTE MARP SLIDES INPUT }}

## OUTPUT FORMAT
Output only valid MARP markdown. No prose outside the MARP structure.

Start with the frontmatter block:

---
marp: true
{{ MARP_THEME }}
paginate: true
size: {{ SLIDE_RATIO }}
---

Then produce slides in this exact sequence:

SLIDE 1 — TITLE SLIDE
  # [Volume N] · [Part N.N]: [Part Title]
  ## [Series Title]
  One-line descriptor (from Core Concept, first sentence)

SLIDE 2 — WHAT YOU'LL LEARN
  ## What You'll Learn
  The 5 Takeaways from Insight Block as bullet points
  (rewrite as "You'll be able to…" statements for this slide)

SLIDES 3 to N — ONE SLIDE PER ITEM in Slide-by-Slide Breakdown
  Format per slide:
  ## [Slide Title]
  - [Talking point 1]
  - [Talking point 2]
  - [Talking point 3]
  (max 5 bullets, max 12 words per bullet)
  <!-- [VISUAL: description from Visual Suggestion] -->

SLIDE N+1 — ANCHOR ANALOGY
  ## [Analogy Name]
  Present the analogy as 3–5 short bullets or a two-column layout
  that makes the comparison scannable.

SLIDE N+2 — WORKED EXAMPLE
  ## In Practice
  Split into two visible blocks:
  Left or top block labelled "Before" — the weak version
  Right or bottom block labelled "After" — the improved version
  Use a fenced code block if the example contains prompt text.

SLIDE N+3 — INSIGHT BLOCK
  ## What You Now Know
  5 bullets — one per Takeaway from Insight Block
  Sub-bullet for each: Watch Out → one-line correct approach

SLIDE N+4 — CTA SLIDE
  ## Your Next Step
  The CTA in 2–3 short lines, large and uncluttered.
  Series title, volume number, and part number as a small sub-line at bottom.

## RULES
- Maximum 5 bullets per slide body.
- Maximum 12 words per bullet.
- No prose paragraphs on any slide — bullets or short phrases only.
- No speaker notes — this is a PDF-export deck.
- Prompt text or code examples must use fenced code blocks
  with a language identifier (e.g. ```text or ```python).
- Visual suggestions go in HTML comments: <!-- [VISUAL: ...] -->
  They are placeholders only — do not render as slide content.
- Do not output any text outside the MARP markdown structure.

## SELF-CHECK (append verbatim)
□ Valid MARP frontmatter — correct theme name applied
□ Title slide includes volume number and part number
□ No slide has more than 5 bullets
□ No bullet exceeds 12 words
□ No prose paragraphs on any slide
□ Worked Example slide has visible Before/After blocks
□ Code/prompt examples use fenced code blocks with language identifier
□ No speaker notes present
□ File exports to PDF without error via MARP CLI or VS Code
```

---

### PE — Title & Description Pack

**Run this after the Master Draft is fully approved, or directly from the
PP Handoff Block when using the short-form path.**

```
## ROLE
You are a content strategist and SEO copywriter producing platform-
optimised titles, descriptions, and copy for every distribution channel.

## INPUT
{{ PASTE COMPLETED MASTER DRAFT — or PP Handoff Block if short-form path }}

## OUTPUT FORMAT
Output all five blocks below, clearly labelled.

--- YOUTUBE / REEL TITLE ---
[Max 60 characters. Lead with benefit or problem solved.
Include volume and part number. No clickbait that doesn't deliver.]

--- LINKEDIN POST ---
[150–200 words.
Structure: bold hook line → 3–5 value bullets → bridge sentence → CTA.
2–3 relevant hashtags max. Line break between every 1–2 sentences.]

--- INSTAGRAM CAPTION ---
[80–120 words. Conversational, first-person.
Hook must land in the first 125 characters (before "more" cutoff).
End with a question to drive comments.]
HASHTAGS: [20–25 tags — mix of niche, mid-range, and broad reach]

--- SEO META DESCRIPTION ---
[Max 155 characters. Primary keyword placed naturally.
Describe what the reader learns. End with a soft CTA verb.]

--- DOCUMENT / SLIDE COVER TITLE ---
[Max 8 words. Used on the DOCX cover page and MARP title slide.
Benefit-led. Must match the Part title from the planner.]

--- POSITIONING FLAG ---
[yes / no]
[If yes: note in one sentence what the title-writing process revealed
about positioning that differs from the PP framing. Bring this back
to the Course Planner before the next course iteration.]

## RULES
- YouTube title: no ALL CAPS, no emoji, lead with keyword.
- Instagram: first 125 characters must work as a standalone sentence.
- Never duplicate the same sentence verbatim across platforms.
- Match TONE from the Master Draft (or PP Handoff Block if short-form).

## SELF-CHECK (append verbatim)
□ YouTube title ≤ 60 characters, includes part reference
□ LinkedIn post 150–200 words with correct structure
□ Instagram hook works as standalone in first 125 characters
□ Instagram has 20–25 hashtags
□ Meta description ≤ 155 characters
□ Document/slide cover title ≤ 8 words
□ No copy duplicated verbatim across platforms
□ Positioning flag completed
```

---

## Revision Loop

| Problem | Where to fix |
|---|---|
| Output is too generic | Enrich P0 — add concrete examples to Sections 4 and 5. Never fix generic outputs in the format prompt. |
| Wrong tone | Add 2–3 phrasing examples to the P0 TONE field: "Write like this: [example]. Not like this: [bad example]." |
| Tone is right for some parts but not others | Override TONE in the Per-Part Fields of P0. The Handoff Block default still applies to all other parts. |
| DOCX structure is off | Re-run PA with a correction block: "REMINDER: [violated rule]. Fix this section: [paste bad output]." |
| MARP bullets too long | Append to PB: "REMINDER: max 12 words per bullet. Rewrite all bullets exceeding this limit." |
| Inconsistency across DOCX and slides | Lock P0 first. Inconsistency almost always means P0 was not finalised before format runs began. |
| Volume scope is too broad | Edit the PP output directly before running any P0. Split into two volumes and flag in Review Notes. |
| Part count per volume is too high | Merge two parts or move one to the next volume. Edit PP — never patch in P0. |
| Planner suggested wrong parts | Edit the PP output before running any Master Draft. Never patch downstream. |
| PE surfaces a better positioning angle | Note it in the Positioning Flag. Bring it back to PP for the next course — do not patch the current course mid-run. |

> **Golden Rule:** Fix problems upstream, not downstream. If both formats share
> the same issue, the fix belongs in the Master Draft — not in PA and PB
> separately. If multiple parts share the same issue, the fix belongs in the
> PP output — not in individual P0 runs.

---

## Cross-Format Consistency Gate

Before distributing any format, confirm all three:

1. **Core concept** — stated the same way in the DOCX intro and on MARP Slide 2
2. **CTA** — identical in intent on the DOCX CTA page and MARP final slide
3. **Anchor Analogy** — same name and framing in both formats

If any of these diverge, return to the Master Draft before publishing.

---

*Content Generation Ecosystem · v5.0 · Updated May 2026*
*Active formats: DOCX Handout (PA) · MARP Slides (PB) · Title Pack (PE)*
*HTML Tutorial and Carousel prompts deferred — restore in v6.0 when ready*