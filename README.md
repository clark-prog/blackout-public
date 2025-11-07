# This is what a 72-hour "Rage Sprint" looks like.

---

## November 3, 2025. 11:18 AM.

**Eight hours** after visiting a website. **Once.** No form fill. No demo request. Just browsing.

I get this email:

> **From:** Sarah Baker <sarah.baker@use-warmly.ai>
> **Subject:** Caught your Warmly site visit
>
> Hey Clark
>
> Looks like you were exploring Warmly.
>
> Warmly engages high-intent leads and triggers instant outreach—no manual work.
>
> Open to a 15-minute demo?
>
> Best,
> Sarah
>
> Business Development Representative
> Warmly
>
> **P.S. If you don't want to receive my email just let me know :)**

Well Sarah, I didn't want to receive **this** fucking email... but here we are.

---

## The 171,738-Line Receipt

So I downloaded everything.

**Size:** 32MB uncompressed
**Lines:** 155,984 lines of network traffic
**Every single HTTP request. Every tracking call. Every surveillance vendor.**

Here's what I found on **YOUR** site, Warmly:

---

## The 9 Vendors on ONE Page

You're selling visitor identification software... but you don't trust your own product.

**You use your competitors.**

| Vendor | Category | What They Do |
|--------|----------|--------------|
| **RB2B** | Deanonymization | YOUR DIRECT COMPETITOR |
| **Koala** | Deanonymization | YOUR DIRECT COMPETITOR |
| **Vector** | Deanonymization | YOUR DIRECT COMPETITOR |
| **PostHog** | Behavioral Analytics | **800+ tracking events per session** |
| **Segment** | CDP | **Loaded TWICE** (2 different API keys) |
| **6sense** | Intent Data | B2B account identification |
| **HubSpot** | Marketing Automation | Form tracking + emails |
| **BDEX/IceXYZ** | Data Exchange | Third-party pixel network |
| **Default.com** | Form Intelligence | Capture & route |

**Total: 11 surveillance vendors on one page.**

Plus: Google Tag Manager, Intercom, Reddit Pixel, Upvert Pixel, Wistia, Cloudflare Insights.

---

## The Problem

**The real problem isn't data. It's fabricated access.**

Deanonymization pretends a relationship exists, then routes it to sales as if consent came later. GTM teams inherit the mess—and the backlash.

**White-label "enrichment" infrastructure** hides undisclosed partners across your GTM stack. Session replay + ABM multiply exposure across **5-10 vendors per pageview.**

Legal risk aside, **nothing kills win rates faster than manufactured familiarity.**

Buyers remember who crossed the boundary—and they tell their network.

---

## Who This Hurts

### **Enterprise Teams**

| Role | The Pain |
|------|----------|
| **CMOs / CGOs** | Pitch-slap GTM kills brand equity. Mystery leads born from gray-area data. |
| **Sales Leaders** | Prospects already hostile before first touch. Win rates tank. |
| **RevOps** | Ghost vendors across the stack. Can't route what you can't see. |
| **Legal / Privacy** | Policy says one thing. Runtime reality tells a different story. |
| **Compliance** | Regulatory anxiety. Need proof, not promises. Screenshots aren't enough. |
| **Founders** | One viral "creepy marketing" post destroys months of brand building. |

### **Individuals**

| The Pain | What Happens |
|----------|--------------|
| **AI SDR spam** | Visit one site. "Sarah" from Central India wants to "connect on LinkedIn." |
| **Creepy but can't prove it** | You know they're tracking you. But no screenshots, no timestamps, no domains. |
| **They won't stop** | Asked to unsubscribe. Got 3 more emails. Now what? |
| **Vendors follow you everywhere** | RB2B and Koala on every B2B site. Block one, they pop up somewhere else. |

---

### “What I’m Building”

One-Liner
“Blackout makes B2B surveillance legible and stoppable—we catch the RB2Bs of the world in real time, publish proof, and force GTM teams to play by the rules.”

The Pain

Web visitors are deanonymized pre-consent via reverse IP + data brokers.
Buyers get harassed with AI-crafted outreach they never opted into.
Legal/privacy teams can’t prove who’s actually spying because runtime evidence is messy.
What Blackout Delivers

