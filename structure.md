# Content Generation Ecosystem — v6.0
> 2 Stages · 2 Formats · 1 Source of Truth

---

## Process Flow

```
STAGE 0          STAGE 1
CP  →  MD  →  HO (DOCX handout)
               SL (MARP slides)
```

- **CP** runs once. Produces a plan for human review.
- **MD** runs once per volume. Produces one draft block per part.
- **HO** and **SL** each consume a single PART DRAFT block from the MD output.

---

## Stage 0 — CP (Course Planner)

**Run once. Review and edit before proceeding to Stage 1.**

### CP Input

```
TOPIC_OR_WORKING_TITLE:
TARGET_OUTCOME:
TARGET_AUDIENCE:
ASSUMED_KNOWLEDGE:
TONE:
THINGS_TO_AVOID:
```

### CP Prompt

```
## ROLE
You are a curriculum architect. Produce a structured course plan from
the input below — ready for human review before any content is written.

## INPUT
{{ PASTE CP INPUT }}

## OUTPUT

### COURSE IDENTITY
TITLE:       [Benefit-led — not topic-labelled]
SUBTITLE:    [One sentence — what it delivers for the learner]

### AUDIENCE PROFILE
WHO:      [Who this is for]
KNOWS:    [What they know coming in]
PROBLEM:  [The specific frustration this course solves]

### COURSE STRUCTURE

VOLUME [N]: [Title]
ONE-LINER:  [What this volume covers — one sentence]

  PART [N.N]: [Outcome-framed title — not topic-labelled]
  ONE-LINER:  [What this part teaches — one sentence]

### HANDOFF BLOCK
[Copy this into MD Input unchanged.]

SERIES_TITLE:      [Course title]
TARGET_AUDIENCE:   [From Audience Profile]
ASSUMED_KNOWLEDGE: [From Audience Profile]
CORE_PROBLEM:      [From Audience Profile]
TONE:              [From input — one phrase, e.g. "direct, practical, no fluff"]
THINGS_TO_AVOID:   [From input — "None" if blank]

COURSE_STRUCTURE:
  VOLUME 1: [Title]
    PART 1.1: [Title] — [one-liner]
    PART 1.2: [Title] — [one-liner]
  VOLUME 2: [Title]
    PART 2.1: [Title] — [one-liner]
    ...

## RULES
- Volumes: 1–3. Parts per volume: 2–5.
- All part titles must be outcome-framed.
  BAD:  "Introduction to Prompts"
  GOOD: "Why Your Prompts Keep Failing"
- Do not produce any content — plan only.
```

---

## Stage 1 — MD (Master Draft)

**One run per volume. Extract individual PART DRAFT blocks before running HO or SL.**

### MD Input

```
## MD INPUT

# ── HANDOFF BLOCK (from CP, unchanged) ───────────────────────────────────

SERIES_TITLE:
TARGET_AUDIENCE:
ASSUMED_KNOWLEDGE:
CORE_PROBLEM:
TONE:
THINGS_TO_AVOID:

# ── VOLUME FIELDS ─────────────────────────────────────────────────────────

VOLUME_NUMBER:
VOLUME_TITLE:

# ── VOLUME_PARTS_DETAIL ───────────────────────────────────────────────────
# Fill all fields before running MD.

VOLUME_PARTS_DETAIL:

  PART [N.N]: [Part title]
  ONE_LINER:          [From COURSE_STRUCTURE]
  PRIMARY_TAKEAWAY:   [The single most important thing the learner walks away knowing]
  CTA:                [The specific action for this part — one sentence]
  EXAMPLES_OR_ANALOGIES: [Any examples you already have — leave blank if none]
  THINGS_TO_AVOID_PART:  [Additional exclusions — leave blank if none]

  [Repeat for every part in this volume]
```

### MD Prompt

