# ZoomInfo GTM Studio: Pre-Consent Surveillance Evidence

> **"You can block the researcher. You can't block the evidence."**

---

## What Happened

On November 25, 2025, ZoomInfo CEO Henry Schuck posted a product demo of GTM Studio on LinkedIn — their AI-powered platform that "identifies person-level website visits."

A security researcher analyzed the GTM Studio landing page and documented extensive pre-consent surveillance infrastructure. The findings were posted as a comment on the CEO's LinkedIn post.

**Within minutes, the researcher was blocked.**

No correction. No clarification. Just silence.

This evidence pack ensures the findings cannot be suppressed.

---

## Key Findings

| Finding | Evidence |
|---------|----------|
| **50+ tracking requests before consent** | Network capture shows tracking fires before consent banner loads |
| **Sardine.ai biometrics enabled** | `enableBiometrics: true` in decoded config |
| **PerimeterX fingerprinting** | Collector fires at request #79 (pre-consent) |
| **DNS fingerprinting active** | `enableDNS: true` in Sardine config |
| **118 unique tracking domains** | Contacted on single page load |
| **Session fingerprinting** | Fraud detection API creates session pre-consent |

---

## The Smoking Gun

### Decoded Sardine.ai Configuration

```json
{
  "enableBiometrics": true,
  "enableDNS": true,
  "partnerId": "zoominfo",
  "dBaseDomain": "d.sardine.ai",
  "environment": "production"
}
```

This configuration was decoded from a base64-encoded payload in the collector iframe URL.

**Translation:**
- Mouse movements tracked by default
- Typing patterns recorded
- DNS fingerprinting enabled
- ZoomInfo has a formal partnership with Sardine.ai
- This is production, not testing

---

## The Irony

ZoomInfo markets GTM Studio as a tool to "identify person-level website visits."

Yet on their **own landing page** for this product, they deploy:
- **3 external identity/fingerprinting vendors** (Sardine.ai, PerimeterX, IdentityMatrix.ai)
- **Behavioral biometrics before consent**
- **118 different tracking domains**

**Even the visitor identification vendor doesn't trust their own product for visitor identification.**

---

## For Marketers: Why This Matters To You

You're not a privacy lawyer. You're trying to hit pipeline targets. So why should you care?

### 1. Your Budget Is Buying Legal Exposure

Every dollar spent on vendors with pre-consent violations is a dollar spent on future legal liability. When the class action hits, "we didn't know" isn't a defense — it's an admission of negligence.

**The question isn't IF this data is actionable. It's IF you'll be named in the complaint.**

### 2. Your "Intent Data" Is Legally Toxic

Data collected without consent can't be legally processed. That means:
- Your lead scores are built on violations
- Your ABM campaigns target illegally-collected profiles  
- Your attribution models include tainted signals

You're not optimizing. You're compounding liability.

### 3. Your Customers Are The Plaintiffs

The people you're tracking without consent? They're the same people you're trying to convert. When they find out (and they will), you haven't just lost a deal — you've created an adversary with standing.

**Every visitor is a potential plaintiff. Every page view is evidence.**

### 4. Your Vendor's Compliance Is YOUR Compliance

GDPR Article 26. CCPA 1798.100. Your contracts say "vendor warrants compliance." Courts say you're jointly liable anyway. When ZoomInfo's violations become public record, your legal team will ask: "Who approved this vendor?"

That answer is in your Slack history.

### 5. Your Competitors Will Use This Against You

Imagine losing an enterprise deal because the prospect's security team Googled your martech stack and found this evidence pack. Imagine the RFP question: "Do you use vendors with documented pre-consent violations?"

**Your vendor choices are discoverable. Choose accordingly.**

---

## The Hard Truth

Marketing has operated in a "move fast, ask forgiveness" mode for 15 years. That era is ending.

