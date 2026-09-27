---
name: prefmark-relay-update
description: Turn a founder email, meeting notes or a call summary into a proposed update on the right PrefMark deal, which the investor then accepts or dismisses in PrefMark. Use when the investor shares new information about a company and wants PrefMark to have it.
---

# Relay an update to PrefMark

The update becomes a proposal. It changes nothing until the investor accepts it in PrefMark, and you must say so.

## Steps

1. **Find the deal.** `resolve_deal` with the company name or the message subject. On `ambiguous`, ask the investor which deal. On `none`, tell them the deal is not in PrefMark and offer to add it with `add_deals`. Continue only after they confirm, then resolve the new deal.
2. **Read what PrefMark already has.** `get_evidence` for the deal, so you can tell the investor what is new, what matches and what disagrees.
3. **Pick out what was actually said.**
   - `statement`: the substance, as close to verbatim as you have it, at most 1000 characters.
   - `claims`: only figures that were stated outright, at most five, using the fact keys in the PrefMark rule. Write each value as stated. Never compute, convert or infer one.
   - `source`: `founder` if the company said it, `user` if it is the investor's own note, `third_party` for anyone else.
   - `occurred_at`: when it was said, if the material shows it.
   - `idempotency_key`: stable for this message, for example `gmail:<message-id>` or `meeting:<meeting-id>`.
4. **Confirm before sending** when the investor has not already asked you to send it. Show the statement and the claims.
5. **Send** with `submit_deal_event`, using the deal's `company_id` and its `company_name` exactly as PrefMark shows it.
6. **Tell the investor the outcome**, using the result statuses in the PrefMark rule. For `pending_review`, give the `review_url` and say it lands only if they accept it. For each claim, say whether PrefMark found that it supports, contradicts, is new, or cannot be checked.

## A whole email from the investor's mailbox

When the investor asks to send a deal email itself to PrefMark ("send the latest email from the Acme founder to PrefMark"), read it with your own mail tool and call `import_email` with its fields (the Message-ID header as `rfc_message_id` when shown, your tool's own id as `message_id`) and its text exactly as written, instead of summarising it into `submit_deal_event`. PrefMark files it like a forwarded email: on the deal when it clearly matches, otherwise in Incoming. Only deal email the investor asked for; ask before sending more than five.

## Do not

- Split one message into many proposals to get around limits.
- Send guesses, estimates or figures you worked out yourself as claims.
- Say the memo or stance changed.
