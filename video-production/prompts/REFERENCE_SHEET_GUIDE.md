# Nano Banana 2 — Reference Sheet Generation Guide
# PHASE 1: Generate these 3 reference images FIRST at 4K
# PHASE 2: Use them as image_url inputs for all scene generations

---

## HOW THE REFERENCE PIPELINE WORKS

### The Problem with Text-Only Prompts
Every generation interprets "reflective silver-white" slightly differently.
Over 40-60 images, the figure's material drifts, lighting shifts, node
designs diverge. By image 30, your opening shot and closing shot look
like they're from different videos.

### The Solution: Image-Anchored Generation
Nano Banana 2's edit endpoint accepts up to 14 reference images alongside
a text prompt. The model uses these references to anchor style, material,
color, and design — treating your approved references as ground truth.

### The Pipeline
```
PHASE 1: Generate 3 Reference Sheets (text-to-image endpoint)
              ↓
         Review & Approve (iterate if needed)
              ↓
PHASE 2: Generate ALL scene stills (edit endpoint)
         Input: scene prompt + 2-3 reference images
              ↓
         Consistent output across every frame
```

---

## REFERENCE SHEET 1: CHARACTER TURNAROUND

**Endpoint:** `fal-ai/nano-banana-2` (text-to-image)
**Resolution:** 4K
**Aspect Ratio:** 16:9

```
A character concept art turnaround sheet showing a featureless human figure 
in three poses arranged side by side on a pure deep navy-black background 
(#0a1628). 

LEFT: Front-facing view, standing neutral pose, arms relaxed at sides.
CENTER: Three-quarter front view, standing with weight shifted slightly 
to one side, one hand raised to chest height as if gesturing.
RIGHT: Side profile view, standing straight.

The figure has absolutely no facial features — no eyes, mouth, nose, ears, 
or hair. Completely smooth featureless head. The entire body surface is 
fully smooth, reflective, polished silver-white material with a chrome-like 
finish. No lines, no seams, no joints, no cracks, no artifacts anywhere on 
the surface. The reflections on the surface subtly show the surrounding 
teal and amber lighting.

The figure wears a simple dark charcoal hoodie with the hood down, slightly 
oversized, sleeves reaching the wrists, over dark fitted trousers and 
minimal dark shoes. The clothing has realistic fabric texture and folds 
that contrast with the perfectly smooth reflective skin.

Dramatic teal (#00d4aa) rim lighting from behind-left. Subtle warm amber 
(#f59e0b) fill light from the right. Each pose is lit identically. Clean 
dark background with no environment — only subtle volumetric haze at the 
feet. Thin teal horizontal line at the base like a ground plane reference.

Professional concept art layout. Studio lighting. Ultra-realistic 3D 
rendering. Crisp, sharp detail. No motion blur. This is a design reference 
sheet, not a narrative scene.
```

### What to Evaluate
- [ ] Material finish: Does the silver-white look like polished ceramic/chrome? Not plastic?
- [ ] Featureless face: Smooth and intentional, not like a rendering error?
- [ ] Hoodie contrast: Dark fabric reads clearly against reflective skin?
- [ ] Reflections: Does the teal/amber lighting show in the surface reflections?
- [ ] Consistency: Do all 3 poses look like the same character?
- [ ] Proportions: Natural human proportions, not distorted?

### If It Needs Adjustment
- Too chrome/mirror-like → change "chrome-like finish" to "polished ceramic finish with subtle reflectivity"
- Too plastic → change to "wet-look polished porcelain material with high specular highlights"
- Too dark → add "the figure is brightly lit, the reflective surface is predominantly white with teal and amber color reflections"
- Seams/joints visible → emphasize "absolutely seamless, the surface transitions from head to neck to body with zero visible boundaries"

---

## REFERENCE SHEET 2: ENVIRONMENT & LIGHTING BIBLE

**Endpoint:** `fal-ai/nano-banana-2` (text-to-image)
**Resolution:** 4K
**Aspect Ratio:** 16:9

```
A cinematic environment mood reference showing a dark atmospheric interior 
space. No people or characters. This is a lighting and color palette 
reference.

The scene is a vast dark room — deep navy-black (#0a1628) walls and ceiling 
that fade into pure darkness. The floor is polished dark concrete, highly 
reflective, catching all light sources.

THREE DISTINCT LIGHT SOURCES are visible:
1. TEAL: A cluster of teal (#00d4aa) LED-like lights on a dark server rack 
   on the left third of the frame, casting cool teal light across the floor 
   and nearby fog.
2. AMBER: A warm amber (#f59e0b) light source on the right — like light 
   spilling through a doorway or from a warning indicator — casting warm 
   streaks across the floor.
3. WHITE: A single cool white overhead spotlight in the center, creating a 
   focused pool of light on the floor below it.

Volumetric fog fills the lower third of the space, visible where it 
catches each light source — appearing teal near the left, amber near the 
right, and white in the center. The fog creates natural atmospheric depth.

Small particle dust floats in the light beams. The ceiling is lost in 
darkness above. The overall mood is cinematic noir — dark, atmospheric, 
controlled.

Wide establishing shot, eye level. 28mm lens equivalent. Deep depth of 
field. Ultra-realistic 3D rendering. Film grain. This is a reference for 
color palette and atmospheric lighting, not a narrative scene.
```

### What to Evaluate
- [ ] Navy-black reads as deep blue-black, not pure black or grey?
- [ ] Teal and amber are distinct and vivid against the dark environment?
- [ ] Volumetric fog looks natural and atmospheric, not like a flat overlay?
- [ ] The three light sources create clear color zones without muddying together?
- [ ] Floor reflections add depth?
- [ ] Overall mood: does it feel cinematic, premium, slightly ominous?