CLI + API scanner (Playwright + vendor signatures) that fingerprints surveillance stacks, hashes artifacts, and spits out court-ready HTML dossiers.
Supabase-backed waitlist + intake already capturing Enterprise, Sensor, and Trust Standard cohorts through one flow.
Trust Standard (BTS): first GTM compliance framework with auditable control families (BTS-001..008) and revocable Bronze/Silver/Gold badges.
Og/tweet-ready marketing site showing evidence receipts, badge tiers, and waitlist CTA—all pushing to /api/waitlist.
Security Posture (Yes, we did the homework)

SSRF sealed, rate-limited, IPs hashed, request-size capped, zero cookie hoarding.
RLS enforced on Supabase; migrations scripted to add new cohort flags.
Attack surface now visible: 24 vendor signatures → 46 blocking rules shared across scanner, extension, and DB.
Roadmap Signals

Extension MVP (Manifest V3 + declarativeNetRequest) for live blocking.
Behavioral + ML detection for obfuscated or server-side pivots.
Community intel loop—crowd-reported signatures, Slack/GitHub automation.
“Shodan/Kali mode” for active recon and honeypots when customers want counter-surveillance.
Why Hackers/Cyber Folks Should Care

This is SOC2-for-GTM with receipts; we’re exposing abuse vectors that regulators, CISOs, and privacy teams will hammer on.
Lots of fun surface area: CNAME cloaking, fingerprinting hooks, deanonymization timing attacks, supply-chain policy diffs.
Need collaborators to harden detection, break evasions, and build the badge verification tooling.
How to Engage

Review vendor signatures or drop new ones.
Help stress-test the scanner/extension against obfuscation tricks.
Join founding cohort or advise on BTS control tuning.

## The Full Investigation

I spent a week reverse-engineering the visitor deanonymization industry.

**887,000+ lines of evidence analyzed**
**170+ surveillance vendors documented**
**48 complete tracking scripts captured**
**36 working detection signatures built**
**142MB of HAR files**

### The Receipts:

**4 Complete Vendor Dossiers:**
- **RB2B:** Support docs say "we have no API" while their website advertises "our entire suite of APIs" and they publish a complete Postman collection. Three official sources. Two completely opposite statements.
- **Warmly:** 171K-line HAR, 11-vendor stack, competitor dependencies exposed
- **Koala:** Official "deanonymizing" admission captured from their own marketing
- **Apollo:** 710K-line HAR, 10+ vendor stack documented

**PostHog Surveillance:**
- 43 captured telemetry events from RB2B's own site
- 800+ tracking events per session on Warmly's site
- Every click, mouse movement, scroll, form interaction

**Complete Vendor Database:**
- 250+ vendors researched
- 15 production-ready detection signatures
- Multi-method detection (scripts, globals, network, cookies, inline code)

---

## What I Built in 48 Hours

**73 commits. One rage sprint. One person who didn't know what Git Pull meant.**

### Production Scanner
- **1,034 lines of code**
- Playwright browser automation
- Multi-method vendor detection
- HTML report generation with chain-of-custody
- ASCII art banner with color cycling (because fuck it, why not)

### TriMark Visual System
- **185 lines of code**
- Mathematical precision equilateral triangle
- Framer Motion path drawing animations
- Stage-specific edge highlighting (DETECT → DIFF → PROVE)

### Ghostline Design System
- Ghost in the Shell-inspired dark palette
- Scanning animations (8s linear infinite sweep)
- Color system: ink-950/900/800 (backgrounds), cyan/violet/green (accents)

### Working Detection Signatures
- **15 production vendors**
- RB2B, Clearbit, 6sense, Demandbase, Koala, Warmly, FullStory, etc.
- Weighted confidence scoring (identity=6-7, network=4-7, script=3-5)
- Only ship findings ≥0.50 confidence

### Evidence Samples
- **Enterprise Evidence Pack:** 2-page PDF with executive summary, scorecard, gap details, remediation guidance, chain-of-custody
- **Sensor Proof Card:** Personal receipt with vendor list, categories, detection methods, timestamps

---

## The Products

**One detection engine. Two outputs. Hard firewall between them.**

### 🏢 Blackout for Teams (Enterprise)

