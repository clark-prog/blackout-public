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

## About This Release

This evidence pack is released in the public interest.

Vendor surveillance infrastructure should be transparent and verifiable, not suppressed when documented.

**Released by:** [Blackout Security Research](https://deployblackout.com)  
**Date:** November 25, 2025  
**License:** CC BY 4.0 (Attribution required)

---

## Blackout Friday — November 29, 2025

**Free forensic scans. 100 domains. 24 hours.**

Find out what YOUR vendors are hiding.

→ [deployblackout.com](https://deployblackout.com)

---

> *"You can block the researcher.*  
> *You can't block the evidence."*
