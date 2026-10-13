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

