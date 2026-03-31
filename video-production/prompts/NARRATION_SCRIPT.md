# SIPHIO Privacy Toolkit — Final Narration Script (v2)
# Duration: ~2 minutes (120 seconds)
# Word Count: ~300 words
# 15 shots × 8 seconds each
# Voice: Deep, confident, tutorial-paced documentary tone

---

## BEAT 1: THE HOOK (0:00 - 0:16)

**[Shot 1.2 — IP Address Reveal | 8 sec]**

"Ever wonder how hackers route their entire machine through encrypted relays so their ISP can't see a single packet? This is the exact stack they use."

**[Shot 1.1 — Exposed Figure | 8 sec]**

"Right now, your IP address is attached to every connection you make. It tells websites who your provider is, where you live, and lets anyone track you across the web."

---

## BEAT 2: THE PROBLEM (0:16 - 0:24)

**[Shot 2.1 — Direct Connection | 8 sec]**

"Without protection, your computer connects directly to every server. Your ISP sees every domain. The website sees your IP. Everyone in between is watching."

---

## BEAT 3: TOR (0:24 - 0:56)

**[Shot 3.1 — Three Tor Nodes | 8 sec]**

"Tor routes your traffic through three encrypted relays — Guard, Middle, and Exit. Your data gets wrapped in three layers of encryption."

**[Shot 3.2 — Encryption Layers | 8 sec]**

"Each relay strips one layer. No single relay ever knows both who you are and where you're going."

**[Shot 3.3 — Guard Node Perspective | 8 sec]**

"The guard knows your IP but not the destination. The exit knows the destination but not your IP. That separation is what makes you invisible."

**[Shot 6.2 — ISP Cocoon | 8 sec]**

"Your ISP? All they see is encrypted traffic to one IP address. Nothing else."

---

## BEAT 4: DNS LEAKS (0:56 - 1:12)

**[Shot 4.1 — DNS Leak Split | 8 sec]**

"But one mistake breaks everything. Using socks5 without the 'h' means your DNS queries leak straight to your ISP. They see every domain you look up — even though the traffic goes through Tor."

**[Shot 2.2 — The Watchers | 8 sec]**

"One missing letter. That's the difference between anonymous and completely exposed."

---

## BEAT 5: THE TOOLS (1:12 - 1:36)

**[Shot 5.1 — Proxychains Shield | 8 sec]**

"Proxychains forces applications through Tor at the system level — even apps that don't support proxy settings. It intercepts every network call before it leaves your machine."

**[Shot 7.1 — SIP Trap | 8 sec]**

"On macOS, system binaries are protected by SIP. Using the system curl with proxychains silently fails — traffic goes direct with no warning."

**[Shot 7.2 — Forgotten Command | 8 sec]**

"Run ten commands through Tor but forget the proxy flag on one — that single command exposes your real IP to the target."

---

## BEAT 6: VERIFY + CLOSE (1:36 - 2:00)

**[Shot 8.1 — Verification Terminal | 8 sec]**

"Never assume you're anonymous. Always verify. Hit the Tor project API — if IsTor returns true and the IP isn't yours, you're clean."

**[Shot 6.1 — Blueprint Diagram | 8 sec]**

"Tor, socks5h, proxychains, DNS leak prevention. No single layer is enough. The combination is what makes you untraceable."

**[Shot 8.2 — Disappearance / Close | 8 sec]**

"Now you know the exact stack. Full guide linked below."

---

# SHOT-TO-NARRATION MATCH VERIFICATION

