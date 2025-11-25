# CCPA/CPRA Compliance Analysis: ZoomInfo GTM Studio

## Applicable Regulations

- **CCPA** - California Consumer Privacy Act (Civil Code §1798.100-199.100)
- **CPRA** - California Privacy Rights Act (effective January 1, 2023)

## Findings Summary

ZoomInfo's GTM Studio landing page exhibits data collection and sharing practices that may raise concerns under CCPA/CPRA provisions.

---

## Concern 1: Right to Know (§1798.100)

### Requirement
> A consumer shall have the right to request that a business that collects personal information about the consumer disclose... the categories of personal information it has collected.

### Documented Behavior

**Data collection observed but potentially undisclosed:**
- Sardine.ai biometrics (mouse movements, typing patterns)
- PerimeterX device fingerprinting
- 118 third-party domain connections

**Privacy policy observations:**
- Sardine.ai partnership not explicitly disclosed
- Biometric data collection not specifically itemized

---

## Concern 2: Right to Opt-Out of Sale/Sharing (§1798.120)

### Requirement
> A consumer shall have the right, at any time, to direct a business that sells or shares personal information about the consumer to third parties not to sell or share the consumer's personal information.

### Documented Behavior

**Pre-consent data sharing observed to:**
- Google Ads (multiple accounts)
- Bing Ads
- TikTok Pixel
- Snapchat Pixel
- LinkedIn Ads
- Clickagy

These connections fire before opt-out opportunity is presented.

---

## Concern 3: Sensitive Personal Information (§1798.121)

### CPRA Definition
> "Sensitive personal information" includes... personal information collected and analyzed concerning a consumer's... behavior

### Documented Behavior

**Potentially sensitive data collected pre-consent:**
- Behavioral biometrics via Sardine.ai (`enableBiometrics: true`)
- Device fingerprint (PerimeterX)

---

## Concern 4: Notice at Collection (§1798.100(b))

### Requirement
> A business that collects personal information shall, at or before the point of collection, inform consumers as to the categories of personal information to be collected.

### Documented Behavior

**Timing observations:**
- Fingerprinting begins before consent banner interaction
- Biometrics collection starts before disclosure opportunity

---

## Potential Regulatory Exposure

### CCPA Penalties
- Up to $2,500 per unintentional violation
- Up to $7,500 per intentional violation

*Note: Whether penalties would apply depends on regulatory or judicial determination of actual violations.*

---

**Analysis Conducted By:** Blackout Security Research  
**Date:** November 25, 2025  
**Disclaimer:** This analysis is for informational purposes only. It does not constitute legal advice. Consult qualified legal counsel for specific guidance.
