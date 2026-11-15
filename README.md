# Cutloom

An independent, static, local-video clipping studio. Original interface and identity; media capture code adapted from the user's existing Clipwave engine. No backend, hosted service, external dependencies, AI, URL imports or remote media uploads.

## Run / GitHub Pages

Serve this directory as a static site, e.g. `python3 -m http.server 8000`, or publish its files at a GitHub Pages repository root. All assets use relative paths; hash navigation also works under a repository subpath. No build step or API keys are needed. Live site: https://1animepahe-svg.github.io/cutloom-studio/

## How to use

1. Editor → choose a locally stored video supported by the browser (up to 500 MiB). Seek; enter start/end or set them to the playhead. Clips are limited to 120 seconds.
2. Select a format (9:16, 1:1, 4:5, 16:9), centered fill/crop or fit, enter optional caption text and placement, and include or mute source audio. The canvas preview uses the same drawing path as export. Brand kit controls caption color globally.
3. Export WebM in real time; keep the tab visible and device awake. Cancel is available. Download in Clip library before leaving or refreshing.
4. Save project saves edit settings locally; reopening requires reselecting the source file. Name and rounded size are compared as a convenience only, not a secure file identity check. Brand color is a global setting, not stored per project.

## Limits and privacy

- Only project metadata/settings and brand color persist in browser localStorage; browser data clearing, private mode, or unavailable/full storage may remove/prevent persistence. Video content and session clip blobs are not saved. Clips disappear on reload or closing. Filenames and caption text are stored in localStorage when saving a project.
- MediaRecorder plus canvas capture outputs WebM (VP8/VP9 depending on browser); no MP4, no background processing. It renders 360×640, 360×360, 360×450 or 640×360 respectively. Export is real-time, not frame-accurate: startup can include a still frame or silence and the end can overshoot. Timing depends on device/browser; recorded WebM may lack duration metadata. Export stops when the tab is hidden or rendering stalls.
- Audio capture uses Web Audio when available; source audio capture and supported file codecs vary by browser. If audio fails, try silent export. Physical phones and Safari have not been verified.
- Captions are manually typed and remain for the entire clip; they are not timed or generated. Cropping is centered. The brand kit changes caption color only; no logos, custom fonts, automatic branding, AI, cloud, account, link importing, face tracking, MP4 or automatic subtitles.
- Use only videos you have permission to edit.

## Testing

`node --check app.js && node --check engine.js`. `test_local.py` is a Playwright/Chromium smoke test. It expects a local HTTP server on port 18756, Chromium at `/usr/bin/chromium`, ffprobe, and `/tmp/cutloom-small.mp4` (a short H.264/AAC clip). Tested with a 4-second 320×180 sample: local load and seek, 4:5 fit preview, captions, color, saved project restore after reload, audio and silent downloads, and temporary library. The audio export had VP8 360×450 video and Opus audio; decoded audio was non-silent. The muted export had no audio stream. No page errors or horizontal overflow at a 390px viewport. Browser and device behavior will vary.
