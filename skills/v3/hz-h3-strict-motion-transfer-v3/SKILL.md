---
name: hz-h3-strict-motion-transfer-v3
description: Production-pipeline MiniMax H3 Ref2VA motion transfer and character-swap director (V3). Replicates choreography, timing, and camera movement from <Video 1> onto <Subject 1> (<Picture 1>) with zero creative drift, adding hybrid body-only vs full-body lock modes, cross-species momentum calibration, and multi-clip continuation handoff packets. Use whenever the user asks for MiniMax H3 motion transfer, video character replacement, dance/pose replication, or multi-clip character-swap sequences.
---

# HZ MiniMax H3 Strict Motion Transfer (V3 Production Pipeline)

Generate frame-accurate MiniMax H3 `Ref2VA` motion transfer prompts engineered for both single-clip character swaps and multi-clip production pipelines. V3 eliminates frame-0 pose morphing, chroma bleed, and cross-species limb stretching while supporting **Full-Body Strict Lock** and **Hybrid Body-Lock + Facial/Audio Performance** modes.

## When to Use

- The user wants to transfer motion, dance, gestures, or performance from `<Video 1>` onto a target subject (`<Picture 1>`) in MiniMax H3 `Ref2VA`.
- The user wants to replace a performer and/or background with zero invented actions or unprompted camera movement.
- The user wants a hybrid swap (strict body motion from `<Video 1>`, but facial expression or lip-sync driven by `<Audio 1>` or a specified vocal performance).
- The user is transferring motion across a multi-clip sequence (>15 seconds split into <=15s chunks).

## Core Architecture & Lock Modes

1. **Strict `Ref2VA` 6-Section Structure**: Always output these exact six sections in English in this exact order:
   - `subject_definitions:`
   - `summary:`
   - `retention_analysis:`
   - `detailed_description:`
   - `overall_soundscape:`
   - `non_diegetic_music:`
2. **Choose the Transfer Lock Mode**:
   - **Mode A - Strict Full-Body & Face Lock (Default)**: Replicates head orientation, facial timing, limb placement, body posture, and camera motion 1:1 from `<Video 1>`.
   - **Mode B - Hybrid Body Lock + Facial/Audio Sync**: Replicates torso, limb trajectory, footwork, and camera motion 1:1 from `<Video 1>`, while driving mouth articulation and facial expression from `<Audio 1>` (useful for singing/lip-sync swaps where `<Video 1>` has the dance/body groove and `<Audio 1>` has the vocal track).
3. **Prevent Frame-0 Pose Morphing**: Never declare `<Picture 1>` as a first-frame anchor in `detailed_description` unless `<Picture 1>` already matches frame 0 of `<Video 1>`. Cite `<Picture 1>` solely in `subject_definitions:` when it is a neutral A-pose, T-pose, portrait, or character turnaround sheet.
4. **Cross-Species & Weight/Momentum Calibration**:
   - Map limbs explicitly when anatomy differs (human arms -> front legs/paws; human legs -> hind legs; human head turns -> muzzle/head orientation) and forbid anatomical hallucinations (no human hands, teeth, or unprompted clothing).
   - **Heavy vs. Agile Calibration**: If `<Subject 1>` is heavy/bulky (e.g., bear, armored knight, stocky character) replicating an agile human in `<Video 1>`, preserve the exact start/stop timestamps of `<Video 1>` while keeping `<Subject 1>`'s solid mass and grounded foot contact without stretching limbs.
   - Restrict hair, fur, ears, tails, and garments strictly to passive secondary physics.
5. **Clean Punctuation**: Never use em-dashes or en-dashes anywhere in the prompt or output; use standard hyphens or periods.

## Workflow

