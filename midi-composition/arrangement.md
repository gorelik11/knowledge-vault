# Arrangement — VSTi Specs & Orchestration

## VSTi Libraries

### CSS (Cinematic Studio Strings)
- Full string orchestra: Violins 1, Violins 2, Violas, Cellos, Basses
- Legato: auto-detected from overlapping notes
- Key switches for articulations (sustain, staccato, pizzicato, tremolo, etc.)
- CC1 = dynamics (crossfade pp→ff), CC11 = expression
- Runs in Kontakt or standalone

### Berlin Strings (Orchestral Tools)
- First Violins, Second Violins, Violas, Cellos, Basses
- Capsule engine (standalone, no Kontakt needed)
- Adaptive legato system
- CC1 = dynamics, CC11 = expression
- More detailed articulations than CSS

### General VSTi Loading in REAPER
- MCP: `add_fx(track_index, "VSTi: Plugin Name")`
- Lua: `TrackFX_AddByName(track, "VSTi: Plugin Name", false, -1)`
- VST3: prefix with "VST3i:" instead of "VSTi:"
- Parameters: `set_fx_param` / `TrackFX_SetParam` (normalized 0-1)

---

## String Quartet Ranges

| Instrument | Low | MIDI | Comfortable High | Extended |
|---|---|---|---|---|
| Violin 1 | G3 | 55 | A6 | C7 |
| Violin 2 | G3 | 55 | E5 | A5 |
| Viola | C3 | 48 | D5 | G5 |
| Cello | C2 | 36 | A3 (thumb: D4) | A4 |

### Key MIDI Note Numbers
C2=36, C3=48, C4=60 (middle C), C5=72, C6=84, C7=96

---

## Voice Splitting (Piano → String Quartet / Orchestra)

### Algorithm: Top/Bottom + Voice-Leading Proximity
1. Read all MIDI notes from source item
2. Group notes by simultaneous onset time (quantize threshold)
3. Sort each chord group by pitch (high → low)
4. Assign: highest = Vln1, next = Vln2, next = Viola, lowest = Cello
5. When fewer notes than voices: use voice-leading proximity (each voice follows nearest pitch)
6. Write separated notes to destination MIDI tracks

### Edge Cases
- 3-note chord: `assign_three_notes_to_four_voices` with proximity logic
- 2-note chord: outer voices get priority (melody + bass)
- 1-note chord: goes to melody (Vln1)
- REAPER has no built-in voice extraction — must script it

---

## Articulation Control

### Key Switches
- MIDI notes in low range (C0-B0, pitches 24-35) that trigger articulation changes
- Inserted as short notes just before the actual note
- Each library has its own key switch map
- Can be inserted via MCP `add_midi_note` with low pitch values

### Standard MIDI CC for Orchestral
| CC | Function | Notes |
|----|----------|-------|
| CC1 | Dynamics/Mod | Controls dynamic crossfade (pp to ff), changes timbre |
| CC7 | Volume | Master volume, usually 100-127 |
| CC11 | Expression | Volume without timbre change, for cresc/dim |
| CC64 | Sustain Pedal | On/off |

### Articulation Systems in REAPER
- **Reaticulate** (most popular): uses Program Changes, translates to key switches
- **ReaKS**: alternative keyswitch tool
- **X-Raym Auto-Keyswitch**: child tracks per articulation

---

## MCP Tools for MIDI
- `create_track`, `set_track_color` — setup
- `add_fx` — load VSTi instruments
- `create_midi_item` — create MIDI containers (measure-based)
- `add_midi_notes` — bulk note insertion (efficient)
- `get_midi_notes` — read notes (for voice splitting input)
- Key switches: `add_midi_note` with low pitch (24=C0, etc.)

### MCP Limitations
- **No CC insertion** — need Lua via reapy for CC1, CC11, expression curves
- **No Program Change insertion** — need Lua for Reaticulate control
- For CC/expression: use `MIDI_InsertCC(take, false, false, ppq, 0xB0, 0, cc_num, value)`

---

## Practical Workflow
1. Record guitar via Jam Origin MIDI Guitar → single MIDI track
2. Edit/quantize MIDI as needed
3. Voice split script → 4+ tracks (Vln1, Vln2, Viola, Cello, Bass...)
4. Load VSTi on each track (CSS or Berlin Strings)
5. Add expression/dynamics (CC1, CC11 via Lua CC insertion)
6. Add articulation key switches (MCP or Reaticulate)
7. Refine: adjust velocity, timing, voicing, iterate

---

## Cross-Composer Patterns (for arrangement)
- Evans voicings + Brahms independence = rootless chords as interlocking lines
- Jarrett pedal + Mahler spacing = cello drone + extreme upper spacing
- Cosma melody + Rachmaninov inner chromatic = emotional power
- Scriabin color + Gladkov theatrical = mystic to comic contrast
