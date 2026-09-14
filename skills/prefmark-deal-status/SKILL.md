---
name: prefmark-deal-status
description: Show where a PrefMark deal stands, including its stance, what the decision hangs on, what changed since the investor last looked, open blockers and the next action. Use when the investor asks about a company, a deal or where things stand.
---

# Where a deal stands

## Steps

1. `resolve_deal` with the company name. Follow the PrefMark rule for exact, ambiguous and none, and never guess between candidates.
2. `get_deal` with the deal id. It returns stance, the reason for it, the next action, what the decision hangs on, active risks, key facts, the open question count and proposals waiting for review.
3. `get_what_changed` with the deal id and no `since`. That compares against the investor's last review in PrefMark. Pass `since` (ISO-8601) only when the investor names a time.
4. If there are blockers or the investor asks about diligence, `get_open_questions`.
5. If the investor asks about a number, `get_evidence`, and keep each figure's tier next to it.

## Answer shape

- **Stance** in one line: Greenlight, Watch or Pass, and the reason PrefMark gives.
- **Hangs on**: what the decision depends on.
- **Since last time**: what moved. If nothing material changed, say exactly that.
- **Open**: blockers first, then the count of other open questions.
- **Next action**.
- **Waiting for review**: any pending proposals, with their review links.

Keep founder-claimed figures labelled as the company's own. Never present them as fact.
