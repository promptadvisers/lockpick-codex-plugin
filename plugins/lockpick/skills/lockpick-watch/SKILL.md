---
name: lockpick-watch
description: Use when the user asks what changed between Lockpick scans, whether a deployed fix is still observed, or how to recheck a site.
---

# Compare and recheck

Resolve the site with lockpick_list_sites and its scans with lockpick_list_scans. Compare only compatible scans of the same origin and assessment level.

Use lockpick_compare_scans for a scan that has a baseline. Report each earlier finding as fixed, still vulnerable or inconclusive (the `outcome` of each change), and new findings as new, without converting inconclusive into fixed.

## Triage

- **New, high severity:** lead with these. Say what changed, which URL or record, and who fixes it. Offer `lockpick-fix` or `lockpick-dns`.
- **Regressions:** a finding that was fixed in an earlier run and is back. Call these out by name, since they usually mean a deploy or DNS change undid a fix.
- **Fixed:** confirm briefly. It is good news worth one line.
- **Still vulnerable:** list with how long each has been open.
- **Inconclusive:** say plainly that these could not be checked this time. Inconclusive is never fixed.

## Recheck

Start only the check the user asked for.

- **Full recheck.** If the user asks for a new scan after a deployment, read lockpick_get_allowance and explain the cost before starting it. A full recheck counts as a scan at its depth. Use lockpick-scan to start it with a stable idempotency key.
- **DNS check again.** For a supported public-record finding, use lockpick-dns. That check is free and leaves the original grade unchanged.

## Schedules

This plugin does not create or edit schedules. Direct scheduling requests to the Lockpick web app. Do not promise background monitoring or notifications from this conversation.
