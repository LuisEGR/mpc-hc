# HLG (iPhone HDR) video in MPC-HC: samples and screenshots

For the `hdr-to-sdr-shader` branch of MPC-HC (EVR-CP / Sync renderer convert HLG to SDR).

## Videos

| File | What it is |
|---|---|
| `IMG_8843_3s.MOV` | First 3 s of an iPhone 14 Pro video, stream-copied (no re-encode): HEVC Main 10, 3840×2160 shown rotated to portrait, 60 fps, HLG (ARIB STD-B67), BT.2020, with sound. The Dolby Vision configuration box isn't kept (the MOV muxer can't write it); the picture and its HLG tags are untouched. |
| `IMG_8843_3s.av1.mp4` | First 3 s of the same video's AV1 copy, stream-copied: AV1 Main 10-bit, 2160×3840, 60 fps, HLG, BT.2020, Dolby Vision profile 10.4, with sound. |

Both are HLG, so the problem is not specific to AV1: MPC-HC shows the iPhone's own HEVC file
washed out too.

## Screenshots

`screenshots/` has one PNG per clip × time × player, `<clip>-<player>-<time>.png`:

- **clip:** `mov` or `av1`
- **player:**
  - `browser`: Microsoft Edge (Chromium) playing the clip, the reference for how HLG should look on an SDR screen
  - `mpc-before`: MPC-HC with EVR-CP, setting `ConvertHLGToSDR=0` (the code path from before the change)
  - `mpc-after`: MPC-HC with EVR-CP and the change (setting on, the default)
- **time:** 0.5 s, 1.5 s, 2.5 s (MPC-HC paused and seeked there through its web interface;
  Edge seeked with `currentTime`)

`comparison-mov.png` and `comparison-av1.png` put them side by side: rows are the times,
columns Edge | MPC-HC before | MPC-HC with fix.

Captured on Windows 11, NVIDIA RTX 3060, SDR display, MPC-HC built from the branch (x64 Release).
