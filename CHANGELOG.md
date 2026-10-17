# Changelog

Release notes for every version are also on the [Releases page](https://github.com/SPARTANAC95/slate-player/releases).

## 1.2.0 — 2026-10-17

### New

- **A filmstrip you can actually watch** (`T`). It no longer races past 30 tiles a second while playing: the strip holds still, the middle tile plays live, and the pictures either side cross-fade in place. Four views:
  - **Frames**: every frame around the playhead; shows Time while playing and fades back to the frames around wherever you pause.
  - **Time**: one exact picture per interval, ½ s to 5 min apart (`Ctrl`+wheel or −/+).
  - **Shots**: one picture per shot. The cuts are found automatically in the background, so the strip changes exactly when the picture cuts.
  - **Whole**: the entire video across the strip.
- **Jump between shots**: `Shift`+`↓` / `Shift`+`↑` land on the first frame after the next / previous cut.
- **Everything in one menu**: the ☰ button (top left, or `F10`) lists every feature in labelled groups with its shortcut, and the gear opens Settings. The side panel's tabs are labelled, the control bar is grouped, and in / out points have their own icons.
- **Strips and shot lists are remembered** per video, so a file you've opened before shows its filmstrip at once.
- **Frame decoding: Auto / GPU / CPU** (Settings → Frame engine). Playback always uses the GPU; Auto picks the faster decoder for stepping and scrubbing (all CPU cores for 4K H.264 on 8+ core machines), and GPU keeps the processor idle. Video info shows which one is in use.

### Fixed

- Compare: both videos fit fully, and the A / B labels sit neatly in the corners.
- The right-click menu ran off the bottom of the window, and the view menu was cut off on the right.
- Filmstrip tiles were empty while playing.

## 1.1.0 — 2026-10-16

The first public release.

### New

- **Smooth hold-to-scrub**: holding `,` `.` (or the arrows in focus mode) glides through frames and speeds up the longer you hold (`Shift`/`Alt`: faster); letting go lands on the exact frame.
- **Drag to scrub**: right-drag the picture (left-drag in focus mode).
- **Adjustable loupe** (`Q`): `Ctrl`+wheel zooms it (1.5–32×), `Ctrl+Shift`+wheel resizes it; sharp at any display scaling, with a pixel grid and an exact pixel probe.
- **Audio scrubbing** (`U`) and a **waveform** on the timeline.
- **Frame export**: every frame of the in/out range as PNG/JPEG (`Ctrl+Shift+E`), or a **contact sheet** (`Ctrl+Shift+K`).
- **Compare** two videos frame-locked (`Ctrl+Shift+C`, or `Ctrl`-drop a file): wipe, side by side, toggle (`V`), difference.
- **Automatic updates** for the installed version.

### Fixed

- Exports, previews and clip cuts from some MKV/WebM files started one frame early.
- Frames just before a keyframe in open-GOP HEVC MP4s could decode from the wrong starting point.
