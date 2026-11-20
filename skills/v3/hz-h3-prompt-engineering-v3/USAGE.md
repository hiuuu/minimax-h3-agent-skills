# Usage Guide: HZ MiniMax H3 Production Pipeline Prompt Engineer (V3)

## What It Does
Includes everything in V2 plus **Multi-Clip Continuation Handoff Packets** (>15s sequences), a **Dialogue & Lip-Sync Word-Budget Calculator**, and **Platform Input Slot Mapping** (Local Checkpoints / ComfyUI / RunningHub / API).

## Example Prompts

### 1. Multi-Clip Sequence (>15 Seconds)
> Use `hz-h3-prompt-engineering-v3`. I am building a 30-second sequence split into three 10-second clips in Ref2VA. Start with Clip 1 where `<Subject 1>` (`<Picture 1>`) enters an abandoned library at night, and give me the Next-Clip Handoff Packet at the end.

### 2. Lip-Sync & Dialogue Timing Check
> Use `hz-h3-prompt-engineering-v3` in I2VA mode (6 seconds). `<Picture 1>` is an old sailor on a pier. Have him say in Persian: «این دریا هیچ‌وقت چیزی رو پس نمی‌ده، فقط قرض می‌گیره.» Check if the word budget fits 6 seconds.

### 3. ComfyUI / Local Checkpoint Mapping
> Use `hz-h3-prompt-engineering-v3` for a Ref2VA clip combining `<Picture 1>` (character), `<Picture 2>` (environment), and `<Audio 1>` (voice timbre). Show me which asset maps to each reference label and checkpoint.
