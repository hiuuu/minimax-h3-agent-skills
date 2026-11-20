# Usage Guide: HZ MiniMax H3 Adaptive Prompt Engineering (V2)

## What It Does
Guides you through creating or debugging single-clip MiniMax H3 prompts (`T2VA`, `I2VA`, `FL2VA`, `L2VA`, `Ref2VA`) using a one-question-at-a-time adaptive interview, locked decision memory, and surgical regeneration diagnosis.

## Example Prompts

### 1. Start a New Scene via Adaptive Interview (`T2VA`)
> Use `hz-h3-prompt-engineering-v2`. I want a 10-second 16:9 moody cyberpunk alley scene in T2VA where a detective lights a cigarette in the rain. Ask me one question at a time to lock the details.

### 2. Interpolate Between First and Last Frame (`FL2VA`)
> Use `hz-h3-prompt-engineering-v2` in FL2VA mode for an 8-second clip. Picture 1 is the character standing before a closed wooden door; Picture 2 is the character standing inside the sunlit room with the door open.

### 3. Fix a Broken Generation (`Regeneration Diagnosis`)
> Use `hz-h3-prompt-engineering-v2` to fix this prompt. In my last generation, the character walked right-to-left in Shot 1, then suddenly flipped to left-to-right in Shot 2, and the glass on the table reappeared intact after breaking: [paste your prompt].
