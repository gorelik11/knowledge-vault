# Video Production Project — Codex Context

## Overview
- Project: Video production knowledge base and tools for Final Cut Pro workflows
- Path: `/Volumes/KINGSTON/Video Production`
- GitHub: https://github.com/gorelik11/knowledge-vault
- Goal: FCPXML manipulation, video editing automation, knowledge documentation

## Key Knowledge Files
- `docs/fcpxml-reference.md` — FCPXML format internals (structure, time values, multicam, resources, DTD validation)
- `docs/fcpxml-multicam-framerate-conversion.md` — procedure for transferring multicam cuts between different framerates

## Working Rules
- Read existing docs before writing new content
- FCPXML is strict about DTD validation — every `ref="rN"` must have a matching resource
- Time values are rational numbers in seconds (`N/Ds`)
- Frame boundaries matter: title offsets and clip positions must align to the timeline framerate grid

## Do
- Verify resource references before generating FCPXML output
- Snap time values to frame boundaries when required
- Test generated FCPXML by checking for common pitfalls (see multicam conversion doc)
- Keep docs concise and example-driven

## Don't
- Don't assume angleIDs match between different multicam instances (always map by name/content)
- Don't copy transitions or effects without verifying their resource IDs exist in the target
- Don't convert timeline offset/duration when both projects share the same timeline framerate
- Don't edit `CLAUDE.md`

## MCP Tools
- **fcpxml-mcp-server** (https://github.com/DareDev256/fcpxml-mcp-server): 53 tools for FCPXML analysis/editing via MCP. Python 3.10+, supports FCPXML v1.8–v1.11. Not yet installed — evaluate if FCPXML work becomes frequent.

## Claude Compatibility
- Specialized Claude agents may exist under `.claude/agents/`
- Codex should keep its project notes in `AGENTS.md`
