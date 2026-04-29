# Email Campaigns — Knowledge Index

## Overview
Venue outreach campaigns for Kolot the Voices and future projects.
Path: /Volumes/KINGSTON/Facebook Scraper/kolot_campaign/

## Current State
- Main script: campaign.py (universal, config-driven)
- Scheduling: schedule_drafts.py (Selenium → Gmail)
- Google blocks after ~40 actions/session → Firefox re-login between batches
- caffeinate required during long runs
- Polish character encoding: UTF-8 mandatory in IMAP

## Topics — load when relevant

| Topic | File | Trigger keywords |
|-------|------|-----------------|
| Pipeline reference | [pipeline-reference.md](pipeline-reference.md) | "campaign.py", "pipeline", "как отправлять", "SMTP", "IMAP" |
| Jazz Poland campaign | [jazz-pl/](jazz-pl/index.md) | "кампания", "venue", "Польша", "jazz venues" |
| Gemini agent | [gemini-agent.md](gemini-agent.md) | "Gemini", "agent", "токены кончились" |

## Key Rules (from memory)
- Never auto-send emails — always draft/preview first
- 40/day safe limit (25-30 new + follow-ups)
- Gmail Draft flag: must preserve \Draft
- decisions_log.csv and schedule_log.csv: verify after every batch
