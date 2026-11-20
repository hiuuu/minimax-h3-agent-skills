---
name: hz-h3-strict-motion-transfer
description: Generate strict, literal MiniMax H3 Ref2VA motion transfer and character-swap prompts from a reference video (<Video 1>) and target identity/environment image (<Picture 1>) without creative reinterpretation, invented actions, or unprompted camera movement. Use whenever the user asks for MiniMax H3 motion transfer, video character replacement, dance/pose transfer, or strict movement replication from a reference clip.
---

# HZ MiniMax H3 Strict Motion Transfer (Pro Production Edition)

Generate production-ready MiniMax H3 `Ref2VA` prompts engineered specifically for frame-accurate motion transfer, subject replacement, and multi-shot video replication. This skill eliminates common generative video failure modes, including pose morphing from static reference images, anatomical hallucinations, edge bleeding on chroma backdrops, and unprompted camera drift, by strictly locking temporal, spatial, and camera behavior to `<Video 1>` while isolating visual identity and environment assets.

## When to Use

- The user wants to transfer motion, dance, gestures, facial performance, or combat movement from a reference video (`<Video 1>`) onto a target character (`<Picture 1>`).
- The user wants to replace a performer and/or background in an existing clip using MiniMax H3 `Ref2VA` with zero creative embellishment.
- The user asks for literal, non-creative H3 motion replication, video character swap, or multi-cut reference video replication.

## Core Rules & Bug-Prevention Architecture

1. **Strict `Ref2VA` Mode & Exact Section Order**: Always use the exact 6-section `Ref2VA` structure in English:
   - `subject_definitions:`
   - `summary:`
   - `retention_analysis:`
   - `detailed_description:`
   - `overall_soundscape:`
   - `non_diegetic_music:`
2. **Prevent the "Frame-0 Pose Morph" Bug**: Never declare `<Picture 1>` as a first-frame anchor in `detailed_description` unless the character in `<Picture 1>` is literally standing in the exact frame-0 pose of `<Video 1>`. If `<Picture 1>` is an A-pose, T-pose, portrait, or turnaround sheet, cite `<Picture 1>` **only** inside `subject_definitions:` so H3 extracts appearance without warping the opening frames to match the static image's posture.
3. **Zero Creative Interpretation**: Explicitly forbid adding gestures, secondary poses, introductory/ending beats, fades, slow-motion ramps, or unprompted camera moves (such as cinematic push-ins, orbits, or zooms) not present in `<Video 1>`.
4. **Anatomical, Proportion & Cross-Species Mapping**:
   - **Human-to-Human / Stylized Humanoid**: Map head tilt, shoulder line, elbow/wrist flexion, hip rotation, knee bend, and foot placement directly. Preserve target character proportions (e.g., stocky build, chibi head ratio, armor bulk) without stretching limbs to match a slender human performer.
   - **Human-to-Animal / Creature**: Map limbs explicitly (human arms to front legs/paws; human legs/steps to hind legs; human head turns to animal head/muzzle orientation) and forbid anthropomorphic distortions (no human hands/fingers, no human mouth/teeth morphs, no unprompted clothing).
   - **Secondary Physics Lock**: Hair, fur, ears, tails, capes, and loose clothing may move **only** as passive physical consequences of the replicated motion, never initiating independent actions.
5. **Clean Asset Separation**:
   - `<Subject 1>`: Target performer identity, face/head structure, proportions, textures/fur/skin, and outfit from `<Picture 1>` (or multiple reference angles `<Picture 1>`, `<Picture 2>` if provided).
   - `<Subject 2>` (when replacing background): Exact environment or solid backdrop (e.g., solid chroma green screen or studio wall) sourced from its image.
   - `<Video 1>`: Motion, pose sequence, timing, screen position, occlusions, and camera movement reference.
   - `<Audio 1>` (only if audio is explicitly requested): Original audio signal (`fully_copy` or `reference`).
6. **Multi-Cut Reference Video Handling**: If `<Video 1>` is a single continuous shot, write `[Shot 1]` with no timestamp. If `<Video 1>` contains hard cuts that must be preserved, mirror the exact cut timestamps (`[Shot 2] At 00:SS.mmm, the camera cuts to...`) and explicitly state in `summary:` that the cut structure of `<Video 1>` is preserved.
7. **Punctuation & Clean Syntax**: Never use em-dashes or en-dashes anywhere in the prompt or output; use standard hyphens or periods.

## Workflow

### Step 1: Audit Inputs & Ask Only What Is Missing (Max 1 Question)
Inspect the user's message. If critical parameters are missing, ask **one concise, combined question** covering only what is unknown:
- **Target Subject (`<Picture 1>`)**: Who/what replaces the performer (human, stylized character, animal), and is `<Picture 1>` a neutral character sheet or already aligned with frame 0?
- **Environment & Edge Control**: Keep `<Video 1>`'s background, replace with `<Picture 1>`'s solid/chroma backdrop, or use a separate background image (`<Picture 2>`)?
- **Clip Specs & Audio**: Confirm duration (must be 2-15s for H3 `Ref2VA`), whether `<Video 1>` has internal cuts, and whether audio is `N/A` or copied from `<Audio 1>`.

