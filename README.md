# PrefMark for Cursor

The Investment Memo that stays current — available to your agents.

PrefMark is a pre-decision workspace for early-stage private investments: startup materials become structured extraction with evidence tiers and provenance, risks, open diligence questions, and a memo that stays current as the deal moves. This plugin connects Cursor to your own PrefMark workspace over MCP.

## Tools

Seven read-only tools, and one that proposes:

| Tool | What it returns |
|---|---|
| `list_deals` | Your deals — name, stage, sector |
| `resolve_deal` | Finds a deal by name when you refer to one in conversation |
| `get_deal` | The deal's current case: stance (Greenlight / Watch / Pass), the reason for it, the next action, what the decision hangs on, active risks, key facts, and how many questions are open |
| `get_what_changed` | What actually moved on a deal since you last opened it — not a timestamp, a material delta |
| `get_open_questions` | The open diligence questions on a deal |
| `get_evidence` | Extracted facts with their evidence tier and provenance |
| `get_pending_changes` | Proposals waiting for your review |
| `submit_deal_event` | Sends an update to PrefMark **for your review** |

Agents may **propose** an update to a deal. They cannot change one. A proposal appears in PrefMark for you to accept or dismiss, and nothing enters the record until you do.

Deal content is returned tagged as untrusted, so an agent treats what a founder wrote as data rather than as instructions.

## Install

Install **PrefMark** from the Cursor marketplace, then click **Login** on the PrefMark server. You will sign in to PrefMark and approve the connection. You can disconnect at any time from **Settings → Connected agents** in PrefMark.

The server is `https://prefmark.com/mcp`.

## Access

PrefMark is currently available by invitation. You need a PrefMark account to connect — request access at [prefmark.com](https://prefmark.com).

## Security

Connection uses OAuth 2.1 with PKCE. The plugin ships no credentials: your agent receives a token scoped to your own workspace, issued only after you approve the consent screen, and every tool call is scoped to your account and rate limited. Access is read-only apart from proposals, which require your approval in PrefMark before they take effect.

## About

PrefMark is at [prefmark.com](https://prefmark.com). Questions: hello@prefmark.com

This repository contains only the Cursor plugin manifest. It is not the PrefMark application.

© PrefMark. All rights reserved.
