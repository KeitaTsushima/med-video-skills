---
description: Analyze shot composition, camera angles, and visual patterns from extracted frames
---

# analyze-composition

Analyze the visual composition of extracted frames from $ARGUMENTS.

If the argument is a video file, first run `extract-frames` on it. If it is a directory of already-extracted frames, use those directly.

## Instructions

View every frame and analyze each for:

1. **Shot size**: ECU (extreme close-up), CU (close-up), MCU (medium close-up), MS (medium shot), MWS (medium wide), WS (wide shot), EWS (establishing wide shot)
2. **Camera angle**: high angle, eye level, low angle, bird's eye, POV
3. **Composition**: rule of thirds, center (日の丸), off-center, symmetrical, diagonal, leading lines
4. **Subject placement**: where is the main subject in the frame

Then identify patterns across the sequence:

- Shot size distribution (count of each type)
- Shot size rhythm (how sizes alternate — does it avoid monotony?)
- Angle variety
- Dominant composition style
- Any notable techniques (POV shots, progressive pull-outs, match cuts implied by framing)

## Output format

```
## Per-frame analysis
| Frame | Shot size | Angle | Composition | Subject placement | Notes |
|-------|-----------|-------|-------------|-------------------|-------|

## Patterns
### Shot size distribution
- ECU: N, CU: N, MCU: N, MS: N, WS: N, EWS: N

### Shot size rhythm
(describe the wave pattern — e.g., "opens wide, tightens to CU, opens again")

### Composition tendencies
- ...

### Notable techniques
- ...

## Assessment
(overall evaluation: is there enough variety? any monotony risks? suggestions?)
```
