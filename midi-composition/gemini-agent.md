# Using the AI Agent for MIDI Composition

When Claude Code tokens run out, use the Gemini-powered AI agent as a backup.

## Quick Start

```bash
agent composition          # MIDI/arrangement context only
agent reaper composition   # combined with REAPER context
```

## What the Agent Can Do

- **Voice splitting:** "Split this piano MIDI into string quartet parts"
- **REAPER control:** "Create 4 tracks for string quartet with CSS VSTi"
- **Read MIDI:** "What notes are in the MIDI item on track 1?"
- **Write scripts:** "Write a Lua script to transpose selected MIDI notes up an octave"
- **Arrangement help:** "Suggest voicing for Cmaj9 across string quartet"

## Example Prompts

```
You: Create a string quartet setup in REAPER with CSS on each track
You: Read the MIDI on track 1 and split into 4 voices
You: Write a reapy script to add CC1 expression curve
You: What's the range of viola in MIDI note numbers?
```

## REAPER Access

The agent uses reapy via shell commands. Make sure `activate_reapy_server.py` is running in REAPER.

```
Agent: [run_command] python3 -c "import reapy; ..."
```

## Context File

The agent loads `contexts/composition.md` with voice ranges, VSTi info, and MIDI workflows. Claude Code can update this file as your workflow evolves.

## Limitations vs Claude Code

- No direct MCP tools (600+ in Claude) — uses reapy shell commands instead
- No CC insertion shortcut — needs explicit reapy scripts
- No real-time MIDI editing — works through scripts
