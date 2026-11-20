# Usage Guide: HZ MiniMax H3 Strict Motion Transfer (V2)

## What It Does
Generates literal, frame-accurate MiniMax H3 `Ref2VA` motion transfer prompts from `<Video 1>` onto `<Subject 1>` (`<Picture 1>`) with zero creative reinterpretation, preventing frame-0 pose morphing and chroma-key edge spill.

## Example Prompts

### 1. Human Dance to Stylized Character on Chroma Green
> Use `hz-h3-strict-motion-transfer`. Transfer the exact dance choreography and camera framing from `<Video 1>` (10 seconds) onto the stylized character in `<Picture 1>`, replacing the room background with the solid chroma green backdrop in `<Picture 1>`. Silent (`N/A`).

### 2. Cross-Species Motion Transfer (Human to Animal)
> Use `hz-h3-strict-motion-transfer`. Replicate the exact boxing shadow-boxing moves from `<Video 1>` (8 seconds) onto the fluffy golden retriever in `<Picture 1>` standing upright on its hind legs. Keep `<Video 1>`'s gym background and static camera.
