---
name: prefmark-meeting-notes
description: After a meeting about a deal (a founder call, a customer reference, a partner meeting), save the notes to that deal in PrefMark. Use when the investor asks to send meeting notes or a call summary to PrefMark, or when a scheduled task or automation asks for it after a meeting.
---

# Send meeting notes to PrefMark

This chat's own meeting notes (Fireflies or Circleback, or notes the investor pastes) are the source. PrefMark receives only the note you send with `add_note`. Granola notes reach PrefMark on their own through Settings, Integrations, so do not send them again (on a Grok Bot, Granola is not a plugin on this bot).

## Steps

1. **Find the deal.** Call `resolve_deal` with the company name from the meeting title or the notes. If it answers ambiguous or none, ask the investor which deal, and stop until they say.
2. **Write the note from the meeting's own summary**, in the meeting's language:
   - who was in the meeting, by name and role, only as the notes name them;
   - what was said about the business: figures, customers, the round, the team, risks, answers to open questions;
   - the action items, with who owns each.

   Keep figures exactly as stated and say who stated them ("the CEO said ARR is $1.2M"). Do not add anything the meeting did not say, and do not include the full transcript unless the investor asks for it.
3. **Pick the source**: `founder` for a call with the company, `customer` for a customer reference, `partner` for your own partners, `expert` for an expert call, else `other`.
4. **Send it** with `add_note`: `company_id`, a short `title` such as "Call with the CEO, Sep 30", the note as `text`, and the `source`.
5. **Report in two lines:** which deal it went to, and that PrefMark reads the note. Any change it suggests to the memo, a figure or the stance waits in PrefMark as Needs review. Give the Accept in PrefMark link when one is returned.

## Do not

- Save notes from a meeting that is not about an investment, or personal, medical or legal content.
- Guess the deal when the name is unclear.
- Say that the memo, the stance or a figure changed.
