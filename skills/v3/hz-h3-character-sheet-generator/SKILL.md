---
name: hz-h3-character-sheet-generator
description: Generates specialized multi-view character reference sheets for MiniMax H3 (Ref2VA), p-h3, Pika, and Omni Flash across 5 structured layouts (Omni Flash 2-panel close-up + full-body, H3 Master Triad with macro texture grid, Full-Body Turnaround + Multi-Angle Heads, 10-Expression Emotion Grid, and Annotated Production Model Sheet). Includes a toggleable face-masking optimization (ON by default on full-body views) so video models anchor facial identity strictly from high-resolution close-ups without low-res face distortion.
---

# HZ MiniMax H3 & Omni Flash Character Sheet Generator

Design production-ready character reference sheets optimized for image-to-video and multimodal reference pipelines (**MiniMax H3 `Ref2VA`**, **p-h3**, **Pika**, and **Omni Flash**). Instead of generic turnaround prompts that cause facial distortion or text-bleeding in video generation, this skill enforces clean studio geometry, zero unwanted labels, and **Face-Masked Full-Body Anchors** by default.

## When to Use

- The user wants to create a character sheet, turnaround sheet, expression sheet, or model sheet for **MiniMax H3**, **p-h3**, **Pika**, or **Omni Flash**.
- The user wants to convert an existing character portrait or description into one of the **5 specialized reference sheet layouts**.
- The user wants full-body turnaround views with **masked-out faces** (replaced by a solid background-colored oval) so the video model pulls facial identity exclusively from high-resolution close-ups.

## The 5 Character Sheet Layouts

Consult `references/sheet_blueprints.md` for exact grid proportions and copy-ready prompt templates:

1. **Type 1: Omni Flash & H3 Rapid Identity Sheet (`omni-rapid`)**
   - **Layout**: 16:9 two-panel split. Left half = high-resolution head-and-shoulders close-up portrait; Right half = single full-body standing figure (**3/4 Front View** by default for maximum depth + outfit coverage, or **Direct Front View** if symmetrical chest logos/patterns matter).
   - **Why it works**: Gives `Omni Flash` and `H3 Ref2VA` maximum pixel density on the face while keeping a clean, uncluttered full-body silhouette.
2. **Type 2: H3 Master Triad Sheet (`h3-master-triad`)**
   - **Layout**: 16:9 three-zone layout. Left = large head-and-shoulders portrait; Center = 3 full-body turnaround views (Front, Side Profile, Back); Right = 2x3 grid of 6 extreme macro detail crops (eye, nose, mouth, ear, hair/fur, and fabric/material weave).
   - **Why it works**: Ideal for `H3 Ref2VA` (`<Picture 1>`) where close-up shots need pores, iris detail, and fabric weave fidelity.
3. **Type 3: Full-Body Turnaround + Multi-Angle Heads (`full-turnaround-heads`)**
   - **Layout**: 16:9 two-row layout. Top row = 5 full-body views (Front, 3/4 Front, Right Side, Back, Left Side); Bottom row = 3 large head-and-shoulders close-ups (Front, 3/4 Front, Side Profile).
   - **Why it works**: Prevents side-profile hallucination during camera orbits or profile dialogue shots in `H3 Ref2VA` and `Pika`.
4. **Type 4: 10-Expression & Lip-Sync Emotion Grid (`expression-grid`)**
   - **Layout**: 16:9 symmetrical 2x5 grid of 10 chest-up portraits (`Happy`, `Surprised`, `Angry`, `Sad`, `Wink`, `Sleepy`, `Smug`, `Goofy`, `Disgusted`, `Terrified`).
   - **Why it works**: Supplies emotional range and mouth shapes for dialogue and `<Audio 1>` singing/lip-sync clips.
5. **Type 5: Annotated Production Model Sheet (`production-bible`)**
   - **Layout**: 16:9 four-row production bible with title header, `TURNAROUND` (4 views + height guide lines), `HEAD CLOSE-UPS` (6 expressions), `WARDROBE EVOLUTION` (`W1`-`W6`), and `HANDS & ACTIONS` vignettes.
   - **Why it works**: Best for 2D animation bibles, storyboard planning, and client approvals.

## Core Optimization Rules

