# Brain — Master Knowledge Map

## Who
Dima Gorelik — guitarist, composer, Reiki practitioner. Based in Warsaw, Poland.
Band: Kolot the Voices (23 compositions, 7 countries/languages).
Israeli citizen, Ukrainian-born. Multicultural identity = creative asset.
Full strategic profile: [_shared/strategic-profile.md](_shared/strategic-profile.md)

## Machines
| Machine | OS | AI Tools | Vault Path | Node |
|---------|----|----------|------------|------|
| High Sierra | Darwin 17.7 | Claude Code v2.1.42 | ~/Knowledge/ | v18.20.8 |
| Big Sur | macOS 11.0.1 | Claude Code v2.1.42 + Codex | ~/Knowledge/ | v18.20.8 |
| (future Mac Mini) | TBD | TBD | ~/Knowledge/ | TBD |

## System Constraints
- Claude Code v2.1.42 pinned (MCP bug in v2.1.79+, see [_infrastructure/claude-code-bugs.md](_infrastructure/claude-code-bugs.md))
- Brew dead on High Sierra — PyMuPDF 1.23.26 for PDF, no poppler
- Playwright: system browsers only, Google blocks CAPTCHA
- Agents workaround: read .md manually, launch via Task tool (v2.1.42 no native agent support)
- ENABLE_TOOL_SEARCH=false in ~/.claude/settings.json

## MCP Servers (local per machine, NOT synced)
- **reaper** (reapy): ~15 tools, requires activate_reapy_server.py
- **total-reaper** (Lua): 600+ tools, requires mcp_bridge.lua
- **playwright**: npx @playwright/mcp@latest (Social-Media)
- **lighthouse**: (Social-Media)

## Projects
| Project | Vault Section | Path | Description |
|---------|--------------|------|-------------|
| ReaScripts | [reascripts/](reascripts/index.md) | ~/ReaScripts/ | REAPER scripts, JSFX, audio analysis |
| MIDI-Composition | [midi-composition/](midi-composition/index.md) | ~/MIDI-Composition/ | Composition, arrangement, VSTi |
| Grants | [grants/](grants/index.md) | /Volumes/KINGSTON/Funds/ | Goethe IKF + future grants |
| Email Campaigns | [email-campaigns/](email-campaigns/index.md) | /Volumes/KINGSTON/Facebook Scraper/ | Venue outreach (Kolot) |
| Social Media | [social-media/](social-media/index.md) | ~/Social-Media/ | YouTube SEO, website, social |

## Strategic Context
- Jazz Forum blocks Dima → all state-linked Polish festivals closed
- Strategy: independent venues (email) + German market (Tom Dayan) + grants
- Goethe IKF application submitted (2026-91828)
- Kolot campaign: 133 sent, 77 scheduled, ~116 drafts remaining
- Key relationships: Tom Dayan (Berlin), Agata Skrzypek (vocals), Krzysztof Ścierański (bass)

## Cross-Project Agents
- [_agents/strategic-advisor.md](_agents/strategic-advisor.md) — career strategy, cross-project synergies
- [_agents/doc-writer.md](_agents/doc-writer.md) — text/copy (grants, emails, social media)

## Hooks & Usage
- PostToolUse hook → ~/.claude/usage-logs/YYYY-MM-DD.log
- Statusline with $ cost estimate: ~/.claude/statusline.sh
