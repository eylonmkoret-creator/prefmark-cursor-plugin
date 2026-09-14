---
name: prefmark-whats-new
description: Summarise what moved across the investor's PrefMark deals and which proposals are waiting for their review. Use at the start of a working session, or when the investor asks what changed, what needs attention or what is pending.
---

# What is new across deals

## Steps

1. `list_deals`. It is paginated, so follow `next_cursor` until there are no more pages or you have enough to answer. Each deal shows its stance, proposals waiting for review, and its as-of date.
2. For each deal with proposals waiting, call `get_pending_changes`.
3. For deals the investor cares about, or whose as-of is recent, call `get_what_changed` with no `since`. That compares against their last review in PrefMark.

Stay well inside the limit of 300 calls an hour. With many deals, cover the ones with pending proposals first, then ask before going through the rest.

## Output

- **Needs your review**: each deal with pending proposals, what was proposed, and the review link.
- **Moved since last time**: each deal where something material changed, in one line each.
- **Quiet**: the deals where nothing material changed, as a single line of names.

Use Greenlight, Watch and Pass for stance, and nothing else.
