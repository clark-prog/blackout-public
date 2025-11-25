# CCPA/CPRA Violation Analysis: ZoomInfo GTM Studio

## Applicable Regulations

- **CCPA** - California Consumer Privacy Act (Civil Code §1798.100-199.100)
- **CPRA** - California Privacy Rights Act (effective January 1, 2023)

## Findings Summary

ZoomInfo's GTM Studio landing page may violate multiple CCPA/CPRA provisions through undisclosed data collection and sharing practices.

---

## Violation 1: Right to Know (§1798.100)

### Requirement
> A consumer shall have the right to request that a business that collects personal information about the consumer disclose... the categories of personal information it has collected.

### Violation Evidence

**Undisclosed data collection:**
- Sardine.ai biometrics (mouse movements, typing patterns)
- PerimeterX device fingerprinting
- 118 third-party domain connections

**Privacy policy deficiencies:**
- Sardine.ai partnership not disclosed
- Biometric data collection not specified

---

## Violation 2: Right to Opt-Out of Sale/Sharing (§1798.120)

### Requirement
> A consumer shall have the right, at any time, to direct a business that sells or shares personal information about the consumer to third parties not to sell or share the consumer's personal information.

### Violation Evidence

**Pre-consent data sharing observed:**
- Google Ads (3 accounts)
- Bing Ads
- TikTok Pixel
- Snapchat Pixel
- LinkedIn Ads
- Clickagy

All fire BEFORE any opt-out opportunity is presented.

---

## Violation 3: Sensitive Personal Information (§1798.121)

### CPRA Definition
> "Sensitive personal information" includes... personal information collected and analyzed concerning a consumer's... behavior

### Violation Evidence

**Sensitive data collected pre-consent:**
- Behavioral biometrics via Sardine.ai (`enableBiometrics: true`)
- Device fingerprint (PerimeterX)

---

## Violation 4: Notice at Collection (§1798.100(b))

### Requirement
> A business that collects personal information shall, at or before the point of collection, inform consumers as to the categories of personal information to be collected.

### Violation Evidence

**Missing disclosures at collection:**
- No notice before fingerprinting begins
- Biometrics collection not disclosed before it starts

---

## California Attorney General Enforcement

### CCPA Penalties
- Up to $2,500 per unintentional violation
- Up to $7,500 per intentional violation

---

**Analysis Conducted By:** Blackout Security Research  
**Date:** November 25, 2025  
**Disclaimer:** This analysis is for informational purposes. Consult legal counsel for specific advice.
