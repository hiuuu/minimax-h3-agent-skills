# Character Sheet Layout Blueprints & Prompt Templates

Use these five production-tested blueprints to generate clean, consistent character reference sheets optimized for **MiniMax H3 (`Ref2VA`)**, **Pika**, **p-h3**, and **Omni Flash**.

---

## Universal Prompt Engineering Rules for Character Sheets

1. **Resolution & Aspect Ratio**: Always target `16:9` (or `21:9` for wide multi-row sheets) so horizontal full-body turnarounds and facial grids have maximum pixel density without squishing.
2. **Even Studio Lighting**: Specify `flat, even, shadowless neutral studio lighting` so video models do not bake dramatic directional shadows into the character's skin or clothing.
3. **Zero Text Labels (Except Type 5)**: Video reference encoders (`Ref2VA` / `Omni Flash`) can accidentally bleed on-screen text labels (`FRONT`, `SIDE`, `HAPPY`) into generated video frames. Keep **Types 1, 2, 3, and 4 completely free of text, watermarks, or borders**, and use clean typography **only** in Type 5 (Production Model Sheet).
4. **Face-Masking Toggle (`face_mask_mode`)**:
   - **Default (`ON` for Types 1, 2, 3)**: In full-body turnaround figures, replace the facial features inside the head contour with a smooth, blank oval matching the exact solid background color (`face features cleanly masked out with solid background-colored oval`), leaving hair, ears, neck, and head silhouette intact. This forces `H3 Ref2VA` and `Omni Flash` to read facial identity exclusively from the high-resolution close-up portraits, preventing low-resolution full-body face distortion.
   - **Optional (`OFF`)**: Render natural facial features on all full-body figures when the sheet is used for direct storyboard visualization or standalone art.

---

## Type 1: Omni Flash & H3 Rapid Identity Sheet (`omni-rapid`)

**Best For**: `Omni Flash 1.2`, `MiniMax H3 Ref2VA`, and fast subject-consistency workflows where the model needs maximum facial resolution paired with a single clean full-body outfit anchor.

### Layout Structure (16:9 Horizontal Split)
- **Left Half (50% width)**: High-resolution chest-up / head-and-shoulders close-up portrait of the character facing forward (or slight 15-degree angle) with a calm neutral expression, sharp eye and skin/fur detail.
- **Right Half (50% width)**: Single full-body standing figure from head to toe showing complete outfit proportions, posture, and footwear.
  - *Angle Selection*: Default to **3/4 Front View** (reveals chest, side profile depth, sleeve cut, and stance simultaneously in a single figure); switch to **Direct Front View** if symmetrical chest logos/patterns are critical.
- **Face-Masking Default (`ON`)**: The full-body figure on the right has its facial features cleanly masked out with a solid background-colored oval while preserving hair and head outline.

### Prompt Template (Type 1)
```text
Clean two-panel character reference sheet on a solid neutral [light gray / off-white] studio background, 16:9 widescreen composition, zero text, no labels, no dividing lines. On the left half, a sharp, high-resolution head-and-shoulders close-up portrait of [CHARACTER DESCRIPTION], facing forward with a neutral expression, detailed eyes, skin/fur texture, and hair. On the right half, a single full-body standing figure of the exact same character in a three-quarter front view from head to shoes, wearing [OUTFIT & FOOTWEAR DESCRIPTION], [OPTIONAL: with the facial features inside the head contour cleanly masked out by a smooth solid [light gray / off-white] oval matching the background while keeping hair and head silhouette intact]. Flat, even, shadowless studio lighting, crisp edges, consistent colors and proportions.
```

---

## Type 2: H3 Master Turnaround + Portrait + Macro Detail Sheet (`h3-master-triad`)

**Best For**: `MiniMax H3 Ref2VA` and `p-h3` workflows requiring 360-degree body geometry, high-resolution facial identity, and close-up material/texture fidelity in a single `<Picture 1>` asset.

### Layout Structure (3-Zone Asymmetric Grid, 16:9)
- **Left Column (~28% width)**: Large, crisp head-and-shoulders front portrait with neutral expression.
- **Center Zone (~44% width)**: Three full-body standing figures arranged side-by-side in **Front View**, **Side Profile View**, and **Back View**, aligned on the same ground plane and height scale.
  - *Face-Masking Default (`ON`)*: Facial features on the Front and Side full-body figures are cleanly masked out with a solid background-colored oval.
- **Right Column (~28% width)**: A 2x3 vertical grid of 6 extreme macro detail tiles showing:
  1. Left eye & eyebrow macro
  2. Nose & skin/fur pore texture macro
  3. Lips / mouth & jawline macro
  4. Ear & side-hairline macro
  5. Hair strand / fur / horn / material macro
  6. Signature fabric weave / emblem / armor texture macro

### Prompt Template (Type 2)
```text
Three-zone professional character reference sheet on a solid uniform [off-white / neutral gray] background, 16:9 aspect ratio, no text, no labels. Left section (one-third width): a large, ultra-sharp head-and-shoulders front portrait of [CHARACTER DESCRIPTION] with a neutral expression. Center section: three full-body standing turnaround views aligned at equal height showing front view, side profile view, and back view of the character wearing [OUTFIT & FOOTWEAR DESCRIPTION], [OPTIONAL: with the facial features on the full-body figures cleanly masked out using a smooth solid [off-white / neutral gray] oval matching the background while preserving hair and head silhouette]. Right section: a 2x3 grid of six square extreme close-up macro detail crops showing the eye, nose, mouth, ear, hair/fur texture, and clothing fabric pattern. Even, diffused, shadowless studio lighting, strict color and identity consistency across every panel.
```

---

