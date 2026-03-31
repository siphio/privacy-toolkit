# SIPHIO Privacy Toolkit — Video Style Reference & Master Prompt Guide

---

## 1. DESIGN CONCEPT

### Vision Statement
A cinematic 3D documentary explainer that merges **fern's** emotionally immersive mannequin storytelling with **Blackfiles HD's** dark tech-informational aesthetic. The result: a privacy toolkit walkthrough that *feels* like a high-budget documentary but *teaches* like the best technical explainer.

### Two Visual Modes

| Mode | Purpose | When Used |
|---|---|---|
| **Cinematic Story** | Emotional narrative, spatial metaphors | Hook, transitions, the "journey" through Tor |
| **In-World Technical** | Teaching mechanisms, showing commands | DNS leaks, socks5 comparison, verification |

The modes share the same 3D world — technical content appears as **holographic overlays and terminal projections within the scene**, not as a separate 2D layer. The only exception is the **complete architecture diagram** which breaks into a clean 2D blueprint-style layout as the visual "money shot."

---

## 2. VISUAL IDENTITY

### The Figure
- **Material:** Reflective silver-white, polished ceramic/chrome finish
- **Features:** Completely featureless — no eyes, mouth, ears, or hair
- **Surface:** Perfectly seamless and ultra-polished. NO lines, seams, joints, cracks, or artifacts
- **Body type:** Neutral, average human proportions
- **Clothing:** When clothed, simple dark or neutral garments (hoodie, jacket) that contrast with the reflective skin. Otherwise nude mannequin form
- **Posture conveys emotion:** Hunched = vulnerable, upright = in control, leaning forward = curiosity

