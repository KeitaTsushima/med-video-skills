---
description: Extract frames from a video file at a specified interval for visual review
---

# extract-frames

Extract frames from the video file $ARGUMENTS for visual analysis.

## Instructions

1. Get the video duration using ffprobe
2. Determine the extraction strategy:
   - For videos under 15s: extract at 0.5s intervals
   - For videos 15–60s: extract at 1s intervals (1 fps)
   - For videos over 60s: extract at 2s intervals
3. Extract frames to a temp directory using:

```bash
ffmpeg -y -v quiet -i "INPUT" -vf "fps=FPS_VALUE" -q:v 2 "/tmp/frames_BASENAME/frame_%03d.jpg"
```

4. Report how many frames were extracted
5. View ALL extracted frames using the Read tool — do not skip any
6. For each frame, briefly note:
   - What is shown (subject, action)
   - Shot size (ECU / CU / medium / wide / establishing)
   - Any visible text or subtitles

## Output format

```
## Extraction summary
- Source: filename
- Duration: Xs
- Frames extracted: N (at Xfps)
- Output: /tmp/frames_BASENAME/

## Frame-by-frame
| Frame | Time | Description | Shot size |
|-------|------|-------------|-----------|
```
