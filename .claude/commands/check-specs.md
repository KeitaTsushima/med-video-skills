---
description: Extract and report technical specs (resolution, codec, fps, duration, audio format) for all video and audio files
---

# check-specs

Extract technical metadata from all video and audio files in the directory $ARGUMENTS.

## Instructions

For each video file (.mp4, .mov, .avi, .mxf), run:

```bash
ffprobe -v quiet -print_format json -show_format -show_streams "FILE"
```

Extract and report:
- Duration
- Resolution (width x height)
- Codec (video + audio)
- Frame rate
- Audio sample rate, bit depth, channels
- File size

For each audio-only file (.wav, .mp3, .aac, .flac), extract:
- Duration
- Codec / format
- Sample rate, bit depth, channels
- File size

## Output format

Present results as a table:

```
## Video files
| File | Duration | Resolution | FPS | Video Codec | Audio Codec | Audio Rate | Size |
|------|----------|------------|-----|-------------|-------------|------------|------|

## Audio files
| File | Duration | Format | Sample Rate | Bit Depth | Channels | Size |
|------|----------|--------|-------------|-----------|----------|------|

## Notes
- (any inconsistencies, mixed resolutions, mismatched frame rates, etc.)
```

Flag any inconsistencies across files (e.g., mixed resolutions, different frame rates) — these matter for editing.
