# Plain stacks against slot-merged stacks

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

