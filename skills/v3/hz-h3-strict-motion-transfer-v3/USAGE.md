# Usage Guide: HZ MiniMax H3 Strict Motion Transfer (V3 Production Pipeline)

## What It Does
Builds on V2 with **Hybrid Lock Modes** (Full-Body Lock vs. Body-Only Lock + `<Audio 1>` Lip-Sync), **Cross-Species Weight/Momentum Calibration**, and **Multi-Clip Continuation Handoff Packets** for >15s reference videos.

## Example Prompts

### 1. Hybrid Body Motion + Audio Lip-Sync Swap
> Use `hz-h3-strict-motion-transfer-v3` in Mode B (Hybrid Body Lock + Audio Sync). Replicate the exact stage gestures and body groove from `<Video 1>` (12 seconds) onto `<Subject 1>` (`<Picture 1>`), while driving mouth lip-sync and facial expression from `<Audio 1>`.

### 2. Multi-Clip Motion Transfer (>15 Seconds)
> Use `hz-h3-strict-motion-transfer-v3`. My reference dance video is 28 seconds long. Help me split it into two 14-second Ref2VA prompts for `<Subject 1>` (`<Picture 1>`) with a Next-Clip Handoff Packet between Clip 1 and Clip 2.
