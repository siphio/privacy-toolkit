# Video Production Assets

All assets, prompts, and documentation for the SIPHIO Privacy Toolkit explainer video.

## Quick Start — Pick Up Where We Left Off

### What's Done ✅
- Visual identity system designed (chrome mannequin, navy/teal/amber palette)
- 4 reference sheets generated and approved
- 15 scene stills generated and approved
- Narration script written and verified against all shots
- Veo 3.1 animation prompts written for all 15 shots

### What's Next ⬜
1. **Record voiceover** → Use `prompts/NARRATION_SCRIPT.md` in ElevenLabs
2. **Animate scene stills** → Use `prompts/VEO_ANIMATION_PROMPTS.md` with Veo 3.1, feeding each scene still from `scene-stills/` as the ingredient image
3. **Assemble in CapCut** → Drop VO on audio track, lay animated clips in timeline order, add text overlays per the script, colour grade, sound design
4. **Export and post to X**

## Folder Structure

```
video-production/
├── VIDEO_PRODUCTION_GUIDE.md          # Complete production bible
├── README.md                          # This file
├── references/                        # Approved reference sheets
│   ├── REF1_character_detail_sheet.jpeg
│   ├── REF1B_character_fullbody_turnaround.jpeg
│   ├── REF2_environment_colour_bible.jpeg
│   └── REF3_props_ui_elements.jpeg
├── scene-stills/                      # All 15 generated scene images
│   ├── S1_1_hook_exposed_figure.jpeg
│   ├── S1_2_ip_address_reveal.jpeg
│   ├── S2_1_direct_connection.jpeg
│   ├── S2_2_the_watchers.jpeg
│   ├── S3_1_three_tor_nodes.jpeg
│   ├── S3_2_encryption_layers.jpeg
│   ├── S3_3_guard_node_perspective.jpeg
│   ├── S4_1_dns_leak_split.jpeg
│   ├── S5_1_proxychains_intercept.jpeg
│   ├── S6_1_blueprint_diagram_v1_flat.jpeg    # Unused — too flat
│   ├── S6_1_blueprint_diagram_v2_holographic.jpeg  # ✅ Use this one
│   ├── S6_2_isp_cocoon.jpeg
│   ├── S7_1_macos_sip_trap.jpeg
│   ├── S7_2_forgotten_command.jpeg
│   ├── S8_1_verification_terminal_v1.jpeg      # Unused — skyline bg
│   ├── S8_1_verification_terminal_v2_fixed.jpeg  # ✅ Use this one
│   └── S8_2_disappearance_close.jpeg
├── prompts/                           # All generation prompts
│   ├── NARRATION_SCRIPT.md            # Final voiceover script
│   ├── VEO_ANIMATION_PROMPTS.md       # Veo 3.1 prompts for all 15 shots
│   ├── NANO_BANANA_SCENE_PROMPTS.md   # Image generation prompts
│   ├── STYLE_REFERENCE.md             # Master prompt architecture
│   └── REFERENCE_SHEET_GUIDE.md       # How the reference system works
└── scripts/                           # Automation scripts (future)
```

## Shot Timeline (Final Edit Order)

| # | Time | Shot File | Category | Description |
|---|------|-----------|----------|-------------|
| 1 | 0:00 | S1_2_ip_address_reveal | B | Hook — "Ever wonder how hackers..." |
| 2 | 0:08 | S1_1_hook_exposed_figure | A | Problem — IP attached to everything |
| 3 | 0:16 | S2_1_direct_connection | A | Direct connection, watchers watching |
| 4 | 0:24 | S3_1_three_tor_nodes | A | Tor's three relays explained |
| 5 | 0:32 | S3_2_encryption_layers | A | Onion layers being peeled |
| 6 | 0:40 | S3_3_guard_node_perspective | A | Guard knows who, not where |
| 7 | 0:48 | S6_2_isp_cocoon | A | ISP sees nothing |
| 8 | 0:56 | S4_1_dns_leak_split | B | DNS leak — socks5 vs socks5h |
| 9 | 1:04 | S2_2_the_watchers | B | "One missing letter" |
| 10 | 1:12 | S5_1_proxychains_intercept | A | Proxychains shield |
| 11 | 1:20 | S7_1_macos_sip_trap | B | SIP blocks proxychains |
| 12 | 1:28 | S7_2_forgotten_command | B | One forgotten command leaks |
| 13 | 1:36 | S8_1_verification_terminal_v2_fixed | B | Verify with Tor API |
| 14 | 1:44 | S6_1_blueprint_diagram_v2_holographic | C | Full stack diagram |
| 15 | 1:52 | S8_2_disappearance_close | A | "Now you know the exact stack" |

## Key Files to Read First

1. `VIDEO_PRODUCTION_GUIDE.md` — The complete production bible
2. `prompts/NARRATION_SCRIPT.md` — Record this in ElevenLabs
3. `prompts/VEO_ANIMATION_PROMPTS.md` — Use these to animate each still
