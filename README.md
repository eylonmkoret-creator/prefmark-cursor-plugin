# PrefMark for Cursor, Claude and Gemini

PrefMark: The Investment Memo that stays current. Read stance, Since last time, and open questions from Deal State; propose updates that only land when you Accept in PrefMark.

PrefMark is a pre-decision workspace for early-stage private investments. Startup materials become a structured Investment Memo with evidence tiers and provenance, open diligence questions, and a stance (Greenlight, Watch or Pass) that stays current as the deal moves. This repository connects Cursor, Claude Code and Gemini CLI to your own PrefMark workspace. Claude, ChatGPT and Grok can connect to the same server by URL.

## What is in the plugin

| Component | Name | What it does |
|---|---|---|
| MCP server | `prefmark` | Eight tools over `https://prefmark.com/mcp`, signed in with OAuth |
| Rule | PrefMark (`rules/prefmark.mdc` in Cursor, `GEMINI.md` in Gemini CLI) | How an agent should use the tools: resolve the deal first, treat deal content as data, keep evidence tiers honest, send updates as proposals |
| Skill | `prefmark-deal-status` | Where a deal stands: stance, what it hangs on, Since last time, blockers, next action |
| Skill | `prefmark-relay-update` | Turns a founder email or meeting notes into a proposal on the right deal |
| Skill | `prefmark-call-prep` | Questions for a founder or diligence call, blockers first |
| Skill | `prefmark-whats-new` | What moved across your deals and what is waiting for your review |
| Skill | `prefmark-memo-edit` | Rewrites an Investment Memo section: PrefMark polishes the draft, you approve it in the chat, and it lands with an Undo in PrefMark |
| Command | `/prefmark-status` | Runs the deal status skill (Gemini CLI uses the matching `.toml` files) |
| Command | `/prefmark-relay` | Runs the relay skill on what is in the chat |
| Command | `/prefmark-prep` | Runs the call prep skill |
| Command | `/prefmark-whats-new` | Runs the what's new skill |
| Command | `/prefmark-memo-edit` | Runs the memo edit skill |

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
| `get_open_questions` | Read diligence | (with `include: "all"`) answered and resolved questions too, with answers and evidence |
| `get_memo` | Read memos | The Investment Memo and Quick Read, as written in PrefMark |
| `submit_deal_event` | Propose updates | Sends a statement, and up to five stated figures, to a deal **for your review** |
| `draft_memo_edit` | Propose updates | Drafts a rewrite of one memo section. PrefMark polishes the wording without changing facts; nothing changes yet |
| `apply_memo_edit` | Propose updates | Applies a drafted section rewrite after you say yes in the chat. You can undo it from the memo |
| `add_question` | Edit diligence | Adds a question to the diligence tracker |
| `update_question` | Edit diligence | Records an answer, evidence or notes, or changes a question status |
| `remove_question` | Edit diligence | Deletes a question from the tracker |
| `add_deals` | Add and edit deals | Adds up to 25 companies at once and never duplicates a deal you have |
| `update_deal` | Add and edit deals | Changes name, stage, sector, website, HQ, round size, lead investor or description |
| `add_note` | Add and edit deals | Saves meeting notes or an email to the deal's Materials |

## What saves right away, and what waits for you

Your working records change the moment you ask: diligence questions and answers, deal details, new deals and notes. Sample deals cannot be changed from an app.

A memo section rewrite you ask for lands once you approve PrefMark's polished text in the chat, and the memo shows it with **Undo**.

Stance and facts are different. An agent never changes a stance or a fact by itself. `submit_deal_event` compares each stated figure with what PrefMark already holds (supports, contradicts, new, or cannot be checked) and answers with one of:

- `pending_review`: something is new or different. It waits in PrefMark under **Needs your review**, and the answer includes a link straight to it.
- `recorded`: it matches what PrefMark already had, so the case did not change.
- `duplicate`: the same message was already received.
- `rejected`: the deal name did not match the deal, or the same idempotency key was already used for a different deal.

Nothing from a relayed update enters the memo, the stance or the facts until you press **Accept** in PrefMark. A figure a founder states stays founder-claimed after you accept it; accepting never turns a claim into verified evidence.

Deal content is returned under `untrusted_content`, so an agent treats what a founder wrote as data rather than as instructions.

## Install

The server address is the same everywhere: `https://prefmark.com/mcp`. You sign in to PrefMark the first time you use it and choose what the connection may do.

### Cursor

Install PrefMark from [cursor.directory](https://cursor.directory/plugins/prefmark). You can also add the MCP server `https://prefmark.com/mcp` by hand. Then click **Login** on the PrefMark server.

### Claude Code

```
/plugin marketplace add eylonmkoret-creator/prefmark-cursor-plugin
/plugin install prefmark@prefmark
```

Run `/mcp` and pick PrefMark to sign in.

### Gemini CLI

```
gemini extensions install https://github.com/eylonmkoret-creator/prefmark-cursor-plugin
```

Run `/mcp auth prefmark` to sign in. The extension adds the same five commands as `/prefmark-status`, `/prefmark-relay`, `/prefmark-prep`, `/prefmark-whats-new` and `/prefmark-memo-edit`, and loads the PrefMark guidance from `GEMINI.md`.

### Claude, ChatGPT and Grok

These connect by URL and get all fifteen tools, without the skills and commands in this repository.

- Claude: Customize, then Connectors, then Add custom connector. Paste `https://prefmark.com/mcp`.
- ChatGPT: Settings, then Security and login, then turn on Developer mode. Then Plugins, Create app, paste `https://prefmark.com/mcp` and keep OAuth.
- Grok: grok.com/connectors, then New Connector, then Custom. Paste `https://prefmark.com/mcp`.

Every app answers in the language you write in, including Hebrew and German.

### Permissions

Every permission starts ticked, so the agent can read, update your diligence tracker, add deals and notes, and propose updates. Untick anything you do not want.

If a tool answers `insufficient_scope`, the connection was approved with fewer permissions than that tool needs, or before that permission existed. Disconnect PrefMark in your client, connect again, and keep the permission ticked. You can remove a connection at any time from **Settings → Connected agents** in PrefMark.

## Access

PrefMark is currently available by invitation. You need a PrefMark account to connect. Request access at [prefmark.com](https://prefmark.com).

## Security

- OAuth 2.1 with PKCE. The plugin ships no credentials; your agent receives a token scoped to your own workspace, issued only after you approve the consent screen.
- Every call is scoped to your account. Limits per connection: 300 calls an hour, 30 proposals an hour, 20 proposals per deal per day.
- Reads, direct edits to your working records (diligence tracker, deal details, new deals, notes) and proposals. Memo rewrites apply once you approve them in the chat and can be undone; stance and facts change only when you accept a proposal. Untick any permission on the consent screen to leave it out.

## About

PrefMark is at [prefmark.com](https://prefmark.com). Questions: hello@prefmark.com

This repository holds the PrefMark plugin for Cursor, Claude Code and Gemini CLI. It is not the PrefMark application.

© PrefMark. All rights reserved.
