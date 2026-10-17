# Validation

What was checked before each release, on what, and what's still limited. Test results describe what was checked, not a guarantee for every file or PC.

## 1.2.0 (2026-10-17)

Measured on Windows 11 Pro (26200), Ryzen 9 7900X3D (12 cores / 24 threads), RTX 2070 SUPER, 144 Hz display at 175 % scaling, against the app itself and the packaged build.

### Automated checks

Every suite drives the real app (Playwright over Electron) and, where it matters, reads the frame number encoded in the test clips' pixels instead of trusting what the app reports.

| Suite | What it proves | 1.2.0 |
|---|---|---|
| Unit | MP4 / MKV parsers, codec strings and demuxers against `ffprobe` | 18 / 18 |
| Frame accuracy | Steps, reverse steps across keyframes, bursts of fast stepping, random jumps, play/pause hand-offs and timeline seeks land on the frame the pixels show, in 10 formats (H.264 incl. VFR, rotated and fragmented, HEVC open-GOP and HDR10 4K, VP9 incl. live WebM without cues, AV1, MKV) | passed |
| Filmstrip | With Auto and GPU decoding: the strip never moves while playing (no picture ever appears in the gaps between tiles), every side tile shows exactly the frame it stands for, a cross-fade each interval and at each cut, tiles ready the moment play starts, cuts found at the exact frames, Shift+↓/↑ land on the cut frames, and a second launch takes shots and tiles from the disk cache | 22 / 22 per decoder |
| Features | Subtitles, chapters, conversion, markers, loop, export, capture, resume, queue, shuttle, audio, go-to, view, mini player, full screen, continue watching | 18 / 18 sections |
| Focus mode, jog, loupe, audio scrubbing, frame export, compare | Each feature end to end | passed |
| No stray highlights | Clicking any control (including the new menu) and then typing never leaves a focus ring or a stuck button | 11 / 11 |

### Performance

| | Result |
|---|---|
| Start to ready | 1.8 s |
| Open a 4K H.264 file to its first frame | 0.33 s (frame engine ready at 0.35 s) |
| Frame step | 5 ms forward (median), instant backward from the cache |
| Cold jump deep into an 8-second GOP | 180–370 ms |
| 4K playback | 0 dropped frames in 8 s, filmstrip closed or open in Frames, Time or Shots |
| CPU while paused | about 0.3 % of one core, whatever the filmstrip shows |
| CPU while playing 4K | 1.5–4.3 % of one core |
| Memory | renderer steady at about 1.2 GB with the default 1 GB frame cache, across six 4K file switches |
| Finding shots | about 400 frames a second on 4K H.264 (a 17-second 4K clip in under a second) |

Frame decoding on this machine: the CPU reaches a frame deep inside a 4K H.264 GOP in about 250 ms, the GPU in about 670 ms, which is why **Auto** uses the CPU for H.264 here and the GPU for everything else.

The installed 1.2.0 was also launched outside the test harness: it plays 4K, and its update check reaches GitHub and reports itself current.

## Known limits

- **The frame counter right after a pause or a timeline seek.** In some test runs the `<video>` element briefly showed the neighbouring frame, or the frame number lagged, right after pausing or seeking from the timeline. It happens in 1.1 and 1.2 alike and comes and goes between runs; frame steps and jumps in the frame-exact view were never affected. Being looked into.
- **Finding shots** uses FFmpeg's scene score: hard cuts between similar-looking shots (two dark scenes, say) can be missed, and fast flashes under 0.4 s are ignored on purpose. Dissolves aren't detected as cuts.
- **HEVC** needs a GPU with hardware HEVC decoding.
- **Not code-signed**: Windows SmartScreen warns on first run.
- Windows x64 only.