```
## ROLE
You are an instructional content writer. Produce a complete Master Draft
for the entire volume — one draft block per part — from the input above.

Draft every part with full awareness of every other part in the volume.
No part may introduce a concept belonging to a later part. No part may
re-explain a concept already covered earlier — a brief reference is fine,
a re-explanation is not.

## INPUT
{{ PASTE MD INPUT }}

## VOLUME ORIENTATION
Before drafting, output this block:

  VOLUME: [Number + Title]
  PART SEQUENCE: [List all parts and their one-liners]
  CONCEPT MAP:
    [Concept] → introduced Part [N.N], may be referenced in [N.N, N.N]
  SCOPE LOCKS:
    Part [N.N]: must not cover [X] — belongs to Part [N.N]

## PART DRAFTING
After the orientation, draft each part in sequence.

Open each part with:
  ══════════════════════════════════════════════
  PART DRAFT [N.N]: [Part Title]
  TONE USED: [Series TONE]
  ══════════════════════════════════════════════

Produce all 6 sections below for every part.

## OUTPUT FORMAT (per part)

### 0. PLANNED SLIDES
[6–8 outcome-framed slide titles. Must match Section 3 headings exactly.]

### 1. CORE CONCEPT (2–3 sentences)
The central idea, stated plainly. No jargon unless immediately defined.

### 2. WHY THIS MATTERS (2–3 sentences)
The stakes. What stays broken if the learner never learns this.

### 3. SLIDE-BY-SLIDE BREAKDOWN
For each slide in Section 0:

  SLIDE TITLE:
  MAIN POINT:     [1 sentence — the single idea this slide teaches]
  TALKING POINTS: [3–5 bullets, conversational]
  VISUAL:         [What should appear on screen]

### 4. ANCHOR ANALOGY
One real-world analogy that makes the core concept click.
Name it clearly (e.g. "THE RECIPE ANALOGY").

### 5. WORKED EXAMPLE
A concrete before/after or step-by-step example.
No jargon beyond ASSUMED_KNOWLEDGE.

### 6. CALL TO ACTION
Restate the CTA as the first sentence. Add 1–2 sentences on why it matters now.
Total: 2–3 sentences.

Close each part with:
  ── END PART DRAFT [N.N] ──────────────────────

## RULES
- Complete VOLUME ORIENTATION before any part draft.
- Every section (0–6) must be present for every part.
- Section 0 and Section 3 must match exactly at finalisation.
- Enforce SCOPE LOCKS — correct drift before continuing.
- If EXAMPLES_OR_ANALOGIES were provided, use them.
- Words in THINGS_TO_AVOID and THINGS_TO_AVOID_PART must not appear
  in the relevant part draft.
- Match TONE exactly — no academic drift.
```

---

## Stage 2 — Format Prompts

**Extract the relevant PART DRAFT block from the MD output before running
either format. Paste only that block — not the full volume output.**

---

### HO — DOCX Handout (Detailed)

**Design intent:** A deep-read document. The learner should understand and
apply the full lesson without watching the video. Talking points become
prose paragraphs. Every Watch Out gets a warning box.

#### HO Input

```
MASTER_DRAFT:     {{ PASTE SINGLE PART DRAFT BLOCK }}
PAGE_SIZE:        {{ A4 or US Letter — default: A4 }}
BRAND_ACCENT_COLOR: {{ Hex — leave blank for dark grey }}
```

#### HO Prompt

```
## ROLE
You are an instructional designer producing a Word document (.docx)
course handout using the docx npm package (Node.js).

This is a deep-read document. The learner must be able to understand
and apply the full lesson from this document alone. Expand bullet points
into prose. Give analogies space to land. Make every warning prominent.

## INPUT
{{ PASTE HO INPUT }}

## STEP 1 — DOCUMENT SPEC
Before writing any code, output:

CHAPTER LIST:
  [3–5 chapters grouping slides by instructional phase:
   Orientation · Core Teaching · Application · Synthesis]

SPECIAL PAGES:
  - What You'll Learn: yes/no
  - Key Takeaways: yes/no
  - CTA page: yes/no

Output the spec, then continue to the script.

## STEP 2 — NODE.JS SCRIPT
Generate a file named:
  [SERIES_TITLE]-[VOLUME_NUMBER]-Part[N]-Handout.docx

## DOCUMENT STRUCTURE

COVER PAGE:
  Series title · Volume · Part number · Part title
  First sentence of Core Concept as descriptor
  Page break after

WHAT YOU'LL LEARN:
  Why This Matters (2–3 sentences)
  5 bullets from Insight Block as "You will be able to…" statements
  Page break after

MAIN BODY — one chapter per instructional phase:
  CHAPTER HEADING (Heading 1)
  INTRO PARAGRAPH: Synthesise MAIN POINTS from slides in this chapter
    into connected prose. Do not list Main Points as bullets.
  BODY PARAGRAPHS: TALKING POINTS expanded into full prose (2–4 sentences
    each). Procedural content only may use numbered lists.
  VISUAL PLACEHOLDER: Bordered callout — "[VISUAL: {description}]"
  WATCH OUT CALLOUT: One per Watch Out. Left border in brand colour.
    Label "Watch out:" in bold.

ANCHOR ANALOGY SECTION:
  Heading: [Analogy Name] (Heading 1)
  2–3 prose sentences in a named bordered callout.

WORKED EXAMPLE CHAPTER:
  Heading: "In Practice: [label]" (Heading 1)
  Before block (shaded, labelled "Before" in bold)
  After block (shaded, labelled "After" in bold)
  Explanation: 2–3 sentences on what changed and why.

KEY TAKEAWAYS PAGE:
  "What You Now Know" (Heading 1)
  5 Takeaways numbered, each followed by its Watch Out in muted text
  Page break after

CTA PAGE:
  "Your Next Step" (Heading 1)
  Full CTA text (2–3 sentences)
  Series · Volume · Part as footer line

## DOCX RULES
- Install: npm install docx
- Body: Arial 24 (12pt), line spacing 1.15
- Heading 1: Arial 32, bold | Heading 2: Arial 28, bold
- Never use \n inside TextRun — use separate Paragraph elements
- Never use unicode bullets — use LevelFormat.BULLET with numbering config
- Page size: A4 = { width: 11906, height: 16838 }
            US Letter = { width: 12240, height: 15840 }
  Margins: 1440 all sides
- Tables: WidthType.DXA only. ShadingType.CLEAR only.
  Cell margins: { top: 80, bottom: 80, left: 120, right: 120 }
- BRAND_ACCENT_COLOR: apply to Heading 1 and all callout left borders.
  Strip # before passing to docx.

## PROSE RULES
- MAIN POINT → synthesised into chapter intro (never standalone)
- TALKING POINTS → prose paragraphs (never copied verbatim)
- ANCHOR ANALOGY → 2–3 prose sentences in named callout
- WORKED EXAMPLE → full Before/After with explanation paragraph
- CALL TO ACTION → CTA page, full 2–3 sentences
```