The surveillance infrastructure that powered the "growth at all costs" playbook is now:
- **Documented** (you're reading the evidence)
- **Discoverable** (public GitHub repo)
- **Actionable** (GDPR, CCPA, CIPA all apply)

You can either:
1. **Audit your stack now** and remove liability before it crystallizes
2. **Wait for the subpoena** and explain why you ignored public evidence

The vendors won't protect you. Your contracts won't protect you. Only your choices will.

---

## Evidence Contents

```
zoominfo-gtm-studio/
├── FINDINGS.md              # Full technical analysis
├── TIMELINE.md              # CEO post → comment → block sequence
├── code/
│   ├── sardine-config.json  # Decoded biometrics configuration
│   ├── perimeterx.md        # PerimeterX infrastructure details
│   └── tracking-sequence.md # Complete request timeline
├── methodology/
│   └── how-we-tested.md     # Reproduction instructions
└── legal/
    ├── gdpr-violations.md   # EU compliance analysis
    ├── ccpa-violations.md   # California privacy law analysis
    └── cipa-exposure.md     # California wiretapping exposure
```

---

## How To Verify (5 Minutes)

1. Open Chrome in Incognito mode
2. Open DevTools (F12) → Network tab
3. Enable "Preserve log"
4. Navigate to: `https://www.zoominfo.com/products/gtm-studio`
5. **DO NOT interact with consent banner**
6. Count requests that fire before you see the banner

### What To Look For

- `collector-pxosx7m0dx.px-cloud.net` — PerimeterX fingerprinting
- `*.d.sardine.ai/bg.png` — Sardine behavioral biometrics
- `gw-app.zoominfo.com/gw/ziapi/fraud-detection` — Session fingerprinting

---

## Legal Implications

### GDPR (EU)
- **Article 5(3):** Cookie consent required before tracking
- **Article 6:** No lawful basis for biometric processing
- **Article 9:** Behavioral biometrics may constitute special category data

### CCPA/CPRA (California)
- **Right to Know:** Sardine.ai partnership not disclosed
- **Right to Opt-Out:** No opt-out before tracking begins
- **Sale of Personal Information:** Data shared with 40+ third parties

### CIPA (California)
- **Wiretapping:** Biometric collection without consent may constitute wiretapping
- **Two-party consent:** California requires all-party consent for recording

---

## The CEO's Response

When presented with documented evidence of:
- Pre-consent tracking violations
- Behavioral biometrics collection
- 118 tracking domains on a single page

The CEO of a publicly traded company chose to:
- **Block the researcher**
- NOT dispute the findings
- NOT provide clarification

---

## Legal Disclaimer

**THIS IS NOT LEGAL ADVICE.**

The information contained in this evidence pack is provided for informational and educational purposes only. Nothing herein constitutes legal advice, and no attorney-client relationship is created by accessing, reading, or using this information.

**You should consult with a qualified attorney** licensed in your jurisdiction before taking any action based on the information presented here. Privacy law is complex, varies by jurisdiction, and is subject to change. What constitutes a violation in one jurisdiction may not apply in another.

**Blackout is not a law firm.** We are ethical marketers, security researchers, and mission-driven experts documenting technical findings about GTM vendor disclosure, Marketing compliance standards, and what can be done to take back the definition of "good marketing" from the "Growth at cost" assholes that stole it. We make no representations or warranties about:
- The legal accuracy or completeness of any analysis
- The applicability of cited regulations to your specific situation
- The current state of any company's tracking practices (which may change)
- The outcome of any legal action based on this information

**All findings are based on publicly observable behavior** at the time of testing. Network captures, decoded configurations, and request timelines represent a point-in-time snapshot. Vendors may modify their practices after publication.

**If you believe you have been harmed** by pre-consent tracking or surveillance practices, consult a privacy attorney or contact your local data protection authority. Do not rely solely on this document to assess your legal rights or remedies.

By accessing this evidence pack, you acknowledge that you have read and understood this disclaimer.

---

## About This Release

This evidence pack is released in the public interest.

Vendor surveillance infrastructure should be transparent and verifiable, not suppressed when documented.

**Released by:** [Blackout Research](https://deployblackout.com)  
**Date:** November 25, 2025  

---

## Blackout Friday — November 29, 2025

**Free forensic scans. 100 domains. 24 hours.**

Find out what YOUR vendors are hiding.

→ [deployblackout.com](https://deployblackout.com)

---

> *"You can block the researcher.*  
> *You can't block the evidence."*
