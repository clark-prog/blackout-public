# CIPA Wiretapping Analysis: ZoomInfo GTM Studio

## Applicable Law

**California Invasion of Privacy Act (CIPA)**
- California Penal Code § 630-638
- Two-party consent state for recordings
- Private right of action for violations

## Relevant Provisions

### Penal Code § 631 - Wiretapping

> Any person who, by means of any machine, instrument, or contrivance... willfully and without the consent of all parties to the communication, or in any unauthorized manner, reads, or attempts to read, or to learn the contents or meaning of any message, report, or communication while the same is in transit...

---

## CIPA Application to Web Tracking

### Emerging Case Law

Recent California cases have extended CIPA to certain web tracking technologies:

| Case | Holding |
|------|---------|
| *Javier v. Assurance IQ* (9th Cir. 2022) | Session replay may constitute wiretapping |
| *Calhoun v. Google* (N.D. Cal. 2022) | Analytics collection can implicate CIPA |
| *Yoon v. Lululemon* (C.D. Cal. 2023) | Session replay without consent violates CIPA |

---

## ZoomInfo Exposure Analysis

### Sardine.ai Behavioral Biometrics

**Technology:** Real-time capture of:
- Mouse movements (cursor path, velocity, acceleration)
- Typing patterns (keystroke timing, rhythm)
- Scroll behavior (speed, direction, patterns)

**CIPA Concerns:**

1. **Real-time interception:** Biometrics captured as user interacts
2. **Third-party transmission:** Data sent to `d.sardine.ai` domain
3. **No consent obtained:** Collection begins pre-consent
4. **Behavioral content:** Captures HOW user communicates with site

### Argument for CIPA Violation

Behavioral biometrics constitute "communications" because they:
- Represent user's intended interactions with website
- Reveal thought patterns (hesitation, decision-making)
- Are intercepted by third party (Sardine.ai) without consent

---

## Potential CIPA Damages

### Statutory Damages (§ 637.2)

> Any person who has been injured by a violation of this chapter may bring an action... for either:
> (a) $5,000 or three times the amount of actual damages, whichever is greater

### Per-Violation Analysis

If each page load with biometrics collection = 1 violation:
- **Minimum damages:** $5,000 per affected user
- **Class action potential:** Significant given ZoomInfo's traffic

---

## Evidence for CIPA Claims

This evidence pack contains:
- Sardine.ai config showing `enableBiometrics: true`
- Timing evidence showing pre-consent collection
- Third-party domain proving external transmission
- Methodology for reproduction

---

**Analysis Conducted By:** Blackout Security Research  
**Date:** November 25, 2025  
**Disclaimer:** This is legal analysis, not legal advice. Consult qualified California counsel.
