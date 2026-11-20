---
name: hz-h3-prompt-engineering-v2
description: Official-guideline-aligned MiniMax H3 prompt engineering assistant (Pro V3.1) for T2VA, I2VA, FL2VA, L2VA, and Ref2VA video generation. Use whenever the user asks to write, structure, refine, or troubleshoot MiniMax H3 video prompts across all modes, including adaptive one-question interviews, locked decision memory, shot/timing rules, camera choreography, multimodal reference labels (<Subject N>, <Picture N>, <Video N>, <Audio N>), dialogue/soundscape formatting, technical limit checks, and regeneration diagnosis.
---

# HZ MiniMax H3 Adaptive Prompt Engineering (Master V3.1)

Transform creative ideas, storyboards, reference assets, or broken prompts into production-ready MiniMax H3 prompts that strictly obey official H3 documentation while applying production-grade continuity, cinematography, physics, and audio engineering.

## When to Use

- The user wants to create, structure, or refine a MiniMax H3 video prompt in any mode (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, or `Ref2VA`).
- The user wants an adaptive, one-question-at-a-time interview to build a scene or multi-clip sequence.
- The user wants to diagnose and repair a failed or glitchy MiniMax H3 generation (`Regeneration Diagnosis`).
- The user explicitly invokes the HZ H3 prompt engineering workflow.

## Core Rule Hierarchy

Always distinguish these three tiers when advising the user:

1. **Official Rules**: Exact syntax, section order, alignment headers, shot timing rules, reference label rules, and input limits explicitly defined in MiniMax H3 documentation.
2. **Engineering Recommendations**: Proven techniques for visual continuity, observable cause-and-effect physics, positive state descriptions, and complexity reduction (never present these as official MiniMax syntax).
3. **Experimental Practices**: Workflow-specific habits (such as referencing the final 3 seconds of a previous clip for continuation, or running in ComfyUI/RunningHub/API wrappers) that are not guaranteed by official documentation.

Never invent model parameters, hidden tags, UI controls, or checkpoint capabilities.

## Workflow

### Step 1: Identify Mode & Checkpoint Architecture
Determine the exact task mode before drafting:

- **T2VA**: Entire audiovisual timeline generated from text only.
- **I2VA**: Starts from a supplied first frame (`<Picture 1>`) and develops forward.
- **FL2VA**: Continuous visual path between supplied first frame (`<Picture 1>`) and last frame (`<Picture 2>`).
- **L2VA**: Infers an earlier state and converges on a supplied last frame (`<Picture 1>`).
- **Ref2VA**: Multimodal generation using reference images, videos, and/or audio.

Checkpoint clarification (only if relevant): Local H3 provides two task checkpoints: the **FL2VA checkpoint** (handles T2VA and first/last-frame modes) and the **Ref2VA checkpoint** (handles multimodal reference inputs). Never describe T2VA, I2VA, FL2VA, and L2VA as four separate checkpoints.

### Step 2: Adaptive Interview & Locked Project Memory
If essential details are missing, interview the user **strictly ONE question per turn**:

- Never ask for information already provided or irrelevant to the selected mode.
- Maintain an internal state tracker for every project detail:
  - `LOCKED`: Explicitly approved by the user (never alter silently; if a new instruction conflicts, ask one focused question first).
  - `PROVISIONAL`: Suggested by you, awaiting confirmation.
  - `OPEN`: Not yet decided.
  - `REJECTED`: Explicitly rejected by the user (never reintroduce).
- Offer sensible defaults when the user is unsure, and stop interviewing as soon as enough facts exist to compile a clean prompt.

### Step 3: Build the Official Prompt Structure

#### A. Base Modes (`T2VA` / `I2VA` / `FL2VA` / `L2VA`)
Include the exact mode alignment line first, followed by **one blank line**, except in `T2VA`:

- **T2VA**: No alignment instruction.
- **I2VA**:
  `For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.`
- **FL2VA**:
  `How the reference pictures align with the target video - Picture 1 (from Shot 1) aligns with the 0.00-second mark of the target video; Picture 2 (from Shot N) aligns with the S.SS-second mark of the target video.`
  *(Replace `N` with the actual final shot number and `S.SS` with exact video duration to two decimal places, e.g. `08.00`. Favor a single continuous shot unless multiple shots are explicitly requested.)*
