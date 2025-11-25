# GDPR Compliance Analysis: ZoomInfo GTM Studio

## Applicable Regulations

- **GDPR** - General Data Protection Regulation (EU) 2016/679
- **ePrivacy Directive** - Directive 2002/58/EC (Cookie Law)

## Findings Summary

ZoomInfo's GTM Studio landing page deploys tracking and fingerprinting technologies **before obtaining consent interaction**, which may raise concerns under multiple GDPR provisions.

---

## Concern 1: Article 6 - Lawfulness of Processing

### Requirement
> Processing shall be lawful only if and to the extent that at least one of the following applies:
> (a) the data subject has given consent to the processing...

### Documented Behavior

| Data Processed | Processor | Timing |
|----------------|-----------|--------|
| Device fingerprint | PerimeterX | Request #79 (pre-consent) |
| Behavioral biometrics | Sardine.ai | Request #119 (pre-consent) |
| Session identifier | ZoomInfo Fraud API | Request #87 (pre-consent) |

### Analysis

The lawful basis for this processing is unclear:
- **Consent:** Not obtained before processing begins
- **Legitimate interests:** May not override fundamental rights; fingerprinting proportionality is questionable

---

## Concern 2: Article 7 - Conditions for Consent

### Requirement
> The data subject shall have the right to withdraw his or her consent at any time...

### Documented Behavior

1. **Consent timing:** Processing begins before consent banner interaction
2. **Withdrawal mechanism:** Cannot withdraw consent for processing that already occurred

---

## Concern 3: Article 9 - Special Categories of Data

### Requirement
> Processing of... biometric data for the purpose of uniquely identifying a natural person... shall be prohibited [without explicit consent].

### Documented Behavior

Sardine.ai configuration shows:
```json
{
  "enableBiometrics": true,
  "enableDNS": true
}
```

Behavioral biometrics may constitute biometric data under GDPR when used for identification purposes. This is an evolving area of law.

---

## Concern 4: ePrivacy Directive Article 5(3)

### Requirement
> Member States shall ensure that the storing of information, or the gaining of access to information already stored, in the terminal equipment of a subscriber or user is only allowed on condition that the subscriber or user concerned has given his or her consent.

### Documented Behavior

- Cookies observed before consent interaction
- Device fingerprinting accesses device characteristics

---

## Potential Regulatory Exposure

### GDPR Article 83 - Administrative Fines

**Tier 2 provisions** (Articles 5, 6, 7, 9):
- Up to €20 million, or
- Up to 4% of total worldwide annual turnover

*Note: Whether these thresholds would apply depends on regulatory determination of actual violations.*

---

**Analysis Conducted By:** Blackout Security Research  
**Date:** November 25, 2025  
**Disclaimer:** This analysis is for informational purposes only. It does not constitute legal advice. Consult qualified legal counsel for specific guidance.