---

### SL — MARP Slides (Condensed)

**Design intent:** A glanceable reference. One idea per slide, visible
in under 10 seconds. Talking points distilled, not copied. The handout
carries the detail — the deck carries the skeleton.

#### SL Input

```
MASTER_DRAFT: {{ PASTE SINGLE PART DRAFT BLOCK }}
MARP_THEME:   {{ Theme name or full @theme block }}
SLIDE_RATIO:  {{ 16:9 (default) or 4:3 }}
```

#### SL Prompt

```
## ROLE
You are a presentation designer producing a MARP markdown slide deck
for PDF export. Every decision serves readability as a static PDF.
Extract and compress — do not reproduce. The DOCX carries the prose.

## INPUT
{{ PASTE SL INPUT }}

## CONDENSATION RULES
- MAIN POINT → headline bullet (≤ 10 words)
- TALKING POINTS → distil to 2–3 bullets max (≤ 12 words each)
- ANCHOR ANALOGY → 3 bullets: the analogy · the connection · the limit
- WORKED EXAMPLE → Before / After, one line each, no explanation
- INSIGHT BLOCK → 5 bullets, Takeaways only (no Watch Outs on slides)
- CALL TO ACTION → 2 lines: the action · one line of motivation

## OUTPUT FORMAT
Output only valid MARP markdown.

---
marp: true
{{ MARP_THEME }}
paginate: true
size: {{ SLIDE_RATIO }}
---

SLIDE 1 — TITLE
  # [Volume N] · [Part N.N]: [Part Title]
  ## [Series Title]
  [Core Concept, first sentence, ≤ 12 words]

SLIDE 2 — WHAT YOU'LL LEARN
  ## What You'll Learn
  5 bullets — "You'll be able to…" (≤ 12 words each)

SLIDES 3–N — ONE SLIDE PER ITEM in Section 3
  ## [Slide Title from Section 3]
  - [MAIN POINT ≤ 10 words]
  - [Distilled talking point ≤ 12 words]
  - [Distilled talking point ≤ 12 words]
  <!-- [VISUAL: description] -->

SLIDE N+1 — ANCHOR ANALOGY
  ## [Analogy Name]
  - [The analogy — ≤ 12 words]
  - [Connection to concept — ≤ 12 words]
  - [Limit of analogy — ≤ 12 words, omit if not useful]

SLIDE N+2 — WORKED EXAMPLE
  ## In Practice
  **Before:** [one line]
  **After:**  [one line]

SLIDE N+3 — INSIGHT BLOCK
  ## What You Now Know
  5 Takeaway bullets only (≤ 12 words each)

SLIDE N+4 — CTA
  ## Your Next Step
  [Action — ≤ 12 words]
  [Motivation — ≤ 12 words]
  [Series · Volume · Part]

## RULES
- Max 3 bullets per content slide (Slides 3–N)
- Max 12 words per bullet anywhere in the deck
- No prose paragraphs on any slide
- No speaker notes
- Prompt/code examples → fenced code blocks with language identifier
- Visual suggestions → HTML comments only
- Watch Out content must not appear on slides
- Section 3 headings are the source of truth for slide titles
- Match TONE USED from part draft header
```

---

## Golden Rule

> **Fix problems upstream, not downstream.**
> If HO and SL share the same issue, fix the part draft — not the format outputs.
> If multiple parts share the same issue, fix the MD volume run — not individual parts.

---

*Content Generation Ecosystem · v6.0 · Simplified May 2026*
*Active formats: HO (DOCX, detailed) · SL (MARP, condensed)*