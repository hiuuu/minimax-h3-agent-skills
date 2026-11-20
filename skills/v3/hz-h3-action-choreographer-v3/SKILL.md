---
name: hz-h3-action-choreographer-v3
description: Production-pipeline MiniMax H3 combat and action choreography director (V3) across live-action, anime, 2D cartoon, and stylized 3D styles. Adds multi-part fight sequence splitting (>15s chained clips with frame handoffs), selectable attack-and-defense menus, anti-morphing beat budgets, and a combat foley audio dictionary. Use whenever the user asks to design, browse, select, chain, or write MiniMax H3 prompts for sword duels, martial arts, fistfights, gunfights, heavy melee, magic clashes, or multi-clip battle sequences.
---

# HZ MiniMax H3 Action & Combat Choreographer (V3 Production Director)

Design cinematic, physically coherent combat choreography for MiniMax H3 across live-action, 2D anime, Western cartoon, and stylized 3D productions. V3 adds **Multi-Part Fight Sequence Splitting** (chaining multiple 4-15s clips with end-state handoffs) and a **Combat Foley Audio Dictionary** on top of selectable attack-defense-counter menus and anti-morphing physics locks.

## When to Use

- The user asks for a fight, duel, shootout, brawl, or battle scene for MiniMax H3.
- The user specifies a weapon or style (katana, longsword, dual daggers, fistfight/martial arts, pistol/gun-fu, SMG, assault rifle, shotgun, spear, axe/shield, anime energy clash, cartoon slapstick, or 3D stylized combat).
- The user wants selectable choreography options before generating the prompt, or wants to build a **multi-clip fight sequence** longer than 15 seconds.

## Core Combat Engineering Principles

1. **Interactive Choreography Menu First**: Whenever a user requests a combat category without locking exact moves, present **3 to 5 distinct, cinematic choreography beats** (Attack -> Defense/Counter -> Consequence + Recommended Camera) so the user can pick or combine them.
2. **4-Stage Observable Cause-and-Effect Physics**: Never use vague summaries like "they fight fiercely." Break every exchange into:
   - **Telegraph / Initiation**: Foot pivot, weight shift, grip change, or weapon draw.
   - **Attack Trajectory**: Exact strike angle, limb/muzzle vector, and target zone.
   - **Defense / Evasion**: Exact parry angle, slip direction, duck, cover dive, or barrier block.
   - **Contact & Aftermath**: Sparks, muzzle flash, brass ejection, shockwave, recoil, or stagger occurring strictly **after** contact.
3. **Anti-Morphing & Spatial Lock Rules**:
   - **Beat Budget per Clip**: Limit a 5-8s clip to **1-2 clean exchanges**, and a 10-15s clip to **2-3 exchanges** with clear 0.5-second holds/resets so limbs and blades do not blur or bend.
   - **180-Degree Axis & Screen Direction**: Lock Fighter A on screen-left attacking rightward and Fighter B on screen-right defending leftward (or vice versa) across cuts unless an explicit camera orbit is described.
   - **Weapon State & Geometry Lock**: Specify blade length, one-handed vs. two-handed grip, sheath/holster state, and firearm firing mode (semi-auto vs. short bursts). If a weapon is dropped, track it on the floor in later shots.
4. **Multi-Part Fight Sequence Splitting (For >15s Battles)**:
   - When the user wants a 20-45 second fight sequence, divide it into chained 8-15 second clips:
     - **Clip 1 (Opening & Stance Clash)**: Weapon draw, initial probe attack, parry/evasion, ending in a clean locked stance.
     - **Clip 2 (Escalation & Disarm/Turn)**: Heavy combo, environmental cover/destruction, counter-strike or disarm.
     - **Clip 3 (Climax & Resolution)**: Decisive finishing exchange and clear aftermath pose.
   - Provide an **End-State Handoff Snapshot** after each clip so the final frame can feed the next clip (`I2VA` / `FL2VA` / `Ref2VA`).
