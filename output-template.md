<!--
This file defines the fixed structure every /research report must follow.
It's read by the agent at the end of the pipeline, after patterns, scores,
and opportunities have been generated.

The SAME structure below is built in TWO places, both treated as primary
outputs — not one as a fallback for the other:

1. A local HTML file (research/[flow]-[date]/report.html)
   - Written via Filesystem MCP, self-contained (embedded/linked
     screenshots from the same folder), works offline
   - No external dependency, so it's always produced, every run
   - Can be opened immediately in a browser, or later hosted (GitHub
     Pages, Vercel, Netlify) and shared as a link

2. A Paper file (via Paper MCP)
   - Live, shareable, commentable, good for team collaboration
   - Built if the Paper MCP is connected and working

Both carry identical content. If Paper MCP fails or isn't connected,
the HTML report alone is a complete, usable deliverable — not a degraded
fallback.
-->

# Output Template

## 1. Summary
3-4 sentences at the very top. What's common across competitors, what
stands out, and the single biggest opportunity. This is what gets read
if nothing else is.

## 2. Patterns (ranked, most common first)
Organized by PATTERN, not by competitor — deduplicated, not repeated once
per competitor.

For each pattern:
- Name (e.g. "Single-field progressive quantity selector")
- Competitors using it (count + names, e.g. "4 of 5 — Notion, Linear, Asana, Zapier")
- 1-2 representative screenshots (not all of them)
- One line on why it matters

## 3. Score Table
One row per competitor, one column per rubric criterion (from rubric.md).
Each cell: the number + a one-line reason.

| Competitor | Info Density | Steps-to-Value | Error Clarity | Edge-Case Handling |
|---|---|---|---|---|
| Notion | 4/5 — reason | 3/5 — reason | 2/5 — reason | 3/5 — reason |
| Linear | ... | ... | ... | ... |

## 4. Edge Cases
Short callouts, each tied to a specific screenshot.
Format: Competitor — what it does differently — why it matters.

## 5. Opportunities
Gaps, weaknesses, whitespace — filtered through context.md's principles
and constraints. This is the payoff section: what you could do differently.

## 6. Full Screenshot Appendix (collapsed / separate section)
Every screenshot, organized by competitor, step-by-step, labeled.
This is reference material — opened only when verifying a claim above
or digging into one competitor's full flow. Not the first thing read.

---

## Re-run Behavior
If Memory finds a prior run of this same flow, add a "What Changed Since
Last Run" section directly under the Summary, before Patterns. Keep the
rest of the structure identical so reports stay comparable run to run.

---

## HTML Build Notes
- One self-contained file: `research/[flow]-[date]/report.html`
- Screenshots referenced via relative paths to the same folder
  (`./screenshots/[competitor]/step-01.png`), so the whole folder stays
  portable — zip it or host it, links still work
- Embedded CSS, no external stylesheet dependency
- Collapsed/accordion section for the Full Screenshot Appendix, so the
  page opens short and expands on demand

## Paper Build Notes
- One frame/section per numbered block above
- Full Screenshot Appendix as its own page or a collapsed frame, so it
  doesn't dominate the first view
- If this is a re-run, add the "What Changed" frame at the top