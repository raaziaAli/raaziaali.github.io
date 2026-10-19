# Classrooms of the Future

Three classrooms for learning by doing, by Raazia Ali. Live site: https://raaziaali.github.io

| Path | What it is |
|------|------------|
| `index.html` | Landing page: classroom tour (math, photography, earth science), daily challenge, path finder, contact form |
| `math/` | **Mrs. Ali's Classroom** (mathematics): the original interactive math hub, 40+ tools and games |
| `algebra/` | **Algebra 1 & Algebra 2**: course page (`algebra/index.html`) plus one standalone studio per unit (`a1-…`, `a2-…`) |
| `trig-calculus/` | **Trigonometry & Calculus**: course page plus one standalone studio per unit (`t1–t6`, `c1–c7`) |
| `geometry/` | **Geometry Course**: course page (`geometry/index.html`) plus one standalone studio per topic, four units |
| `photography/` | **Photography Classroom**: virtual camera, lens lab, lesson roadmap, stops cheat sheet |
| `earth-science/` | **Earth Science Classroom**: course as rock layers, seismic wedge lab, gamma-ray log lab, industry training |
| `Grade6.html` … `functions-and-graphs.html` | Math lessons and tools linked from Mrs. Ali's Classroom |
| `privacy.html` | Privacy policy |
| `archive/` | Older versions of pages, kept for reference (not linked) |

Other tools live in their own repositories and appear under the same site
(`/math-interactives/`, `/Algebra-1/`, `/mathquest/`, `/Descriptive-Statistics/` …).

## Geometry course
- Each studio in `geometry/` is a single self-contained HTML file in the same style as `angle-studio.html`. `geometry/SPEC.md` is the build spec they follow.
- Add `?embed=1` to any studio URL to hide its header and footer for embedding in an iframe; add `#tab-3` to open a specific lesson tab. The course page has a copy-the-embed-code helper.
- To add a studio: list it in `UNITS` in `geometry/index.html`, and add a card to the matching `geoUnit…` list in `TOOLS` in `math/index.html`.

## Algebra courses
- Same conventions as the geometry studios (`algebra/SPEC.md`), including `?embed=1` and `#tab-N`.
- To add a studio: add it to `COURSES` in `algebra/index.html`, and to `alg1Units` / `alg2Units` in `TOOLS` in `math/index.html`.
- The math hub's Algebra tab has Algebra 1 / Algebra 2 sub-tabs; link straight to one with `/math/#algebra-1` or `/math/#algebra-2`.

## Trigonometry & Calculus courses
- Same conventions (`trig-calculus/SPEC.md`), including `?embed=1` and `#tab-N`.
- To add a studio: add it to `COURSES` in `trig-calculus/index.html`, and to `trigUnits` / `calcUnits` in `TOOLS` in `math/index.html`.
- Link straight to a course sub-tab with `/math/#trigonometry` or `/math/#calculus`.

## Adding things
- **A math tool:** add a line to the `TOOLS` list near the bottom of `math/index.html`. The five course tabs (Middle School Math, Gamified Classroom, Geometry, Algebra, Trigonometry & Calculus) are set in the `SUBJECTS` list just below it: each tab is a list of groups, and a group with no tools shows a "Coming soon" card. Link straight to a tab with `/math/#algebra`, `/math/#trig-calculus`, etc.
- **A daily-challenge question:** add it to the `BANK` list in `index.html` (subject `earth`, `math` or `photo`).
- **A photography or earth science lesson:** change its status from "Coming soon" to "Lab ready" and link it in that classroom's page.
- Use links that start with `/` so they work on the custom domain.