| Time | Shot | What Viewer Sees | What Viewer Hears | Match |
|------|------|-----------------|-------------------|-------|
| 0:00 | 1.2 IP Reveal | Amber IP address blazing on chrome figure | "How hackers route through encrypted relays" | ✅ IP visible = immediate context |
| 0:08 | 1.1 Exposed Figure | Figure leaking amber trails everywhere | "Your IP is attached to every connection" | ✅ Leaking data = the problem |
| 0:16 | 2.1 Direct Connection | Amber trail to server, watchers below | "ISP sees every domain, everyone watching" | ✅ Exposed trail + watchers |
| 0:24 | 3.1 Tor Nodes | Three icospheres, encryption trail | "Three encrypted relays — Guard, Middle, Exit" | ✅ Exact visual match |
| 0:32 | 3.2 Encryption Layers | Onion orb being peeled by node | "Each relay strips one layer" | ✅ Layer being removed |
| 0:40 | 3.3 Guard Perspective | Figure visible, destination foggy | "Guard knows IP, not destination" | ✅ Clear vs fog split |
| 0:48 | 6.2 ISP Cocoon | Teal bubble, ISP powerless above | "ISP sees encrypted traffic, nothing else" | ✅ Protected figure, dim ISP |
| 0:56 | 4.1 DNS Leak Split | Amber leak left, teal safe right | "socks5 without 'h' means DNS leaks" | ✅ Split comparison |
| 1:04 | 2.2 Watchers | Surveillance panels surrounding figure | "Difference between anonymous and exposed" | ✅ Surrounded by trackers |
| 1:12 | 5.1 Proxychains | Teal shield redirecting particles | "Proxychains forces apps through Tor" | ✅ Interception visual |
| 1:20 | 7.1 SIP Trap | Red lock vs green unlock screens | "System curl silently fails" | ✅ Blocked vs safe path |
| 1:28 | 7.2 Forgotten Command | Row of terminals, one amber leak | "Forget proxy on one command" | ✅ One bad terminal |
| 1:36 | 8.1 Verification | Holographic terminal, confident figure | "Hit the Tor API, IsTor returns true" | ✅ Terminal check |
| 1:44 | 6.1 Blueprint | Architecture diagram in server room | "The combination makes you untraceable" | ✅ Full stack visible |
| 1:52 | 8.2 Close | Teal-wrapped figure, safe, resolved | "Now you know the exact stack" | ✅ Resolution callback |

**All 15 shots verified ✅ — every narration line matches its visual.**

---

# DELIVERY NOTES

## Pacing Guide
- Beat 1 (Hook): Energetic, grab attention, slightly faster pace
- Beats 2-3 (Problem + Tor): Steady, clear, explanatory
- Beat 4 (DNS Leak): Slow down on "one mistake breaks everything" — dramatic weight
- Beat 5 (Tools): Quick, punchy, each shot is a distinct warning
- Beat 6 (Close): Calm, confident, resolved — slow down on final line

## Pause Points (add 0.5-1 sec silence)
- After "This is the exact stack they use." (let it land)
- Before "But one mistake breaks everything." (tension build)
- Before "Now you know the exact stack." (resolution breath)

## Emphasis Words (slightly louder/slower in delivery)
- "every connection"
- "three layers"
- "No single relay"
- "one mistake"
- "silently fails"
- "untraceable"

## ElevenLabs Settings
- Voice: Deep male, documentary tone (try "Adam", "Antoni", or "Daniel")
- Stability: 0.50
- Similarity Boost: 0.75
- Style: 0.30
- Speed: 1.0x
- Export: WAV, 44.1kHz, mono

## Text Overlays for CapCut

| Time | Shot | Text Overlay |
|------|------|-------------|
| 0:02 | 1.2 | IP: 86.185.130.249 |
| 0:24 | 3.1 | GUARD → MIDDLE → EXIT |
| 0:58 | 4.1 | socks5:// vs socks5h:// |
| 1:06 | 2.2 | DNS LEAK = EXPOSED |
| 1:20 | 7.1 | /usr/bin/curl ✗ → /opt/homebrew/bin/curl ✓ |
| 1:40 | 8.1 | {"IsTor": true, "IP": "185.220.101.16"} |
| 1:48 | 6.1 | Tor + SOCKS5h + Proxychains + DNS Protection |
| 1:56 | 8.2 | @siphio · Full guide ↓ |

## CTA Strategy
- Final shot (8.2) shows "@siphio · Full guide ↓"
- Pin comment with link to github.com/siphio/privacy-toolkit
- Post caption: "The complete anonymity stack explained in 2 minutes. Full setup guide: [link]"
