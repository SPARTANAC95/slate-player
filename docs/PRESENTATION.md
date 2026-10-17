# How the screenshots were made

Every image in this repository is the real Slate Player interface, captured from the app itself (not the screen) in a fresh profile. Nothing was edited afterwards except resizing to 1600 px wide.

## The demo film: *Six Skies*

The video in the screenshots is an original 24-second, 4K, 24 fps film made for them: six procedural shots (dawn ridges, an aurora, ocean light, a nebula, dunes and out-of-focus city lights), each drawn by a GLSL shader on the GPU and encoded with FFmpeg, with a generated ambient soundtrack so the timeline shows a waveform. No third-party footage, photographs or music are used. Dark and bright shots alternate so every cut is a clear one for the Shots view.

The colour-graded copy in the Compare screenshot is the same film through FFmpeg's `eq` and `colorbalance` filters (more contrast and saturation, warmer).

## Capture

- Slate Player 1.2.0 on Windows 11, window 1600 × 900 at 175 % display scaling (captured at 2802 × 1577).
- A fresh, empty profile, the default lavender accent and ambient light on.
- The hero is paused on the third shot with the Shots filmstrip open; *Frames* is three frame steps into the aurora; *Scopes* is on the dunes; the menu is open over the city lights; *Compare* is a wipe on the dawn shot.

The scripts that render the film and drive the captures are kept with the app's source.
