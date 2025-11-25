# Timeline: ZoomInfo CEO Response to Evidence

**Date:** November 25, 2025  
**Subject:** Henry Schuck (CEO, ZoomInfo) LinkedIn Post & Response

---

## Sequence of Events

### 1. CEO Posts GTM Studio Demo

**Time:** ~09:00 CST  
**Platform:** LinkedIn  
**Author:** Henry Schuck, CEO & Founder at ZoomInfo | Nasdaq Listed: GTM

**Post Content:**
> "Identify Person-Level Website Visits --> Filter and Enrich --> Use AI to customize a message --> Execute with SDRs and AEs - one platform, no brittle waterfalls, easy action. This is GTM AI."

---

### 2. Researcher Conducts Live Analysis

**Time:** ~09:15 CST  
**Action:** Chrome DevTools analysis of https://www.zoominfo.com/products/gtm-studio

**Findings:**
- 234 network requests captured
- 118 unique tracking domains identified
- Pre-consent tracking violations documented
- Sardine.ai biometrics config decoded
- PerimeterX fingerprinting confirmed

---

### 3. Researcher Posts Comment

**Time:** ~09:25 CST  
**Platform:** LinkedIn (comment on CEO's post)

**Comment:**
> Hold up... So, why does the GTM Studio landing page:
>
> - Sets 40+ cookies pre-consent
> - Fires PerimeterX **immediately** on page load
> - Starts Sardine biometrics collection **before** consent banner interaction
> - Creates user session creates and fingerprinting **before** any consent choice
> - And it collects Mouse movements and typing patterns collected **by default**
>
> So, let me get this straight — ZoomInfo fingerprints your mouse movements, typing patterns, and DNS before you even see the consent banner.
>
> Got it.

---

### 4. Researcher Blocked

**Time:** ~09:30 CST (within ~5 minutes of comment)  
**Action:** Henry Schuck blocks researcher on LinkedIn

**Evidence:**
- Post visible to friends who checked simultaneously
- Post not visible to researcher
- Standard LinkedIn block behavior confirmed

---

### 5. Response Assessment

**What ZoomInfo Did NOT Do:**
- Issue a correction
- Provide a clarification
- Dispute the technical findings
- Explain the pre-consent tracking
- Address the Sardine.ai partnership

**What ZoomInfo DID Do:**
- Block the researcher
- Silence the comment from public view
- Continue displaying the original post

---

## Interpretation

### The Block vs. Response Decision

When presented with documented evidence of:
- Pre-consent tracking violations
- Behavioral biometrics collection
- 118 tracking domains on a single page

The CEO of a publicly traded company chose to:
- Block the researcher
- NOT dispute the findings
- NOT provide clarification

### What This Suggests

1. **The findings cannot be easily refuted** - If false, a simple correction would suffice
2. **Legal/PR concern** - Leaving detailed technical accusations visible was deemed risky
3. **Suppression over transparency** - Silencing was preferred to dialogue

---

## Public Interest Implications

### For ZoomInfo Customers
- Are you aware of the surveillance infrastructure on ZoomInfo properties?
- Is this same infrastructure deployed on YOUR website via their products?
- Have you conducted consent compliance audits?

### For Regulators
- Pre-consent biometric collection may violate GDPR, CCPA, CIPA
- Sardine.ai partnership not disclosed in privacy policy
- 118 third-party domains contacted without explicit consent

### For Journalists
- Public company CEO blocked researcher rather than addressing compliance concerns
- Evidence preserved and reproducible
- Pattern of suppression over transparency

---

> "You can block the researcher.  
> You can't block the evidence."

---

**Documented by:** Blackout Security Research  
**Date:** November 25, 2025