If the user already provided enough context, skip questioning and build the prompt directly.

### Step 2: Construct the 6-Section Prompt

Follow this exact blueprint:

1. **`subject_definitions:`**
   - `<Subject 1>` is the [character/creature description] from `<Picture 1>`, preserving [facial structure, eyes, hair/fur, body proportions, clothing, and distinctive accessories].
   - `<Subject 2>` (if replacing background) is the [exact environment / solid chroma green backdrop] from `<Picture 1>` (or `<Picture 2>`).
   - `<Video 1>` is the motion reference providing the performer's choreography, pose sequence, movement timing, screen position, and camera motion.
   - `<Audio 1>` (only if requested) is the audio track from `<Video 1>` to be preserved/referenced.

2. **`summary:`**
   - Begin with `[video editing]`.
   - State clearly that the target video is an edited version of `<Video 1>`, replacing the original performer with `<Subject 1>` (and replacing the original environment with `<Subject 2>` if applicable), replicating the reference performance frame-accurately with no newly invented motion or camera additions.

3. **`retention_analysis:`**
   - List every active reference label using exact official markers (`fully_preserved`, `partially_preserved`, `attribute_transfer`, `weak_reference` for visuals; `fully_copy`, `partially_copy`, `reference`, `weak_reference` for audio):
     - `<Subject 1> (appears in [Shot 1]): partially_preserved` - preserve identity, facial features, textures, and proportions while adapting posture and limb positions to replicate `<Video 1>`.
     - `<Subject 2> (appears in [Shot 1]): fully_preserved` - preserve the exact backdrop appearance and uniform lighting.
     - `<Video 1> (appears in [Shot 1]): attribute_transfer` - replicate pose sequence, movement timing, directional changes, screen position, and camera motion frame-accurately with zero embellishment.

4. **`detailed_description:`**
   - **Opening Paragraph (Style & Asset Lock)**: Establish visual realism/style, lighting consistency, and state that `<Video 1>` is the sole source of motion, timing, and camera behavior.
   - **`[Shot 1]` (No timestamp on Shot 1)**:
     - **Pose, Trajectory & Timing Lock**: Require frame-by-frame correspondence in pose, limb placement, joint angles, body orientation, facing direction, screen coordinates, holds, weight shifts, acceleration, deceleration, and stillness.
     - **Anatomical & Proportion Lock**: Detail exact limb mapping (especially for cross-species or stylized proportions), forbid anatomical hallucinations, and restrict hair/fur/clothing motion strictly to passive physical reaction.
     - **Occlusion & Self-Contact Handling**: Specify that when limbs cross in front of the torso or face in `<Video 1>`, `<Subject 1>`'s corresponding limbs maintain clean depth ordering without merging or disappearing.
     - **Camera & Framing Lock**: Replicate `<Video 1>`'s exact framing, focal perspective, tracking, or stillness with zero added push-ins, zooms, orbits, or reframing.
     - **Environment & Silhouette Separation**: Describe the target background (`<Subject 2>` or preserved `<Video 1>` scene) and require crisp edge separation (especially around fine hair, fur, or chroma key boundaries) with no stray props, text, or extra subjects.
     - **Ending Lock**: End on the exact final pose and screen position of `<Video 1>` with no extra outro beat, hold extension, or fade.

5. **`overall_soundscape:`**
   - Output `N/A` unless ambient or physical action sounds are specifically requested.

6. **`non_diegetic_music:`**
   - Output `N/A` unless background music is specifically requested.

### Step 3: Pre-Delivery Audit
Before outputting the prompt:
- Confirm duration is within **2-15 seconds** (`Ref2VA` official limit: max 3 videos, max 15s total video duration, max 9 images, max 12 files total).
- Verify no `<Picture N>` is mistakenly treated as `[Shot 1]` frame 0 unless explicitly confirmed by the user.
- Check that every label in `subject_definitions:` appears identically in `retention_analysis:` and `detailed_description:`.

## Gotchas

- **Chroma Green / Solid Backdrop Spill**: When replacing a real room in `<Video 1>` with a solid chroma green backdrop (`<Subject 2>`), explicitly instruct H3 to keep even studio lighting on the backdrop and crisp edge separation on hair/fur so shadows or floor reflections from `<Video 1>` do not bleed onto the green screen.
- **Scale Mismatch**: If `<Subject 1>` is much shorter or bulkier than the human in `<Video 1>`, state whether `<Subject 1>` should match the human's vertical screen height or keep its natural proportions centered on the human's hip/foot anchor point.
- **Duration Over 15 Seconds**: MiniMax H3 `Ref2VA` caps reference video duration at 15 seconds. If the user's clip is longer, instruct them to split it into <=15s segments and maintain continuity between clips.
