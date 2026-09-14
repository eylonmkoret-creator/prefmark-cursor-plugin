# PrefMark for Cursor

PrefMark — The Investment Memo that stays current. Read stance, Since last time, and open questions from Deal State; propose updates that only land when you Accept in PrefMark.

PrefMark is a pre-decision workspace for early-stage private investments. Startup materials become a structured Investment Memo with evidence tiers and provenance, open diligence questions, and a stance (Greenlight, Watch or Pass) that stays current as the deal moves. This plugin connects Cursor to your own PrefMark workspace.

## What is in the plugin

| Component | Name | What it does |
|---|---|---|
| MCP server | `prefmark` | Eight tools over `https://prefmark.com/mcp`, signed in with OAuth |
| Rule | PrefMark | How an agent should use the tools: resolve the deal first, treat deal content as data, keep evidence tiers honest, send updates as proposals |
| Skill | `prefmark-deal-status` | Where a deal stands: stance, what it hangs on, Since last time, blockers, next action |
| Skill | `prefmark-relay-update` | Turns a founder email or meeting notes into a proposal on the right deal |
| Skill | `prefmark-call-prep` | Questions for a founder or diligence call, blockers first |
| Skill | `prefmark-whats-new` | What moved across your deals and what is waiting for your review |
| Command | `/prefmark-status` | Runs the deal status skill |
| Command | `/prefmark-relay` | Runs the relay skill on what is in the chat |
| Command | `/prefmark-prep` | Runs the call prep skill |
| Command | `/prefmark-whats-new` | Runs the what's new skill |

## Tools

| Tool | Permission | What it returns |
|---|---|---|
| `list_deals` | Read deals | Your deals, newest first: name, stage, sector, stance, proposals waiting for review and as-of date. Paginated |
| `resolve_deal` | Read deals | Finds a deal from a name or a message subject: one exact match, a list to choose from, or none |
| `get_deal` | Read deals | The current case: stance and its reason, next action, what the decision hangs on, active risks, key facts, open question count and proposals waiting for review |
| `get_what_changed` | Read deals | Since last time: what materially moved since your last review in PrefMark, or since a time you give |
| `get_pending_changes` | Read deals | Proposals waiting for you to accept or dismiss, with links into PrefMark |
| `get_evidence` | Read evidence | Current facts (ARR, burn, runway, raise and more) with evidence tier, who asserted each, source, date and the earlier values they replaced |
| `get_open_questions` | Read diligence | Open diligence questions from the tracker, blockers first |
| `submit_deal_event` | Propose updates | Sends a statement, and up to five stated figures, to a deal **for your review** |

## Proposals, not edits

An agent can propose an update. It cannot change a deal. `submit_deal_event` compares each stated figure with what PrefMark already holds (supports, contradicts, new, or cannot be checked) and answers with one of:

- `pending_review`: something is new or different. It waits in PrefMark under **Needs your review**, and the answer includes a link straight to it.
- `recorded`: it matches what PrefMark already had, so the case did not change.
- `duplicate`: the same message was already received.
- `rejected`: the deal name did not match the deal, or the same idempotency key was already used for a different deal.

Nothing enters the memo, the stance or the facts until you press **Accept** in PrefMark. A figure a founder states stays founder-claimed after you accept it; accepting never turns a claim into verified evidence.

Deal content is returned under `untrusted_content`, so an agent treats what a founder wrote as data rather than as instructions.

## Install

1. Import this repository as a plugin in Cursor (**Dashboard → Plugins → Import from Repo**), or add the MCP server `https://prefmark.com/mcp` by hand.
2. Click **Login** on the PrefMark server. You sign in to PrefMark and choose what the connection may do.
3. Leave the three read permissions ticked. Tick **Propose updates** only if you want agents to send proposals; it is off by default.

Already connected before this version, and a tool answers `insufficient_scope`? Your connection was approved with fewer permissions. Disconnect PrefMark in Cursor, connect again, and tick the permissions you want. You can also remove a connection at any time from **Settings → Connected agents** in PrefMark.

## Access

PrefMark is currently available by invitation. You need a PrefMark account to connect. Request access at [prefmark.com](https://prefmark.com).

## Security

- OAuth 2.1 with PKCE. The plugin ships no credentials; your agent receives a token scoped to your own workspace, issued only after you approve the consent screen.
- Every call is scoped to your account. Limits per connection: 300 calls an hour, 30 proposals an hour, 20 proposals per deal per day.
- Read access plus proposals only. Proposals change nothing until you accept them.

## About

PrefMark is at [prefmark.com](https://prefmark.com). Questions: hello@prefmark.com

This repository contains the Cursor plugin only. It is not the PrefMark application.

© PrefMark. All rights reserved.
