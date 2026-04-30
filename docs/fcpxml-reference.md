# FCPXML Format Reference

## Basics
- FCPXML is Apple's XML interchange format for Final Cut Pro projects
- Version 1.8 is used by current FCP X
- Has `<!DOCTYPE fcpxml>` DTD — FCP validates resource references strictly

## Structure
```
fcpxml
  resources/        — format, media, asset, effect definitions
    format          — frame rate + resolution (e.g., frameDuration="100/2500s" = 25fps)
    media           — compound clips, multicam clips
    asset           — source media files
    effect          — transitions, titles, generators
  library/
    event/
      project/
        sequence/   — the timeline
          spine/    — primary storyline (list of clips)
```

## Time Values
- All times are rational numbers in seconds: `N/Ds` (e.g., `135600/2500s` = 54.24 seconds)
- Integer times also valid: `62s`, `8s`
- Frame duration defines the framerate:
  - `100/2500s` = 1/25s = **25fps**
  - `1001/24000s` = **23.976fps**
  - `1000/25000s` = **25fps** (alternative representation)
  - `1001/30000s` = **29.97fps**

## mc-clip (Multicam Clip) Attributes
- `offset` — position on the **sequence timeline** (in timeline framerate)
- `duration` — length on the **sequence timeline** (in timeline framerate)
- `start` — playback start position **within the multicam** (in multicam framerate)
- `ref` — reference to a `<media>` resource containing a `<multicam>` element
- `name` — display name (must match the media name for clean import)

## mc-source (Angle Selection)
- `angleID` — GUID identifying which multicam angle to use
- `srcEnable` — what to take from this angle: `video`, `audio`, `all`
- Multiple mc-source elements per mc-clip: one for video, one for audio (can be different angles)

## Multicam Structure
```xml
<media id="r2" name="MyMulticam">
    <multicam format="r1" tcStart="0s" tcFormat="NDF">
        <mc-angle name="Camera 1" angleID="GUID1">
            <gap .../>           <!-- silence/black before content -->
            <ref-clip .../>      <!-- actual media -->
        </mc-angle>
        <mc-angle name="Camera 2" angleID="GUID2">
            <ref-clip .../>
        </mc-angle>
    </multicam>
</media>
```

## Conform Rate
- `<conform-rate srcFrameRate="23.98"/>` on mc-clip: tells FCP the source framerate
- Used when multicam framerate differs from timeline framerate
- Frame-for-frame mapping: each source frame maps to one timeline frame
- Speed factor: multicam advances at `timeline_fps / multicam_fps` rate
- `<conform-rate srcFrameRate="25" scaleEnabled="0"/>` on ref-clip inside multicam angle: source plays at native speed, no conform

## Resource References (DTD Validation)
- Every `ref="rN"` attribute MUST have a corresponding `<format|media|asset|effect id="rN">` in resources
- FCP will **refuse to import** the file if any ref points to a non-existent resource ID
- Common offenders: transition effects (Cross Dissolve = `r14`, Audio Crossfade = `r15`) that exist in one project but not another

## Title Elements
- `lane="1"` — title overlays on the primary storyline
- `offset` — absolute position in the **sequence timeline** (not relative to parent mc-clip)
- Must be on a frame boundary of the timeline framerate
- `ref` points to an effect resource (e.g., Motion template)

## Transitions
- `<transition>` elements sit between clips in the spine
- Reference effect resources for video (`filter-video ref=...`) and audio (`filter-audio ref=...`)
- Both video and audio effect IDs must exist in resources
