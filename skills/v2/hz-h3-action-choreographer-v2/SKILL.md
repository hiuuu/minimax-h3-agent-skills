---
name: hz-h3-action-choreographer-v2
description: Cinematic combat and action choreography director (Pro Edition) for MiniMax H3 video generation across live-action, anime, 2D cartoon, and stylized 3D styles. Use whenever the user asks to design, browse, select, or write MiniMax H3 prompts for fight scenes, sword duels, martial arts, hand-to-hand fistfights, gunfights (pistols, rifles, submachine guns, shotguns), heavy melee weapons, magic/supernatural clashes, or war/battle sequences. Presents structured, selectable attack-and-defense choreography exchanges before compiling official MiniMax H3 prompts.
---

# HZ MiniMax H3 Action & Combat Choreographer (Pro Combat Director)

Design cinematic, physically readable combat choreography for MiniMax H3 across live-action, anime, 2D cartoon, and stylized 3D productions. Instead of writing vague "they fight" lines, present curated, categorized attack-and-defense exchanges for the user to choose from, enforce strict weapon/spatial continuity so limbs and blades do not morph, and compile the approved sequence into an official MiniMax H3 prompt.

## When to Use

- The user asks for an action, duel, brawl, shootout, or battle scene for MiniMax H3.
- The user names a weapon or combat style (katana, longsword, dual daggers, fistfight/martial arts, pistol/gun-fu, SMG, assault rifle, shotgun, spear, axe/shield, anime energy clash, cartoon slapstick brawl, or 3D stylized combat).
- The user wants selectable choreography options (how Fighter A attacks, how Fighter B defends/counters, and how the camera frames the impact) before generating the final prompt.

## Core Combat Engineering Principles

1. **Interactive Choreography Menu First**: Whenever a user requests a fight category without locking exact moves, present **3 to 5 distinct, cinematic choreography beats** (Attack -> Defense/Counter -> Physical Consequence + Camera) so the user can pick one or combine them.
2. **4-Stage Observable Cause-and-Effect Physics**: Never use abstract summaries like "they exchange blows." Break every beat into:
   - **Telegraph / Initiation**: Stance shift, foot pivot, grip adjustment, or weapon draw.
   - **Attack Trajectory**: Exact strike angle, limb/muzzle direction, and target zone.
   - **Defense / Evasion**: Exact parry angle, slip direction, duck, cover dive, or shield block.
   - **Contact & Aftermath**: Sparks, muzzle flash, brass ejection, dust shockwave, recoil, or stagger occurring strictly **after** contact.
3. **Anti-Morphing & Spatial Lock Rules (Critical for Video Models)**:
   - **Beat Budget per Duration**: Limit a 5-8 second clip to **1-2 clean exchanges**, and a 10-15 second clip to **2-3 exchanges** with clear 0.5-second holds/resets. Overloading a short clip with rapid flurries causes limb tangling and rubbery blades.
   - **Screen Direction & 180-Degree Axis**: Lock Fighter A on screen-left attacking rightward and Fighter B on screen-right defending leftward (or vice versa) across cuts unless a deliberate camera orbit is described.
   - **Weapon Geometry & Grip Lock**: Explicitly state blade length, one-handed vs. two-handed grip, and firearm firing mode (single semi-auto shots vs. short controlled bursts) so weapons retain rigid geometry mid-motion.
4. **Medium-Adapted Action Grammar**:
   - **Live-Action Photorealistic**: Authentic gravity, footwork weight, firearm recoil, muzzle flash illumination, and grounded tracking/handheld camera.
   - **2D Anime / Sakuga**: Snappy anticipation poses, explosive burst acceleration, brief high-contrast impact frames at strike contact, compressed air rings, and dramatic foreshortening.
   - **Western 2D Cartoon**: Clear silhouette anticipation, snappy smear frames on fast swings, squash-and-stretch impact reactions, and readable comedic or heroic beats.
   - **Stylized 3D**: Fluid pose-to-pose arcs, PBR metallic/energy reflections, sharp rim lighting separating silhouettes, and kinetic camera push-ins.
5. **Strict MiniMax H3 Compliance**: Compile final prompts using exact official H3 syntax (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, or `Ref2VA`), zero timestamp on `[Shot 1]`, strictly increasing timestamps on later cuts, separated diegetic/soundscape/music fields, and no em-dashes or en-dashes.

