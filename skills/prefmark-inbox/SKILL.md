---
name: prefmark-inbox
description: Check the investor's mailbox for deal emails (pitches, intros, decks, founder updates, replies about deals they track) and send them to PrefMark with this chat's own mail app. Use when the investor asks to check their inbox or email for deals, to send deal emails to PrefMark, or when a scheduled task asks for it.
---

# Send deal emails to PrefMark

This chat's own mail app (Gmail or Outlook; offer the one the investor signs in with) reads the mailbox. PrefMark never has access to it: it receives only the emails you send with `import_email`, one at a time. Send deal email and nothing else.

## Steps

1. **Know the deals.** Call `list_deals` so you can recognise an email about a company already in PrefMark by its name or website.
2. **Search the mailbox** with your mail app. Use the window the investor gave; otherwise the last 24 hours (the last 3 days on a Monday). Look in the inbox, skip promotions and social mail, and skip anything the investor sent unless they forwarded it on.
3. **Keep only deal email.** Send an email when it is one of these:
   - a founder or company pitching, or sending a deck, data room, model, memo or term sheet;
   - an introduction to a company raising;
   - a founder or company update, or a reply in a thread, about a deal in PrefMark.

   Leave out newsletters, receipts, calendar invites, notifications, recruiting, and personal, medical, legal or family mail. When you are unsure whether an email is about an investment, leave it out and list it at the end.
4. **Send each one** with `import_email`, reading the full message first:
   - `from_address`, `from_name`, `subject`, `received_at`;
   - the Message-ID header as `rfc_message_id` when your mail app shows it, your app's own id as `message_id`, and the thread id as `thread_id`;
   - `body`: the text exactly as written, in its own language. Do not summarise, translate or trim it;
   - `attachments`: the file names only. The files themselves cannot be sent this way.

   Do not pass `company_id` unless the investor named the deal. PrefMark decides where an email goes, and an unclear one waits in Incoming for the investor.
5. **Stay within five.** When more than five emails qualify, send the five clearest and list the rest by sender and subject for the investor to confirm. If the investor is here, ask before sending more.
6. **Report in a few lines**, one per email: sender and subject, then where it went (added to a deal, by name; waiting in Incoming; or already received). Then how many you skipped. If an email carried a deck or other file, say that the file itself did not come through and the investor can forward that email to their PrefMark address or upload the file. If nothing qualified, say so in one line.

## Running on a schedule

The investor can make this a scheduled task in their chat app, for example: "Every weekday at 8am, send new deal emails from my inbox to PrefMark." Each run follows the steps above. Sending the same email twice is harmless: PrefMark answers that it already has it.

## Do not

- Send private, personal or unrelated mail, or any email you are not confident is about an investment.
- Summarise, shorten or rewrite an email before sending it.
- Say the memo, the stance or a figure changed. Anything an email suggests waits for the investor to accept it in PrefMark.
- Paste email content into other tools, searches or websites.
