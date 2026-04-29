# Claude Code Architecture Insights (v2.1.88 source leak, 2026-03-31)

## Source
- npm v2.1.88 shipped with 59.8MB source map (missing .npmignore entry)
- 1,900 files, 512K LOC TypeScript, 50+ tools, 44 feature flags
- Analysis repos: ccunpacked.dev, instructkr/claw-code (Rust+Python rewrite)
- Local copy: /Volumes/KINGSTON/claw-code-main/

## Key Patterns Applicable to Our Workflow

### 1. Three-Tier Memory (already using tiers 1-2)
- Tier 1: MEMORY.md (≤200 lines) — always in context every turn
- Tier 2: topic files (strategic-profile.md, etc.) — loaded on demand
- Tier 3: session transcripts — searched via grep when needed
- Memory = hints requiring verification, not ground truth

### 2. autoDream Consolidation
- Background process: orient → gather → consolidate → prune
- Runs on cheap model (Haiku), costs ~$0.01-0.03 per run
- Keeps memory under 200 lines / 25KB
- Could implement via Task tool + model:haiku at session end
- Useful for: Goethe grant strategy evolution, campaign progress tracking

### 3. Blocking Budget (proactive action limits)
- 15-second window, max 2 proactive messages
- Reactive responses unlimited
- Relevant for: email campaign automation, YouTube bulk updates

### 4. Coordinator Mode (not available on v2.1.42)
- Lead agent spawns parallel workers with restricted permissions
- Workers share prompt cache (cost optimization)
- Workers get isolated git worktrees
- Future feature — watch for in upgrades

### 5. CLAUDE.md Reinsertion
- After /compact, CLAUDE.md is reinjected into context
- This is why instructions survive compaction
- User strategy: exit at 50% context is valid but /compact achieves similar result

## Unreleased Features (in codebase but flagged)
- KAIROS: always-on daemon with webhooks, daily logs, proactive actions
- Buddy: virtual pet system (species/rarity from account ID)
- UltraPlan: 30-min planning sessions on Opus
- Bridge: remote control from phone/browser
- Voice Mode + Computer Use integrations
- UDS Inbox: inter-session communication via Unix domain sockets

## Claw-Code (Rust Rewrite) Compatibility
- Rust edition 2021, rustls-tls (no OpenSSL dependency)
- Works on Big Sur / Ventura for sure
- High Sierra (10.13) — risky, no CI testing
- Still v0.1.0, far from parity with TS version
- Not practical to use as replacement for Claude Code currently

## Code Quality Assessment
- ~7/10 — god files >5K LOC, 250 files with feature flags
- Claude Code ranked 39th among terminal harnesses in benchmarks
- Value is in architectural patterns, not implementation quality
