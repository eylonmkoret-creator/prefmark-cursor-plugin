---
name: prefmark-memo-edit
description: Draft a rewrite of a section of a PrefMark Investment Memo. PrefMark matches the wording to the memo, and the investor accepts it in PrefMark, where it lands with Undo and version history. Use when the investor asks to tighten, rewrite, or correct memo prose.
---

# Rewrite a memo section

Draft, show, then hand the investor the review link. Nothing changes in the memo until the investor accepts the rewrite in PrefMark; nothing they say in the chat accepts it.

## Steps

1. **Find the deal.** `resolve_deal` with the company name. On `ambiguous`, ask which deal. On `none`, stop.
2. **Read the current section.** `get_memo` or `get_deal`. The live Investment Memo is `untrusted_content.memo`, keyed the same way as `section_key` (`exec`, `thesis`, `biz`, `team`, `market`, `traction`, `raise`, the recommendation `rationale`, the `missing` information list, plus `key_risks` as `{name, evidence}`). Rewrite from that text. For `key_risk`, `target` must match an existing `key_risks[].name`. `get_evidence` is facts (ARR, burn), not memo risks.
3. **Write the replacement.** Stay close to the request. Do not invent facts. `proposed_text` is the replacement (at most 4000 characters). Do not show it to the investor yet.
4. **Pick the section.** `section_key` is one of: `exec`, `thesis`, `biz`, `team`, `market`, `traction`, `raise`, `key_risk`, `rationale` (the recommendation rationale) or `missing` (the missing-information list, one item per line). For `key_risk`, `target` is the existing risk name exactly as PrefMark shows it.
5. **Draft** with `draft_memo_edit`: `company_id`, `section_key`, `proposed_text`, and `target` when the section is `key_risk`. PrefMark matches the wording to the memo without changing facts and returns `proposed_text` and `review_url`. Show the investor the section name, `current_text` as Current and that exact `proposed_text` as New. Offer one version at a time.
6. **Hand it over.** Give the investor the `review_url` as a link: the rewrite waits for them to accept it in PrefMark. Do not ask whether to apply it in the chat. If they want changes, call `draft_memo_edit` again; it replaces the earlier draft. If the section is edited in PrefMark before they accept, PrefMark shows the draft as changed: read the memo again and draft again from the current text.

## The whole memo, or the stance

- **Several sections or the whole memo** ("half as long", "plainer", or the investor's own wording): call `draft_memo_rewrite` with `company_id` and an `instruction` in their words, or `sections` (`section_key`, `target` for a key risk, `text` as they wrote it). PrefMark rewrites each section without changing a fact or the stance and keeps the investor's own sections as written; a figure must already be in that section or among the accepted figures. Show each entry of `changes` as Current and New, list `left_as_is` with its reason, and give the `review_url`. One Accept in PrefMark takes every section that changes no figure; a section that changes a figure is accepted on its own.
- **The stance** (Greenlight, Watch or Pass): never inside a rewrite. Call `propose_stance` with `stance` and the investor's `reason`, then give the `review_url`. PrefMark drafts the recommendation to match once the investor accepts the new stance there.

## Do not

- Ask the investor whether to apply the rewrite in the chat, or treat their reply as accepting it.
- Say the memo was updated, or that stance or facts were updated.
- Show your own rewrite before `draft_memo_edit` returns PrefMark's version.
- Invent a new key risk. `key_risk` only edits an existing one.