### The Environments
- **Primary palette:** Deep navy (#0a1628) base, teal (#00d4aa) for data/positive elements, warm amber (#f59e0b) for danger/warnings
- **Lighting:** Dramatic, directional. Strong rim lighting in teal or amber. Deep shadows. Volumetric haze/fog for atmosphere
- **Surfaces:** Dark concrete, brushed metal, glass panels. Server rooms, dark offices, abstract void spaces
- **Mood:** Cinematic noir — think Blade Runner 2049 meets a premium tech presentation

### Data Visualization Language
- **Data in motion:** Teal luminous particle trails / light streams
- **Danger / leaks:** Amber/orange glowing paths, fractured/scattered particles
- **Encryption layers:** Concentric translucent shells around data (like actual onion layers), each a slightly different teal shade
- **Nodes (Tor relays):** Glowing geometric structures — cubes or spheres — floating in dark space, connected by light trails
- **IP addresses / text:** Rendered as holographic projections floating in the scene, monospace font, slight glow
- **Terminal output:** Projected onto surfaces (desks, walls, floating screens) within the 3D scene — NOT as a post-production overlay

### Color Coding System
| Element | Color | Hex |
|---|---|---|
| Safe / encrypted / anonymous | Teal | #00d4aa |
| Danger / leak / exposed | Amber-orange | #f59e0b |
| Neutral data flow | Cool white-blue | #94a3b8 |
| Your figure / identity | Silver-white (reflective) | — |
| Background / void | Deep navy-black | #0a1628 |
| Tor nodes | Bright teal glow | #06ffd0 |
| ISP / surveillance | Warm red-amber | #ef4444 |

---

## 3. MASTER BASE PROMPT

This is the foundation prompt that should prefix every scene generation. Adjust the **[SCENE-SPECIFIC]** block per shot.

```
A highly stylized 3D render in cinematic documentary style. Deep navy-black 
environment (#0a1628) with dramatic teal (#00d4aa) and warm amber (#f59e0b) 
accent lighting. Volumetric haze and atmospheric fog. The scene features a 
featureless human figure with no facial features, fully smooth and reflective 
silver-white polished material — no lines, no seams, no joints, no cracks, 
no artifacts on the figure's surface.

[SCENE-SPECIFIC DESCRIPTION]

Cinematic 16:9 composition. Ultra-realistic 3D rendering. Shallow depth of 
field with bokeh on background elements. Film grain overlay. Desaturated 
color palette with selective teal and amber highlights. Documentary framing.
```

### Prompt Modifiers (append as needed)

**Camera angles:**
- `Wide establishing shot, low angle looking up` — for power/scale
- `Over-the-shoulder medium shot` — for intimate/focused moments  
- `Eye-level close-up on hands/desk` — for technical detail
- `Top-down surveillance-style angle` — for vulnerability/exposure
- `Dramatic Dutch angle` — for tension moments (DNS leak reveal)
- `Slow dolly-in framing` — for reveals

**Lighting presets:**
- `Harsh cold overhead fluorescent lighting` — sterile, exposed, ISP surveillance
- `Warm amber side lighting through blinds` — danger, warning scenes
- `Cool teal rim lighting from behind, face in shadow` — anonymity, stealth
- `Split lighting — teal left, amber right` — comparison shots (safe vs unsafe)
- `Soft diffused overhead with strong backlight` — resolution, success

**Atmosphere presets:**
- `Heavy volumetric fog, light rays cutting through` — mystery, the unknown
- `Clean minimal atmosphere, sharp focus` — technical clarity
- `Particle dust floating in light beams` — data in transit
- `Dark with isolated pools of light` — isolation, anonymity

---

## 4. SCENE-BY-SCENE PROMPT GUIDE

### BEAT 1: THE HOOK (0:00 - 0:30)
*Narration: "Every time you go online, you leave a trail..."*

**Shot 1.1 — The Exposed Figure**
```
[SCENE] The figure sits alone at a minimal desk with a glowing laptop screen 
in a vast dark void. Hundreds of thin amber light trails emanate from the 
figure's body in all directions, stretching into the darkness — representing 
data leaking everywhere. The figure is hunched, unaware. The trails connect 
to faint, ominous shapes in the far background (surveillance towers, server 
racks). Over-the-shoulder medium shot, slight high angle looking down at the 
figure. Heavy volumetric fog with amber-tinted light.
```

**Shot 1.2 — The IP Address Reveal**
```
[SCENE] Close-up on the figure's chest/torso area. A holographic text label 
floats in front of the figure reading "IP: 86.185.130.249" in glowing amber 
monospace font. Thin amber data trails connect from the text outward in all 
directions. The figure's reflective surface shows distorted reflections of 
the text. Eye-level close-up, shallow depth of field. Dark background with 
single harsh amber spotlight from above.
```

---

### BEAT 2: HOW THE INTERNET NORMALLY WORKS (0:30 - 1:15)
*Narration: "Before understanding how to disappear, you need to understand what happens when you type a URL..."*

**Shot 2.1 — The Direct Connection**
```
[SCENE] Wide shot showing the figure on the left at a desk, and a large 
glowing server structure on the far right, connected by a single bright 
exposed amber light trail running directly between them. Above the trail, 
small holographic labels float: "DNS Query", "TCP Connection", "HTTP Request". 
Below the trail, a row of dark watching shapes (representing ISP, network 
observers) with small red indicator lights, all facing the exposed trail. 
Wide establishing shot, low angle. Clean atmosphere with the light trail 
cutting through darkness.
```

**Shot 2.2 — The Watchers (Who Sees What)**
```
[SCENE] The figure stands in the center of a dark circular room, spotlight 
from directly above. Surrounding the figure at different distances are four 
translucent wall-like panels arranged in a ring. Each panel has a holographic 
label: "Your ISP", "The Website", "Your Network", "Government". Each panel 
glows with a different intensity of amber — the ISP panel glows brightest 
and closest. Thin amber data lines connect from the figure to each panel. 
High angle shot looking down into the circular room. Dramatic pool of light 
on the figure, panels partially in shadow.
```

---

### BEAT 3: TOR — THE ONION ROUTER (1:15 - 2:45)
*Narration: "Tor works by wrapping your data in layers of encryption, like the layers of an onion..."*

**Shot 3.1 — The Three Nodes**
```
[SCENE] Wide panoramic shot of a dark void with three large glowing teal 
geometric structures (spheres or cubes) arranged in a line from left to 
right, connected by luminous teal light trails. The figure stands small on 
the far left. A larger server structure sits on the far right (the website). 
Each node is labeled with floating holographic text: "GUARD", "MIDDLE", 
"EXIT". The light trail between the figure and Guard node is triple-layered 
(three concentric glowing rings around the trail). Between Guard and Middle, 
double-layered. Between Middle and Exit, single-layered. Between Exit and 
the server, the trail turns plain white — unencrypted. Wide establishing 
shot, slightly low angle for grandeur. Volumetric teal-tinted fog.
```

**Shot 3.2 — The Encryption Layers (Onion Metaphor)**
```
[SCENE] Close-up on a glowing orb of data floating in dark space. The orb 
has three visible concentric translucent shells — outer shell bright teal, 
middle shell medium teal, inner shell deep teal with a warm white core 
(the actual data). The outer shell is being peeled away by abstract light 
tendrils reaching from a nearby Guard node structure. Macro close-up, very 
shallow depth of field. Background is pure dark void with subtle particle 
dust. Teal rim lighting.
```

**Shot 3.3 — Guard Node Perspective**
```
[SCENE] View from behind the Guard node structure, looking back at the 
figure. The figure is clearly visible (amber highlight on the figure — the 
Guard knows your IP). But looking forward from the Guard toward the Middle 
and Exit nodes, the path dissolves into obscured fog and scattered light — 
the Guard cannot see the destination. Split composition: clear/sharp on the 
left (figure visible), foggy/obscured on the right (destination hidden). 
Over-the-shoulder shot from behind the Guard node. Split teal/fog lighting.
```

**Shot 3.4 — Exit Node Perspective (Reverse)**
```
[SCENE] View from behind the Exit node, looking at the website server 
(clearly visible in amber light on the right). Looking backward through the 
relay chain, the Middle and Guard nodes are obscured in fog, and the figure 
is completely invisible — hidden in darkness. Reverse composition of Shot 
3.3: foggy/dark on the left (identity hidden), clear/sharp on the right 
(destination visible). Over-the-shoulder shot from behind the Exit node.
```

---

### BEAT 4: SOCKS5 vs SOCKS5h — THE DNS LEAK (2:45 - 3:45)
*Narration: "This single letter — 'h' — is the difference between anonymous and exposed..."*

**Shot 4.1 — The Dangerous Path (socks5://)**
```
[SCENE] Split scene. The figure sits at a desk on the left. Two paths 
emanate from the figure. Path 1 (amber/danger) goes DIRECTLY upward to a 
large structure labeled "ISP DNS" — this path is bright, exposed, dangerous. 
Path 2 (teal/safe) goes right through Tor nodes to the server. But the 
damage is done — the ISP already sees the DNS query. The ISP structure has 
a glowing amber eye-like indicator. Holographic terminal text floats near 
the figure: "socks5://127.0.0.1:9050". Wide shot, dramatic split lighting — 
amber on the DNS leak side, teal on the Tor side.
```

**Shot 4.2 — The Safe Path (socks5h://)**
```
[SCENE] Same composition as 4.1 but transformed. Now there is only ONE path 
from the figure — it goes entirely through the teal Tor relay chain. The DNS 
query resolves at the Exit node (small holographic "DNS" label at the Exit). 
The ISP structure is now dark, inactive, seeing nothing. The whole scene is 
bathed in calm teal light. Holographic terminal text near the figure reads: 
"socks5h://127.0.0.1:9050" with the "h" highlighted in bright teal. Wide 
shot, unified teal lighting. Clean atmosphere.
```

---

### BEAT 5: PROXYCHAINS (3:45 - 4:30)
*Narration: "Some apps ignore your proxy settings entirely. Proxychains intercepts them..."*

**Shot 5.1 — The Interception**
```
[SCENE] The figure reaches toward a floating application icon/window. But 
between the figure's hand and the app, a translucent teal shield/barrier 
has materialized — this is Proxychains. The app's data (small amber light 
particles) hits the shield and is redirected downward through a teal conduit 
toward the Tor proxy. Without the shield, the particles would have gone 
straight out into the exposed dark void. Medium shot, eye level. The shield 
has subtle hexagonal patterns. Teal glow emanating from the barrier.
```

---

### BEAT 6: THE COMPLETE STACK (4:30 - 5:15)
*Narration: "Here's how it all fits together..."*

**Shot 6.1 — The Blueprint (2D BREAKOUT — the one exception)**
```
[SCENE] THIS IS THE ONLY 2D-STYLE SHOT. Clean dark navy background. A 
technical blueprint/schematic showing the complete data path: 

YOUR MACHINE (figure icon) → Tor Daemon (localhost:9050) → [encrypted 
tunnel] → GUARD NODE → MIDDLE NODE → EXIT NODE → TARGET WEBSITE

Each component is rendered as a clean line-art diagram with teal accent 
lines on dark navy. Connection lines show encryption state. Labels are 
crisp monospace white text. The style resembles an engineering blueprint 
or architectural drawing — clean, precise, authoritative. 16:9 layout 
optimized for readability. Subtle grid lines in the background.
```

**Shot 6.2 — What Your ISP Sees**
```
[SCENE] Return to 3D. The figure sits at the desk, fully wrapped in a 
glowing teal cocoon of encryption. In the background, the ISP structure 
watches but can only see a single opaque teal stream going to a generic 
IP address (the Guard node). Holographic text near the ISP reads: "Sees: 
encrypted traffic to [Guard IP]. Nothing else." The ISP structure is 
dimmed, frustrated, impotent. Medium-wide shot. The figure glows with 
quiet confidence. Cool teal atmosphere.
```

---

### BEAT 7: COMMON MISTAKES (5:15 - 6:15)
*Narration: "All of this breaks if you make one of these mistakes..."*

**Shot 7.1 — macOS SIP Trap**
```
[SCENE] Two terminal screens side by side, projected onto a wall in the 
dark environment. Left screen (amber glow, DANGER): shows the path 
"/usr/bin/curl" with a red lock icon and text "SIP PROTECTED — Proxychains 
BLOCKED". Right screen (teal glow, SAFE): shows "/opt/homebrew/bin/curl" 
with a green unlock icon. Between them, the figure looks at the viewer 
(facing camera). The amber screen has thin crack-like amber light lines 
spreading from it like a fracture. Eye-level front-facing shot. Split 
amber/teal lighting.
```

**Shot 7.2 — The One Forgotten Command**
```
[SCENE] A row of 10 small holographic terminal windows floating in front 
of the figure. Nine of them glow teal (safe, through Tor). One — the 
middle one — glows bright amber with an exposed data trail shooting 
straight up to the ISP structure above. The figure reaches toward the 
amber window too late. Close medium shot on the row of terminals. The 
amber window is the focal point. Dramatic amber spotlight on the leak.
```

---

### BEAT 8: VERIFICATION & CLOSE (6:15 - 7:00)
*Narration: "Never assume you're anonymous. Always verify..."*

**Shot 8.1 — The Verification**
```
[SCENE] The figure sits at the desk. A large holographic terminal screen 
floats in front of them displaying: {"IsTor": true, "IP": "185.220.101.16"} 
in crisp teal monospace text. The "true" value glows bright teal. Below 
it, a second line shows the comparison: the figure's real IP crossed out 
in amber, replaced by the exit node IP in teal. The figure sits upright, 
confident, in control. Medium shot, slight low angle (empowering). Clean 
teal atmosphere, calm and resolved.
```

**Shot 8.2 — The Disappearance (Final Shot)**
```
[SCENE] Wide shot callback to Shot 1.1. The figure at the desk in the vast 
dark void. But now, instead of amber trails leaking everywhere, the figure 
is wrapped in a subtle teal glow, and no trails extend outward at all. The 
figure is invisible to the watching shapes in the background — they are 
dark, deactivated. The figure sits upright, calm, anonymous. Wide shot, 
same angle as the opening but transformed. Clean, quiet, teal-tinted 
atmosphere. Sense of resolution and safety.
```

---

## 5. NANO BANANA 2 GENERATION NOTES

### Technical Settings
- **Aspect ratio:** 16:9 (mandatory for YouTube)
- **Resolution:** 2K or 4K for final frames (1K for rapid iteration/testing)
- **Output format:** PNG
- **Character consistency:** Use the edit endpoint to feed reference images of the figure back in for each new scene to maintain identity

### Consistency Strategy
1. **Generate the figure first** — Create 3-4 standalone shots of the silver-white figure in different poses against a neutral dark background. These become your reference images.
2. **Feed references into every generation** — Use Nano Banana 2's edit endpoint with your reference figure images as inputs when generating scene stills.
3. **Lock the lighting early** — The first scene you're happy with becomes the lighting reference for all others.
4. **Batch by environment** — Generate all "desk scenes" together, all "void/node scenes" together, etc. to maintain environmental consistency.

### Prompt Engineering Tips for Nano Banana 2
- Use photographic language: "85mm portrait lens", "f/2.8 bokeh", "wide-angle establishing shot"
- Be explicit about what is NOT in the image: "no facial features", "no seams", "no artifacts"
- Describe lighting with direction: "rim light from behind left", "key light from upper right"
- Include the film grain and color grade in the prompt — Nano Banana 2 understands these as stylistic choices
- For text rendering: spell out exactly what the text should say, use quotes, specify the font style ("monospace", "sans-serif")

---

## 6. VEO 3.1 ANIMATION NOTES

### Workflow
1. Generate still with Nano Banana 2
2. Use as "ingredient image" in Veo 3.1
3. Prompt Veo with subtle motion: camera drift, particle animation, light flicker
4. Chain 8-second clips with Scene Extension for longer sequences

### Motion Philosophy
- **Camera:** Slow, deliberate movements. Gentle dolly-in, subtle pan. Never fast or jerky.
- **Data trails:** Flowing particle motion along predetermined paths
- **Holograms:** Subtle float/hover animation, gentle pulse
- **Figure:** Minimal movement. A turn of the head, shift of posture. Stillness = power.
- **Transitions:** Cross-dissolve between scenes, not hard cuts (in edit, not in Veo)

### Key Animation Moments
- Data trails flowing from figure to ISP (Beat 2)
- Encryption layers wrapping around data orb (Beat 3)  
- DNS leak — amber particles shooting to ISP (Beat 4)
- The protective teal cocoon forming around the figure (Beat 8)

---

## 7. CONDENSED SCRIPT OUTLINE (5-8 min)

| Beat | Time | Topic | Shots | Narration Focus |
|---|---|---|---|---|
| 1 — Hook | 0:00-0:30 | You leave a trail | 1.1, 1.2 | IP = home address, why it matters |
| 2 — Normal Internet | 0:30-1:15 | How browsing works | 2.1, 2.2 | DNS → TCP → HTTP, who sees what |
| 3 — Tor | 1:15-2:45 | Three relay system | 3.1-3.4 | Guard/Middle/Exit, encryption layers |
| 4 — DNS Leak | 2:45-3:45 | socks5 vs socks5h | 4.1, 4.2 | The "h" that saves you |
| 5 — Proxychains | 3:45-4:30 | Forcing apps through Tor | 5.1 | Interception metaphor |
| 6 — Full Stack | 4:30-5:15 | Complete architecture | 6.1, 6.2 | Blueprint diagram + ISP view |
| 7 — Mistakes | 5:15-6:15 | 3 biggest gotchas | 7.1, 7.2 | macOS SIP, forgotten commands |
| 8 — Verify & Close | 6:15-7:00 | Prove anonymity | 8.1, 8.2 | Check → callback to opening |

**Total shots: ~14 primary + B-roll transitions**
**Total Nano Banana 2 generations: ~40-60 images (multiple angles/variations per shot)**
**Total Veo 3.1 clips: ~20-25 animated sequences**

---

## 8. POST-PRODUCTION NOTES

### Color Grade
- Desaturate by 15-20% globally
- Boost contrast +10%
- Teal/orange color grade (already baked into the AI generation, reinforce in edit)
- Subtle film grain overlay
- Slight vignette on all shots

### Sound Design
- Dark ambient electronic score (think Trent Reznor/Atticus Ross)
- Keyboard/typing SFX for terminal moments
- Digital data whoosh sounds for light trails
- Subtle bass thrum for danger moments
- Clean, confident VO — not dramatic, authoritative but accessible

### Edit Rhythm (fern-style)
- Scene cuts every 3-5 seconds
- Visual change at every sentence boundary
- B-roll insert between primary shots
- 90-second micro-cliffhangers: end Beat 2 with "But what if none of them could see you?" → Beat 3 Tor reveal
