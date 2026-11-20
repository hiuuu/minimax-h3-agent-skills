# MiniMax H3 Agent Skills

A modular suite of production-grade **Agent Skills** engineered for **MiniMax H3** video and audio generation workflows (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, and `Ref2VA`), as well as compatible image generators (`p-h3`, Pika, Omni Flash 1.2) used for character sheet preparation.

These skills enforce official MiniMax H3 structural rules, reference-label isolation, temporal continuity, strict motion transfer, cinematic action choreography, and identity-locked character sheet design.

---

## Included Skills Overview

The repository is organized into **V2 (Core Production)** and **V3 (Multi-Clip Production Pipeline)** tiers:

| Skill Folder | Tier | Primary Purpose |
| :--- | :---: | :--- |
| **`hz-h3-prompt-engineering-v3`** | V3 | Master prompt architect covering all 5 official H3 modes (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, `Ref2VA`), adaptive single-question interviews, lip-sync word budgeting, multi-clip handoff packets, and targeted regeneration diagnosis. |
| **`hz-h3-strict-motion-transfer-v3`** | V3 | Frame-accurate `Ref2VA` video-to-video motion transfer (`[video editing]`) with zero creative drift, cross-species limb mapping, occlusion depth ordering, and optional hybrid facial/audio lip-sync locking. |
| **`hz-h3-action-choreographer-v3`** | V3 | Interactive combat & action scene director offering categorized attack/defense choreographies (swords, martial arts, gun-fu, tactical rifles, heavy weapons, magic, slapstick) across live-action, anime, cartoon, and 3D styles, plus a Combat Foley dictionary. |
| **`hz-h3-character-sheet-generator`** | V3 | Generates identity-locked character reference sheet prompts across 5 specialized layouts (`omni-rapid`, `h3-master-triad`, `full-turnaround-heads`, `expression-grid`, and `production-bible`) with default **background-colored face masking** on full-body views to prevent low-resolution facial distortion. |
| **`hz-h3-prompt-engineering-v2`** | V2 | Core H3 master prompt engineering system with locked decision memory, 16-category failure diagnosis, and official formatting validation. |
| **`hz-h3-strict-motion-transfer`** | V2 | Core zero-drift motion transfer system preventing Frame-0 pose morphing, chroma spill, and camera hallucination. |
| **`hz-h3-action-choreographer-v2`** | V2 | Core combat choreography menu and anti-morphing beat budget system for single-clip action generation. |

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
        ├── hz-h3-action-choreographer-v3/
        │   ├── SKILL.md
        │   ├── USAGE.md
        │   └── references/
        │       └── combat_choreography_catalog.md
        └── hz-h3-character-sheet-generator/
            ├── SKILL.md
            ├── USAGE.md
            └── references/
                └── sheet_blueprints.md
```

---

## Installation & Usage

### 1. Claude Code / Pi / Workbuddy / Cursor (Agent Skills Standard)
Clone the repository and copy the desired skill folders from `skills/v3/` (recommended) into your global or project-level skills directory:

```bash
git clone https://github.com/hiuuu/minimax-h3-agent-skills.git
mkdir -p ~/.claude/skills
cp -r minimax-h3-agent-skills/skills/v3/* ~/.claude/skills/
```

For project-scoped installation, copy them into `.claude/skills/` or `.agents/skills/` inside your workspace root.

### 2. Google Gemini (Custom Skills / Gems)
1. Open **Skill Management Settings** (or Gem Manager) in Gemini.
2. Create a new skill and paste the contents of the target `SKILL.md` file.
3. For **`hz-h3-action-choreographer-v3`** and **`hz-h3-character-sheet-generator`**, attach their corresponding `references/*.md` files as knowledge documents.

### 3. Any LLM Interface (System Prompt)
Copy the full contents of any `SKILL.md` file into your system instructions or custom GPT/project prompt. Check each skill's `USAGE.md` file for ready-to-use trigger examples.

---

## Official MiniMax H3 Technical Reference

All prompt-generating skills enforce the documented MiniMax H3 constraints:

| Parameter | Official Specification |
| :--- | :--- |
| **Supported Modes** | `T2VA`, `I2VA`, `FL2VA`, `L2VA`, `Ref2VA` |
| **Local Checkpoints** | `FL2VA` (supports `T2VA`, `I2VA`, `FL2VA`, `L2VA`) and `Ref2VA` (multimodal reference inputs) |
| **Duration** | `4–15` seconds per generation |
| **Frame Rate & Audio** | `24 FPS` / `32 kHz` stereo audio |
| **Resolution** | `768px` shorter side default (`2K` via `H3-Regenerate-2K`) |
| **Aspect Ratios** | `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16` |
| **Ref2VA Input Caps** | Max **9** images, max **3** videos (`2–15s` each, `15s` total), max **3** audio clips (`2–15s` each, `15s` total), max **12** total files |

---

## Typical End-to-End Production Workflow

1. **Design the Character (`hz-h3-character-sheet-generator`):** Generate a `16:9` character reference sheet (e.g., `h3-master-triad` or `omni-rapid`) with full-body face masking enabled so facial identity comes exclusively from high-resolution close-ups.
2. **Choreograph or Transfer Motion:**
   - Use **`hz-h3-action-choreographer-v3`** to select and script multi-beat combat sequences in live-action, anime, cartoon, or 3D styles.
   - Or use **`hz-h3-strict-motion-transfer-v3`** to transfer exact choreography from `<Video 1>` onto `<Subject 1>` against a clean backdrop (`<Subject 2>`).
3. **Engineer & Extend Shots (`hz-h3-prompt-engineering-v3`):** Assemble multi-clip sequences using the `Next-Clip Handoff Packet` to maintain spatial, wardrobe, and audio continuity across 15-second boundaries.

---

## License

Released under the [MIT License](LICENSE).