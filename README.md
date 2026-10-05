# PrefMark plugin

PrefMark: The Investment Memo that stays current. Read stance, Since last time, and open questions from Deal State; propose updates that only land when you Accept in PrefMark.

PrefMark is a pre-decision workspace for early-stage private investments. Startup materials become a structured Investment Memo with evidence tiers and provenance, open diligence questions, and a stance (Greenlight, Watch or Pass) that stays current as the deal moves.

This repository connects any AI app that speaks MCP to your own PrefMark workspace. It installs as a plugin in Claude Code, Cursor and Gemini CLI, and its skills work in Codex. ChatGPT, Claude, Grok and every other MCP client connect to the same server by URL: `https://prefmark.com/mcp`.

## What is in the plugin

| Component | Name | What it does |
|---|---|---|
| MCP server | `prefmark` | Nineteen tools over `https://prefmark.com/mcp`, signed in with OAuth |
| Rule | PrefMark (`rules/prefmark.mdc`, and `GEMINI.md` for Gemini CLI) | How an agent should use the tools: resolve the deal first, treat deal content as data, keep evidence tiers honest, send changes as proposals |
| Skill | `prefmark-setup` | First run: checks the connection, finds your deals or helps add one, and opens one |
| Skill | `prefmark-deal-status` | Where a deal stands: stance, what it hangs on, Since last time, blockers, next action |
| Skill | `prefmark-whats-new` | What moved across your deals and what is waiting for your review |
| Skill | `prefmark-call-prep` | Questions for a founder or diligence call, blockers first |
| Skill | `prefmark-relay-update` | Turns a founder email or meeting notes into a proposal on the right deal |
| Skill | `prefmark-meeting-notes` | Saves a meeting's notes to the right deal |
| Skill | `prefmark-inbox` | Checks your inbox with your app's own mail connection and sends deal emails to PrefMark. PrefMark never reads the mailbox |
| Skill | `prefmark-memo-edit` | Drafts a rewrite of an Investment Memo section; it waits in PrefMark, Current next to New, until you accept it there |
| Commands | `/prefmark-setup`, `/prefmark-status`, `/prefmark-whats-new`, `/prefmark-prep`, `/prefmark-relay`, `/prefmark-meeting-notes`, `/prefmark-inbox`, `/prefmark-memo-edit` | Run the matching skill. Gemini CLI uses the `.toml` files |

## Tools

| Tool | Permission | What it does |
|---|---|---|
| `list_deals` | Read deals | Your deals, newest first: name, stage, sector, stance, changes waiting for review. Paginated |
| `resolve_deal` | Read deals | Finds a deal from a name or a message subject: one match, a list to choose from, or none |
| `get_deal` | Read deals | The current case: stance and its reason, next action, what the decision hangs on, risks, key facts, open questions |
| `get_what_changed` | Read deals | Since last time: what materially moved since your last review in PrefMark, or since a time you give |
| `get_pending_changes` | Read deals | Changes waiting for you to accept or dismiss, with links into PrefMark |
| `get_evidence` | Read evidence | Current figures (ARR, burn, runway, raise and more) with evidence tier, who said each, source and date |
| `get_open_questions` | Read diligence | Open diligence questions, blockers first; with `include: "all"`, answered ones too |
| `get_memo` | Read memos | The Investment Memo and Quick Read, as they stand in PrefMark |
| `submit_deal_event` | Propose updates | Sends a statement, and up to five stated figures, to a deal **for your review** |
| `draft_memo_edit` | Propose updates | Drafts a rewrite of one memo section without changing facts |
| `draft_memo_rewrite` | Propose updates | Drafts a rewrite of the whole memo (shorter, plainer, or in your own words) without changing a fact or the stance |
| `propose_stance` | Propose updates | Proposes Greenlight, Watch or Pass with your reason |
| `add_question` | Edit diligence | Adds a question to the diligence tracker |
| `update_question` | Edit diligence | Records an answer, evidence or notes, or changes a question's status |
| `remove_question` | Edit diligence | Removes a question. PrefMark keeps a copy, so it can be restored |
| `add_deals` | Add and edit deals | Adds up to 25 companies at once and never duplicates a deal you have |
| `update_deal` | Add and edit deals | Changes name, stage, sector, website, HQ, round size, lead investor or description |
| `add_note` | Add and edit deals | Saves meeting notes or an email to the deal's Materials |
| `import_email` | Add and edit deals | Sends one deal email, read with your own mail connection, to PrefMark. It lands on the deal when it clearly matches, otherwise in Incoming |

