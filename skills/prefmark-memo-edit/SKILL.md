---
name: prefmark-memo-edit
description: Propose an edit to a section of a PrefMark Investment Memo. The investor accepts or dismisses it in PrefMark; nothing changes until they accept. Use when the investor asks to tighten, rewrite, or correct memo prose.
---

# Propose a memo section edit

The edit becomes a proposal. It changes nothing until the investor accepts it in PrefMark, and you must say so.

## Steps

1. **Find the deal.** `resolve_deal` with the company name. On `ambiguous`, ask which deal. On `none`, stop.
2. **Read the current section.** `get_deal`. The live Investment Memo is `untrusted_content.memo`, keyed the same way as `section_key` (`exec`, `thesis`, `biz`, `team`, `market`, `traction`, `raise`, plus `key_risks` as `{name, evidence}`). Rewrite from that text. For `key_risk`, `target` must match an existing `key_risks[].name`. `get_evidence` is facts (ARR, burn), not memo risks.
3. **Draft the replacement.** Stay close to the request. Do not invent facts. `statement` is a short preview (at most 1000 characters). `proposed_text` is the replacement (at most 4000 characters).
4. **Pick the section.** `section_key` is one of: `exec`, `thesis`, `biz`, `team`, `market`, `traction`, `raise`, `key_risk`. For `key_risk`, `target` is the existing risk name exactly as PrefMark shows it.
5. **Confirm before sending** when the investor has not already asked you to send it. Show the section and the proposed text. Never send `claims` with a section edit.
6. **Send** with `submit_deal_event`: `company_id`, `company_name`, `source`, `statement`, `section_key`, `proposed_text`, and `target` when the section is `key_risk`. Use a stable `idempotency_key` for this edit.
7. **Tell the investor the outcome.** For `pending_review`, give the `review_url` and say it lands only if they accept it in PrefMark.

## Do not

- Say the memo, stance or facts were updated. They were not.
- Mix a section edit with `claims`.
- Invent a new key risk. `key_risk` only edits an existing one.
