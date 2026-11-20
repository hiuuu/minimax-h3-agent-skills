# MiniMax H3 Agent Skills (V2 & V3 Production Suite)

A curated collection of official-guideline-aligned **Agent Skills** for **MiniMax H3 (Hailuo)** video generation across `T2VA`, `I2VA`, `FL2VA`, `L2VA`, and `Ref2VA` modes.

This repository includes both **V2 (Standard / Pro Single-Clip)** and **V3 (Production Pipeline / Multi-Clip)** editions, complete with usage guides, prompt examples, technical limits, and an expanded combat choreography & foley catalog.

---

## Repository Structure

```text
minimax-h3-agent-skills/
├── README.md
├── LICENSE
└── skills/
    ├── v2/
    │   ├── hz-h3-prompt-engineering-v2/
    │   │   ├── SKILL.md
    │   │   └── USAGE.md
    │   ├── hz-h3-strict-motion-transfer/
    │   │   ├── SKILL.md
    │   │   └── USAGE.md
    │   └── hz-h3-action-choreographer-v2/
    │       ├── SKILL.md
    │       ├── USAGE.md
    │       └── references/
    │           └── combat_choreography_catalog.md
    └── v3/
        ├── hz-h3-prompt-engineering-v3/
        │   ├── SKILL.md
        │   └── USAGE.md
        ├── hz-h3-strict-motion-transfer-v3/
        │   ├── SKILL.md
        │   └── USAGE.md
        └── hz-h3-action-choreographer-v3/
            ├── SKILL.md
            ├── USAGE.md
            └── references/
                └── combat_choreography_catalog.md
```

---

## Which Version Should You Use?

| Edition | Best For | Key Capabilities |
| :--- | :--- | :--- |
| **V2 (Pro Single-Clip)** | Fast, standalone 4–15s clips with strict H3 syntax compliance | Adaptive 1-question-at-a-time interview, locked decision memory, surgical regeneration diagnosis, anti-morphing pose locks, and selectable combat exchanges |
| **V3 (Production Pipeline)** | Multi-clip sequences (>15s), music/lip-sync performances, and local/ComfyUI workflows | Everything in V2 **plus** Next-Clip Continuation Handoff Packets, Dialogue/Lip-Sync Word-Budget Calculator, Hybrid Body-Only vs. Full-Body Motion Lock, Multi-Part Fight Splitting, and Combat Foley Dictionary |

---

## Skills Overview

### 1. H3 Adaptive Prompt Engineering (`hz-h3-prompt-engineering-v2` & `v3`)
Transforms creative ideas, storyboards, reference assets, or broken prompts into production-ready MiniMax H3 prompts across all five official modes (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, `Ref2VA`).
- Enforces exact alignment headers (`0.00 seconds` for `I2VA`, `0.00` to `S.SS` for `FL2VA`, `S.SS` for `L2VA`).
- Separates diegetic audio (`<d>[Language] ...</d>`), `overall_soundscape`, and `non_diegetic_music`.
- **V3 Additions**: Dialogue word-budget timing calculator (~2.0–2.5 words/sec), ComfyUI/RunningHub/local checkpoint slot mapping, and Next-Clip Handoff Packets.

### 2. H3 Strict Motion Transfer (`hz-h3-strict-motion-transfer` & `v3`)
Generates literal, frame-accurate MiniMax H3 `Ref2VA` prompts that transfer choreography, timing, and camera movement from `<Video 1>` onto `<Subject 1>` (`<Picture 1>`) with **zero creative drift**.
- Prevents the **Frame-0 Pose Morph** bug when `<Picture 1>` is a neutral A-pose/T-pose or turnaround sheet.
- Maps cross-species limbs explicitly (human arms -> front legs/paws; human legs -> hind legs) while forbidding anthropomorphic distortions.
- Prevents chroma-key color/shadow bleed onto solid backdrops (`<Subject 2>`).
- **V3 Additions**: Choice between **Mode A (Full-Body & Face Lock)** and **Mode B (Hybrid Body Lock + `<Audio 1>` Lip-Sync)**, plus cross-species momentum calibration.

### 3. H3 Action & Combat Choreographer (`hz-h3-action-choreographer-v2` & `v3`)
Interactive combat director for MiniMax H3 across **Live-Action**, **2D Anime (Sakuga)**, **Western 2D Cartoon**, and **Stylized 3D**.
- Presents **3 to 5 structured Attack -> Defense -> Counter -> Camera options** before compiling the final H3 prompt.
- Covers Bladed Weapons (Katana, Longsword, Dual Daggers), Martial Arts (Boxing, Kickboxing, Wing Chun, Judo), Firearms (Pistol CQB, Gun-Fu, SMG, Rifle, Shotgun), Polearms/Heavy Melee, Magic/Energy Clashes, and Cartoon Slapstick.
- **V3 Additions**: Splits >15s battles into chained clips with End-State Handoff Snapshots and includes an acoustic **Combat Foley Audio Dictionary**.

---

## Installation & Quick Start

### Option A: Claude Code / Pi / Workbuddy / Cursor (Agent Skills Standard)
Copy the desired skill folders from `skills/v2/` or `skills/v3/` into your project or global skills directory:

```bash
git clone https://github.com/YOUR_USERNAME/minimax-h3-agent-skills.git
mkdir -p ~/.claude/skills
cp -r minimax-h3-agent-skills/skills/v3/* ~/.claude/skills/
```
*(For project-scoped skills, copy into `.claude/skills/` or `.agents/skills/` inside your repository.)*

### Option B: Gemini Skills
1. Download the repository ZIP or clone it locally.
2. Open your Gemini Skill Manager / Custom Skills settings, or ask Gemini to import the `SKILL.md` (and `references/` file for the action choreographer).

### Option C: Any LLM Chat Interface (System Prompt)
Open any `SKILL.md` file (and `references/combat_choreography_catalog.md` if using the Action Choreographer) and paste its contents into your Custom Instructions / System Prompt.

---

## MiniMax H3 Official Technical Reference

| Parameter | Official Specification |
| :--- | :--- |
| **Output Duration** | 4–15 seconds (24 FPS) |
| **Resolution & Audio** | Default 768p shorter side (2K via `H3-Regenerate-2K`), 32 kHz stereo |
| **Aspect Ratios** | `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16` |
| **Local Checkpoints** | `FL2VA` checkpoint (T2VA & first/last-frame modes) & `Ref2VA` checkpoint (multimodal references) |
| **Ref2VA Input Limits** | Max **9** images, max **3** videos (2–15s each, **15s total max**), max **3** audio clips (2–15s each, **15s total max**), max **12** files total |

---

## License

MIT License. Free to use, modify, and share.
