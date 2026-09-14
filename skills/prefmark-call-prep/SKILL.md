---
name: prefmark-call-prep
description: Prepare for a founder or diligence call on a PrefMark deal, using its open questions with blockers first, the figures that are still founder-claimed or missing, and what the decision hangs on. Use when the investor has a call or meeting coming up with a company.
---

# Prepare for a call

## Steps

1. `resolve_deal`, then `get_deal` for the stance and what the decision hangs on.
2. `get_open_questions`. It returns blockers first, then the rest, each with an id.
3. `get_evidence`. Note every figure that is founder-claimed or missing, since those are what the call can firm up.
4. `get_what_changed`, so the investor does not re-ask something already answered since their last review.

## Output

- **What the decision hangs on**, in a line or two.
- **Ask first**: the blocking questions, worded as PrefMark's tracker has them.
- **Then**: the remaining open questions, most material first.
- **Figures to confirm**: founder-claimed or missing numbers, each with what PrefMark currently holds and its tier.
- **Your suggestions**: any extra question you think is worth asking goes here, clearly marked as your suggestion. It is not in PrefMark's tracker, so never present it as though it were.

After the call, offer to relay what the founder said with the prefmark-relay-update skill.
