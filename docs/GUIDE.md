# Slate Player user guide

Everything Slate Player does, and where to find it. The quickest way in is the **☰ menu** in the top-left corner (`F10`): it lists every feature with its shortcut. `Ctrl+K` searches every command by name, and `?` shows all the keys.

- [Install and update](#install-and-update)
- [Opening videos](#opening-videos)
- [Playing and stepping](#playing-and-stepping)
- [The filmstrip](#the-filmstrip)
- [Focus mode](#focus-mode)
- [Looking closely](#looking-closely)
- [Comparing two videos](#comparing-two-videos)
- [Saving frames and exporting](#saving-frames-and-exporting)
- [Subtitles and audio](#subtitles-and-audio)
- [Settings](#settings)
- [Where your data lives](#where-your-data-lives)
- [Troubleshooting](#troubleshooting)

## Install and update

Download `Slate-Player-Setup-<version>.exe` from the [latest release](https://github.com/SPARTANAC95/slate-player/releases/latest) and run it. You can install just for yourself (no administrator rights needed) or for everyone on the PC. Windows 10 or 11, x64.

The builds aren't code-signed yet, so SmartScreen may say "Windows protected your PC". Choose *More info → Run anyway*. To check a download, compare its hash with the release's `SHA256SUMS.txt`:

```powershell
Get-FileHash .\Slate-Player-Setup-1.2.0.exe -Algorithm SHA256
```

**Updates.** The installed app checks GitHub shortly after it starts and every few hours, downloads new versions in the background and offers *Restart to update*; if you ignore it, the update installs the next time you quit. Turn this off in **Settings → Updates**. Version 1.0.0 had no updater: install the latest setup file once and updates arrive from then on.

**Portable.** `Slate-Player-<version>-portable.exe` runs without installing and leaves your system alone, but it doesn't update itself.

**FFmpeg (optional).** Install [FFmpeg](https://ffmpeg.org/) and make sure `ffmpeg` and `ffprobe` are on your `PATH` (for example `winget install Gyan.FFmpeg`). It powers exports, contact sheets, finding shots, the timeline waveform, audio scrubbing, embedded subtitles and the automatic fixes for files Windows can't play. Everything else works without it. The bottom of **Settings** shows the FFmpeg version it found.

## Opening videos

- Drag videos, a folder of videos, or a subtitle file onto the window.
- `Ctrl+O` opens videos, `Ctrl+Shift+O` a whole folder.
- In File Explorer, **Open with → Slate Player** (the installer offers it for common video types).
- The home screen lists what you've watched recently, with thumbnails; Slate resumes where you left off.

Several files make a **queue** (side panel → *Up next*, `Alt+1`): `N` / `Shift+N` move through it, and the next video starts automatically at the end.

If a file uses something Windows can't decode (AVI, MPEG-4 Part 2 video, AC3 / DTS / TrueHD audio, 10-bit H.264 and similar), Slate re-wraps or converts it with FFmpeg the first time, keeping the picture untouched whenever it can, and caches the result for next time.

## Playing and stepping

| Key | Does |
|---|---|
| `Space` | Play / pause |
| `,` `.` | Previous / next frame. Hold to glide through frames; it speeds up the longer you hold. |
| `Alt+,` `Alt+.` | 10 frames |
| `Shift+PageUp` / `Shift+PageDown` | Previous / next keyframe |
| `Shift`+`↑` / `Shift`+`↓` | Previous / next shot |
| `←` `→` | 5 seconds (change it in Settings); `Shift` 1 s, `Ctrl` 30 s |
| `J` `K` `L` | Shuttle backward / pause / forward; press again to go faster |
| `[` `]` | Slower / faster; `Backspace` back to 1× |
| `Home` `End` | Start / end |
| `0`–`9` | Jump to 0 %–90 % |
| `Ctrl+G` | Go to `1:23`, `01:02:03:12`, `f1234` or `50%` |

- **Drag to scrub:** right-drag the picture; slow drags move about a frame per 7 pixels, quick flicks cover more ground.
- **The mouse wheel** over the picture steps frames by default (Settings can make it seek or change volume); `Ctrl`+wheel zooms.
- Click the time in the control bar to switch between time, timecode and frame numbers.
- **FRAME-EXACT** in the control bar means you're looking at a frame decoded by Slate's own frame engine, exactly the one the frame number says.

## The filmstrip

Press `T` (or the filmstrip button in the control bar). The strip never slides past you: the middle tile is now, and the tiles either side are the moments before and after. When time moves on, their pictures cross-fade in place.

- **Frames**: every single frame around the playhead. Scroll over it to step, click a frame to land on it, drag to pull through. While the video plays it shows Time (no one can read 30 tiles a second), then fades back to frames when you pause.
- **Time**: one exact picture per interval, from ½ second to 5 minutes apart. Change the spacing with −/+ or `Ctrl`+wheel over the strip.
- **Shots**: one picture per shot. The cuts are found in the background (it needs FFmpeg; about 10 seconds for a 3-minute 4K trailer, longer for a film) and remembered, so the next time it's instant. The middle tile is the shot playing now; click another to jump to its first frame.
- **Whole**: the entire video across the strip; click anywhere to go there.

The pictures for Time and Shots are decoded ahead of time, even while you're paused, so pressing play shows finished tiles straight away. They're kept on disk per video (up to 500 MB in total, oldest first), so a file you've opened before shows its strip at once.

## Focus mode

`Shift+F` or a click of the mouse wheel on the picture: everything disappears (controls, panels, the cursor) and the window goes full screen. The keys switch to an editor layout:

| Key | Does |
|---|---|
| `←` `→`, `A` `D`, mouse wheel | 1 frame (hold to glide) |
| `Shift` + those | 10 frames |
| `Ctrl` + `←` `→` | 1 second |
| `↑` `↓` | Previous / next keyframe |
| `Shift`+`↑` `↓` | Previous / next shot |
| `Tab` | A small frame counter in the corner |
| `Esc`, double-click, wheel click | Leave |

Single clicks do nothing in focus mode, so a stray click never starts playback.

## Looking closely

- **View** (the *Fit* button, or `Z` to cycle): fit, fill or 1:1 source pixels; zoom at the cursor with `Ctrl`+wheel up to 64×, pan by dragging, rotate (`R`), mirror, aspect-ratio overrides.
- **Loupe** (`Q`): a magnifier that follows the pointer, 1.5–32×, with a pixel grid and an exact source-pixel probe. `Ctrl`+wheel zooms it, `Ctrl+Shift`+wheel resizes it.
- **Scopes** (side panel → *Scopes*, `Alt+4`): RGB histogram, luma waveform and vectorscope, live while you play or step.
- **Adjust** (side panel → *Adjust*, `Alt+3`): brightness, contrast, saturation and hue, remembered per video.
- **Info** (`Alt+5`): codec, resolution, frame rate, HDR, bit depth, keyframes, and which decoder is in use.
- **Stats for nerds** (`Ctrl+I`): live decode and cache numbers.

## Comparing two videos

`Ctrl+Shift+C`, or hold `Ctrl` while dropping a second video. B is locked to A frame for frame by timestamp, so a 60 fps remaster lines up with a 30 fps original.

- **Wipe**: drag the divider. **Side by side**. **Toggle** (`V` flips; hold `V` to peek at B). **Difference**, with 1–8× gain to make subtle changes visible. `Shift+V` cycles the modes.
- `Alt+[` / `Alt+]` shift B by a frame when the two don't start together; ⇄ swaps which side each one is on.
- Zoom, pan, rotation and the loupe apply to both; the loupe reads whichever picture is under the pointer.
- `Esc` stops comparing.

## Saving frames and exporting

- `S` saves the frame on screen as a full-resolution PNG (Pictures\Slate Player); `Shift+S` copies it to the clipboard.
- Mark a range with `I` (in) and `O` (out); `X` clears it. The loop button in the control bar shows the range and can repeat it.
- `Ctrl+E` exports the range as a clip: **lossless** (fast, cuts at keyframes), **frame-exact** (re-encodes, on your GPU when available) or **GIF**.
- `Ctrl+Shift+E` exports every frame of the range as PNG or JPEG, named by frame number.
- `Ctrl+Shift+K` makes a contact sheet: 12, 24 or 48 frames picked evenly, with timecodes, as one image.
- `B` drops a marker at the current frame; markers are listed in the side panel (*Chapters*) and saved with the video.

## Subtitles and audio

- Subtitles: SRT, WebVTT and ASS/SSA. A subtitle file next to the video with the same name loads automatically; embedded text tracks load on demand. `C` turns them on/off, `Shift+C` cycles tracks; delay (`Alt+-` / `Alt+=`), size, position and style are in the subtitles menu and the *Adjust* panel.
- Audio: volume up to 200 %, `M` mutes, `A` cycles audio tracks, **night mode** evens out loud effects and quiet dialogue, **mono** mixes every channel to both ears.
- **Audio scrubbing** (`U`): every frame you step to plays the sound under it, so cuts, words and hits can be found by ear.

## Settings

Open them with the gear (top right) or `Ctrl+,`.

- **Playback**: resume where you left off, play the next video automatically, click the picture to play/pause, how far the arrow keys jump, what the mouse wheel does, frames per wheel notch, audio scrubbing, the timeline waveform.
- **Appearance**: accent colour, ambient light around the picture, whether focus mode goes full screen, the focus-mode frame counter, how soon the controls hide.
- **Frame engine**: the frame-exact engine itself; **Frame decoding**, Auto / GPU / CPU (Auto picks the faster decoder: all CPU cores for 4K H.264 on 8+ core PCs, the GPU for everything else; GPU keeps the processor idle; playback always uses the GPU); and the frame cache size (more cache = longer instant reverse stepping).
- **Updates**: update automatically (installed version only).
- **Compatibility**: fix unsupported files automatically.
- **Saving**: where frames and exports go.
- **Storage**: the size of the converted-files cache, and clearing it.

## Where your data lives

Everything stays on your PC, in `%APPDATA%\Slate Player`:

| Folder / file | What |
|---|---|
| `settings.json`, `library.json` | Settings, recent files, resume positions, markers |
| `Thumbnails\` | Filmstrip pictures, per video (capped at 500 MB, oldest first) |
| `Shots\` | The cuts found in each video |
| `Waveforms\` | Timeline waveforms |
| `Converted\` | Files converted to play (clear it in Settings → Storage) |

Uninstalling keeps this folder; delete it to start fresh. Slate Player has no account, sends no analytics, and only goes online to check GitHub for updates.

## Troubleshooting

- **"Windows protected your PC"**: the build isn't code-signed. Check the download against `SHA256SUMS.txt`, then *More info → Run anyway*.
- **Exports, Shots or the waveform say they need FFmpeg**: install FFmpeg and restart Slate Player; the bottom of **Settings** shows the version it found.
- **A file won't play**: with FFmpeg installed and *Fix unsupported files automatically* on, Slate converts it the first time. Otherwise, open an [issue](https://github.com/SPARTANAC95/slate-player/issues/new/choose) with the file's codec details from the *Info* panel (please don't attach private videos).
- **Stepping feels slow on very long-GOP files**: a bigger frame cache (Settings → Frame engine) keeps more frames ready; Auto decoding already picks the faster decoder for your PC.