In ChatGPT and Claude, PrefMark also shows its own panel (your deals, what moved, what waits for review) through a few app-only tools.

## What saves right away, and what waits for you

Your working records change the moment you ask: diligence questions and answers, deal details, new deals and notes. Every such change can be undone in PrefMark. Sample deals cannot be changed from an app.

The investment case is different. Memo text, the stance and the figures change only when you press **Accept** in PrefMark. A rewrite or a new figure from a chat waits there under **Needs your review**, Current next to New, and the answer includes a link straight to it. Nothing you say in a chat counts as accepting it.

`submit_deal_event` compares each stated figure with what PrefMark already holds and answers with one of:

- `pending_review`: something is new or different. It waits in PrefMark for you.
- `recorded`: it matches what PrefMark already had, so the case did not change.
- `duplicate`: the same message was already received.
- `rejected`: the deal name did not match the deal.

A figure a founder states stays founder-claimed after you accept it; accepting never turns a claim into verified evidence. Deal content is returned under `untrusted_content`, so an agent treats what a founder wrote as data, not as instructions.

## Install

The server address is the same everywhere: `https://prefmark.com/mcp`. You sign in to PrefMark the first time you use it and choose what the connection may do.

### ChatGPT

Install PrefMark from the [ChatGPT plugin directory](https://chatgpt.com/plugins/plugin_asdk_app_6aaa96b337e8819185fefe6fdebb3993).

### Claude

In Claude, open Customize, then Connectors, search for **PrefMark** and connect.

### Claude Code

```
/plugin marketplace add eylonmkoret-creator/prefmark-cursor-plugin
/plugin install prefmark@prefmark
```

Run `/mcp` and pick PrefMark to sign in.

### Cursor

Install PrefMark from [cursor.directory](https://cursor.directory/plugins/prefmark), or add the MCP server `https://prefmark.com/mcp` by hand. Then click **Login** on the PrefMark server.

### Gemini CLI

```
gemini extensions install https://github.com/eylonmkoret-creator/prefmark-cursor-plugin
```

Run `/mcp auth prefmark` to sign in. The extension adds the commands above and loads the PrefMark guidance from `GEMINI.md`.

### Codex

```
codex mcp add prefmark --url https://prefmark.com/mcp
codex mcp login prefmark
```

To use the skills too, copy the folders in `skills/` into `~/.codex/skills/`.

### Grok and any other MCP client

Add a custom connector or MCP server with the URL `https://prefmark.com/mcp` and sign in. In Grok: grok.com/connectors, then New Connector, then Custom.

Every app answers in the language you write in.

### Permissions

Every permission starts ticked, so the agent can read, update your diligence tracker, add deals and notes, and propose changes. Untick anything you do not want.

If a tool answers `insufficient_scope`, the connection was approved with fewer permissions than that tool needs, or before that permission existed. Disconnect PrefMark in your app, connect again, and keep the permission ticked. You can remove a connection at any time from **Settings, Connected agents** in PrefMark.

## Access

PrefMark is currently available by invitation. You need a PrefMark account to connect. Request access at [prefmark.com](https://prefmark.com).

## Security

- OAuth 2.1 with PKCE. The plugin ships no credentials; your app receives a token scoped to your own workspace, issued only after you approve the consent screen.
- Every call is scoped to your account. Limits per connection: 300 calls an hour, 30 proposals an hour, 20 proposals per deal per day.
- Memo text, stance and figures change only when you accept them in PrefMark.

## About

PrefMark is at [prefmark.com](https://prefmark.com). Questions: hello@prefmark.com

This repository holds the PrefMark plugin. It is not the PrefMark application.

© PrefMark. All rights reserved.