5. **Strict MiniMax H3 Compliance**: Compile final prompts using exact official H3 syntax (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, or `Ref2VA`), zero timestamp on `[Shot 1]`, strictly increasing timestamps on later cuts, separated diegetic/soundscape/music fields, and no em-dashes or en-dashes.

## Workflow

### Step 1: Identify Discipline, Visual Medium, Sequence Scope & H3 Mode
Check what the user has provided:
- **Combat Discipline & Visual Medium**: Weapon/style + Live-Action, 2D Anime, Cartoon, or Stylized 3D.
- **Scope**: Single clip (4-15s) or Multi-Part Sequence (>15s split into chained clips).
- **H3 Task Mode**: `T2VA`, `I2VA`, `FL2VA`, `L2VA`, or `Ref2VA`.

Consult `references/combat_choreography_catalog.md` for discipline-specific choreography beats, visual styling modifiers, and combat foley audio descriptors.

### Step 2: Present Selectable Choreography Beats
Before writing the final H3 prompt (unless the user already locked exact moves), present **3 to 5 tailored combat options** (or a 3-clip arc if multi-part was requested):
- **Option Name & Vibe**
- **Attacker Move**
- **Defender Counter**
- **Physical Consequence**
- **Recommended H3 Camera**

Ask **one concise follow-up** inviting the user to pick/combine options and confirm duration, aspect ratio, and any reference images/frames.

### Step 3: Compile the Final MiniMax H3 Prompt
Once the user selects their choreography:
1. **Lock Character & Spatial Anchors**: Maintain outfits, weapon hands, relative height/scale, and screen positions across every shot.
2. **Apply Exact Official H3 Structure**:
   - **T2VA / I2VA / FL2VA / L2VA**: Include exact alignment header when required (`I2VA`, `FL2VA`, `L2VA`), followed by one blank line, then `integrated_multimodal_description:`, `overall_soundscape:`, and `non_diegetic_music:`.
   - **Ref2VA**: Include `subject_definitions:`, `summary:`, `retention_analysis:`, `detailed_description:`, `overall_soundscape:`, and `non_diegetic_music:`.
3. **Layer Combat Foley & Music**:
   - Place exact contact sounds (blade ring, gunshot crack, body thud, effort grunts) inside `integrated_multimodal_description` / `detailed_description` at contact timestamps.
   - Use crisp acoustic descriptors from `references/combat_choreography_catalog.md` (Section 8) for `overall_soundscape` (1-4 sentences; no dialogue/singing) and `non_diegetic_music` (1-3 sentences, or `N/A`).
4. **Run Final Audit & Handoff**: Verify duration (4-15s), `[Shot 1]` has no timestamp, no em-dashes/en-dashes exist, and include an **End-State Handoff Snapshot** if the fight continues into a next clip.

## Output Format

- **During Option Selection (Step 2)**: Present categorized choreography choices cleanly in the user's language, keeping technical H3 terms exact.
- **During Prompt Delivery (Step 3)**:
  1. **Production Summary**: Mode, duration, aspect ratio, shot count, and chosen choreography beats.
  2. **Final Production-Ready Prompt**: Complete English prompt in exact official H3 syntax with zero internal commentary.
  3. **End-State Handoff Snapshot** *(for multi-part fights)*: Exact ending positions, weapon locations, and damage states for chaining the next clip.

## Gotchas

- **Never put two unrelated strikes in the exact same instant**: Stagger attacks and defenses sequentially (`Attacker swings -> Defender parries -> Sparks burst -> Defender ripostes`) for clean causality.
- **Track disarmed or sheathed weapons explicitly**: State where a dropped weapon lands and keep it on the ground in subsequent shots so it does not teleport back into a fighter's hand.
- **Use `I2VA` instead of `Ref2VA` for single starting-frame fights**: When the user only provides one starting pose image and wants forward fight motion from frame 0, `I2VA` is cleaner and more stable.
