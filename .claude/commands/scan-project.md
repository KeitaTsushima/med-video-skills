---
description: Scan a video production project directory and report its structure and assets
---

# scan-project

Scan the video production project directory at $ARGUMENTS and report a structured overview.

## Instructions

1. Display the directory structure as a tree
2. Classify all files into these categories:
   - Video footage (.mp4, .mov, .avi, .mxf, etc.)
   - Audio assets (.wav, .mp3, .aac, .flac, etc.)
   - Image assets (.png, .jpg, .psd, .tiff, etc.)
   - Project files (DaVinci Resolve, Premiere, After Effects, etc.)
   - Exports / final renders
   - Scripts & documents (.md, .txt, .pdf, etc.)
3. For each category, report the file count and approximate total size
4. Note any observations: naming conventions, versioning patterns, missing assets, or anything unusual

## Output format

```
## Project Structure
(tree view)

## Assets
### Video footage (N files, ~XX MB)
- filename ...

### Audio assets (N files, ~XX MB)
- filename ...

(etc.)

## Observations
- ...
```
