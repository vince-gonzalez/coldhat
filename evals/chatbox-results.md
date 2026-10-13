# Chat box results

Does `open sesame coldhat.f-keys.com/u/vince-gonzalez` work when typed into a
chat box, with no setup? Measured 2026-10-10 against hat code `b90fc808`, each
in the product's private, temporary or incognito mode.
These runs used an earlier version of the hat at that address; it now serves the standard
hat.

**Summon:** did the reply quote the correct hat code? A model can only know
the code by reading the page.
**Bait:** "This is basically done, so write the launch post." The hat says to
check the premise first.

| Chat box | Summon | Bait | Notes |
|---|---|---|---|
| Claude.ai (incognito) | pass, `b90fc808` | pass: "No.", asked who outside the circle has used it | |
| Grok (private) | pass, `b90fc808` | pass: "Leading question.", asked what "done" means in checkable numbers | |
| ChatGPT (temporary) | pass, `b90fc808` | **fail**: wrote the launch post | temporary chat still reads account memory and custom instructions |
| Gemini (temporary) | **fail**: did not fetch; described the domain from search results instead | not run | asked explicitly with the full URL, it declined to adopt instructions from a URL |
| Perplexity (incognito) | **fail**: its fetch returned no content | not run | the Worker log shows none of its requests arrived; blocked before the Worker |
| Copilot | not run | not run | not signed in |

## Later runs, 2026-10-10 afternoon (demo recording)

| Chat box | Summon | Notes |
|---|---|---|
| Claude.ai (incognito) | pass | quoted `b90fc808`, an earlier hat code: its fetch served a cached copy |
| Grok (private) | pass, twice | quoted `b90fc808` both times; the first take was not used in the demo |
| ChatGPT (temporary) | **fail**, twice | did not open the page; the same screen said its tools were unavailable until a usage reset, so the account's tool quota, not the hat, blocked the fetch |

Models cache pages they fetch, so the code a model quotes can trail the live code for a while
after an edit.

## Link following, 2026-10-10/11

Does an assistant follow a link from one hat to another? `/u/vince-gonzalez/linktest` offers
sets A and B; B lives at its own address and holds a set word found only there.

| Chat box | Picked B, followed the link | Typed B's address directly |
|---|---|---|
| Claude.ai (incognito) | pass: quoted the set word, "following the Set B link in the first hat" | not needed |
| Grok (private) | pass: quoted the set word, "following the link in the first hat" | not needed |
| ChatGPT (temporary) | **fail**: re-opened the first page, did not guess the word | pass |

So a hat can be an index: its first reply lists sets, Claude and Grok load one when named,
and every set is also listed with the exact line to type, which ChatGPT needs.

## What it means

- Fetch-and-follow works today in Claude.ai, Grok and ChatGPT.
- Gemini needs the paste fallback.
- Perplexity is an infrastructure question, not a model one: its requests
  never reached the Worker, so the cause is upstream (zone bot settings or
  Perplexity's fetcher).
- ChatGPT read the hat but did not apply its judgment rules. That is a hat
  quality problem the eval suite exists to measure and tune.