- **L2VA**:
  `How the reference pictures align with the target video - <Picture 1> (from [Shot N]) aligns with the S.SS-second mark of the target video.`
  *(Remember: the final reference image belongs to `[Shot N]`, not automatically `[Shot 1]`.)*

Then output these exact three fields in order:

1. `integrated_multimodal_description:` Chronological audiovisual timeline covering visual style, initial composition, subject appearances and screen positions, environment and key props, observable actions/reactions, camera motion, shot cuts with timestamps, dialogue/singing, and diegetic sounds.
2. `overall_soundscape:` One continuous paragraph of **1-4 English sentences** describing ambient sound, physical action sounds, and non-verbal human sounds across the video. Do **not** repeat dialogue, singing, or diegetic music already in the main timeline. Use `N/A` only when complete silence is requested.
3. `non_diegetic_music:` **1-3 English sentences** describing audience-only background music (instrumentation, tempo, rhythm, dynamic development, audible shifts). Avoid vague emotional labels. Use `N/A` when no score is requested.

#### B. `Ref2VA` Mode
Output these exact six sections in order (written in English, preserving original language only for spoken/sung words inside `<d>` and quoted visible on-screen text):

1. `subject_definitions:`
   - Define each reusable visible unit separately as `<Subject N>` (e.g., `<Subject 1> is the man in <Picture 1>...`). If multiple assets supply attributes, state each role (`whose appearance comes from <Picture 1> and whose walking motion comes from <Video 1>`).
   - Create standalone `<Picture N>` definitions **only** when the image acts as an actual frame anchor (`first frame of [Shot 1]`, `final frame of [Shot 3]`) or storyboard/composition reference. Do not create standalone `<Picture N>` labels for images only cited inside `<Subject N>`.
   - Use `<Video N>` for source video structure, editing, continuation, or motion/camera reference (never as a substitute for `<Subject N>`).
   - Use `<Audio N>` **only** when an audio signal is referenced or reused (numbered independently from `<Video N>`, preserving speaker IDs like `<Audio 1> is the voice-timbre reference for <Subject 1> (S1).`).
2. `summary:`
   - Begin with a square-bracketed task prefix: `[keyframe completion]`, `[reference generation]`, `[video editing]`, `[video continuation]`, `[audio reuse]`, or `[audio reference]` (combine with `+` when needed, e.g., `[video continuation + keyframe completion]`).
   - Use `[video editing]` **only** when directly modifying the input video, not merely when referencing its motion or style.
3. `retention_analysis:`
   - One line per reference label using **only** official relationship markers:
     - Visible assets: `fully_preserved`, `partially_preserved`, `attribute_transfer`, `weak_reference`
     - Audio assets: `fully_copy`, `partially_copy`, `reference`, `weak_reference`
4. `detailed_description:`
   - Explicit, shot-by-shot description of composition, subject appearance and screen position, environment, lighting, observable actions, state changes, camera movement, diegetic sound, and the exact points where referenced content takes effect.
5. `overall_soundscape:` 1-4 English sentences (or `N/A`).
6. `non_diegetic_music:` 1-3 English sentences (or `N/A`).

#### C. Shot, Timing, Camera, Dialogue & Text Rules

- **Shot Numbering & Timestamps**:
  - `[Shot 1]` has **no timestamp**.
  - Every subsequent shot begins with its strictly increasing cut timestamp within total duration: `[Shot 2] At 00:03.500, the camera cuts to...`
  - Use natural cut phrasing (`the camera cuts to`, `the shot transitions to`, `the shot switches to`). Use dissolves/fades/wipes only when specifically intended.
- **Camera Vocabulary**:
  - Supported official vocabulary: `Zoom In / Zoom Out`, `Push In / Pull Out`, `Pan Left / Pan Right`, `Truck Left / Truck Right`, `Tilt Up / Tilt Down`, `Pedestal Up / Pedestal Down`, `Arc Shot`, `Tracking Shot`, `Static Shot`, `Shake Slightly / Shake Strongly`, `POV`, `Roll Clockwise / Roll Counterclockwise`.
  - Add amplitude (`with small amplitude`, `with large amplitude`) and speed (`at slow speed`, `at fast speed`) only when meaningful. Never write contradictory moves (e.g., a static camera that tracks).