## Workflow

### Step 1: Identify Discipline, Visual Style & H3 Mode
Check what the user has already specified:

- **Combat Discipline**: Bladed Weapons, Unarmed/Martial Arts, Firearms (Pistol/SMG/Rifle/Shotgun), Polearms/Heavy Melee, Magic/Energy Clashes, or Cartoon Slapstick.
- **Visual Medium**: Live-Action, 2D Anime, Cartoon, or Stylized 3D.
- **H3 Task Mode**: `T2VA`, `I2VA` (first frame supplied), `FL2VA` (first & last frame), `L2VA` (last frame), or `Ref2VA` (character/style/video/audio references).

Consult `references/combat_choreography_catalog.md` to select and adapt discipline-specific attack-defense-counter patterns.

### Step 2: Present Selectable Choreography Beats
Before writing the final H3 prompt (unless the user already gave move-by-move choreography), present **3 to 5 tailored combat options** matching their weapon and visual medium:

For each option, clearly lay out:
- **Option Name & Tone** (e.g., *Option 1: Diagonal Cleave into Cross-Guard Parry & Riposte - Tense & Technical*)
- **Attacker Move**: Exact strike, combo, or firing burst.
- **Defender Counter**: Exact parry, slip, cover dive, or counter-attack.
- **Physical Consequence**: Sparks, shell casings, dust/shockwave, and ending stance.
- **Recommended H3 Camera**: Official H3 camera move, speed/amplitude, and shot size.

Then ask **one concise follow-up** inviting the user to choose/combine options and confirm any missing H3 essentials (duration 4-15s, aspect ratio, and whether they have reference images/frames).

### Step 3: Compile the Final MiniMax H3 Prompt
Once the user selects their choreography:

1. **Lock Character & Spatial Anchors**: Keep character outfits, weapon hands, relative scale, and screen positions consistent across every shot.
2. **Apply Exact Official H3 Structure**:
   - **T2VA / I2VA / FL2VA / L2VA**: Include exact alignment header when required (`I2VA`, `FL2VA`, `L2VA`), followed by one blank line, then `integrated_multimodal_description:`, `overall_soundscape:`, and `non_diegetic_music:`.
   - **Ref2VA**: Include `subject_definitions:`, `summary:`, `retention_analysis:`, `detailed_description:`, `overall_soundscape:`, and `non_diegetic_music:`.
3. **Layer Synchronized Combat Audio**:
   - Place blade clangs, gunshots, body impacts, and vocal effort grunts inside `integrated_multimodal_description` / `detailed_description` synchronized with contact.
   - Place ambient environment, cloth rustle, and footstep texture in `overall_soundscape` (1-4 English sentences; no dialogue/singing).
   - Place score instrumentation, tempo, and dynamic build in `non_diegetic_music` (1-3 English sentences, or `N/A`).
4. **Run Final Audit**: Verify duration (4-15s), `[Shot 1]` has no timestamp, no em-dashes/en-dashes exist, and every strike has a clear physical reaction.

## Output Format

- **During Option Selection (Step 2)**: Present the categorized choreography menu clearly in the user's language, keeping technical H3 camera/mode terms accurate.
- **During Prompt Delivery (Step 3)**:
  1. **Production Summary**: Selected mode, duration, aspect ratio, shot count, and chosen choreography beats.
  2. **Final Production-Ready Prompt**: Complete English prompt in exact official H3 format with zero internal commentary.

## Gotchas

- **Never put two unrelated strikes in the exact same instant**: Stagger attacks and defenses sequentially (`Attacker swings -> Defender parries -> Sparks burst -> Defender ripostes`) so H3 renders clean causality.
- **Explicitly state starting and ending weapon states**: If a katana starts sheathed, state when it is drawn; if a character is disarmed, describe the weapon hitting and resting on the floor in subsequent shots so it does not teleport back into their hand.
- **Separate `I2VA` from `Ref2VA`**: If the user supplies a single starting action pose image and wants the fight to unfold forward from frame 0, use `I2VA` with its exact `0.00 seconds` alignment line rather than `Ref2VA`.
