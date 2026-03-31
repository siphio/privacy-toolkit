# SIPHIO Privacy Toolkit — Visual Production Guide

> A complete reference for recreating and extending the cinematic 3D documentary visual style used in the Privacy & Anonymity Toolkit explainer video.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Design Concept](#2-design-concept)
3. [Visual Identity System](#3-visual-identity-system)
4. [Reference Image System](#4-reference-image-system)
5. [Generation Platform & Settings](#5-generation-platform--settings)
6. [Master Prompt Architecture](#6-master-prompt-architecture)
7. [Scene-by-Scene Prompt Library](#7-scene-by-scene-prompt-library)
8. [Animation Pipeline (Veo 3.1)](#8-animation-pipeline-veo-31)
9. [Post-Production (CapCut)](#9-post-production-capcut)
10. [Lessons Learned](#10-lessons-learned)

---

## 1. Project Overview

**Goal:** Create a 5-8 minute cinematic explainer video covering network anonymity (Tor, SOCKS5, Proxychains, DNS leaks) based on the [Privacy & Anonymity Toolkit README](https://github.com/siphio/privacy-toolkit/blob/main/README.md).

**Style References:**
- **[fern](https://www.youtube.com/@fern-tv)** — 3D mannequin figures, cinematic environments, documentary storytelling with ~4.5M subscribers
- **[Blackfiles HD](https://youtube.com/@blackfiles-hd)** — Hacker history documentaries, dark atmospheric editing, stock footage + motion graphics + kinetic typography

**Hybrid Approach:** Fern's cinematic 3D mannequin storytelling merged with Blackfiles' dark tech-informational visual language.

**Tools Used:**
- **Nano Banana 2** (via Enhancor.ai) — Scene still generation with reference image consistency
- **Veo 3.1** (Google) — Image-to-video animation
- **ElevenLabs** — AI voiceover
- **CapCut** — Final assembly, text overlays, colour grading, sound design

---

## 2. Design Concept

### Two Visual Modes

The video alternates between two modes that share the same 3D world:

| Mode | Purpose | Visual Language | When Used |
|------|---------|----------------|-----------|
| **Cinematic Story** | Emotional narrative, spatial metaphors | 3D figures in environments, data as light trails | Hook, transitions, Tor journey, closing |
| **In-World Technical** | Teaching mechanisms | Holographic overlays, terminal projections within the scene | DNS leaks, commands, verification |

Technical content appears as **holographic overlays and terminal projections within the 3D scene** — not as a separate 2D layer. The single exception is the architecture blueprint diagram, which is rendered as a holographic panel floating in the server room environment.

### Hood Storytelling Device

The figure's hood state carries narrative meaning:
- **Hood UP** = Vulnerable, exposed, danger scenes (opening hook, DNS leak danger side, forgotten command)
- **Hood DOWN** = In control, safe, resolution scenes (Tor nodes, closing shot, verification)

### Colour Storytelling

| Colour | Meaning | Used For |
|--------|---------|----------|
| **Teal (#00d4aa)** | Safe, encrypted, anonymous | Tor trails, encryption layers, safe connections, closing |
| **Amber (#f59e0b)** | Danger, exposed, leaked | DNS leaks, unprotected connections, ISP surveillance |
| **Deep Navy (#0a1628)** | Base environment | All backgrounds |

---

## 3. Visual Identity System

### The Figure

| Attribute | Specification |
|-----------|--------------|
| **Material** | Reflective silver-white chrome finish, polished, catches teal/amber light in reflections |
| **Features** | Completely featureless — no eyes, mouth, nose, ears, hair. Smooth head |
| **Surface** | Perfectly seamless. No lines, seams, joints, cracks, or artifacts |
| **Clothing** | Olive-khaki oversized hoodie with drawstrings, dark fitted trousers, minimal dark shoes |
| **Proportions** | Natural average human proportions |
| **Body type** | Neutral |

### The Environments

| Element | Specification |
|---------|--------------|
| **Base palette** | Deep navy-black (#0a1628) |
| **Server room** | Dark server racks with teal (#00d4aa) LED indicators, polished concrete floor |
| **Void scenes** | Pure dark void with volumetric fog, minimal environmental detail |
| **Floor** | Always reflective — catches light sources and colour accents |
| **Fog** | Volumetric, concentrated in lower third, catches coloured light sources |
| **Lighting** | Dramatic, directional. Strong rim lighting. Deep shadows |

### Data Visualization Language

| Element | Visual Treatment |
|---------|-----------------|
| **Encrypted data in transit** | Teal luminous particle trails with concentric rings (layers = encryption depth) |
| **Exposed/leaked data** | Amber scattered particles, fragmented, chaotic |
| **Tor relay nodes** | Teal crystalline icospheres with bright edges, luminous white-teal cores, orbiting particles |
| **ISP surveillance** | Dark monolithic structure with glowing amber circular "eye" indicator |
| **Holographic UI panels** | Semi-transparent dark glass with teal glowing borders, monospace text |
| **Encryption layers** | Concentric translucent teal shells around a warm white data core |
| **Protective encryption** | Teal translucent bubble/cocoon surrounding the figure |

### Full Colour Palette

| Colour | Hex | Usage |
|--------|-----|-------|
| Deep Navy-Black | `#0a1628` | All backgrounds |
| Teal | `#00d4aa` | Safe/encrypted elements, Tor nodes, data trails |
| Bright Teal | `#06ffd0` | Highlights, bright accents on nodes |
| Amber-Orange | `#f59e0b` | Danger, leaks, ISP surveillance, exposed data |
| Danger Red-Amber | `#ef4444` | Critical warnings, ISP eye indicators |
| Cool White | `#94a3b8` | Neutral data, unencrypted connections |

---

## 4. Reference Image System

### Why References Matter

Text prompts alone produce inconsistent results across 15+ generations — the figure's material drifts, lighting shifts, node designs diverge. Feeding approved reference images into every generation via the edit endpoint anchors the model to specific visual decisions.

### The Three Reference Sheets

#### Reference 1: Character Detail Sheet
**What it locks:** Chrome material finish, hoodie colour/texture, hood up vs down states, sleeve/cuff detail, fabric contrast against chrome skin.

**Generation prompt:**
```
A character concept art turnaround sheet showing a featureless human figure 
in three poses arranged side by side on a pure deep navy-black background 
(#0a1628). 

LEFT: Front-facing view, standing neutral pose, arms relaxed at sides. 
CENTER: Three-quarter front view, standing with weight shifted slightly 
to one side, one hand raised to chest height as if gesturing. 
RIGHT: Side profile view, standing straight.

The figure has absolutely no facial features — no eyes, no mouth, no nose, 
no ears, no hair. Completely smooth featureless head. The entire body 
surface is fully smooth, reflective, polished silver-white material with 
a chrome-like finish that catches light beautifully. No lines, no seams, 
no joints, no cracks, no artifacts anywhere on the surface. The reflections 
on the surface subtly show the surrounding teal and amber lighting.

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

**What to evaluate:**
- Chrome material: polished ceramic/chrome, not plastic
- Featureless face: smooth and intentional in all poses
- Hoodie contrast: dark fabric against reflective skin
- Teal/amber reflections visible in surface
- Consistency across all poses

**Note:** The model generated the hoodie as olive-khaki rather than charcoal. This was approved and kept — it creates warm earthy contrast against the chrome that works better than pure charcoal.

#### Reference 1B: Character Full Body Turnaround
**What it locks:** Full body proportions, legs, shoes, hood-down state from all angles.

**Generation prompt:**
```
A character concept art turnaround sheet showing a featureless human figure 
in three poses arranged side by side on a pure deep navy-black background 
(#0a1628). 

LEFT: Front-facing view, standing neutral pose, arms relaxed at sides. 
CENTER: Three-quarter front view, standing with weight shifted slightly 
to one side, one hand raised to chest height as if gesturing. 
RIGHT: Side profile view, standing straight.

[Same figure description as Reference 1]

Professional concept art layout. Studio lighting. Ultra-realistic 3D 
rendering. Crisp, sharp detail. No motion blur.
```

**Result:** The model generated a 4-pose turnaround (front, 3/4, side, back) which was even more useful than requested.

#### Reference 2: Environment & Colour Bible
**What it locks:** Navy-black base colour, teal accent behaviour, amber accent behaviour, split lighting for comparison shots, volumetric fog density, floor reflectivity.

**Generation prompt:**
```
A cinematic environment and colour reference guide for a 3D animated 
documentary. No people or characters. Six panels arranged in a 3x2 grid 
showing lighting scenarios and colour palette.

TOP LEFT — "Primary Environment": A vast dark server room interior. Deep 
navy-black walls (#0a1628) fading into darkness. Rows of dark server racks 
receding into background with subtle teal (#00d4aa) LED indicator lights. 
Polished dark concrete floor reflecting all light sources. Single cool 
white overhead spotlight creating a focused pool of light in center. 
Volumetric fog in the lower third catching the light. Cinematic noir.

TOP CENTER — "Teal Accent Lighting": Same dark environment dominated by 
teal (#00d4aa) light. Teal light sources from server racks cast cool 
blue-green light across surfaces and fog. Represents "safe/encrypted" state.

TOP RIGHT — "Amber Accent Lighting": Same dark environment dominated by 
warm amber-orange (#f59e0b) light. Amber light spills from warning 
indicators. Represents "danger/exposed" state.

BOTTOM LEFT — "Split Lighting": Dark environment lit with teal from left 
and amber from right, showing how the two accent colours coexist in 
comparison scenes. Visible divide where they meet.

BOTTOM CENTER — "Volumetric Fog Reference": Close-up of fog catching 
multiple light sources. Demonstrates atmospheric density and behaviour.

BOTTOM RIGHT — "Colour Palette Swatch": Clean graphic showing five colour 
swatches: Deep Navy-Black (#0a1628), Teal (#00d4aa), Bright Teal (#06ffd0), 
Amber-Orange (#f59e0b), Danger Red-Amber (#ef4444).

Professional reference layout. Ultra-realistic 3D rendering. 16:9.
```

#### Reference 3: Props & UI Elements
**What it locks:** Holographic terminal panel design, Tor relay node icosphere design, encrypted vs leaked data trail visual language, ISP surveillance monolith design.

**Generation prompt:**
```
A prop and UI element reference sheet for a 3D animated documentary about 
network privacy. No people. Six panels on deep navy-black background.

TOP LEFT — "Holographic Terminal Panel": Floating semi-transparent dark 
glass panel with thin bright teal (#00d4aa) glowing border. Displays teal 
monospace terminal text. Soft teal glow illuminates nearby fog.

TOP CENTER — "Tor Relay Node": Glowing icosphere of translucent teal 
crystalline material with bright edges and luminous white-teal core. Teal 
light trails extend from sides. Orbiting light particles. Floats above 
reflective dark surface.

TOP RIGHT — "Data Trail - Encrypted": Horizontal teal light trail with 
three concentric rings representing triple-layer encryption. Flowing 
particles suggest directional motion.

BOTTOM LEFT — "Data Trail - Exposed/Leaked": Horizontal amber-orange 
light trail. Scattered fragmented particles, no concentric rings. Looks 
vulnerable compared to encrypted trail.

BOTTOM CENTER — "ISP Surveillance Structure": Dark imposing monolithic 
structure with single glowing amber circular eye indicator. Ominous.

BOTTOM RIGHT — "Network Path Composition": Small demo showing nodes 
connected by trails to a server — the Tor relay path visual language.

Professional design reference layout. Ultra-realistic 3D rendering. 16:9.
```

**Post-generation edit:** The initial terminal text was garbled. Used the edit endpoint with the generated image as reference to fix it:
```
Edit this reference sheet. Keep all six panels exactly as they are. 
Make only these two changes:

1. TOP LEFT: Replace garbled text with three clean lines:
Line 1: $ curl --proxy socks5h://127.0.0.1:9050
Line 2: https://check.torproject.org/api/ip
Line 3: {"IsTor": true, "IP": "185.220.101.16"}

2. BOTTOM RIGHT: Make the network path diagram larger, filling more 
of the panel.

Change nothing else.
```

### Which References to Use Per Shot

| Scene Type | References Needed |
|------------|------------------|
| Figure in dark void (no network elements) | Character detail sheet + Character full body turnaround |
| Figure with nodes/trails/UI elements | Character detail + Full body + Props/UI reference |
| Figure in server room | Character detail + Full body + Environment/colour reference |
| Server room with network elements | Character detail + Full body + Environment + Props/UI |
| Standalone diagram/technical | Environment/colour reference only |

---

## 5. Generation Platform & Settings

### Platform: Enhancor.ai
- **Text-to-image model:** Kora Nano Banana 2
- **Image editing (with references):** Nano Banana 2 edit endpoint
- **Reference images:** Fed via the edit endpoint as input images alongside text prompts

### Standard Settings

| Setting | Value |
|---------|-------|
| Aspect Ratio | 16:9 (landscape YouTube standard) |
| Resolution | 2K for scene stills, 4K for reference sheets |
| Output Format | PNG |

### Cost Summary
- Reference sheets (4K, ~6 generations including iterations): ~$1-2
- Scene stills (2K, 15 shots + 2 re-generations): ~$1.50
- **Total image generation cost: ~$3-4**

---

## 6. Master Prompt Architecture

### Prompt Structure

Every scene prompt follows this structure:

```
[CONTEXT] — What type of scene and which references to match
[FIGURE DESCRIPTION] — Character details anchored to reference
[SCENE CONTENT] — What's happening, what elements are present
[ENVIRONMENT] — Setting, lighting, atmosphere
[CAMERA] — Angle, lens, depth of field
[TECHNICAL] — Rendering quality, format, style
[REFERENCE ANCHOR] — Explicit instruction to match reference images
```

### Key Prompt Patterns That Work

**For the figure (always include):**
```
The featureless chrome mannequin figure from the reference — same 
reflective silver-white material, same olive hoodie with hood [UP/DOWN]
```

**For cinematic quality (always end with):**
```
Film grain. Ultra-realistic 3D rendering. Cinematic 16:9 composition.
```

**For camera angles:**
- Power/scale: `Wide establishing shot, low angle looking slightly up`
- Intimacy/vulnerability: `Over-the-shoulder medium shot, slight high angle`
- Technical detail: `Eye-level close-up, 85mm portrait lens`
- Empowerment: `Medium shot, slight low angle looking up`
- Surveillance: `High angle shot looking down`

**For lighting presets:**
- Danger/exposure: `Harsh amber spotlight from above, deep shadows`
- Safety/anonymity: `Cool teal rim lighting from behind, face in shadow`
- Comparison: `Split lighting — teal left, amber right`
- Resolution: `Calm teal-tinted atmosphere, clean minimal fog`

**For implied animation (Category A shots):**
```
The figure is caught mid-moment, slightly turning toward...
Small bright particles flow along the trails from left to right...
```

### What NOT to Include in Prompts

- Don't include text labels for Category A shots (those get Veo animation — text warps)
- Don't describe too many simultaneous actions (model gets confused)
- Don't mix 2D and 3D instructions in the same prompt
- Don't reference specific hex codes for the figure material — describe it visually instead

---

## 7. Scene-by-Scene Prompt Library

### Shot Categories

| Category | Animation Approach | Text Strategy |
|----------|-------------------|---------------|
| **A — Hero Animation** | Full Veo 3.1 motion (camera, particles, fog) | NO text in still — add in CapCut post |
| **B — Locked Frame** | Minimal Veo (ambient pulse, particle drift, static camera) | Text baked into screens/surfaces OK |
| **C — Static** | No Veo — animated with CapCut keyframes/motion graphics | Can include detailed text/diagrams |

### Complete Shot List

| # | Shot | Category | Hood | References | Description |
|---|------|----------|------|------------|-------------|
| 1.1 | Hook — Exposed Figure | A | UP | Char only | Figure at desk, amber data trails leaking everywhere |
| 1.2 | IP Address Reveal | B | UP | Char only | Close-up, amber IP hologram on chest |
| 2.1 | Direct Connection | A | UP | Char only | Exposed amber trail to server, watchers below |
| 2.2 | The Watchers | B | DOWN | Char + Env | Figure in server room spotlight, amber surveillance panels |
| 3.1 | Three Tor Nodes | A | DOWN | Char + Props | Wide panoramic, three icospheres, encryption layer trail |
| 3.2 | Encryption Layers | A | — | Char + Props | Macro close-up of onion data orb being peeled |
| 3.3 | Guard Node Perspective | A | DOWN | Char + Props | Behind node looking at figure (clear) vs destination (fog) |
| 4.1 | DNS Leak Split | B | UP/DOWN | Char + Props | Split screen — amber danger left, teal safe right |
| 5.1 | Proxychains Intercept | A | DOWN | Char + Props | Teal hexagonal shield redirecting amber particles |
| 6.1 | Blueprint Diagram | C | — | Env + Props | Holographic architecture diagram in server room |
| 6.2 | ISP View / Cocoon | A | DOWN | Char + Env | Figure in teal encryption bubble, ISP watching helplessly |
| 7.1 | macOS SIP Trap | B | UP | Char + Env | Split — amber locked screen vs teal unlocked screen |
| 7.2 | Forgotten Command | B | UP | Char + Props | Row of teal terminals, one amber leaking upward |
| 8.1 | Verification Terminal | B | DOWN | Char + Props | Figure at desk, teal holographic terminal, confident |
| 8.2 | Disappearance / Close | A | DOWN | Char only | Callback to 1.1 — teal glow, no trails, deactivated watchers |

### Full Prompts

All 15 scene prompts are documented in the companion file: `remaining-scene-prompts.md`

---

## 8. Animation Pipeline (Veo 3.1)

### Shot Categories for Animation

**Category A — Full Veo Motion:**
Shots 1.1, 2.1, 3.1, 3.2, 3.3, 5.1, 6.2, 8.2

Generate WITHOUT text. Prompt Veo for:
- Slow cinematic camera movement (dolly-in, gentle pan)
- Particle flow along data trails
- Volumetric fog drift
- Subtle ambient light pulsing

Example Veo prompt:
```
Slow cinematic camera dolly-in. Luminous teal data particles flow 
along the light trail from left to right. The figure's reflective 
surface catches shifting light. Subtle volumetric fog drifts. Dark 
ambient atmosphere. No camera shake. Smooth controlled movement.
```

**Category B — Locked Frame + Ambient:**
Shots 1.2, 2.2, 4.1, 7.1, 7.2, 8.1

Text baked into the still. Prompt Veo for:
- Static camera, NO movement
- Subtle light pulsing on holographic elements
- Faint particle dust drift
- Gentle glow fluctuation

Example Veo prompt:
```
Static camera, no movement. Subtle ambient light pulsing on holographic 
displays. Faint particle dust drifting. Gentle glow fluctuation on 
teal and amber light sources. The figure remains perfectly still.
```

**Category C — CapCut Only:**
Shot 6.1

No Veo animation. Animate in CapCut with keyframe zoom/pan on the still image, plus motion graphic elements (lines drawing on, labels appearing).

### Veo 3.1 Settings
- **Resolution:** 1080p or 4K
- **Duration:** 8 seconds per clip (native)
- **Scene Extension:** Chain clips using final frame of previous clip as input for next
- **Ingredients to Video:** Feed scene still + character reference + environment reference (up to 4 images)
- **Cost:** ~$0.40/second standard, ~$0.15/second fast

### Scene Extension Technique
For shots needing >8 seconds:
1. Generate clip 1 from the scene still
2. Screenshot the final frame of clip 1
3. Feed that frame as the ingredient for clip 2
4. Repeat for clip 3 if needed
5. This creates smooth continuous camera movement across 16-24 seconds

---

## 9. Post-Production (CapCut)

### Text Overlays
- All Category A shots need text added in CapCut (terminal commands, IP addresses, labels)
- Style: White or teal monospace font with subtle glow effect
- Match the holographic panel aesthetic from the props reference

### Colour Grade
- Desaturate 15-20% globally
- Boost contrast +10%
- Teal/orange colour grade (reinforce what's already in the AI generation)
- Subtle film grain overlay
- Slight vignette on all shots

### Sound Design
- Dark ambient electronic score (Trent Reznor / Atticus Ross style)
- Keyboard/typing SFX for terminal moments
- Digital data whoosh sounds for light trails
- Subtle bass thrum for danger/amber moments
- Clean confident VO — authoritative but accessible

### Edit Rhythm (fern-style)
- Scene cuts every 3-5 seconds
- Visual change at every sentence boundary
- B-roll inserts between primary shots
- 90-second micro-cliffhangers between beats

### Auto-Captions
- White monospace font, subtle dark background
- Match the holographic text aesthetic

---

## 10. Lessons Learned

### What Worked Well

1. **Reference image system** — Feeding approved references into every generation dramatically improved consistency across 15+ shots. Without this, the figure's material and proportions would drift.

2. **Letting the model surprise you** — Several shots came back better than described. The watchers in Shot 2.1 became hooded shadow figures with red eyes (not what was prompted, but more effective). The surveillance panels in Shot 2.2 self-labelled with real tracking categories. Accept good accidents.

3. **Olive hoodie colour** — The model defaulted to olive-khaki instead of the prompted dark charcoal. This was kept because it creates better contrast against the chrome skin and reads clearly in the dark environments.

4. **Hood up/down as narrative device** — Small detail, huge impact. Viewers won't consciously notice, but the emotional shift between "vulnerable" (hood up) and "in control" (hood down) reinforces the story arc.

5. **Edit endpoint for fixes** — When a shot's background was wrong (Shot 8.1 skyline), using the edit endpoint with the generated image as reference to fix just the background while preserving everything else was fast and effective.

### What to Watch For

1. **Environment drift** — Without the environment reference, the model occasionally generates office settings or cityscapes instead of the dark void. Always include relevant environment reference for server room shots.

2. **Text rendering** — Nano Banana 2 handles short text well but garbles longer strings. For Category A shots, skip text entirely. For Category B, keep text short or accept that it'll need cleanup in CapCut.

3. **Consistency across sessions** — If generating across multiple days/sessions, always re-upload the same reference images. Don't rely on the model "remembering" the style.

4. **2D vs 3D mismatch** — A pure flat 2D diagram broke the visual consistency of the whole set. Solved by rendering it as a holographic panel floating in the 3D server room environment instead.

5. **Props reference for any scene with network elements** — If the shot has a Tor node, data trail, ISP monolith, or holographic panel, include the props reference. Otherwise the designs diverge from the established visual language.

### Generation Order for Future Projects

1. Generate reference sheets first (character, environment, props)
2. Approve and iterate until perfect (~$2 budget)
3. Generate bookend shots first (opening and closing) to verify consistency
4. Batch remaining shots grouped by reference combination
5. Fix any background/consistency issues with the edit endpoint
6. Review full set as a sequence before moving to animation

---

## File Structure

```
privacy-toolkit/
├── README.md                          # Privacy toolkit documentation
├── VIDEO_PRODUCTION_GUIDE.md          # This file
├── video-assets/
│   ├── references/
│   │   ├── REF1_character_detail.jpeg
│   │   ├── REF1B_character_fullbody.jpeg
│   │   ├── REF2_environment_colour.jpeg
│   │   └── REF3_props_ui.jpeg
│   ├── scene-stills/
│   │   ├── S1_1_hook_exposed.jpeg
│   │   ├── S1_2_ip_reveal.jpeg
│   │   ├── S2_1_direct_connection.jpeg
│   │   ├── S2_2_watchers.jpeg
│   │   ├── S3_1_tor_nodes.jpeg
│   │   ├── S3_2_encryption_layers.jpeg
│   │   ├── S3_3_guard_perspective.jpeg
│   │   ├── S4_1_dns_leak_split.jpeg
│   │   ├── S5_1_proxychains.jpeg
│   │   ├── S6_1_blueprint_diagram.jpeg
│   │   ├── S6_2_isp_cocoon.jpeg
│   │   ├── S7_1_sip_trap.jpeg
│   │   ├── S7_2_forgotten_command.jpeg
│   │   ├── S8_1_verification.jpeg
│   │   └── S8_2_closing.jpeg
│   └── prompts/
│       └── remaining-scene-prompts.md
```

---

## License

MIT License. This guide is part of the [SIPHIO Privacy Toolkit](https://github.com/siphio/privacy-toolkit).
