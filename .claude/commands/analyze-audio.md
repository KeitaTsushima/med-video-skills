---
description: Analyze audio levels (RMS per second) from a video or audio file
---

# analyze-audio

Analyze audio levels from the file $ARGUMENTS.

## Instructions

### Step 1: Extract audio to WAV

If the input is a video file, extract audio first:

```bash
ffmpeg -y -v quiet -i "INPUT" -ac 1 -ar 16000 -acodec pcm_s16le -f wav /tmp/audio_rms_analysis.wav
```

If the input is already a WAV file, convert to mono 16-bit 16kHz for consistency:

```bash
ffmpeg -y -v quiet -i "INPUT" -ac 1 -ar 16000 -acodec pcm_s16le -f wav /tmp/audio_rms_analysis.wav
```

### Step 2: Compute RMS per second

Run this Python script:

```python
import wave, struct, math

path = '/tmp/audio_rms_analysis.wav'
wf = wave.open(path, 'rb')
sr = wf.getframerate()
nch = wf.getnchannels()
sw = wf.getsampwidth()
nframes = wf.getnframes()
raw = wf.readframes(nframes)
total_samples = nframes * nch
samples = struct.unpack(f'<{total_samples}h', raw)
# If stereo, take left channel only
if nch > 1:
    samples = samples[::nch]
dur = nframes / sr

results = []
for sec in range(int(dur) + 1):
    start = sec * sr
    end = min((sec + 1) * sr, len(samples))
    chunk = samples[start:end]
    if len(chunk) == 0:
        continue
    rms = math.sqrt(sum(s * s for s in chunk) / len(chunk))
    db = 20 * math.log10(rms / 32768) if rms > 0 else -96.0
    bar = '#' * max(0, int((db + 60) / 1.5))
    results.append((sec, db, bar))

for sec, db, bar in results:
    print(f"{sec:3d}s | {db:6.1f} dB | {bar}")
```

### Step 3: Interpret results

- Identify quiet and loud sections
- Note any sudden volume changes
- If script/narration timing is known, check whether audio peaks align with key moments
- Look for the overall volume arc (does it follow a tension curve?)

## Output format

```
## Audio levels (RMS per second)
  0s | -XX.X dB | ####
  1s | -XX.X dB | ######
  ...

## Volume arc
(describe the shape: e.g., "starts quiet, builds at 10s, peaks at 22s, fades out")

## Observations
- ...
```

## Multi-source comparison

If multiple audio files are provided (e.g., final mix + BGM + narration separately), analyze each one and compare:
- Where does narration sit relative to BGM?
- Are there ducking points where BGM drops for narration?
- Do volume peaks across sources align or conflict?

## Known limitations

- The Python script loads all audio frames into memory at once. Fine for files under ~30 minutes (~58MB at 16kHz mono 16-bit), but may need chunked reading for longer files (e.g., full-length films or concerts).
- Requires ffmpeg and Python 3 to be installed on the system.