---

## REFERENCE SHEET 3: UI & NETWORK ELEMENT PROPS

**Endpoint:** `fal-ai/nano-banana-2` (text-to-image)
**Resolution:** 4K
**Aspect Ratio:** 16:9

```
A prop reference sheet showing three digital elements arranged side by side 
on a pure deep navy-black background (#0a1628), like items in a design 
system. Each element is clearly separated with space between them.

LEFT — HOLOGRAPHIC TERMINAL PANEL: A floating semi-transparent dark glass 
panel with thin bright teal (#00d4aa) border edges. The panel displays 
three lines of monospace text in teal: "socks5h://127.0.0.1:9050". The 
panel emits a soft teal glow that illuminates nearby fog particles. It 
hovers at a slight angle. The text is perfectly crisp and legible.

CENTER — TOR RELAY NODE: A glowing icosphere (faceted sphere) made of 
translucent teal crystalline material. Bright teal edges, luminous 
white-teal core. Approximately the size of a basketball relative to the 
frame. Thin teal light trails extend from left and right sides like 
data connections. Small light particles orbit it slowly. It floats above 
a reflective dark surface.

RIGHT — DATA TRAIL: A horizontal luminous teal light trail showing the 
visual language for encrypted data in transit. The trail is made of 
flowing teal particles with a bright core and softer glow falloff. It 
shows three states stacked vertically: top trail has three concentric 
rings (triple encrypted), middle trail has two rings (double encrypted), 
bottom trail is a single line (single layer). The particles suggest 
left-to-right motion.

Professional design reference layout. Studio lighting with teal rim light. 
Ultra-realistic 3D rendering. Crisp detail. Each element is clearly 
defined and isolated for reference purposes.
```

### What to Evaluate
- [ ] Terminal text: Is "socks5h://127.0.0.1:9050" legible and correctly spelled?
- [ ] Panel glass effect: Translucent but not invisible? Teal border visible?
- [ ] Node design: Does the icosphere look like a coherent object, not random geometry?
- [ ] Node glow: Luminous but not blown out?
- [ ] Data trails: Can you distinguish triple/double/single encryption layers?
- [ ] Particle motion: Do the trails suggest directional flow?

---

## PHASE 2: SCENE GENERATION WITH REFERENCES

Once you've approved the 3 reference sheets, every scene uses the EDIT 
endpoint with references fed in.

### API Call Structure

```python
# Using fal.ai edit endpoint with reference images
result = fal.subscribe("fal-ai/nano-banana-2/edit", {
    "input": {
        "prompt": "[SCENE-SPECIFIC PROMPT — see style-reference.md]",
        "image_urls": [
            "URL_OF_CHARACTER_REFERENCE_SHEET",   # Always include
            "URL_OF_ENVIRONMENT_REFERENCE",        # Always include
            "URL_OF_UI_NETWORK_REFERENCE",         # Include when scene has nodes/UI
        ],
        "num_images": 2,       # Generate 2 variations, pick best
        "aspect_ratio": "16:9",
        "resolution": "2K",    # 2K for iteration, 4K for finals
        "output_format": "png",
    }
})
```

### Prompt Modification for Edit Endpoint

When using the edit endpoint with references, your scene prompts should 
EXPLICITLY reference the input images. Modify the prompt to include 
phrases like:

- "The figure matches the character design shown in the reference — same 
  reflective silver-white material, same dark charcoal hoodie, same 
  featureless smooth head."
- "The environment lighting matches the reference — deep navy-black with 
  teal and amber accent lighting, volumetric fog."
- "The Tor relay nodes match the reference design — teal crystalline 
  icospheres with luminous cores and light trail connections."

This tells the model explicitly to anchor to the reference images rather 
than freely interpreting the text description.

### Scene Prompt Template (with reference anchoring)

```
[SCENE PROMPT FROM STYLE-REFERENCE.MD]

The figure's appearance, material, and clothing match the provided character 
reference exactly. The environment lighting and color palette match the 
provided environment reference. [IF APPLICABLE: The network elements and 
holographic UI match the provided prop reference.]
```

---

## GENERATION ORDER (RECOMMENDED)

```
Step 1:  Reference Sheet 1 (Character)     — iterate until approved
Step 2:  Reference Sheet 2 (Environment)    — iterate until approved  
Step 3:  Reference Sheet 3 (Props)          — iterate until approved
Step 4:  Shot 1.1 (Hook — with refs)        — test the pipeline works
Step 5:  Shot 8.2 (Close — with refs)       — verify consistency with 1.1
Step 6:  If 1.1 and 8.2 look consistent → batch generate remaining shots
```

Steps 4 and 5 are the critical consistency test — these are the bookend 
shots of the video (opening and closing). If the figure, lighting, and 
mood match between them, the pipeline is working and you can confidently 
batch generate everything in between.

---

## COST FOR REFERENCE PHASE

| Item | Count | Unit Cost | Total |
|---|---|---|---|
| Reference sheets (4K) | 3 | $0.16 (4K = 2x) | $0.48 |
| Reference iterations (assume 3 rounds each) | 9 | $0.16 | $1.44 |
| Pipeline test shots (2K, 2 variations each) | 4 | $0.08 | $0.32 |
| **Total reference phase** | | | **~$2.24** |

You'll spend about $2 locking the entire visual identity before committing 
to the full $80 production batch. That's the whole point — fail cheap, 
commit expensive.