1. **Full-Body Face-Masking Optimization (`face_mask_mode` — ON by Default for Types 1, 2, 3)**:
   - **The Problem**: In a 16:9 multi-figure turnaround, each full-body head is only ~60-90 pixels tall. Multimodal encoders (`H3 Ref2VA` and `Omni Flash`) average the blurry full-body face with the sharp close-up face, degrading facial likeness.
   - **The Fix**: By default, instruct the image generator to cleanly mask out the facial features inside the head contour of all full-body figures using a smooth, solid oval matching the exact background color (`while keeping hair, ears, neck, and head silhouette intact`).
   - **User Option**: Always inform the user that **Face-Masking is ON by default** for Types 1-3 and offer to turn it **OFF** if they want visible faces on the full-body figures.
2. **Zero Text Labels on AI Reference Sheets (Types 1-4)**:
   - Never add text headers, angle captions (`FRONT`, `SIDE`), or borders to Types 1-4 unless explicitly requested, because video models can hallucinate floating text onto the background or clothing. Reserve text labels strictly for Type 5 (or optional captions in Type 4).
3. **Neutral Studio Lighting & Solid Backdrop**:
   - Always specify `flat, even, shadowless studio lighting` on a uniform solid background (`off-white`, `light neutral gray`, or `dark slate` for bright characters) so directional shadows do not conflict with target video scenes.
4. **H3 `Ref2VA` Integration Ready**:
   - Whenever generating a sheet for MiniMax H3, also provide the ready-to-paste `subject_definitions:` snippet showing how to reference the generated sheet cleanly as `<Picture 1>` (never as a frame-0 anchor, since a multi-view sheet is a character design reference).
5. **Clean Punctuation**: Never use em-dashes or en-dashes anywhere in the prompt or output; use standard hyphens or periods.

## Workflow

### Step 1: Identify Sheet Type, Character Source & Options
Check what the user has provided:
- **Character Input**: New text description OR an attached reference image (`<Picture 1>`) to expand into a sheet.
- **Target Sheet Type**: Type 1 (`omni-rapid`), Type 2 (`h3-master-triad`), Type 3 (`full-turnaround-heads`), Type 4 (`expression-grid`), or Type 5 (`production-bible`). If unspecified, recommend the best match or ask **one concise question**.
- **Optional Settings (Confirm or Apply Defaults)**:
  - `face_mask_mode`: **ON (Default)** for Types 1-3 / **OFF** (visible faces on full-body views).
  - For Type 1 (`omni-rapid`): **3/4 Front Full-Body (Default)** vs. **Direct Front Full-Body**.
  - Background color: `light neutral gray` / `off-white` (or `dark slate` for light/white characters).

### Step 2: Build the Image Generation Prompt
1. Pull the exact structural template from `references/sheet_blueprints.md`.
2. Inject concrete visual anchors (exact hair/fur, eye color, facial structure, outfit layers, footwear, color palette, and art style: photorealistic 8K studio photo, stylized 3D PBR render, or clean 2D cel-shaded art).
3. Apply the `face_mask_mode` clause cleanly if `ON` (specifying the exact background color for the smooth oval mask so there is zero color mismatch).
4. Enforce `16:9` aspect ratio and `zero text, no labels` (for Types 1-4).

### Step 3: Deliver Prompt + H3 / Omni Flash Usage Note
Output:
1. **Sheet Configuration Summary**: Selected Layout Type (1-5), Aspect Ratio (`16:9`), Face-Masking status (`ON` / `OFF`), and Recommended Generator (`p-h3`, `Pika`, `Omni Flash`, `Nano Banana`).
2. **Production Image Prompt**: Complete, ready-to-paste English prompt.
3. **H3 `Ref2VA` Wiring Snippet**: Exact `subject_definitions:` block so the user can immediately plug the resulting sheet into MiniMax H3 without triggering frame-0 pose morphing.

## Gotchas

- **Match Mask Oval Color to Background Color**: If the sheet background is `#E8E8E8` (light neutral gray), explicitly describe the face mask oval as `matching the exact light neutral gray background color` so the generator does not draw a bright white sticker on a gray sheet.
- **White/Pale Characters Need a Medium-Dark Backdrop**: If the character has white fur, white hair, or white clothing, switch the sheet background (and matching face-mask oval) to `medium neutral gray` or `muted slate gray` so silhouettes never clip into the background.
- **Do Not Use Multi-View Sheets as `I2VA` First Frames**: Remind the user that character sheets belong in `Ref2VA` (`subject_definitions:`) or `Omni Flash` character reference slots, never as frame 0 of `I2VA`.
