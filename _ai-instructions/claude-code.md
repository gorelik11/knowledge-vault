# Knowledge Base Protocol — Claude Code

Copy this block into each project's CLAUDE.md, replacing {section} with the project's vault section name.

---

## Knowledge Base
Vault: ~/Knowledge/
Section: {section}/

### Protocol
1. At session start, read `~/Knowledge/{section}/index.md`
2. When a topic listed in the index becomes relevant to the conversation, read the corresponding .md file
3. When a subtopic appears within a loaded topic, read the subtopic .md file
4. NEVER load files from other project sections without explicit user request
5. When unsure if a file is needed — don't load it
6. `brain.md` — only during memory reorganization or by user request
7. Cross-project files (`_infrastructure/`, `_agents/`, `_shared/`) may be loaded when their topic appears, regardless of current section
8. User can always remind you about a topic/subtopic manually

### Trigger Keywords
Each index.md lists topics with their trigger keywords. When you see these keywords in conversation, that's the signal to load the corresponding file.

### What NOT to do
- Do not load the entire vault at session start
- Do not read brain.md routinely — it's for reorganization sessions
- Do not preemptively load files "just in case"

---
