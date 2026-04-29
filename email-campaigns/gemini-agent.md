# Using the AI Agent for Kolot Campaign

When Claude Code tokens run out, use the Gemini-powered AI agent as a backup.

## Quick Start

```bash
agent kolot
```

## What the Agent Can Do

- **Check campaign status:** "Run `python3 /Volumes/KINGSTON/email_campaign.py --status`"
- **Preview next batch:** "Preview the next 10 emails"
- **Create drafts:** "Create Gmail drafts for the next 9 venues"
- **Analyze venues:** "Read venue_filter_results.md and summarize remaining venues"
- **Edit templates:** "Read and update the email template in email_campaign.py"
- **Track responses:** "Check which venues have replied"

## Example Prompts

```
You: What's the campaign status?
You: Read the call_list.md and suggest follow-up strategy
You: How many emails are left to send?
You: Read contacts_final.csv and find all festivals
```

## Context File

The agent loads `contexts/kolot.md` which contains campaign details, file locations, commands, and rules. Claude Code can update this file as the campaign evolves.

## Important

- The agent **cannot send emails automatically** — it can only run the script which requires manual confirmation
- Always use `--draft` mode for safety
- The agent has full file system access — it can read CSVs, edit scripts, etc.