## Type 3: Multi-Angle Full-Body Turnaround + Multi-Angle Head Strip (`full-turnaround-heads`)

**Best For**: `MiniMax H3 Ref2VA`, `Pika`, and 3D/stylized character consistency where the camera orbits around the character or captures side-profile dialogue.

### Layout Structure (2-Row Horizontal Layout, 16:9)
- **Top Row (55% height)**: Five full-body standing turnaround figures evenly spaced from left to right:
  1. **Front View**
  2. **3/4 Front View**
  3. **Right Side Profile**
  4. **Back View**
  5. **Left Side Profile** (or **3/4 Back View**)
  - *Face-Masking Default (`ON`)*: Facial features on all full-body figures are masked with a smooth solid background-colored oval.
- **Bottom Row (45% height)**: Three large head-and-shoulders close-up portraits aligned underneath:
  1. **Front Close-Up**
  2. **3/4 Front Close-Up**
  3. **Side Profile Close-Up**

### Prompt Template (Type 3)
```text
Two-row character turnaround reference sheet on a plain uniform [light gray / off-white] background, 16:9 aspect ratio, no text, no labels, no grid borders. Top row: five evenly spaced full-body standing views of [CHARACTER DESCRIPTION] wearing [OUTFIT & FOOTWEAR DESCRIPTION] in front view, three-quarter front view, right side profile, back view, and left side profile, aligned on the exact same ground line and height scale, [OPTIONAL: with facial features on all five full-body figures cleanly replaced by a smooth solid [light gray / off-white] oval matching the background while keeping hair and head contour intact]. Bottom row: three large, high-detail head-and-shoulders close-up portraits of the same character showing front face, three-quarter angle face, and side profile face with neutral expressions. Even, shadowless studio lighting, exact consistency in hair, clothing, and proportions.
```

---

## Type 4: 10-Expression & Lip-Sync Emotion Grid (`expression-grid`)

**Best For**: Dialogue scenes, singing/lip-sync (`<Audio 1>`), emotional acting in `H3 Ref2VA` / `I2VA`, and stylized 3D/2D characters.

### Layout Structure (2x5 Symmetrical Grid, 16:9)
- **10 Chest-Up / Head-and-Shoulders Panels** arranged in 2 rows of 5 columns on a clean uniform background:
  - **Row 1**: `Happy`, `Surprised`, `Angry`, `Sad`, `Wink / Playful`
  - **Row 2**: `Sleepy / Tired`, `Smug / Confident`, `Goofy / Laughing`, `Disgusted`, `Terrified / Shocked`
- *Labels*: Off by default for pure AI reference input; optionally enabled as clean centered sans-serif captions beneath each tile if requested.

### Prompt Template (Type 4)
```text
Clean 2x5 ten-panel facial expression reference sheet on a uniform solid [dark slate / neutral gray] background, 16:9 aspect ratio, [no text labels / clean white sans-serif emotion labels centered below each portrait]. Ten consistent head-and-shoulders portraits of [CHARACTER DESCRIPTION] arranged in two rows of five, maintaining identical lighting, hair, head proportions, and outfit while displaying ten distinct expressions: top row from left to right showing happy smile, wide-eyed surprised, furrowed angry, tearful sad, and playful wink; bottom row from left to right showing sleepy yawn, confident smirk, open-mouthed goofy laugh, disgusted grimace, and terrified shock. Soft, even studio lighting, crisp facial readability.
```

---

## Type 5: Complete Production Model Sheet (`production-bible`)

**Best For**: 2D animation, comic/storyboard bibles, client presentations, and comprehensive world-building sheets (`PROTAGONIST - CHARACTER MODEL SHEET`).

### Layout Structure (4-Row Annotated Bible, 16:9)
- **Header**: Bold centered title (`[CHARACTER NAME] - CHARACTER MODEL SHEET`).
- **Row 1 (`TURNAROUND`)**: 4 full-body views (`FRONT`, `THREE-QUARTER`, `SIDE`, `BACK`) with faint horizontal height alignment guide lines.
- **Row 2 (`HEAD CLOSE-UPS / EMOTIONS`)**: 6 circular or square head close-ups (`NEUTRAL`, `SAD`, `TIRED`, `WORRIED`, `DETERMINED`, `PROUD`).
- **Row 3 (`WARDROBE EVOLUTION`)**: 4 to 6 full-body outfit variants (`W1` through `W6`) showing costume changes across story arcs.
- **Row 4 (`HANDS & ACTIONS`)**: 5 signature prop/hand interactions and key poses (`HOLDING PROP`, `WALKING`, `SITTING`, `SIGNATURE ACTION`).

### Prompt Template (Type 5)
```text
Comprehensive 16:9 character model sheet on a clean warm off-white paper background with subtle horizontal proportion guide lines and crisp dark sans-serif section labels. Top title centered: "[CHARACTER NAME] - CHARACTER MODEL SHEET". Row 1 labeled "TURNAROUND": four full-body standing views labeled "FRONT", "THREE-QUARTER", "SIDE", and "BACK" of [CHARACTER DESCRIPTION] wearing [PRIMARY OUTFIT]. Row 2 labeled "HEAD CLOSE-UPS (EMOTIONS)": six expressive head portraits labeled "NEUTRAL", "SAD", "TIRED", "WORRIED", "DETERMINED", and "PROUD". Row 3 labeled "WARDROBE EVOLUTION": [NUMBER] full-body standing outfit variations labeled "W1" through "W[N]" showing [OUTFIT VARIATIONS]. Row 4 labeled "HANDS & ACTIONS": five vignettes showing close-up hand gestures and signature poses labeled [ACTION LABELS]. Consistent [ART STYLE] linework, flat cel-shaded colors, clean layout spacing.
```
