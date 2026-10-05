---
name: prefmark-setup
description: First run after PrefMark is installed or connected. Confirms the connection, finds the investor's deals (or helps them add a first one), opens one deal, and explains in one line how PrefMark works with this chat. Use right after install, or when the investor asks how to start with PrefMark.
---

# Set up PrefMark

Goal: by the end of this conversation the investor has one deal open and knows the loop. Keep it short and friendly: two or three short messages, no lists of features.

## Steps

1. **Check the connection.** Call `list_deals`. If the call fails because PrefMark is not connected or the sign-in expired, say so in one sentence and stop.
2. **If there are deals:** name the most recent two or three (name and stance only). Open the newest one with `prefmark_deal` when that tool is available, otherwise read it with `get_deal` and give its stance and why in two sentences. Then ask which deal they want to look at next.
3. **If there are no deals yet**, offer three ways to add one, in this order:
   - upload a deck at prefmark.com (the fastest);
   - send one deal email to PrefMark from this chat, when this chat has Gmail or Outlook connected (offer the one they sign in with): find the email with that app and send it with `import_email` (one email, only after the investor picks it; pass the Message-ID header as `rfc_message_id`);
   - forward a deal email to their PrefMark address (`prefmark_forwarding_address` gives it, when available).

   Also mention that PrefMark has a sample investment to try (Review a sample investment, on the Deals page).
4. **Explain the loop in one line**, in these words or close to them: "Ask about any deal here. Suggested changes wait in PrefMark as Needs review, and you accept them there: I will give you the Accept in PrefMark link."

## Do not

- List every tool or feature.
- Say that anything changed in PrefMark. This setup reads only, apart from an email the investor chose to send.
- Invent a deal, a figure or a person the materials do not name.
