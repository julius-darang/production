---
marp: true
theme: default
paginate: true
style: |
  @import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap');

  :root {
    --blue: #2563eb;
    --blue-light: #eff6ff;
    --blue-mid: #bfdbfe;
    --text: #111827;
    --muted: #6b7280;
    --border: #e5e7eb;
    --white: #ffffff;
    --off-white: #f9fafb;

    /* Extended palette */
    --green: #16a34a;
    --green-light: #f0fdf4;
    --green-mid: #bbf7d0;
    --red: #dc2626;
    --red-light: #fef2f2;
    --red-mid: #fecaca;
    --yellow: #ca8a04;
    --yellow-light: #fefce8;
    --yellow-mid: #fef9c3;
    --purple: #7c3aed;
    --purple-light: #f5f3ff;
    --purple-mid: #ddd6fe;
    --orange: #ea580c;
    --orange-light: #fff7ed;
    --orange-mid: #fed7aa;
  }

  section {
    font-family: 'DM Sans', sans-serif;
    background: var(--white);
    color: var(--text);
    padding: 52px 64px;
    font-size: 18px;
    line-height: 1.6;
  }

  section::after {
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--muted);
  }

  h1 {
    font-family: 'DM Sans', sans-serif;
    font-size: 42px;
    font-weight: 600;
    color: var(--text);
    line-height: 1.2;
    margin-bottom: 0.4em;
  }

  h2 {
    font-family: 'DM Sans', sans-serif;
    font-size: 28px;
    font-weight: 600;
    color: var(--text);
    border-bottom: 2px solid var(--blue);
    padding-bottom: 10px;
    margin-bottom: 24px;
  }

  h3 {
    font-family: 'DM Sans', sans-serif;
    font-size: 20px;
    font-weight: 500;
    color: var(--blue);
    margin-bottom: 8px;
  }

  h4 {
    font-family: 'DM Sans', sans-serif;
    font-size: 16px;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 6px;
  }

  p { color: var(--text); margin: 0.4em 0; }
  ul { padding-left: 1.4em; }
  li { margin-bottom: 10px; color: var(--text); }
  strong { color: var(--blue); font-weight: 600; }
  em { color: var(--muted); font-style: italic; }

  code {
    font-family: 'DM Mono', monospace;
    background: var(--blue-light);
    color: var(--blue);
    padding: 2px 8px;
    border-radius: 4px;
    font-size: 0.88em;
  }

  pre {
    background: var(--text);
    color: var(--white);
    padding: 16px 20px;
    border-radius: 10px;
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    line-height: 1.55;
    overflow-x: auto;
    margin: 16px 0;
  }

  pre code {
    background: none;
    color: inherit;
    padding: 0;
    font-size: inherit;
  }

  blockquote {
    border-left: 4px solid var(--blue);
    background: var(--blue-light);
    padding: 16px 20px;
    margin: 20px 0;
    border-radius: 0 8px 8px 0;
    font-family: 'DM Mono', monospace;
    font-size: 0.82em;
    color: #1e40af;
    line-height: 1.6;
  }

  blockquote p { color: #1e40af; margin: 0; }

  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 15px;
    margin: 16px 0;
  }

  th {
    background: var(--text);
    color: white;
    padding: 10px 14px;
    text-align: left;
    font-weight: 500;
    font-size: 13px;
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.03em;
  }

  td {
    padding: 10px 14px;
    border-bottom: 1px solid var(--border);
    color: var(--text);
  }

  tr:nth-child(even) td { background: var(--off-white); }
  tr:last-child td { border-bottom: none; }

  hr {
    border: none;
    border-top: 1px solid var(--border);
    margin: 24px 0;
  }

  a {
    color: var(--blue);
    text-decoration: none;
  }

  a:hover {
    text-decoration: underline;
  }

  /* ═══════════════════════════════════════════════════════════════
     COVER SLIDE (dark)
  ═══════════════════════════════════════════════════════════════ */
  section.cover {
    background: var(--text);
    color: var(--white);
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  section.cover h1 { color: var(--white); font-size: 46px; }
  section.cover h2 { color: #93c5fd; border-bottom-color: #374151; }
  section.cover p  { color: #9ca3af; }
  section.cover strong { color: #60a5fa; }
  section.cover code { background: #1e3a5f; color: #93c5fd; }
  section.cover blockquote { background: #1f2937; border-color: var(--blue); }
  section.cover blockquote p { color: #bfdbfe; }

  /* ═══════════════════════════════════════════════════════════════
     STEP / ALTERNATE SLIDES
  ═══════════════════════════════════════════════════════════════ */
  section.step { background: var(--off-white); }

  /* ═══════════════════════════════════════════════════════════════
     FINAL CTA SLIDES
  ═══════════════════════════════════════════════════════════════ */
  section.final {
    background: var(--blue);
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  section.final h1 { color: white; font-size: 40px; }
  section.final h2 { color: #bfdbfe; border-bottom-color: #1d4ed8; }
  section.final p  { color: #bfdbfe; font-size: 18px; }
  section.final strong { color: white; }
  section.final em { color: #bfdbfe; }
  section.final code { background: #1d4ed8; color: #dbeafe; }
  section.final a { color: #bfdbfe; }

  /* ═══════════════════════════════════════════════════════════════
     LEAD / CENTERED SLIDE
  ═══════════════════════════════════════════════════════════════ */
  section.lead {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  /* ═══════════════════════════════════════════════════════════════
     HIGHLIGHT BOXES
  ═══════════════════════════════════════════════════════════════ */
  .highlight {
    background: var(--blue-light);
    border: 1px solid var(--blue-mid);
    border-radius: 10px;
    padding: 18px 24px;
    margin: 16px 0;
  }

  .highlight.good, .highlight.success {
    background: var(--green-light);
    border-color: var(--green-mid);
  }

  .highlight.warning {
    background: var(--yellow-light);
    border-color: var(--yellow-mid);
  }

  .highlight.error, .highlight.danger {
    background: var(--red-light);
    border-color: var(--red-mid);
  }

  .highlight.tip {
    background: var(--purple-light);
    border-color: var(--purple-mid);
  }

  .highlight.info {
    background: var(--orange-light);
    border-color: var(--orange-mid);
  }

  /* ═══════════════════════════════════════════════════════════════
     TWO-COLUMN LAYOUT
  ═══════════════════════════════════════════════════════════════ */
  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-top: 16px;
  }

  .col-card {
    background: var(--off-white);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px 20px;
  }

  .col-card .label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 8px;
  }

  /* ═══════════════════════════════════════════════════════════════
     THREE-COLUMN LAYOUT
  ═══════════════════════════════════════════════════════════════ */
  .three-col {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
    margin-top: 16px;
  }

  /* ═══════════════════════════════════════════════════════════════
     STEP BADGE / CONCEPT LABEL
  ═══════════════════════════════════════════════════════════════ */
  .step-badge {
    display: inline-block;
    background: var(--blue);
    color: white;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    font-weight: 500;
    padding: 4px 14px;
    border-radius: 999px;
    margin-bottom: 12px;
    letter-spacing: 0.05em;
  }

  .step-badge.green { background: var(--green); }
  .step-badge.yellow { background: var(--yellow); }
  .step-badge.red { background: var(--red); }
  .step-badge.purple { background: var(--purple); }

  /* ═══════════════════════════════════════════════════════════════
     NUMBERED STEP LIST
  ═══════════════════════════════════════════════════════════════ */
  .step-list {
    counter-reset: steps;
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .step-list li {
    counter-increment: steps;
    display: flex;
    align-items: flex-start;
    gap: 14px;
    margin-bottom: 14px;
  }

  .step-list li::before {
    content: counter(steps);
    background: var(--blue);
    color: white;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    font-weight: 500;
    min-width: 24px;
    height: 24px;
    border-radius: 999px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 2px;
    flex-shrink: 0;
  }

  .step-list li.success::before { background: var(--green); }
  .step-list li.warning::before { background: var(--yellow); }
  .step-list li.error::before { background: var(--red); }

  /* ═══════════════════════════════════════════════════════════════
     TOOL CARD GRID
  ══════════════════════════════��═��══════════════════════════════ */
  .tools {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin-top: 16px;
  }

  .tool-card {
    background: var(--off-white);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px 20px;
  }

  .tool-card .icon  { font-size: 24px; margin-bottom: 6px; }
  .tool-card .name  { font-weight: 600; font-size: 15px; color: var(--text); }
  .tool-card .desc  { font-size: 13px; color: var(--muted); margin-top: 2px; }

  /* ═══════════════════════════════════════════════════════════════
     TOOL PILL GRID (3 columns)
  ═══════════════════════════════════════════════════════════════ */
  .tool-pill-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 10px;
    margin-top: 14px;
  }

  .tool-pill {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 12px 14px;
    display: flex;
    align-items: flex-start;
    gap: 10px;
  }

  .tool-pill .tp-icon { font-size: 20px; flex-shrink: 0; }

  .tool-pill .tp-name {
    font-weight: 600;
    font-size: 13px;
    color: var(--text);
    margin-bottom: 2px;
  }

  .tool-pill .tp-desc {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.45;
  }

  /* ═══════════════════════════════════════════════════════════════
     VERSUS / COMPARISON GRID
  ═══════════════════════════════════════════════════════════════ */
  .versus-grid {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    gap: 0;
    align-items: stretch;
    border-radius: 14px;
    overflow: hidden;
    border: 1px solid var(--border);
    margin: 16px 0;
  }

  .vs-side {
    padding: 18px 20px;
  }

  .vs-side.ai    { background: var(--off-white); }
  .vs-side.agent { background: var(--purple-light); }

  .vs-side .vs-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 10px;
  }

  .vs-side.ai    .vs-label { color: var(--muted); }
  .vs-side.agent .vs-label { color: var(--purple); }

  .vs-side .vs-title {
    font-weight: 700;
    font-size: 18px;
    color: var(--text);
    margin-bottom: 10px;
  }

  .vs-side .vs-item {
    font-size: 13.5px;
    color: var(--muted);
    padding: 5px 0;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: flex-start;
    gap: 8px;
  }

  .vs-side .vs-item:last-child { border-bottom: none; }

  .vs-side .vs-item .vi-icon { flex-shrink: 0; font-size: 15px; }
  .vs-side.agent .vs-item     { border-bottom-color: var(--purple-mid); }

  .vs-divider {
    background: var(--border);
    width: 1px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 13px;
    color: var(--muted);
    writing-mode: horizontal-tb;
    padding: 0 14px;
    background: var(--white);
    border-left: 1px solid var(--border);
    border-right: 1px solid var(--border);
  }

  /* ═══════════════════════════════════════════════════════════════
     ReAct LOOP DIAGRAM
  ═══════════════════════════════════════════════════════════════ */
  .react-loop {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0;
    margin: 16px 0;
    position: relative;
  }

  .rl-node {
    border-radius: 12px;
    padding: 14px 16px;
    text-align: center;
    min-width: 115px;
    flex-shrink: 0;
  }

  .rl-node .rn-icon  { font-size: 26px; margin-bottom: 4px; }
  .rl-node .rn-label { font-weight: 700; font-size: 13px; text-transform: uppercase; letter-spacing: 0.06em; }
  .rl-node .rn-desc  { font-size: 11.5px; color: inherit; opacity: 0.75; margin-top: 3px; line-height: 1.4; }

  .rl-node.observe  { background: var(--green-light); border: 2px solid var(--green-mid); }
  .rl-node.think    { background: var(--purple-light); border: 2px solid var(--purple-mid); }
  .rl-node.act      { background: var(--blue-light); border: 2px solid var(--blue-mid); }
  .rl-node.result   { background: var(--yellow-light); border: 2px solid var(--yellow-mid); }

  .rl-node.observe .rn-label { color: var(--green); }
  .rl-node.think   .rn-label { color: var(--purple); }
  .rl-node.act     .rn-label { color: var(--blue); }
  .rl-node.result  .rn-label { color: var(--yellow); }

  .rl-arrow {
    padding: 0 8px;
    font-size: 20px;
    color: var(--blue);
    flex-shrink: 0;
  }

  .rl-loop-back {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 8px;
    gap: 6px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
  }

  .rl-loop-line {
    height: 2px;
    background: var(--border);
    flex: 1;
    border-radius: 999px;
    max-width: 80px;
  }

  /* ═══════════════════════════════════════════════════════════════
     MEMORY CARD GRID
  ═══════════════════════════════════════════════════════════════ */
  .memory-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 14px;
  }

  .memory-card {
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid var(--border);
  }

  .memory-card .mem-header {
    padding: 9px 14px;
    font-weight: 600;
    font-size: 13px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid var(--border);
  }

  .memory-card.short  .mem-header { background: var(--yellow-light); color: var(--yellow); border-color: var(--yellow-mid); }
  .memory-card.long   .mem-header { background: var(--green-light); color: var(--green); border-color: var(--green-mid); }
  .memory-card.episod .mem-header { background: var(--blue-light); color: var(--blue); border-color: var(--blue-mid); }
  .memory-card.extern .mem-header { background: var(--purple-light); color: var(--purple); border-color: var(--purple-mid); }

  .memory-card .mem-body {
    padding: 10px 14px;
    background: var(--white);
    font-size: 12.5px;
    color: var(--muted);
    line-height: 1.55;
  }

  .memory-card .mem-example {
    padding: 7px 14px;
    background: var(--off-white);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    border-top: 1px solid var(--border);
  }

  /* ═══════════════════════════════════════════════════════════════
     AGENT TRACE (step-by-step walkthrough)
  ═══════════════════════════════════════════════════════════════ */
  .agent-trace {
    background: var(--off-white);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    margin: 14px 0;
  }

  .agent-trace .at-bar {
    background: var(--text);
    padding: 9px 16px;
    font-family: 'DM Mono', monospace;
    font-size: 11.5px;
    color: #9ca3af;
    letter-spacing: 0.04em;
  }

  .agent-trace .at-body {
    padding: 12px 16px;
    display: flex;
    flex-direction: column;
    gap: 7px;
  }

  .at-step {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 13px;
  }

  .at-step .as-badge {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    font-weight: 600;
    padding: 3px 8px;
    border-radius: 4px;
    flex-shrink: 0;
    margin-top: 1px;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .as-badge.observe { background: var(--green-light); color: var(--green); border: 1px solid var(--green-mid); }
  .as-badge.think   { background: var(--purple-light); color: var(--purple); border: 1px solid var(--purple-mid); }
  .as-badge.act     { background: var(--blue-light); color: var(--blue); border: 1px solid var(--blue-mid); }
  .as-badge.result  { background: var(--yellow-light); color: var(--yellow); border: 1px solid var(--yellow-mid); }

  .at-step .as-text {
    font-size: 13px;
    color: var(--text);
    line-height: 1.5;
  }

  .at-step .as-text .as-tool {
    font-family: 'DM Mono', monospace;
    font-size: 11.5px;
    color: var(--blue);
    background: var(--blue-light);
    padding: 1px 6px;
    border-radius: 3px;
  }

  /* ═══════════════════════════════════════════════════════════════
     EXAMPLE CARD GRID
  ═══════════════════════════════════════════════════════════════ */
  .example-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 14px;
  }

  .example-card {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 13px 16px;
    display: flex;
    align-items: flex-start;
    gap: 12px;
  }

  .example-card .ec-icon { font-size: 24px; flex-shrink: 0; }

  .example-card .ec-title {
    font-weight: 600;
    font-size: 13.5px;
    color: var(--text);
    margin-bottom: 3px;
  }

  .example-card .ec-desc {
    font-size: 12.5px;
    color: var(--muted);
    line-height: 1.5;
  }

  .example-card .ec-tools {
    display: flex;
    gap: 5px;
    flex-wrap: wrap;
    margin-top: 6px;
  }

  .example-card .ec-tool {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    padding: 2px 6px;
    border-radius: 3px;
    background: var(--blue-light);
    color: #1e40af;
    border: 1px solid var(--blue-mid);
  }

  /* ═══════════════════════════════════════════════════════════════
     CHEATSHEET TABLE
  ═══════════════════════════════════════════════════════════════ */
  .cheat-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 13.5px;
    margin: 12px 0;
  }

  .cheat-table th {
    background: var(--text);
    color: white;
    padding: 8px 14px;
    text-align: left;
    font-weight: 500;
    font-size: 12px;
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.05em;
  }

  .cheat-table td {
    padding: 9px 14px;
    border-bottom: 1px solid var(--border);
    color: var(--text);
  }

  .cheat-table tr:last-child td { border-bottom: none; }
  .cheat-table tr:nth-child(even) td { background: var(--off-white); }

  .cheat-table .mono {
    font-family: 'DM Mono', monospace;
    color: var(--blue);
    font-size: 12.5px;
  }

  /* ═══════════════════════════════════════════════════════════════
     CODE COMPARISON (side-by-side)
  ═══════════════════════════════════════════════════════════════ */
  .code-compare {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin: 16px 0;
  }

  .code-box {
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid var(--border);
  }

  .code-box .cb-header {
    padding: 8px 14px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .code-box.bad .cb-header {
    background: var(--red-light);
    color: var(--red);
    border-bottom: 1px solid var(--red-mid);
  }

  .code-box.good .cb-header {
    background: var(--green-light);
    color: var(--green);
    border-bottom: 1px solid var(--green-mid);
  }

  .code-box pre {
    margin: 0;
    border-radius: 0;
  }

  /* ═══════════════════════════════════════════════════════════════
     PROCESS FLOW (horizontal arrows)
  ═══════════════════════════════════════════════════════════════ */
  .process-flow {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin: 16px 0;
    flex-wrap: wrap;
  }

  .pf-step {
    background: var(--blue-light);
    border: 1px solid var(--blue-mid);
    border-radius: 8px;
    padding: 12px 16px;
    text-align: center;
    min-width: 100px;
  }

  .pf-step .pf-num {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--blue);
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 4px;
  }

  .pf-step .pf-label {
    font-weight: 600;
    font-size: 14px;
    color: var(--text);
  }

  .pf-arrow {
    font-size: 18px;
    color: var(--blue);
    flex-shrink: 0;
  }

  /* ═══════════════════════════════════════════════════════════════
     TIMELINE (vertical)
  ═══════════════════════════════════════════════════════════════ */
  .timeline {
    position: relative;
    padding-left: 30px;
    margin: 16px 0;
  }

  .timeline::before {
    content: '';
    position: absolute;
    left: 8px;
    top: 0;
    bottom: 0;
    width: 2px;
    background: var(--border);
  }

  .timeline-item {
    position: relative;
    margin-bottom: 20px;
  }

  .timeline-item::before {
    content: '';
    position: absolute;
    left: -26px;
    top: 4px;
    width: 12px;
    height: 12px;
    background: var(--blue);
    border-radius: 50%;
    border: 2px solid var(--white);
  }

  .timeline-item .ti-time {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    margin-bottom: 4px;
  }

  .timeline-item .ti-title {
    font-weight: 600;
    font-size: 15px;
    color: var(--text);
    margin-bottom: 4px;
  }

  .timeline-item .ti-desc {
    font-size: 13px;
    color: var(--muted);
  }

  /* ═══════════════════════════════════════════════════════════════
     CHECKLIST
  ═══════════════════════════════════════════════════════════════ */
  .checklist {
    list-style: none;
    padding: 0;
    margin: 12px 0;
  }

  .checklist li {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    margin-bottom: 8px;
    padding-left: 0;
  }

  .checklist li::before {
    content: '☐';
    font-size: 14px;
    color: var(--muted);
    flex-shrink: 0;
  }

  .checklist li.done::before {
    content: '☑';
    color: var(--green);
  }

  /* ═══════════════════════════════════════════════════════════════
     PROS / CONS LIST
  ═════════════════════════════════════════���═���═══════════════════ */
  .pros-cons {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-top: 16px;
  }

  .pros, .cons {
    border-radius: 10px;
    padding: 16px;
  }

  .pros {
    background: var(--green-light);
    border: 1px solid var(--green-mid);
  }

  .cons {
    background: var(--red-light);
    border: 1px solid var(--red-mid);
  }

  .pros .pc-header, .cons .pc-header {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 12px;
  }

  .pros .pc-header { color: var(--green); }
  .cons .pc-header { color: var(--red); }

  .pros ul, .cons ul {
    padding-left: 1.2em;
    margin: 0;
  }

  .pros li { color: var(--green); }
  .cons li { color: var(--red); }

  /* ═══════════════════════════════════════════════════════════════
     STAT CARD (big number + label)
  ═══════════════════════════════════════════════════════════════ */
  .stat-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
    margin-top: 16px;
  }

  .stat-card {
    background: var(--off-white);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px 20px;
    text-align: center;
  }

  .stat-card .stat-value {
    font-family: 'DM Mono', monospace;
    font-size: 32px;
    font-weight: 600;
    color: var(--blue);
    margin-bottom: 4px;
  }

  .stat-card .stat-label {
    font-size: 13px;
    color: var(--muted);
  }

  /* ═══════════════════════════════════════════════════════════════
     ANCHOR LINK (for navigation)
  ═══════════════════════════════════════════════════════════════ */
  .anchor-link {
    position: relative;
  }

  .anchor-link::before {
    content: '#';
    position: absolute;
    left: -20px;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 14px;
    opacity: 0;
    transition: opacity 0.2s;
  }

  .anchor-link:hover::before {
    opacity: 0.5;
  }

  /* ═══════════════════════════════════════════════════════════════
     FOOTNOTE
  ═══════════════════════════════════════════════════════════════ */
  .footnote {
    font-size: 12px;
    color: var(--muted);
    margin-top: 24px;
    padding-top: 12px;
    border-top: 1px solid var(--border);
  }

  /* ═══════════════════════════════════════════════════════════════
     CODE ROW (inline code with label)
  ═══════════════════════════════════════════════════════════════ */
  .code-row {
    display: flex;
    align-items: center;
    gap: 10px;
    margin: 8px 0;
  }

  .code-row .cr-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    min-width: 80px;
  }

  .code-row code {
    flex: 1;
  }
---

<!-- _class: cover -->

# Slide Title Here

## Subtitle goes here

Brief description or hook.

`tag` · `tag` · `tag`

---

## Normal Slide

- Point one with **bold emphasis**
- Point two with `inline code`
- Point three

<div class="highlight">

**Important note** or key takeaway goes here.

</div>

---

<!-- class: step -->

## Step-by-Step Slide

Use this for process explanations.

<div class="step-list">
  <li>First step — do this</li>
  <li>Second step — then this</li>
  <li>Third step — finally this</li>
</div>

---

## Highlight Box Examples

<div class="highlight">

**Default blue highlight** — for important information.

</div>

<div class="highlight success">

**Green highlight** — for success, good practices, correct answers.

</div>

<div class="highlight warning">

**Yellow highlight** — for warnings, things to be careful of.

</div>

<div class="highlight error">

**Red highlight** — for errors, mistakes, pitfalls.

</div>

<div class="highlight tip">

**Purple highlight** — for tips and tricks.

</div>

<div class="highlight info">

**Orange highlight** — for additional info.

</div>

---

## Two-Column Layout

<div class="two-col">
  <div class="col-card">
    <div class="label">Column One</div>
    <p>Content for the first column. Add any elements here.</p>
  </div>
  <div class="col-card">
    <div class="label">Column Two</div>
    <p>Content for the second column.</p>
  </div>
</div>

---

## Three-Column Layout

<div class="three-col">
  <div class="col-card">
    <h4>Card One</h4>
    <p style="font-size:13px;">Description goes here.</p>
  </div>
  <div class="col-card">
    <h4>Card Two</h4>
    <p style="font-size:13px;">Description goes here.</p>
  </div>
  <div class="col-card">
    <h4>Card Three</h4>
    <p style="font-size:13px;">Description goes here.</p>
  </div>
</div>

---

## Step Badge / Concept Label

<div class="step-badge">CONCEPT 01</div>

## The First Concept

Explanation goes here...

<div class="step-badge green">TIP</div>

## Pro Tip

Extra helpful information.

---

## Numbered Steps (Success)

<div class="step-list">
  <li class="success">This step was successful</li>
  <li class="success">Another success</li>
  <li>This is a regular step</li>
</div>

---

## Versus Comparison

<div class="versus-grid">
  <div class="vs-side ai">
    <div class="vs-label">Option A</div>
    <div class="vs-title">Traditional Way</div>
    <div class="vs-item"><span class="vi-icon">→</span> Point one</div>
    <div class="vs-item"><span class="vi-icon">→</span> Point two</div>
    <div class="vs-item"><span class="vi-icon">→</span> Point three</div>
  </div>
  <div class="vs-divider">vs</div>
  <div class="vs-side agent">
    <div class="vs-label">Option B</div>
    <div class="vs-title">Modern Way</div>
    <div class="vs-item"><span class="vi-icon">→</span> Advantage one</div>
    <div class="vs-item"><span class="vi-icon">→</span> Advantage two</div>
    <div class="vs-item"><span class="vi-icon">→</span> Advantage three</div>
  </div>
</div>

---

## ReAct Loop Diagram

<div class="react-loop">
  <div class="rl-node observe">
    <div class="rn-icon">👁️</div>
    <div class="rn-label">Observe</div>
    <div class="rn-desc">Read current state</div>
  </div>
  <div class="rl-arrow">→</div>
  <div class="rl-node think">
    <div class="rn-icon">🧠</div>
    <div class="rn-label">Think</div>
    <div class="rn-desc">Reason about next step</div>
  </div>
  <div class="rl-arrow">→</div>
  <div class="rl-node act">
    <div class="rn-icon">⚡</div>
    <div class="rn-label">Act</div>
    <div class="rn-desc">Call a tool</div>
  </div>
  <div class="rl-arrow">→</div>
  <div class="rl-node result">
    <div class="rn-icon">📋</div>
    <div class="rn-label">Result</div>
    <div class="rn-desc">Get output</div>
  </div>
</div>

<div class="rl-loop-back">
  <div class="rl-loop-line"></div>
  <span>↩ loop until done ↺</span>
  <div class="rl-loop-line"></div>
</div>

---

## Tool Pill Grid (3 columns)

<div class="tool-pill-grid">
  <div class="tool-pill">
    <div class="tp-icon">🔍</div>
    <div>
      <div class="tp-name">Web Search</div>
      <div class="tp-desc">Search the web for information</div>
    </div>
  </div>
  <div class="tool-pill">
    <div class="tp-icon">💻</div>
    <div>
      <div class="tp-name">Code Execute</div>
      <div class="tp-desc">Run code and get results</div>
    </div>
  </div>
  <div class="tool-pill">
    <div class="tp-icon">📁</div>
    <div>
      <div class="tp-name">File System</div>
      <div class="tp-desc">Read and write files</div>
    </div>
  </div>
</div>

---

## Memory Types Grid

<div class="memory-grid">
  <div class="memory-card short">
    <div class="mem-header">⚡ Short-term</div>
    <div class="mem-body">Current conversation context. Cleared when session ends.</div>
    <div class="mem-example">~200k tokens</div>
  </div>
  <div class="memory-card long">
    <div class="mem-header">💾 Long-term</div>
    <div class="mem-body">Persistent storage between sessions.</div>
    <div class="mem-example">Database</div>
  </div>
</div>

---

## Agent Trace Example

<div class="agent-trace">
  <div class="at-bar">agent reasoning trace</div>
  <div class="at-body">
    <div class="at-step">
      <span class="as-badge observe">Observe</span>
      <span class="as-text">Goal received. <span class="as-tool">web_search</span> available.</span>
    </div>
    <div class="at-step">
      <span class="as-badge think">Think</span>
      <span class="as-text">Search for the information.</span>
    </div>
    <div class="at-step">
      <span class="as-badge act">Act</span>
      <span class="as-text">Calling <span class="as-tool">web_search("query")</span> → results returned.</span>
    </div>
    <div class="at-step">
      <span class="as-badge result">Result</span>
      <span class="as-text">Task complete. Summary returned.</span>
    </div>
  </div>
</div>

---

## Example Card Grid

<div class="example-grid">
  <div class="example-card">
    <div class="ec-icon">🔬</div>
    <div>
      <div class="ec-title">Research Agent</div>
      <div class="ec-desc">Searches, reads, and writes reports.</div>
      <div class="ec-tools">
        <span class="ec-tool">web_search</span>
        <span class="ec-tool">browser</span>
      </div>
    </div>
  </div>
  <div class="example-card">
    <div class="ec-icon">💻</div>
    <div>
      <div class="ec-title">Coding Agent</div>
      <div class="ec-desc">Writes code, runs tests, fixes bugs.</div>
      <div class="ec-tools">
        <span class="ec-tool">read_file</span>
        <span class="ec-tool">run_terminal</span>
      </div>
    </div>
  </div>
</div>

---

## Cheatsheet Table

| Command | Description | Example |
|---------|------------|---------|
| `git init` | Initialize a new repo | `git init my-project` |
| `git add .` | Stage all changes | `git add .` |
| `git commit -m "` | Commit with message | `git commit -m "fix bug"` |
| `git push` | Push to remote | `git push origin main` |

<div class="cheat-table">
  <table>
    <tr><th>Type</th><th>Command</th><th>Use</th></tr>
    <tr><td>Undo</td><td class="mono">git restore</td><td>Discard unstaged changes</td></tr>
    <tr><td>Reset</td><td class="mono">git reset --soft</td><td>Undo commits, keep changes</td></tr>
    <tr><td>Revert</td><td class="mono">git revert</td><td>Safe undo on shared branches</td></tr>
  </table>
</div>

---

## Code Comparison

<div class="code-compare">
  <div class="code-box bad">
    <div class="cb-header">❌ Bad Example</div>
    <pre>git commit -m "fix"</pre>
  </div>
  <div class="code-box good">
    <div class="cb-header">✓ Good Example</div>
    <pre>git commit -m "fix: resolve login bug"</pre>
  </div>
</div>

---

## Process Flow

<div class="process-flow">
  <div class="pf-step">
    <div class="pf-num">Step 1</div>
    <div class="pf-label">Input</div>
  </div>
  <div class="pf-arrow">→</div>
  <div class="pf-step">
    <div class="pf-num">Step 2</div>
    <div class="pf-label">Process</div>
  </div>
  <div class="pf-arrow">→</div>
  <div class="pf-step">
    <div class="pf-num">Step 3</div>
    <div class="pf-label">Output</div>
  </div>
</div>

---

## Timeline

<div class="timeline">
  <div class="timeline-item">
    <div class="ti-time">Week 1</div>
    <div class="ti-title">Set up environment</div>
    <div class="ti-desc">Install tools, configure editor</div>
  </div>
  <div class="timeline-item">
    <div class="ti-time">Week 2-3</div>
    <div class="ti-title">Learn basics</div>
    <div class="ti-desc">Core concepts and syntax</div>
  </div>
  <div class="timeline-item">
    <div class="ti-time">Week 4+</div>
    <div class="ti-title">Build projects</div>
    <div class="ti-desc">Apply knowledge to real work</div>
  </div>
</div>

---

## Pros and Cons

<div class="pros-cons">
  <div class="pros">
    <div class="pc-header">✓ Pros</div>
    <ul>
      <li>Fast development</li>
      <li>Large ecosystem</li>
      <li>Easy to learn</li>
    </ul>
  </div>
  <div class="cons">
    <div class="pc-header">✗ Cons</div>
    <ul>
      <li>Initial setup time</li>
      <li>Can be overwhelming</li>
      <li>Version conflicts</li>
    </ul>
  </div>
</div>

---

## Stat Grid

<div class="stat-grid">
  <div class="stat-card">
    <div class="stat-value">3</div>
    <div class="stat-label">Tools used</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">5</div>
    <div class="stat-label">Steps taken</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">10x</div>
    <div class="stat-label">Speed increase</div>
  </div>
</div>

---

## Code with Label

<div class="code-row">
  <span class="cr-label">Install</span>
  <code>npm install package-name</code>
</div>

<div class="code-row">
  <span class="cr-label">Run</span>
  <code>npm run dev</code>
</div>

<div class="code-row">
  <span class="cr-label">Build</span>
  <code>npm run build</code>
</div>

---

## Checklist

<ul class="checklist">
  <li class="done">First item — already done</li>
  <li>Second item — still pending</li>
  <li class="done">Third item — completed</li>
</ul>

---

## Tool Cards (2 columns)

<div class="tools">
  <div class="tool-card">
    <div class="icon">🔧</div>
    <div class="name">Tool Name</div>
    <div class="desc">Brief description of what this tool does.</div>
  </div>
  <div class="tool-card">
    <div class="icon">⚙️</div>
    <div class="name">Another Tool</div>
    <div class="desc">Brief description of what this tool does.</div>
  </div>
</div>

---

## Footnote

<div class="footnote">

* Based on data from 2024 developer survey. Results may vary.

</div>

---

<!-- class: final -->

# Ready to Start?

## Your CTA message here

[optional link or next steps]

---

<!-- _class: lead -->

## Centered Lead Slide

Use `_class: lead` for centered content slides.

---

<!-- _class: anchor-link -->

## Anchor Links

 Hover to see the anchor symbol.

This slide can be linked to directly.