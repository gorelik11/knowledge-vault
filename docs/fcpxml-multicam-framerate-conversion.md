# FCPXML Multicam Cut Transfer Between Framerates

## Problem
Two FCP projects with the same multicam material but different multicam framerates (e.g., 23.976fps and 25fps). Need to transfer cut points from one project to the other.

## Key Concepts

### Timeline vs Multicam Framerate
- The **sequence timeline** has its own framerate (defined by sequence's `format`)
- The **multicam** has its own framerate (defined by multicam's `format`)
- These can differ — FCP uses `conform-rate` to bridge the gap

### What Each mc-clip Attribute Means
- `offset` = position on the timeline (timeline framerate)
- `duration` = length on the timeline (timeline framerate)
- `start` = position within the multicam (multicam framerate)

### Speed Relationship
When multicam framerate differs from timeline framerate:
- With `conform-rate srcFrameRate="23.98"` on a 25fps timeline:
- Each multicam frame maps to one timeline frame
- Multicam advances at: `timeline_fps / multicam_fps` = `25 / 23.976` per second of timeline
- So: `start[n] = start[0] + offset[n] * (25 / 23.976)`

When multicam and timeline share the same framerate (e.g., both 25fps):
- 1:1 mapping, no speed change
- `start[n] = start[0] + offset[n]`

## Transfer Procedure (23.976fps multicam → 25fps multicam)

### Given
- Source project: 25fps timeline, 23.976fps multicam, has cuts
- Target project: 25fps timeline, 25fps multicam, no cuts (single mc-clip)

### Steps

1. **Extract** all mc-clip elements from source project's spine

2. **Keep offset/duration as-is** — both timelines are 25fps, so timeline positions are identical

3. **Compute new `start` values**: In the target (25fps multicam), start = start_base + offset, where start_base is taken from the target's original single mc-clip `start` attribute

4. **Map angleIDs** — multicam angles have different GUIDs between projects. Match by clip name within the multicam angles

5. **Remove `conform-rate`** elements from mc-clips — not needed when multicam matches timeline framerate

6. **Fix resource references**:
   - `ref` on mc-clips: match to target's media ID
   - `ref` on titles: match to target's effect ID
   - `name` on mc-clips: match to target's media name

7. **Snap title offsets** to target framerate boundaries:
   - For 25fps: offset must be a multiple of `100/2500s` (= 1/25s)
   - Round: `offset_new = round(offset_seconds * 25) / 25`

8. **Remove transitions** that reference effects not defined in target's resources

9. **Update sequence duration** to match source

## Common Pitfalls

1. **DTD validation failure** — FCP strictly validates all `ref="rN"` attributes. If you copy a transition from project A that references effects r14, r15, but project B only has resources up to r12, import will fail entirely

2. **"Not on edit frame boundary"** — title offsets must align to the timeline's frame grid. Values carried over from a different framerate context will be off-grid

3. **Wrong `start` calculation** — the relationship between timeline offset and multicam start depends on the conform-rate speed factor. Simply converting times between framerates is wrong; you must understand the playback speed relationship

4. **Multicam angle IDs** — each multicam instance generates unique GUIDs for angles, even if the source media is identical. Always map by name, never assume IDs match

## Example Angle ID Mapping
```
Source multicam angles:          Target multicam angles:
  "Dima1"    = Dy6TWdm...   →     "Dima 1"   = 9T6F2/A...
  "Sciera1"  = Cg0ReWe...   →     "Angle 1"  = NB+6aDu...
  "Clip 2"   = Ixmy4OI...   →     "KS"       = 4HYEK2p...
  "Clip 3"   = lsICMEe...   →     "KSDima"   = gBSr65p...
```
Names may differ slightly — match by source media content (same asset UIDs).
