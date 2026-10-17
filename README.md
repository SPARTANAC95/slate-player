# Slate Player

A quiet, precise video player for Windows — built for 4K, HDR and genuine
frame-by-frame work.

**[Download the latest release](https://github.com/SPARTANAC95/slate-player/releases/latest)**

- `Slate-Player-Setup-<version>.exe` — installer (per user, no admin needed).
  Updates itself: new versions download in the background and the app offers
  *Restart to update*.
- `Slate-Player-<version>-portable.exe` — runs without installing; doesn't
  update itself.

The builds aren't code-signed, so the first time Windows SmartScreen shows
"Windows protected your PC" — choose *More info → Run anyway*.

## Highlights

- Exact, instant frame stepping on long-GOP 4K (H.264, HEVC, AV1, VP9 —
  MP4, MOV, MKV, WebM), with smooth hold-to-scrub, drag-to-scrub and audio
  scrubbing.
- **A filmstrip that holds still** (new in 1.2): the middle tile plays live
  while the pictures either side cross-fade in place — every frame, one
  picture per interval (½ s to 5 min), one per **shot** (cuts are found
  automatically; `Shift`+`↓` / `Shift`+`↑` jump between them), or the whole
  video.
- Focus mode: nothing on screen but the picture, editor-style frame keys.
- Compare two videos frame-locked: wipe, side by side, toggle, difference.
- Loupe with an exact pixel probe, scopes, zoom to 64×.
- Export clips, every frame of a range as PNG/JPEG, or a contact sheet.
- Subtitles, chapters, markers, a waveform on the timeline, HDR passthrough.
- **Everything one click away** (new in 1.2): the ☰ menu lists every feature
  with its shortcut, the gear opens Settings, and frame decoding runs on the
  GPU or all CPU cores — Auto picks the faster one.

[FFmpeg](https://ffmpeg.org/) on your `PATH` is optional but recommended:
exports, contact sheets, the waveform, audio scrubbing, finding shots,
embedded subtitles and automatic fixes for files Windows can't play natively
all use it.

This repository hosts the releases; the source isn't published here.
