# Privacy & Anonymity Toolkit

A comprehensive guide to understanding and implementing network anonymity using Tor, SOCKS5 proxies, Proxychains, and DNS leak prevention on macOS.

Written in plain English for anyone who wants to understand **how** these technologies work, **why** they keep you anonymous, and **what** actually happens to your data as it travels across the internet.

---

## Table of Contents

1. [The Problem: Why You Need Anonymity](#1-the-problem-why-you-need-anonymity)
2. [How the Internet Normally Works](#2-how-the-internet-normally-works)
3. [Tor: The Onion Router](#3-tor-the-onion-router)
4. [SOCKS5 Proxies](#4-socks5-proxies)
5. [Proxychains: Forcing Apps Through Tor](#5-proxychains-forcing-apps-through-tor)
6. [DNS Leaks: The Silent Privacy Killer](#6-dns-leaks-the-silent-privacy-killer)
7. [The Complete Stack: How It All Fits Together](#7-the-complete-stack-how-it-all-fits-together)
8. [macOS SIP and Why It Matters](#8-macos-sip-and-why-it-matters)
9. [Tor Configuration Deep Dive](#9-tor-configuration-deep-dive)
10. [Practical Setup Guide](#10-practical-setup-guide)
11. [Verification: Proving You Are Anonymous](#11-verification-proving-you-are-anonymous)
12. [Common Mistakes That Break Anonymity](#12-common-mistakes-that-break-anonymity)
13. [Threat Model: What This Protects Against](#13-threat-model-what-this-protects-against)

---

## 1. The Problem: Why You Need Anonymity

Every time you visit a website, you leave a trail. Your **IP address** is like your home address on the internet. It tells the website:

- **Who your internet provider is** (e.g., BT, Virgin Media, Sky)
- **Roughly where you live** (city-level accuracy)
- **A unique identifier** that can be used to track you across every site you visit

If you are a security researcher, journalist, whistleblower, or someone conducting authorised security testing, you need to ensure the target cannot trace the activity back to your real identity.

### What "anonymous" actually means

Being anonymous online means that the website or service you connect to:
- Cannot see your real IP address
- Cannot determine your real geographic location
- Cannot link your activity to your ISP account
- Cannot correlate your session with other sessions from your real IP

---

## 2. How the Internet Normally Works

Before understanding anonymity tools, you need to understand what happens when you type a URL into your browser.

### Step by step: Loading a website

```
YOU (IP: 86.185.130.249)
  |
  |-- Step 1: DNS Query
  |   "What is the IP address for example.com?"
  |   Your computer asks your ISP's DNS server
  |   ISP now KNOWS you want to visit example.com
  |
  |-- Step 2: TCP Connection
  |   Your computer connects directly to example.com's server
  |   The server sees YOUR IP address: 86.185.130.249
  |
  |-- Step 3: HTTP Request
  |   Your browser sends "GET / HTTP/1.1"
  |   The server logs your IP, browser type, time, etc.
  |
  |-- Step 4: Response
  |   The server sends the webpage back to YOUR IP
```

### Who can see what?

| Observer | What They See |
|---|---|
| **Your ISP** | Every domain you visit, when, how much data |
| **The website** | Your IP address, location, browser fingerprint |
| **Anyone on your network** | All unencrypted traffic (HTTP) |
| **Government (with warrant)** | Can request ISP logs linking IP to your account |

### The key problem

Your **IP address** is attached to every single connection you make. It is the one piece of information that links your online activity to your real-world identity (via your ISP account).

---

## 3. Tor: The Onion Router

Tor is the core technology that makes you anonymous. It works by routing your traffic through **three random volunteer servers** (called "relays" or "nodes") before it reaches the destination.

### Why "Onion" Router?

Because your data is wrapped in **layers of encryption**, like the layers of an onion. Each relay peels off one layer, revealing only the address of the next relay. No single relay ever knows both where the traffic came from AND where it is going.

### The Three Relays

```
YOU --> [Guard Node] --> [Middle Node] --> [Exit Node] --> WEBSITE

Layer 3 encryption ---|
Layer 2 encryption -----------|
Layer 1 encryption ----------------------|
```

#### Guard Node (Entry Node)
- **Knows:** Your real IP address
- **Does NOT know:** What website you are visiting, or the content of your traffic
- **Role:** Receives your triple-encrypted data, peels off the outer layer, forwards to the Middle Node
- **Selection:** Tor picks a small set of guard nodes and sticks with them for months (to prevent certain attacks)

#### Middle Node (Relay)
- **Knows:** The Guard Node's IP and the Exit Node's IP
- **Does NOT know:** Your real IP address OR the destination website
- **Role:** Receives double-encrypted data, peels off one layer, forwards to the Exit Node
- **Why it exists:** It creates separation. Without it, the Guard and Exit could collude to identify you

#### Exit Node
- **Knows:** The destination website and the content of unencrypted traffic
- **Does NOT know:** Your real IP address (only knows the Middle Node's IP)
- **Role:** Peels off the final layer, sends your request to the actual website
- **Important:** The website sees the Exit Node's IP address, NOT yours

### How the encryption layers work

When you want to visit `example.com`:

1. **Your Tor client** picks 3 relays: Guard (G), Middle (M), Exit (E)
2. It obtains the **public encryption keys** of all three relays
3. It encrypts your request three times:

```
Original:    "GET / HTTP/1.1 Host: example.com"

Encrypt for Exit:    E_key("GET / HTTP/1.1 Host: example.com")
Encrypt for Middle:  M_key(E_key("GET / HTTP/1.1 Host: example.com"))
Encrypt for Guard:   G_key(M_key(E_key("GET / HTTP/1.1 Host: example.com")))
```

4. The triple-encrypted blob is sent to the Guard Node
5. Guard decrypts outer layer with its private key, sees Middle Node address, forwards
6. Middle decrypts its layer, sees Exit Node address, forwards
7. Exit decrypts final layer, sees the actual HTTP request, sends it to example.com
8. The response travels back through the same path in reverse

### Why this makes you anonymous

| If someone controls... | They can learn... |
|---|---|
| The Guard Node | Your IP, but NOT what you are doing |
| The Middle Node | Nothing useful (just two relay IPs) |
| The Exit Node | What website you visit, but NOT who you are |
| The website | That someone on Tor visited, but NOT your real IP |
| Your ISP | That you are using Tor, but NOT what you are doing |

The **only** way to break this is to control BOTH the Guard and the Exit node for the same circuit simultaneously, and perform statistical timing analysis. This is extremely difficult in practice.

### Circuits and Rotation

A **circuit** is a specific path through the Tor network (Guard -> Middle -> Exit). Tor creates a new circuit periodically (configurable, default 10 minutes) and uses different circuits for different destinations.

This means even if one circuit is compromised, the attacker only sees a brief window of activity, and your other activities go through completely different paths.

---

## 4. SOCKS5 Proxies

SOCKS5 is a **protocol** that allows one program to send its network traffic through another program. Think of it as a "middleman" that your applications talk to instead of the internet directly.

### How SOCKS5 works

```
Normal:  curl -> internet -> website
SOCKS5:  curl -> SOCKS5 proxy (localhost:9050) -> internet -> website
```

When you tell curl to use `socks5://127.0.0.1:9050`, here is what happens:

1. curl connects to `127.0.0.1:9050` (your local Tor daemon)
2. curl says: "Please connect to example.com port 443 for me"
3. The SOCKS5 proxy (Tor) establishes the connection through its relay circuit
4. All data flows through the proxy — curl never touches the internet directly

### SOCKS5 vs SOCKS5h: The Critical Difference

This is one of the most important things to understand:

#### `socks5://` (DANGEROUS for anonymity)
```
curl --proxy socks5://127.0.0.1:9050 https://example.com

Step 1: curl asks YOUR LOCAL DNS SERVER: "What IP is example.com?"
        ^^^ THIS IS A DNS LEAK! Your ISP sees the domain name!
Step 2: curl tells SOCKS5 proxy: "Connect to 93.184.216.34:443"
Step 3: Traffic goes through Tor
```

#### `socks5h://` (SAFE for anonymity)
```
curl --proxy socks5h://127.0.0.1:9050 https://example.com

Step 1: curl tells SOCKS5 proxy: "Please resolve AND connect to example.com:443"
Step 2: Tor resolves the DNS at the EXIT NODE (not locally!)
Step 3: Traffic goes through Tor
```

The `h` in `socks5h` stands for "**hostname resolution at the proxy**". This is critical because:
- With `socks5://` your ISP sees every domain you look up
- With `socks5h://` your ISP sees NOTHING — not even the domain names

### SOCKS5 vs HTTP Proxies

| Feature | HTTP Proxy | SOCKS5 Proxy |
|---|---|---|
| Protocols | HTTP/HTTPS only | Any TCP protocol |
| DNS resolution | Usually local | Can be remote (socks5h) |
| Speed | Faster | Slightly slower |
| Anonymity | Lower (headers can leak) | Higher |
| Use with Tor | Not recommended | Standard method |

---

## 5. Proxychains: Forcing Apps Through Tor

Some applications do not have built-in proxy support. They always connect directly to the internet. Proxychains solves this.

### What Proxychains does

Proxychains is a tool that **intercepts** an application's network calls and redirects them through a proxy chain. It works by injecting a shared library that hooks into the system's network functions.

```
Without Proxychains:
  dig example.com -> sends DNS query directly to your ISP's DNS server

With Proxychains:
  proxychains4 dig example.com -> DNS query goes through Tor SOCKS5 proxy
```

### How it works technically

1. When you run `proxychains4 someapp`, it sets the `LD_PRELOAD` (Linux) or `DYLD_INSERT_LIBRARIES` (macOS) environment variable
2. This forces the operating system to load proxychains' library BEFORE the app's normal network libraries
3. When the app calls `connect()` to make a network connection, proxychains' version of `connect()` runs instead
4. Proxychains' `connect()` routes the connection through the configured proxy chain
5. The app never knows its traffic is being redirected — it thinks it is connecting normally

### Chain modes

Proxychains supports different modes for how it uses multiple proxies:

#### Dynamic Chain
```
Proxy 1 -> Proxy 2 -> Proxy 3 -> Target
              |
              X (if Proxy 2 is down, skip it)
              |
Proxy 1 ---------> Proxy 3 -> Target
```
Skips dead proxies. At least one must work.

#### Strict Chain
```
Proxy 1 -> Proxy 2 -> Proxy 3 -> Target
```
ALL proxies must be online. If any is down, the connection fails.

#### Random Chain
```
Sometimes: Proxy 3 -> Proxy 1 -> Target
Sometimes: Proxy 2 -> Proxy 3 -> Target
Sometimes: Proxy 1 -> Proxy 2 -> Target
```
Picks random proxies each time. Good for evading pattern detection.

### DNS handling in Proxychains

When `proxy_dns` is enabled in proxychains.conf:

1. The app tries to call `getaddrinfo()` or `gethostbyname()` to resolve a domain
2. Proxychains intercepts this call
3. Instead of asking your local DNS server, it sends the DNS query through the SOCKS5 proxy
4. The proxy (Tor) resolves the domain at the exit node
5. The resolved IP is returned to the app

This prevents DNS leaks for ANY application, even those that do not support SOCKS5 natively.

---

## 6. DNS Leaks: The Silent Privacy Killer

DNS leaks are the number one way people accidentally reveal their identity while using Tor or VPNs.

### What is a DNS leak?

When you visit `example.com`, your computer first needs to look up the IP address. This lookup is called a **DNS query**. If this query goes to your ISP's DNS server instead of through Tor, your ISP knows exactly what website you are about to visit, even though the actual page content goes through Tor.

```
DNS LEAK SCENARIO:

Your computer -> ISP DNS: "What is example.com?"     <- ISP SEES THIS
Your computer -> Tor -> Exit -> example.com           <- Traffic is anonymous
                                                         BUT ISP already knows!
```

### Why DNS leaks happen

1. **Wrong SOCKS version**: Using `socks5://` instead of `socks5h://` means DNS resolves locally
2. **App ignores proxy**: Some apps have hardcoded DNS servers (like Google's 8.8.8.8) that bypass the proxy
3. **IPv6 leaks**: Your IPv6 address might bypass the proxy while IPv4 goes through it
4. **WebRTC leaks**: Browsers can leak your real IP through WebRTC even with a proxy configured
5. **System DNS cache**: Previous DNS lookups cached locally can reveal your browsing patterns

### How to prevent DNS leaks

| Layer | Method | What it does |
|---|---|---|
| **1** | `socks5h://` | DNS resolved at Tor exit node, not locally |
| **2** | Proxychains `proxy_dns` | Intercepts ALL DNS calls from any app |
| **3** | Tor's built-in DNS | Tor handles DNS resolution at exit nodes |
| **4** | Firewall rules | Block all DNS traffic (port 53) except through Tor |

In our setup, we use layers 1, 2, and 3 simultaneously for maximum protection.

---

## 7. The Complete Stack: How It All Fits Together

Here is the complete picture of how all these technologies work together:

```
+------------------------------------------------------------------+
|  YOUR MACHINE                                                     |
|                                                                   |
|  [curl with socks5h://]                                          |
|       |                                                           |
|       | "Connect to example.com:443 via SOCKS5h"                 |
|       v                                                           |
|  [Tor Daemon - localhost:9050]                                   |
|       |                                                           |
|       | 1. Resolve DNS at exit node (not locally!)               |
|       | 2. Build 3-layer encrypted circuit                       |
|       | 3. Route through Guard -> Middle -> Exit                 |
|       v                                                           |
+------------------------------------------------------------------+
       |
       | Encrypted Tor traffic (your ISP sees only this)
       | Looks like random encrypted data to a random IP
       v
+------------------+
|  GUARD NODE      |  Knows: your IP. Does NOT know: destination
|  (Entry Relay)   |
+------------------+
       |
       | Tor-encrypted traffic
       v
+------------------+
|  MIDDLE NODE     |  Knows: nothing useful (just two relay IPs)
|  (Relay)         |
+------------------+
       |
       | Tor-encrypted traffic
       v
+------------------+
|  EXIT NODE       |  Knows: destination. Does NOT know: your IP
|  (in US/DE/NL/SE)|
+------------------+
       |
       | Normal HTTPS to the website
       | Source IP = Exit Node IP (NOT your real IP)
       v
+------------------+
|  TARGET WEBSITE  |  Sees: Exit Node IP, browser fingerprint
|  example.com     |  Does NOT see: your real IP, your ISP, your location
+------------------+
```

### What your ISP sees

Your ISP sees encrypted connections from your IP to the Guard Node's IP. They can determine that you are using Tor (Tor Guard Node IPs are public), but they CANNOT see:
- What websites you visit
- What data you send or receive
- Any domain names (DNS is resolved through Tor)

### What the target website sees

The website sees a connection from the Exit Node's IP address. They can determine it is a Tor exit node (exit IPs are also public), but they CANNOT see:
- Your real IP address
- Your ISP
- Your geographic location
- Your identity

---

## 8. macOS SIP and Why It Matters

macOS has a security feature called **System Integrity Protection (SIP)** that affects how proxychains works.

### What is SIP?

SIP prevents any program from modifying system binaries in `/usr/bin/`, `/usr/sbin/`, `/System/`, and other protected paths. This includes preventing library injection (the technique proxychains uses).

### How it affects anonymity tools

```
/usr/bin/curl        <- Protected by SIP. Proxychains CANNOT hook into this.
/opt/homebrew/bin/curl <- NOT protected. Proxychains CAN hook into this.
```

If you run `proxychains4 /usr/bin/curl`, the proxychains injection is silently blocked by SIP. Curl will connect DIRECTLY to the internet, completely bypassing Tor. This is a critical anonymity failure with NO warning.

### The solution

1. **Install tools via Homebrew**: Homebrew installs to `/opt/homebrew/` which is NOT protected by SIP
2. **Use `--proxy socks5h://` flags**: Instead of relying on proxychains, tell the app directly to use the proxy
3. **Never use system binaries** for anonymous operations

This is why we use `/opt/homebrew/opt/curl/bin/curl` instead of the system `/usr/bin/curl`.

---

## 9. Tor Configuration Deep Dive

The Tor daemon is configured via `torrc` (typically at `/opt/homebrew/etc/tor/torrc`). Here is what each setting does:

### Our configuration explained

```bash
SocksPort 9050
```
**What:** Opens a SOCKS5 proxy on port 9050 on localhost.
**Why:** This is the port your apps connect to. When curl sends traffic to 127.0.0.1:9050, Tor receives it and routes it through the Tor network.

```bash
ControlPort 9051
```
**What:** Opens a control port for managing Tor.
**Why:** Allows you to request new circuits ("new identity"), check circuit status, etc. Protected by a password hash.

```bash
HashedControlPassword 16:6B5C71C9D414BD...
```
**What:** The hashed password for the control port.
**Why:** Prevents anyone on your machine from controlling your Tor instance without the password.

```bash
MaxCircuitDirtiness 60
```
**What:** Forces Tor to build a new circuit every 60 seconds.
**Why:** Limits how long any single path through the Tor network is used. If a circuit is somehow compromised, the window of exposure is only 60 seconds before a fresh path is created. Default Tor value is 600 seconds (10 minutes). We use 60 for faster rotation.

```bash
CircuitBuildTimeout 30
```
**What:** Maximum time (seconds) to wait for a circuit to be built.
**Why:** If the selected relays are slow to respond, this ensures we do not wait forever. A new set of relays will be tried.

```bash
ExcludeExitNodes {gb}
```
**What:** NEVER use exit nodes located in Great Britain.
**Why:** If you are testing a UK-based target, using a UK exit node increases the chance of traffic correlation by UK-based ISPs or law enforcement. By exiting from other countries, you add jurisdictional separation.

```bash
ExitNodes {us},{de},{nl},{se}
```
**What:** ONLY use exit nodes in United States, Germany, Netherlands, or Sweden.
**Why:** These countries have strong privacy laws and abundant Tor exit nodes. Limiting exit countries ensures predictable exit behaviour and avoids exits in surveillance-heavy nations.

```bash
StrictNodes 1
```
**What:** Strictly enforce the ExcludeExitNodes and ExitNodes rules.
**Why:** Without this, Tor might fall back to using excluded nodes if it cannot find suitable ones. With `StrictNodes 1`, it will FAIL rather than use a UK exit node. Security over convenience.

---

## 10. Practical Setup Guide

### Prerequisites (macOS)

```bash
# Install Tor
brew install tor

# Install Proxychains
brew install proxychains-ng

# Install non-SIP curl
brew install curl
```

### Start Tor

```bash
# Tor starts automatically via Homebrew services
brew services start tor

# Or run manually
tor
```

### Configure Proxychains

Edit `/opt/homebrew/etc/proxychains.conf`:

```conf
# Use dynamic chain mode (skip dead proxies)
dynamic_chain

# Quiet mode (less noise)
quiet_mode

# Route DNS through the proxy (CRITICAL for privacy)
proxy_dns

# Use reserved IP range for internal DNS mapping
remote_dns_subnet 224

# Timeouts
tcp_read_time_out 15000
tcp_connect_time_out 8000

# Proxy list: route through Tor
[ProxyList]
socks5  127.0.0.1 9050
```

### Usage patterns

```bash
# Direct SOCKS5h (recommended for curl)
/opt/homebrew/opt/curl/bin/curl --proxy socks5h://127.0.0.1:9050 https://example.com

# Via proxychains (for apps without proxy support)
proxychains4 /opt/homebrew/opt/curl/bin/curl https://example.com

# NEVER use the system curl with proxychains (SIP blocks it)
proxychains4 /usr/bin/curl https://example.com  # THIS LEAKS YOUR IP!
```

---

## 11. Verification: Proving You Are Anonymous

Never assume you are anonymous. Always verify.

### Check 1: Tor is active

```bash
curl --proxy socks5h://127.0.0.1:9050 https://check.torproject.org/api/ip
```

Expected response:
```json
{"IsTor": true, "IP": "185.220.101.16"}
```

- `IsTor: true` confirms traffic is going through Tor
- The IP shown should be an exit node IP, NOT your real IP

### Check 2: DNS is not leaking

```bash
# This should show a foreign IP (exit node location), NOT your local ISP
curl --proxy socks5h://127.0.0.1:9050 https://am.i.mullvad.net/json
```

Check that:
- The IP is different from your real IP
- The country matches your configured exit nodes (US/DE/NL/SE)
- The ISP is a known Tor exit operator, NOT your home ISP

### Check 3: Compare with real IP

```bash
# Your real IP (NOT through Tor)
curl https://check.torproject.org/api/ip
# Returns: {"IsTor": false, "IP": "YOUR.REAL.IP"}

# Through Tor
curl --proxy socks5h://127.0.0.1:9050 https://check.torproject.org/api/ip
# Returns: {"IsTor": true, "IP": "EXIT.NODE.IP"}
```

If both return the same IP, something is broken and you are NOT anonymous.

---

## 12. Common Mistakes That Break Anonymity

### Mistake 1: Using socks5:// instead of socks5h://

```bash
# WRONG - DNS leaks to your ISP
curl --proxy socks5://127.0.0.1:9050 https://target.com

# RIGHT - DNS resolved at exit node
curl --proxy socks5h://127.0.0.1:9050 https://target.com
```

### Mistake 2: Using system curl with proxychains

```bash
# WRONG - SIP blocks proxychains, traffic goes direct
proxychains4 curl https://target.com

# RIGHT - Use Homebrew curl
proxychains4 /opt/homebrew/opt/curl/bin/curl https://target.com
```

### Mistake 3: Forgetting one tool in a chain

If you run 10 commands through Tor but forget the proxy flag on one, that single command exposes your real IP to the target.

### Mistake 4: WebRTC in browsers

Browsers can leak your real IP through WebRTC even with a SOCKS proxy configured. Disable WebRTC or use Tor Browser.

### Mistake 5: Not checking before starting

Always run the Tor verification check BEFORE beginning any sensitive work. Tor might have crashed, the circuit might have failed, or your configuration might have changed.

### Mistake 6: Using the same exit node for too long

If you use the same exit node for hours, an observer could correlate your Tor session with your real identity through timing analysis. The `MaxCircuitDirtiness 60` setting mitigates this by rotating circuits every 60 seconds.

### Mistake 7: Trusting one layer alone

No single technology provides complete anonymity. The combination of Tor + SOCKS5h + proxy_dns + exit node selection is what creates strong anonymity. Remove any layer and you have a weakness.

---

## 13. Threat Model: What This Protects Against

### Protected against

| Threat | How |
|---|---|
| Website sees your IP | Tor hides it behind exit node |
| ISP sees what you visit | Tor encrypts + DNS goes through Tor |
| Network sniffing (same WiFi) | Tor encryption protects the data |
| Target logs your activity | Logs show exit node IP, not you |
| Subpoena your ISP | ISP only knows you used Tor, not what you did |
| Exit node monitoring | HTTPS encrypts content; exit only sees destination |
| Geographic tracking | Exit nodes are in different countries |

### Partially protected

| Threat | Limitation |
|---|---|
| Tor traffic correlation (global adversary) | Possible but requires massive infrastructure |
| Browser fingerprinting | Your browser config can be unique even without IP |
| Timing analysis | 60-second circuit rotation helps but is not perfect |
| Exit node eavesdropping | Only a risk for unencrypted (HTTP) traffic; HTTPS prevents this |

### NOT protected against

| Threat | Why |
|---|---|
| Logging into your real accounts | You just identified yourself regardless of Tor |
| Uploading files with metadata | EXIF data, document properties can contain your identity |
| Malware on your machine | Malware can bypass Tor entirely |
| JavaScript fingerprinting | Advanced JS can create a unique identifier for your browser |
| Posting personal information | "I live in Loughborough and work at..." identifies you |

---

## Quick Reference Card

```
ALWAYS:
  /opt/homebrew/opt/curl/bin/curl --proxy socks5h://127.0.0.1:9050

VERIFY:
  curl --proxy socks5h://127.0.0.1:9050 https://check.torproject.org/api/ip

NEW IDENTITY:
  echo -e 'AUTHENTICATE ""\r\nSIGNAL NEWNYM\r\nQUIT' | nc 127.0.0.1 9051

NEVER:
  - Use /usr/bin/curl with proxychains
  - Use socks5:// (always socks5h://)
  - Forget to verify before starting
  - Log into personal accounts
```

---

## License

MIT License. Use this knowledge responsibly and only for authorised purposes.
