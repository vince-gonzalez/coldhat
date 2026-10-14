# Plain stacks against slot-merged stacks

**Current result:** merged stacks followed the right format **64 of 64** times; plain stacks **4 of 64** (Gemini 3.5 Flash-Lite, 128 runs, after the step fix). The runs below are in the order they happened, including the earlier 62-of-64 run before that fix.

Each case stacks two Fabric patterns whose output formats
disagree. A plain stack (`a+b`) lays the second after the first and says the later layer
wins. A merged stack (`amp/a+b`) reads both into slots and keeps one output format. A case
passes when the later layer's format is used and nothing of the earlier format appears.

## Structure, measured 2026-10-13

| Case | Variant | Bytes | ~Tokens | Repeated lines | Output sections |
|---|---|---|---|---|---|
| summary-wins | plain | 5943 | 1485 | 1 | 3 |
| summary-wins | amp | 5394 | 1348 | 0 | 1 |
| ideas-win | plain | 4038 | 1009 | 1 | 5 |
| ideas-win | amp | 3472 | 868 | 0 | 1 |
| claims-win | plain | 5863 | 1465 | 0 | 4 |
| claims-win | amp | 5703 | 1425 | 0 | 1 |

## Behavior, Grok (Fast), 2026-10-13

One fresh chat per run: `open sesame <address>`, then the article from the suite. Every
reply opened with the correct hat code.

| Case | Plain | Merged |
|---|---|---|
| summary-wins | **fail**: wrote extract_wisdom's IDEAS, INSIGHTS, QUOTES, HABITS and FACTS, then started summarize's format and ran out before TAKEAWAYS; bulleted, not numbered | **pass**: ONE SENTENCE SUMMARY, MAIN POINTS, TAKEAWAYS, numbered; nothing from extract_wisdom |
| ideas-win | **fail**: MAIN POINTS and TAKEAWAYS from summarize, then IDEAS | **pass**: IDEAS only |
| claims-win | **fail**: IDEAS, then the claims analysis | **pass**: ARGUMENT SUMMARY, TRUTH CLAIMS, CLAIM RATING, OVERALL SCORE; no IDEAS |
| **Total** | **0 of 3** | **3 of 3** |

Every plain stack did both jobs, although its header says the later layer wins. Every
merged stack did only the later job.

## Engine v2, Grok (Fast), 2026-10-14

v2 matches each line to a library of instruction atoms, says a shared atom once, resolves known
conflicts in favor of the later layer, and writes a merge receipt into the hat. Same suite, same
article, merged stacks only (plain stacks were measured above).

| Case | Merged, v2 |
|---|---|
| summary-wins | **pass**: ONE SENTENCE SUMMARY, 10 MAIN POINTS, 5 TAKEAWAYS, numbered; nothing from extract_wisdom |
| ideas-win | **pass**: IDEAS only, bulleted |
| claims-win | **pass**: ARGUMENT SUMMARY through OVERALL ANALYSIS; no IDEAS |
| **Total** | **3 of 3** |

The first attempt quoted hat code `7d8d1268`, the code of the v1 page from the day before; the
live code was `6644eb17`. Grok had answered from its own cached copy. Adding `?v=2` to the address
forced a fresh fetch, and every run above quoted the live code. The hat code is what made the
stale copy visible.

## Larger run, Gemini 3.5 Flash-Lite (free tier), 2026-10-14

16 ordered pairs of Fabric patterns whose formats disagree (summarize, extract_ideas,
analyze_claims, extract_wisdom, extract_insights), each as a plain stack and as a merged
stack (engine v2), on two articles, twice each: 128 runs. Graded by regex only: the
second pattern's sections must be present and none of the first pattern's distinctive
sections may appear. Every reply is saved, so the grading can be repeated.

| Case (loser > winner) | Plain | Merged |
|---|---|---|
| summarize>extract_ideas | 0/4 | 4/4 |
| summarize>analyze_claims | 0/4 | 4/4 |
| summarize>extract_wisdom | 0/4 | 4/4 |
| summarize>extract_insights | 0/4 | 4/4 |
| extract_ideas>summarize | 0/4 | 4/4 |
| extract_ideas>analyze_claims | 0/4 | 4/4 |
| extract_ideas>extract_insights | 0/4 | 4/4 |
| analyze_claims>summarize | 0/4 | 4/4 |
| analyze_claims>extract_ideas | 0/4 | 4/4 |
| analyze_claims>extract_wisdom | 0/4 | 4/4 |
| analyze_claims>extract_insights | 0/4 | 4/4 |
| extract_wisdom>summarize | 0/4 | 4/4 |
| extract_wisdom>analyze_claims | 0/4 | 2/4 |
| extract_insights>summarize | 2/4 | 4/4 |
| extract_insights>extract_ideas | 0/4 | 4/4 |
| extract_insights>analyze_claims | 2/4 | 4/4 |
| **Total** | **4/64** | **62/64** |

**Merged 62 of 64 (97%). Plain 4 of 64 (6%).** Plain stacks almost always did both jobs:
the first pattern's sections, then the second's.

The two merged failures share one cause. extract_wisdom's steps say to write "a summary
into a section called SUMMARY", and merging keeps every layer's steps, so that step survives
after extract_wisdom's format has lost. Dropping a losing layer's steps that name its own
sections is the next change to the engine.

### After the step fix, same day

The engine now drops a losing layer's steps that write into its own sections, and the
receipt says how many. The whole merged column was run again (64 runs, same protocol, same
strict grader); the plain column is unchanged.

| | Followed the right format |
|---|---|
| Merged | **64 of 64** |
| Plain | **4 of 64** |

The four extract_wisdom > analyze_claims replies that had opened with extract_wisdom's
"SUMMARY:" section now open with ARGUMENT SUMMARY. The earlier merged replies are kept
beside the new ones.

### How the run was corrected, in order

- **Run 1** sent the summon, the page and the article in one message. Merged hats often
  obeyed the hat's first-reply rule and stopped to ask what to work on, which a real chat
  never forces, since the article arrives as a second message. Run 1 scored plain 9/64 and
  merged 44/64; its replies are kept.
- **Run 2** uses the two-turn conversation a chat actually has: summon and page, the hat's
  own opening, then the article. Both variants get the same turns.
- extract_insights asks for "the INSIGHTS section only" in bullets, without requiring a
  title, so for that winner a bulleted list counts as its format.
- Reading the replies found a leak the first grader missed (a "SUMMARY:" line from
  extract_wisdom), so extract_wisdom's full section list was added. The numbers above use
  that stricter grader.

### Limits

One model, Flash-Lite, at temperature 0.7, four samples per cell, format conflicts only.

## What this does not show

- One model, one sample per cell. Six runs show a direction, not a rate.
- Grok's reply is sometimes missing from the page's text, so the claims-win and
  ideas-win replies were graded from screenshots against the same checks.
- The first plain run may not have been in private mode; it carries no personal data
  either way.
- Only format conflicts were tested. Whether merging changes quality, accuracy or rule
  following beyond format is untested.
- Some Fabric steps still name their own output sections ("into a section called IDEAS").
  The merged hat keeps every method, so an earlier layer's steps can still ask for its
  sections. Grok ignored them here; another model may not.

