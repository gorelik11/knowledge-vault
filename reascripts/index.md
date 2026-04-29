# ReaScripts — Knowledge Index

## Project
REAPER scripts, JSFX plugins, audio processing automation.
Repo: ~/ReaScripts/ | GitHub: gorelik11/ReaScripts

## Current State
- MCP: reaper (reapy, ~15 tools) + total-reaper (Lua, 600+ tools)
- Git branch: main
- Active work: Reels Auto-Render (see project docs/superpowers/)

## Topics — load when relevant

| Topic | File | Trigger keywords |
|-------|------|-----------------|
| Script catalog | [scripts-reference.md](scripts-reference.md) | "скрипты", "Lua scripts", "какие скрипты есть", "envelope limiter", "align" |
| JSFX plugins | [jsfx-plugins.md](jsfx-plugins.md) | "JSFX", "limiter", "RCBit", "brickwall", "плагин", "компрессор" |
| Tempo detection | [tempo-detection.md](tempo-detection.md) | "tempo", "madmom", "BPM", "beat detection", "темп", "downbeat" |
| Gemini agent | [gemini-agent.md](gemini-agent.md) | "Gemini", "agent", "токены кончились" |

## Key Technical Notes (from memory)
- `TakeFX_SetParam` uses actual slider values for JSFX, NOT normalized 0-1
- Split-and-move ALWAYS creates gaps — must fill afterwards by moving items
- BPM from downbeat-to-downbeat, NOT from averaging beat intervals
- REAPER BPM is ALWAYS quarter-note based regardless of time signature
- Item selection lost after undo — always re-select
- Process items in REVERSE position order in batch scripts
- Accessor reads from position 0, NOT D_STARTOFFS (offset baked in)
- Envelope points: delete REAPER's auto-created default point at t=0 before writing custom points
- **Madmom:** Python 3.11 at `/Library/Frameworks/Python.framework/Versions/3.11/bin/python3`
- **Compound time signatures (6/8, 12/8):** beats_per_bar = num/3; for simple (4/4, 5/8): beats_per_bar = num
- **Madmom pipeline:** `RNNDownBeatProcessor` → `DBNDownBeatTrackingProcessor(beats_per_bar=[N], fps=100)`
- BPM calculation: x/4: `bpm = x * 60 / bar_dur`, x/8: `bpm = (x/2) * 60 / bar_dur`
- REAPER Python does NOT have madmom — always use subprocess to external Python
- Pattern: subprocess.Popen from ReaScript → external Python with madmom → JSON → back to REAPER
- Within `inside_reaper()` reapy context, use `from reapy import reascript_api as RPR` (no RPR_ prefix)
