```
╔════════════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                            ║
║                  ██████╗ ██████╗ ██╗     ██████╗ ██╗  ██╗ █████╗ ████████╗                 ║
║                 ██╔════╝██╔═══██╗██║     ██╔══██╗██║  ██║██╔══██╗╚══██╔══╝                 ║
║                 ██║     ██║   ██║██║     ██║  ██║███████║███████║   ██║                    ║
║                 ██║     ██║   ██║██║     ██║  ██║██╔══██║██╔══██║   ██║                    ║
║                 ╚██████╗╚██████╔╝███████╗██████╔╝██║  ██║██║  ██║   ██║                    ║
║                  ╚═════╝ ╚═════╝ ╚══════╝╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝                    ║
║                                                                                            ║
║                            will another model keep your rules?                             ║
║                                                                                            ║
╚════════════════════════════════════════════════════════════════════════════════════════════╝
```

**coldHat** puts working rules on any AI chat in one line. Type this into Claude, ChatGPT
or Grok:

```
open sesame coldhat.f-keys.com/u/vince-gonzalez/frontier
```

The assistant reads the hat, answers with its hat code to prove it read it, and works by
those rules for the rest of the chat. **Live at [coldhat.f-keys.com](https://coldhat.f-keys.com).**

![Claude and Grok each put on the frontier hat from one typed line and answer with its hat code](https://raw.githubusercontent.com/vince-gonzalez/coldhat/main/docs/demo-frontier.gif)

Every hat ends with a seal. If the assistant can't quote it, the hat was cut off, and it tells you.

## Addresses

| You want to | Type this after `open sesame` |
|---|---|
| Wear a person's hat | `coldhat.f-keys.com/u/<github-user>` or `.../u/<github-user>/<hat>` |
| Wear one of [Fabric's patterns](https://github.com/danielmiessler/Fabric/tree/main/data/patterns) | `coldhat.f-keys.com/fabric/extract_wisdom` |
| Wear a [prompts.chat](https://prompts.chat) prompt | `coldhat.f-keys.com/prompts/linux-terminal` |
| Stack up to three, later layers winning | `coldhat.f-keys.com/u/vince-gonzalez/editor+fabric/analyze_claims` |
| Merge a stack by slot instead of piling it up | `coldhat.f-keys.com/amp/fabric/extract_ideas+fabric/analyze_claims` |
| Keep rules no other layer can override | put them under `## Locked` in your hat |
| Wear one exact version | `coldhat.f-keys.com/u/<user>/<hat>@<commit>` |
| Check a reply wore the current hat | `coldhat.f-keys.com/verify?address=<hat address>` with the reply |

Every reply starts with the hat mark and code, for example `🎩💨⛄🔬 Hat's on · b7d19023`:
a top hat, a gust, Frosty, then one icon per layer.

Apps that take connectors can add `https://coldhat.f-keys.com/mcp` once and call any of
these by name (tools `wear_hat` and `wear_stack`). A chat that can't browse can still wear
a hat: **Copy hat** on [coldhat.f-keys.com](https://coldhat.f-keys.com), then paste.

## Starter hats

| Hat | Type this |
|---|---|
| Code reviewer: verdict first, findings by severity with line, failure and fix | `open sesame coldhat.f-keys.com/u/vince-gonzalez/reviewer` |
| Grant writer: rubric first, every number sourced, every limit met | `open sesame coldhat.f-keys.com/u/vince-gonzalez/grants` |
| Plain-English editor: shorter, clearer, still your voice | `open sesame coldhat.f-keys.com/u/vince-gonzalez/editor` |
| Frontier: mechanical register, rules over manners | `open sesame coldhat.f-keys.com/u/vince-gonzalez/frontier` |

## Make your own

A hat is a `hat.md` in a public GitHub repository named `coldhat`, so only its owner can
change it. Extra hats go in `hats/<name>.md` and live at `/u/<user>/<name>`. Write one at
[coldhat.f-keys.com/make](https://coldhat.f-keys.com/make), bring the instructions you
already keep for other assistants at [coldhat.f-keys.com/import](https://coldhat.f-keys.com/import),
or start from [coldhat-starter](https://github.com/vince-gonzalez/coldhat-starter).

Facts under `## Status` carry a date and a shelf life
(`- label: value · as of YYYY-MM-DD · check after N days`). The server checks them against
today, and the assistant asks about any that have gone stale before using them.

## Measured, not assumed

- [Which chat boxes fetch a hat](evals/chatbox-results.md)
- [Merged stacks against plain stacks](evals/amp-results.md)

## Safety

A hat is instructions, not a credential, and `open sesame` is not a password. Every hat
page tells the assistant to ignore it unless the person asked for it, and never to ask for
passwords, keys, codes or payment details. Layers from Fabric and prompts.chat credit their
authors; prompts written to make a model drop its rules are not served.
[Report a hat](https://github.com/vince-gonzalez/coldhat/issues/new?labels=report&title=Report%20a%20hat).

The coldHat server and merge engine are proprietary. This repository holds the public
hats, the format, and the results.

---

```
╔════════════════════════════════════════════════════════════╗
║                                                            ║
║      ███████╗      ██╗  ██╗███████╗██╗   ██╗███████╗       ║
║      ██╔════╝      ██║ ██╔╝██╔════╝╚██╗ ██╔╝██╔════╝       ║
║      █████╗  █████╗█████╔╝ █████╗   ╚████╔╝ ███████╗       ║
║      ██╔══╝  ╚════╝██╔═██╗ ██╔══╝    ╚██╔╝  ╚════██║       ║
║      ██║           ██║  ██╗███████╗   ██║   ███████║       ║
║      ╚═╝           ╚═╝  ╚═╝╚══════╝   ╚═╝   ╚══════╝       ║
║                                                            ║
║               ·   C  R  E  A  T  I  V  E   ·               ║
║                                                            ║
║          ────────────────────────────────────────          ║
║                                                            ║
║                      Vincent Gonzalez                      ║
║                         f-keys.com                         ║
║                 ORCID 0009-0005-3640-014X                  ║
║                                                            ║
╚════════════════════════════════════════════════════════════╝
```

Part of [F-Keys](https://f-keys.com) — independent hardware, software
and internet products. See the [working log](https://f-keys.com/log/)
and [live status](https://f-keys.com/status/).
