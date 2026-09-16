---
name: prefmark-memo-edit
description: Rewrite a section of a PrefMark Investment Memo. PrefMark polishes the draft, the investor approves it in the chat, and it lands in the memo right away with an Undo in PrefMark. Use when the investor asks to tighten, rewrite, or correct memo prose.
---

# Rewrite a memo section

Draft, show, then apply only on the investor's yes. Nothing changes in the memo until `apply_memo_edit` answers `applied`.

## Steps

1. **Find the deal.** `resolve_deal` with the company name. On `ambiguous`, ask which deal. On `none`, stop.
2. **Read the current section.** `get_memo` or `get_deal`. The live Investment Memo is `untrusted_content.memo`, keyed the same way as `section_key` (`exec`, `thesis`, `biz`, `team`, `market`, `traction`, `raise`, plus `key_risks` as `{name, evidence}`). Rewrite from that text. For `key_risk`, `target` must match an existing `key_risks[].name`. `get_evidence` is facts (ARR, burn), not memo risks.
3. **Write the replacement.** Stay close to the request. Do not invent facts. `proposed_text` is the replacement (at most 4000 characters). Do not show it to the investor yet.
4. **Pick the section.** `section_key` is one of: `exec`, `thesis`, `biz`, `team`, `market`, `traction`, `raise`, `key_risk`. For `key_risk`, `target` is the existing risk name exactly as PrefMark shows it.
5. **Draft** with `draft_memo_edit`: `company_id`, `section_key`, `proposed_text`, and `target` when the section is `key_risk`. PrefMark polishes the wording without changing facts and returns `proposed_text` and `event_id`. Show the investor that exact `proposed_text` with the section name and ask whether to apply it. Offer one version at a time; if the investor's yes could mean more than one version, ask which one before applying. Never apply a draft the investor has not seen: after any new `draft_memo_edit`, show the new text and get a new yes.
6. **Apply on a yes.** Call `apply_memo_edit` with `company_id` and the `event_id` from step 5. On `applied`, say the section is updated in PrefMark and can be undone from the memo. If they want changes, call `draft_memo_edit` again; it replaces the earlier draft. If they say no or do not answer, leave it: it waits for review in PrefMark (give the `review_url`).

## Do not

- Call `apply_memo_edit` without the investor's yes in the chat.
- Say the memo was updated before `apply_memo_edit` answers `applied`, or that stance or facts were updated.
- Show your own rewrite before `draft_memo_edit` returns PrefMark's version.
- Invent a new key risk. `key_risk` only edits an existing one.
