# Focus HQ — the Daily TLDR

Data only. **No application code lives here, and none ever should.**

This repo exists so the scheduled writer agent has push access to *news bullets*
and to nothing else. The Focus HQ app (private repo `focus-hq`) serves
`/briefing.json` by proxying it straight from here, so a briefing goes live
seconds after it's pushed — no app rebuild.

| file | what it is |
|------|------------|
| `briefing.json` | today's bullets. The app reads exactly this. |
| `briefing-history.json` | every story ever shipped. Read before writing; append after. |

**Schedule: Sunday–Thursday, landing by 07:00 Israel time.** Fri/Sat: no file
written; the app quietly says *"Nothing to add today."* — correct, not a failure.

## Who this is for
Saar is building a **vertical SaaS / B2B platform for service businesses**, at the
intersection of **agentic infrastructure × sales tech × proptech/contech**. He also
does **US real estate wholesale**, and keeps a hand in Israeli tech for
**networking**. A bullet earns its place only if it changes what he builds, who he
calls, or what he buys.

## The four topics — in this order
| id | title | what counts |
|----|-------|-------------|
| `my-market` | **My market** | vertical SaaS for service businesses, sales tech, proptech/contech: funding, launches, M&A. His rivals, his buyers, whoever might acquire him. |
| `agents` | **Agents & AI infra** | agent frameworks, model + tooling releases, pricing shifts, agent-infra rounds. What he builds on — decides build-vs-buy. |
| `us-real-estate` | **US real estate** | **wholesale first** (below), then rates, inventory, distressed supply, investor rules. |
| `israel-tech` | **Israel tech** | rounds, exits, people moving. Networking fuel — a reason to reach out today. |

Four is the cap. A fifth topic means deleting one.

## Hard rules
1. **Max 3 bullets per topic — 3 is a CEILING, never a quota.** A quiet day ships
   1 bullet, or none. Filler is the failure mode. The app enforces the cap; only
   the writer can enforce the floor of *worth reading*.
2. **US real estate leads with wholesale.** Any real wholesaling news — a state
   law, a registration regime, an enforcement action, a shift in assignment rules
   — is bullet #1 that day. Only when there is genuinely nothing does the slot go
   to general US real estate.
3. **Every bullet has a real, working, public link.** No link → not a bullet. No
   paywalls where avoidable: a link he can't open is a dead bullet.
4. **Two lines on screen:** a headline that stands alone, plus a `note` that is
   the single fact that matters — a fragment, no full stop.
5. **News, not commentary.** Something *happened*. A trends essay is not news.
6. **Fresh only** — last ~24–48h (a few days is fine for a slow topic). The app
   hides any briefing whose `date` isn't today: stale news reads as fresh news.
7. **Primary sources** (the company, the regulator, the outlet that broke it) over
   aggregator reposts. The app displays the link's **real domain**, not the
   `source` you type — so a mislabelled link outs itself.
8. **≤24 web searches per run.** Enough for four topics plus a retry.

## Never repeat yourself
Read `briefing-history.json` before writing. Never reuse a url in it, and never
re-tell the same story from a different outlet. **Append every shipped url after
writing.** This is what keeps the TLDR worth opening — the app only hides bullets
he actively dismissed, so a story he scrolled past would come back forever if the
writer didn't own this. An ongoing saga is news again only when something *new*
happened; say what changed.

## Aiming it better
Every bullet he dismisses is scored **relevant / not**, and a rejection can carry a
one-line **`why`** in his words. He pastes that list in from the app
(Settings → News feedback). Treat every `why` as a standing instruction.

## Shape
```json
{
  "date": "YYYY-MM-DD",
  "topics": [
    {
      "id": "my-market",
      "title": "My market",
      "items": [
        {
          "id": "short-slug",
          "title": "The headline",
          "note": "the one fact that matters",
          "source": "Construction Dive",
          "url": "https://…"
        }
      ]
    }
  ]
}
```

## The morning job
1. Read this README and `briefing-history.json`.
2. Research the four topics (web search, ≤24 searches).
3. Write `briefing.json` with **today's** date.
4. Append every shipped url to `briefing-history.json`.
5. Check the JSON parses, then commit + push to `main`. The app picks it up live.

Nothing worth shipping in a topic? Ship it with an empty `items` array — the app
hides empty topics. **Never invent news to fill a card.**
