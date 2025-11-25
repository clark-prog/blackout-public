# GDPR Violation Analysis: ZoomInfo GTM Studio

## Applicable Regulations

- **GDPR** - General Data Protection Regulation (EU) 2016/679
- **ePrivacy Directive** - Directive 2002/58/EC (Cookie Law)

## Findings Summary

ZoomInfo's GTM Studio landing page deploys tracking and fingerprinting technologies **before obtaining valid consent**, violating multiple GDPR provisions.

---

## Violation 1: Article 6 - Lawfulness of Processing

### Requirement
> Processing shall be lawful only if and to the extent that at least one of the following applies:
> (a) the data subject has given consent to the processing...

### Violation Evidence

| Data Processed | Processor | Timing |
|----------------|-----------|--------|
| Device fingerprint | PerimeterX | Request #79 (pre-consent) |
| Behavioral biometrics | Sardine.ai | Request #119 (pre-consent) |
| Session identifier | ZoomInfo Fraud API | Request #87 (pre-consent) |

### Analysis

No lawful basis exists for this processing:
- **Consent:** Not obtained before processing begins
- **Legitimate interests:** Cannot override fundamental rights; fingerprinting is disproportionate

---

## Violation 2: Article 7 - Conditions for Consent

### Requirement
> The data subject shall have the right to withdraw his or her consent at any time...

### Violation Evidence

1. **Consent not obtained first:** Processing begins before consent banner is even displayed
2. **No withdrawal mechanism:** Cannot withdraw consent for processing that already occurred

---

## Violation 3: Article 9 - Special Categories of Data

### Requirement
> Processing of... biometric data for the purpose of uniquely identifying a natural person... shall be prohibited [without explicit consent].

### Violation Evidence

Sardine.ai configuration shows:
```json
{
  "enableBiometrics": true,
  "enableDNS": true
}
```

Behavioral biometrics can constitute biometric data under GDPR when used for identification purposes.

---

## Violation 4: ePrivacy Directive Article 5(3)

### Requirement
> Member States shall ensure that the storing of information, or the gaining of access to information already stored, in the terminal equipment of a subscriber or user is only allowed on condition that the subscriber or user concerned has given his or her consent.

### Violation Evidence

- Cookies set before consent obtained
- Device fingerprinting accesses stored device characteristics

---

## Potential Penalties

### GDPR Article 83 - Administrative Fines

**Tier 2 violations** (Articles 5, 6, 7, 9):
- Up to €20 million, or
- Up to 4% of total worldwide annual turnover

---

**Analysis Conducted By:** Blackout Security Research  
**Date:** November 25, 2025  
**Disclaimer:** This analysis is for informational purposes. Consult legal counsel for specific advice.
