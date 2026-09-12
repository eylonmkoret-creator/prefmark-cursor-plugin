# PrefMark for Cursor

The Investment Memo that stays current — available to your agents.

PrefMark turns messy startup materials into a structured investment review: extraction with evidence tiers and provenance, risks and missing information, diligence questions, and an Investment Memo that stays current as the deal moves. This plugin connects Cursor to your own PrefMark workspace over MCP.

## What your agent can do

Once connected, an agent can read:

- **Deals** — names, current stance (Greenlight / Watch / Pass), and where each one stands
- **Evidence** — extracted facts with their tier and provenance
- **Diligence** — the open questions on a deal, and which are answered
- **Reports** — the Investment Memo and Deal Brief
- **What changed** — the material delta since you last opened a deal
- **Your Lens** — your own mandate preferences, if you have set them up

Agents may also **propose** an update to a deal. They cannot change it. A proposal shows up in PrefMark for you to accept or dismiss, and nothing enters the record until you do.

## Install

Install **PrefMark** from the Cursor marketplace, then click **Login** on the PrefMark server. You will sign in to PrefMark and approve the connection. You can disconnect at any time from **Settings → Connected agents** in PrefMark.

The server is `https://prefmark.com/mcp`.

## Access

PrefMark is currently available by invitation. You need a PrefMark account to connect — request access at [prefmark.com](https://prefmark.com).

## Security

Connection uses OAuth 2.1 with PKCE. The plugin ships no credentials: your agent receives a token scoped to your own workspace, issued only after you approve the consent screen, and every tool call is scoped to your account. Access is read-only apart from proposals, which require your approval in PrefMark before they take effect.

## About

PrefMark is at [prefmark.com](https://prefmark.com). Questions: hello@prefmark.com

This repository contains only the Cursor plugin manifest. It is not the PrefMark application.

© PrefMark. All rights reserved.