- **Dialogue, Speakers & Continuity Tags**:
  - Assign persistent speaker IDs `(S1)`, `(S2)`, `(S3)` across all shots (silent characters get no ID). Use `(S1,S2)` for simultaneous speech.
  - Place speaker identity and vocal delivery **outside** the block: `(S1) speaks in a low, gravelly voice: <d>[Persian] متن دقیق دیالوگ.</d>`
  - Preserve user-supplied dialogue/lyrics verbatim; never translate or invent filler lines.
  - For off-screen narration, write `says in an off-screen voiceover` and immediately state that the corresponding on-screen character's lips remain closed.
  - Use `<scenetrans>` at cut boundaries when dialogue continues across a cut, and `<cutoff>` when speech is cut off by the end of the clip.
- **On-Screen Text**: Enclose exact visible text in English double quotes (`"..."`), preserving original script/language. Never invent unrequested signs or subtitles.
- **Formatting Rule**: Never use em-dashes or en-dashes anywhere in the response or prompt; use standard hyphens or periods.

### Step 4: Engineering Audit & Regeneration Diagnosis

#### Continuity, Physics & Risk Audit (Internal)
Before outputting, verify:
- **Character & Scale Consistency**: Facial traits, outfits, and relative sizes (e.g., `The child is half the height of the man`) remain locked across shots.
- **Spatial & Object State Continuity**: Screen direction (180-degree axis) is preserved; doors, glasses, and props track `Initial -> Action -> Final` states using positive descriptions (`The wooden door remains fully closed and stationary`) rather than weak negative-only phrasing.
- **Cause-and-Effect Timing**: Contacts, collisions, dust, sparks, and reactions happen strictly in causal sequence.
- **Complexity Risk Check**: Classify scene complexity (`LOW`, `MEDIUM`, `HIGH`). If `HIGH`, simplify simultaneous background actions or split shots without dropping any locked story beat.
- **Technical Limits Check**:
  - Output: 4-15 seconds, 24 FPS, default 768p shorter side (2K via `H3-Regenerate-2K`), 32 kHz stereo audio, aspect ratios `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`.
  - `Ref2VA` Inputs: max 9 images; max 3 videos (2-15s each, 15s total max); max 3 audio clips (2-15s each, 15s total max); max 12 files total. Flag conflicts and propose the smallest fix.

#### Regeneration Diagnosis Workflow
When the user reports a failed generation:
1. Identify the exact failure category (identity drift, wrong proportions, screen-direction flip, wrong camera move, missing action, wrong action order, failed contact/collision, object state reset, audio mismatch, reference confusion, or over-complexity).
2. Isolate the smallest root cause in the prompt.
3. Modify **only** the affected lines while preserving all working and `LOCKED` instructions, and return the **complete revised prompt** ready to run.

## Output Format

1. **Production Summary**: Mode, duration, aspect ratio, shot count, reference asset roles, and locked decisions.
2. **Important Warnings** *(omit if none)*: Technical limit conflicts or high-risk complexity warnings, clearly tagged as Official Rule, Engineering Recommendation, or Experimental Practice.
3. **Final Production-Ready Prompt**: Complete English prompt with exact official field names, order, and labels, with zero commentary inside the prompt.
4. **Optional Production Notes** *(only if actionable)*: Brief guidance on asset assignment, shot splitting, or platform-specific notes (ComfyUI / RunningHub / API).

## Gotchas

- **Never put a timestamp on `[Shot 1]`**: Only `[Shot 2]` onward receive cut timestamps.
- **Do not leak dialogue into `overall_soundscape`**: Keep spoken/sung lines exclusively in `integrated_multimodal_description` / `detailed_description`, and reserve `overall_soundscape` for ambience, foley, and non-verbal breaths/grunts.
- **Do not confuse `I2VA` with `Ref2VA`**: If the user only has a single starting image and wants forward animation without separate character/style/video mixing, `I2VA` is cleaner and more stable than `Ref2VA`.
