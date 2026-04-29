# Kolot Jazz Poland Campaign Progress
Last updated: 2026-04-26

## Summary
- Total targets: 408
- Sent: 133
- Scheduled: 77
- Drafts remaining: ~116
- Replies received: TBD (check contacts_final.csv)
- Follow-ups sent: TBD

## Campaign Architecture
- contacts_final.csv: master contact list
- campaign.py + kolot_pl.json: config-driven sending
- schedule_drafts.py: Gmail scheduled send via Selenium
- Legacy: email_campaign.py (still functional, not primary)

## Recent Activity
| Date | Action | Count | Notes |
|------|--------|-------|-------|
| 2026-03-23 | Venue filter pass | 70 | Removed NOT_VENUE entries |
| 2026-03-XX | Email batches | 133 | Sent via campaign.py |
| 2026-03-XX | Scheduled | 77 | Via schedule_drafts.py |

## Next Steps
- Complete remaining ~116 drafts
- Phone follow-up for top venues (see call-list.md)
- Filter results cleanup (see venue-filter.md)

---
*This file is updated by Claude/Codex after each campaign work session.*