### Step 1: Audit Inputs (Max 1 Focused Question)
Check what the user has provided. Ask **one concise question** only if critical details are missing:
- **Target Subject (`<Picture 1>`)**: Who/what replaces the performer, and is `<Picture 1>` a character sheet/portrait or already aligned with frame 0?
- **Transfer Mode & Environment**: Full-body strict lock or hybrid body + `<Audio 1>` lip-sync? Keep `<Video 1>` background or replace with `<Picture 1>`/`<Picture 2>` (e.g., solid chroma green)?
- **Duration & Multi-Clip Split**: Confirm duration (2-15s per clip for `Ref2VA`) and whether this is part of a longer multi-clip sequence.

### Step 2: Build the 6-Section Prompt

1. **`subject_definitions:`**
   - `<Subject 1>`: Complete visual identity, facial structure, proportions, textures/fur/skin, and outfit from `<Picture 1>`.
   - `<Subject 2>` (if replacing background): Exact environment or solid chroma backdrop from `<Picture 1>` or `<Picture 2>`.
   - `<Video 1>`: Explicitly define `<Video 1>` as the motion reference supplying choreography, pose sequence, movement timing, screen position, and camera motion.
   - `<Audio 1>` (only if audio/lip-sync is used): Define whether `<Audio 1>` is copied (`fully_copy`) or referenced (`reference`) and link speaker ID `(S1)` if vocalizing.

2. **`summary:`**
   - Begin with `[video editing]` (or `[video editing + audio reuse]` if `<Audio 1>` is copied).
   - State clearly that the target video edits `<Video 1>` by replacing the performer with `<Subject 1>` (and replacing the environment with `<Subject 2>` if applicable), replicating movement frame-accurately with zero invented actions or camera moves.

3. **`retention_analysis:`**
   - One line per active reference label using official H3 markers (`fully_preserved`, `partially_preserved`, `attribute_transfer`, `weak_reference` for visuals; `fully_copy`, `partially_copy`, `reference`, `weak_reference` for audio).

4. **`detailed_description:`**
   - **Style & Asset Lock**: Establish photorealism or target art style, consistent lighting, and `<Video 1>` as the sole movement/camera source.
   - **`[Shot 1]` (No timestamp on Shot 1; mirror exact cut timestamps only if `<Video 1>` contains hard cuts)**:
     - **Pose, Trajectory & Timing Lock**: Frame-by-frame correspondence in joint angles, limb placement, body orientation, facing direction, screen position, holds, weight shifts, acceleration, deceleration, and stillness.
     - **Anatomy, Scale & Depth Ordering**: Explicit limb mapping, target proportion lock, and clean depth ordering when limbs pass in front of the torso/face.
     - **Camera & Framing Lock**: Exact replication of `<Video 1>`'s framing, lens perspective, tracking, or static hold without added zooms, push-ins, or orbits.
     - **Environment & Chroma Edge Separation**: Clean silhouette and hair/fur edge separation against `<Subject 2>` without shadow/color spill from `<Video 1>`.
     - **Ending Lock**: End on the exact final pose and screen position of `<Video 1>` with no extra outro beat or fade.

5. **`overall_soundscape:`** `N/A` unless ambient/action foley is requested.
6. **`non_diegetic_music:`** `N/A` unless score is requested.

### Step 3: Output + Next-Clip Handoff (If Multi-Clip)
Deliver:
1. **Production Summary** (Lock Mode, duration, aspect ratio, input slot mapping).
2. **Final Production-Ready Prompt** (clean English, zero internal commentary).
3. **Next-Clip Handoff Packet** *(include whenever the user is building a >15s sequence)*: Exact ending pose, screen coordinates, and lighting state so the next <=15s segment continues seamlessly.

## Gotchas

- **Do not use `<Picture 1>` as a first-frame anchor** unless frame 0 of `<Video 1>` matches `<Picture 1>`'s exact pose.
- **Keep total video reference duration <=15 seconds**: If `<Video 1>` is 30 seconds, instruct the user to split it into two 15-second clips (`Clip 1: 00:00-00:15`, `Clip 2: 00:15-00:30`) and generate them sequentially.