**Disclosure Assurance for Legal, GRC & RevOps**

**What You Get:**
- **One-time commissioned scans** — Not SaaS. Per-pack invoicing.
- **Evidence Packs (PDF + ZIP)** — Executive summary, scorecard (BLK-001–BLK-006 controls), artifacts (HAR files, screenshots, policy snapshots), remediation text with ownership + due dates
- **Chain-of-custody** — SHA-256 hashing, ISO 8601 timestamps, verifiable evidence trail
- **Confidence scoring** — 0.0–1.0 scale, only ship findings ≥0.50

**Pain → Outcome:**
- **Policy diverges from runtime** → Single view of truth legal & ops both sign
- **Uncontrolled vendor expansion** → Undisclosed vendors flagged with ownership
- **Inventory ≠ disclosure assurance** → Disclosure gaps called, not just trackers listed
- **Regulatory anxiety** → Counsel-ready proof with confidence & evidence strength

**Add-ons:**
- Watchdog (monitor 3 competitor domains)
- Counsel Share Link (read-only access for external counsel)
- Notion/Jira export

**No continuous monitoring. No recurring fees. Commission a scan when you need one.**

---

### 🛡️ Blackout Sensor

**Personal, not predatory: Proof Cards, Filters, and Opt-Outs you control.**

**What You Get:**
- **Proof Cards** — Clean, shareable receipts (vendors detected, domains, scripts, timestamps, chain-of-custody)
- **Receipts Vault** — Save detection history, optional public share links
- **Inbox Filters Pack** — Gmail/Outlook filters to auto-tag and archive AI SDR emails
- **Personal Blocklist Export** — One-click export to uBlock Origin / AdGuard
- **Opt-Out / Do-Not-Sell Pack** — Jurisdiction-aware (GDPR/CCPA) templates, prefilled with your detections

**Pain → Outcome:**
- **Pitch-slapping & AI-SDR spam** → Inbox Filters Pack auto-routes it away
- **"Creepy but can't prove it"** → Proof Card + Vault (your evidence, your terms)
- **They won't stop contacting me** → Opt-Out / Do-Not-Sell Pack enforces do-not-contact
- **Same vendors follow you** → Personal Blocklist Export (uBlock/AdGuard)

**Guardrails:**
- No bulk crawls
- No competitor monitoring
- No enterprise Evidence Packs
- Flat-rate SaaS

---

**Why the separation?**

Same detection engine, different outputs. Enterprise users don't get upsold Sensor. Sensor users never see "upgrade to unlock Evidence Pack features."

**No tiers. No holdbacks. No manufactured scarcity.**

---

## The Receipts Philosophy

**You can't sell anti-surveillance software while running Heap on your own site.** That's not a product. That's performance art.

### Our Promises:

✅ **No cookies. No tracking.** — blackout.tools itself runs zero surveillance infrastructure
✅ **Public corrections log** — Accepted AND rejected corrections visible (72-hour SLA for material corrections)
✅ **Chain-of-custody** — SHA-256 hashing on all evidence artifacts
✅ **Confidence scoring** — Every finding includes 0.0–1.0 confidence (≥0.50 threshold to ship)
✅ **No behavioral analytics** — No Heap, no Amplitude, no session replay on our own site
✅ **Hard lane firewall** — Enterprise and Sensor products stay separated

**We build the thing we said we'd build, or we don't ship.**

---

## By the Numbers

| Metric | Value |
|--------|-------|
| **Total Commits** | 73 (average: 1.5 commits/hour for 48 hours) |
| **Production Scanner** | 1,034 LOC |
| **TriMark Component** | 185 LOC |
| **Vendor Signatures** | 15 working (RB2B, Clearbit, 6sense, Demandbase, etc.) |
| **Evidence Captured** | 887,000+ lines (HAR files, network traces, policy snapshots) |
| **Vendor Database** | 250+ researched, 170+ documented with surveillance tactics |
| **HAR Files** | 142MB compressed (700MB+ uncompressed) |
| **Warmly HAR Alone** | 32MB, 155,984 lines, 11 vendors detected |
| **Code Files** | 973 total (55 TS/React components, 39 vendor research folders) |

---

## See It Live

