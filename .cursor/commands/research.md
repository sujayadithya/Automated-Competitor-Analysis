# /research command

Triggered by: /research [flow] (optionally: /research [flow], focus on [specifics])

Example: /research add to cart, focus on seat quantity and coupons

Run the following steps in order. Follow .cursorrules for behavior
(blocked competitors, naming conventions, progress updates, when to ask
vs. proceed).

---

## Step 1: Setup Check

Read context.md.

- If it has content in all sections: proceed to Step 2.
- If it's empty or missing key sections: ask the user, one at a time,
  conversationally in chat:
  1. "What's your product and category?"
  2. "Who's your target user?"
  3. "Any design principles I should filter opportunities through?"
  4. "What does an 'irregular flow' usually mean for your product?"
  5. "Any current constraints I should know about (tech, pricing, team)?"
  6. "Any competitors you already know matter, or any to exclude?" (optional)

  Write the answers into context.md in the existing template format.
  Do not proceed to Step 2 until this is done.

## Step 2: Read Rubric

Read rubric.md. Use its criteria and 1-5 definitions for all scoring in
Step 8. If rubric.md is empty, use the built-in defaults (Info Density,
Steps-to-Value, Error Clarity, Edge-Case Handling).

## Step 3: Competitor Discovery

Search the web for 6-8 direct competitors, using context.md's product
category as the search basis. Prioritize:
- Direct competitors in the same category
- Sources like G2, Capterra, "alternatives to X" articles, comparison pages

Exclude anything listed under context.md's "Known Competitors: Exclude."
Include anything listed under "Known Competitors: Include" automatically.

Post the list in chat as a visible update. Do not wait for approval —
proceed directly to Step 4.

## Step 4: Memory Check

Check Memory for a prior run of this exact flow name.

- If found: retrieve the prior patterns and scores. These will be used
  in Step 10 to build a "What Changed Since Last Run" section.
- If not found: proceed normally, no comparison section needed.

## Step 5: Fetch Public Info

For each competitor found in Step 3, use Fetcher to read:
- Pricing page (if the flow involves cost/billing)
- Help docs / knowledge base articles related to the flow
- Changelog or release notes, if relevant

This builds context on how the flow is intended to work before Step 6
captures it live. Skip this for a competitor if no relevant public page
is found — do not block the run on this step.

## Step 6: Capture the Flow

For each competitor:
1. Use Playwright to navigate to the product and locate the flow
   described in the /research command (and any stated focus).
2. Step through the flow as a real user would (click, fill, scroll).
3. Screenshot at each meaningful step — not every pixel change, but
   every state that would matter to a designer reviewing this later
   (start state, mid-flow choices, error states, confirmation/end state).
4. Save each screenshot via Filesystem using the naming convention in
   .cursorrules: research/[flow]-[date]/[competitor]/step-01-[label].png

If blocked (login, CAPTCHA, paywall): mark this competitor "not
captured" with a one-line reason, and move to the next competitor.
Never stop the full run for one blocked competitor.

Post a short progress update after each competitor finishes (per
.cursorrules) — not after each screenshot.

## Step 7: Pattern Extraction

Across all successfully captured competitors:
- Group screenshots/flows by UI pattern (mechanism), not by competitor
  name — e.g. group "all competitors using inline quantity steppers"
  together, regardless of who they are.
- Rank patterns by how many competitors use them.
- For each pattern, note which competitors use it and pick 1-2
  representative screenshots (not all of them).

Do not write a separate description per competitor if multiple
competitors share the same pattern — write it once.

## Step 8: Scoring

For each successfully captured competitor, score against every
criterion in rubric.md. Each score must include a one-line reason
referencing what was actually observed in the screenshots.

Do not score a competitor marked "not captured" — leave it blank with
a note, not a guessed score.

## Step 9: Opportunity Analysis

Using the patterns (Step 7) and scores (Step 8), identify:
- Consensus: what all or most competitors do the same way
- Divergence: where competitors differ, and who scores best at it
- Whitespace: what none of the competitors address well

Filter every opportunity through context.md's design principles and
constraints — an opportunity that conflicts with a stated constraint
should be flagged as such, not presented as straightforwardly actionable.

## Step 10: Build Report

Follow output-template.md's structure exactly. Build both outputs as
primary (not one as fallback for the other):

1. **Local HTML report**: write via Filesystem to
   research/[flow]-[date]/report.html, self-contained, with relative
   links to the screenshots saved in Step 6.
2. **Paper report**: if Paper MCP is connected, build the same content
   there, following output-template.md's Paper build notes.

If this run found a prior run in Step 4, add the "What Changed Since
Last Run" section directly under the Summary.

If Paper MCP fails or isn't connected, still complete the HTML report
in full and note in the chat reply that Paper wasn't available.

## Step 11: Save to Memory

Store this run's patterns, scores, and flow name in Memory, so a future
/research call on the same flow can generate a comparison.

## Step 12: Reply

Post in chat:
- A one-paragraph summary (the single biggest finding/opportunity)
- The local file path to report.html
- The Paper link, if created
- Any competitors marked "not captured," with a one-line reason each

Do not restate the full report content in chat — the files are the
deliverable, the chat message is a pointer to them.