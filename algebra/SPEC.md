# Algebra studio build spec (shared by every simulation)

You are building ONE standalone interactive algebra simulation page for "Mrs. Ali's Classroom", a free site used by a practicing high school math teacher with her students. Quality bar: a polished, correct, genuinely useful classroom tool. A teacher will project it and students will use it on laptops and phones.

## Hard requirements
1. **One self-contained HTML file** at the path you are given. Inline CSS + inline JS. No frameworks, no build step, no external JS. The only external resource allowed is the Google Fonts stylesheet already used by the house style. Pure SVG (preferred) or <canvas> for drawing.
2. **Match the house style exactly.** Read `/home/claude/site/angle-studio.html` lines 1–200 (CSS + page skeleton) and skim `/home/claude/site/geometry/coordinate-line-lab.html` (the best reference for coordinate-grid graphing, snapping and the Challenge tab). Skim their JS for patterns (tab system, board, side panels, drag handles, "verdict" feedback). Reuse its CSS variables, fonts, classes and layout: `.wrap`, `header.masthead` with `.mark` title (gradient text) + `.eyebrow` (e.g. "Algebra 1 · Unit 4 · Systems of Linear Equations"), `nav.tabs` pill tabs, `.stage` grid (board left, `aside#side` panels right), `.board` with `.board-head` (h2 + `.lsn` standards chip), white `svg.canvas` drawing surface, `.bar` controls under the board, `.panel` cards with `h3` + `.pad`, `.eq` formula boxes, `.verdict.good/.bad` feedback, `footer.foot`. Copy the CSS block wholesale and extend it; do not invent a different look.
3. **Tabs = lessons.** 4–6 tabs, each a distinct lesson/investigation, numbered (`<span class="n">01</span>`). The LAST tab must be a **Challenge / Practice** tab: randomly generated problems (at least 3 problem types, infinite supply via a "New problem" button), answer entry, checking with tolerance, a helpful explanation on wrong answers, and a score streak shown in the bar.
4. **Everything is live.** Points/handles are draggable (pointer events, works with mouse AND touch: use `pointerdown/move/up`, `setPointerCapture`, `touch-action:none` on the svg, convert client coords via `getScreenCTM().inverse()`). Every measure shown is computed from the current figure, never hard-coded. Show measurements on the figure and in the side panel. Snap-to-grid option where a coordinate grid is used.
5. **Mathematically correct.** Use correct vocabulary and methods from high school algebra (Common Core / Eureka-EngageNY wording). Each tab's `.lsn` chip shows its CCSS codes (e.g. `A-REI.C.6`, `F-IF.C.7a`). Side panels explain the idea in 2–4 short paragraphs a 15-year-old can follow, show the key formula in `.eq`, and include a "Try this" panel with a concrete investigation prompt. Round displayed values sensibly; show exact fractions where the math is exact (write a small fraction helper), and render math in readable plain text/HTML (superscripts via <sup>, fractions as a/b or stacked HTML) — no MathJax.
6. **Embeddable.** If the URL has `?embed=1` (check `new URLSearchParams(location.search).has('embed')`), add class `embed` to <body> and hide `header.masthead` and `footer.foot` and reduce `.wrap` padding to 10px. Deep-link tabs with `#tab-N` hash (e.g. `#tab-3` opens the third tab) and update the hash on tab click.
7. **Responsive & accessible.** Works at 390px wide (stage stacks to one column, bar wraps, no horizontal scroll). Buttons are real <button>s with aria-selected/aria-pressed as in Angle Studio; svg has role="img" + aria-label; visible focus states.
8. **Footer** includes a back link: `<a href="/algebra/">← Algebra courses</a>` and `<a href="/math/#algebra">Mrs. Ali's Classroom</a>`, styled like other links (color var(--cyan)).
9. `<title>` like `Systems Lab — Algebra 1 Unit 4`. Include `<meta name="viewport">`, `lang="en"`, and the same inline SVG favicon pattern is optional.
10. **No console errors.** Test before you finish (see below). Wrap the whole script in an IIFE with "use strict".

## Test before you report done
Run a local server and a headless check with Playwright (Python `playwright` is installed, chromium available):
```
cd /home/claude/site && (python3 -m http.server 8800 >/dev/null 2>&1 &)
```
Write a small Python script (put it in /tmp/claude-0/-home-claude/57576cfb-6e6a-53e1-8141-5b250b78e5fa/scratchpad/, NOT in the site folder) that, at 1280px and 390px widths, opens every `#tab-N`, collects `pageerror` and console errors, clicks the main buttons on each tab, simulates a drag on at least one handle (page.mouse down/move/up), and screenshots each tab. LOOK at the screenshots (Read the png) and fix layout, overlap, label collisions and clipping. On the Challenge tab, generate several problems and submit a correct answer computed from the page state to confirm checking works. Use a port other than 8765 if it is busy; the server may already be running.

## Report back
Reply with: file path, list of tabs with their standards, anything you could not do, and the verified test result (errors: none). Keep the report under 150 words. Do NOT edit any file other than your own simulation file. Do not run git commands.

## Algebra-specific notes
- Graphs: draw functions as SVG paths sampled densely (handle discontinuities/asymptotes by breaking the path), with a labeled grid, axes, and draggable points where it helps. Let students zoom the window if the topic needs it (± buttons).
- Answer parsing in Challenge tabs must accept equivalent forms: integers, decimals (tolerance), fractions like `-3/4`, and where relevant expressions/equations (e.g. compare polynomials by evaluating at several random x values; compare equations of lines by slope and intercept). Explain the expected format under the input box.
- Name your test scripts with your file's name as a prefix (the scratchpad is shared with other builders working at the same time).