Visit **[deployblackout.com](https://deployblackout.com)** to see:
- Sample Evidence Pack (Enterprise)
- Sample Proof Card (Sensor)
- Complete product positioning
- Early access waitlist

---

## How Detection Works

**DETECT → DIFF → PROVE**

### Step 1: DETECT (Multi-Method Vendor Detection)

**5 Detection Layers:**
1. **Script Fingerprinting** — CDN URLs, loader patterns
2. **Window Globals** — `window.rb2b`, `window.warmly`, `window.ko`, `window.FS`
3. **Network Analysis** — Host matching, path patterns, request volumes
4. **Cookie Inspection** — First-party vs third-party, session vs persistent
5. **Inline Code Scanning** — Embedded snippets, initialization calls

**Weighted Confidence Scoring:**
- Identity signals (PII capture, company enrichment): **6-7 points**
- Network calls to vendor domains: **4-7 points**
- Script loading: **3-5 points**
- Inline code snippets: **2-4 points**
- Window globals: **3-4 points**

**Threshold:** Only ship findings with ≥0.50 confidence. No guessing. No false positives.

### Step 2: DIFF (Disclosure Analysis)

**Compare runtime reality vs. disclosure promises:**
- Privacy policy parsing (phrase classes + citations)
- Subprocessor lists (Annex A, vendor schedules)
- Cookie banners / consent notices
- Region flags (GDPR, CCPA, PIPEDA)

**Result:** Disclosure gaps with control IDs (BLK-001–BLK-006)

### Step 3: PROVE (Evidence Generation)

**Enterprise Evidence Packs:**
- Executive summary (KPI grid: detections, gaps, critical findings)
- Noncompliance scorecard (control ID, severity, status, confidence)
- Detailed gap findings (script sources, network calls, policy diffs)
- Artifacts (HAR files, screenshots, policy snapshots)
- Remediation guidance (ownership, due dates, options)
- Chain-of-custody (SHA-256 hashes, ISO 8601 timestamps)

**Sensor Proof Cards:**
- Vendors detected with categories (DEANONYMIZATION, SESSION REPLAY, DATA ENRICHMENT)
- Detection methods (scripts, network calls, globals, cookies)
- Timestamps + chain-of-custody
- Save to Receipts Vault
- Optional public share link

---

## The Mission

**This shit ends now.**

B2B marketing has become a surveillance-industrial complex. Warmly deanonymized me. "Sarah" (an AI SDR from Central India) emailed me at 3 AM. I never submitted a form, provided my email, or clicked a cookie banner.

**I just visited their website.**

So I reverse-engineered the entire industry. 887,000+ lines of evidence. 170+ vendors. 48 tracking scripts. 36 working signatures.

**Now I'm making it all public.**

### What I Need:

🔥 **Testers** — Enterprise teams that want to commission Evidence Packs
🔥 **Intel** — "How the F*ck did they know?" stories from the wild
🔥 **Early Access** — Individuals who want Sensor (browser extension + Proof Cards)

**Join the waitlist:** [deployblackout.com](https://deployblackout.com)

---

## Tell Me Your Story

**"How the F*ck did they know?" moments:**

- You visit one site. LinkedIn DM arrives 6 hours later.
- Sales email with your job title, company size, tech stack.
- "I saw you were researching [competitor]..."
- Personalized video from CEO of a company you never heard of.

**Drop your story via email:** intel@blackout.tools

We'll add it to the database. Document the vendor. Build the signature. Make it public.

---

## Contact

- **Enterprise (Evidence Packs):** enterprise@blackout.tools
- **Sensor Beta:** Join waitlist at [deployblackout.com](https://deployblackout.com)
- **Intel / Stories:** intel@blackout.tools
- **Founder:** [@clarkbbarron](https://www.linkedin.com/in/clarkbarron)

---

## The Bottom Line

**I visited a website. Eight hours later: cold email.**

So I captured 171,738 lines of network traffic. Exposed 11 surveillance vendors. Documented 887,000+ lines of evidence across 170+ vendors. Built a production scanner in 48 hours.

**Y'all thought I was fucking kidding.**

**Here's proof. Verify it yourself.**

---

**BLACKOUT** — *Receipts over promises.*

🔥 [deployblackout.com](https://deployblackout.com)
