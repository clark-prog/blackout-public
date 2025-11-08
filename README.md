# BLACKOUT — GTM behavior you can verify

**Built by marketers.** Blackout verifies what buyers see and what browsers load—then certifies it against the Blackout Trust Standard (BTS).

**We don't grade influence. We verify behavior.**

---

## What is Blackout?

Continuous, disclosure-grade verification for hidden tracking and white-label surveillance.

Detect what's really running after "Reject All," diff it against what you've disclosed, and auto-generate the receipts.

**Claim:** To our knowledge, the first GTM consequence layer.[^1]
Audits the promise (copy/ads/social) and the payload (runtime/pre-consent), attaches a provenance token, and exports a 48-hour evidence bundle. See [/proof/methodology](https://deployblackout.com/proof/methodology).

[^1]: Defined at /proof/methodology; matrix versioned.

---

## Why Blackout exists

Security earned its standards (SOC 2, ISO 27001). GTM never did.

Cookie banners and pay-to-play rankings masked a simple fact: identity tech, session replay, and ad pixels still fire after "Reject All."

Blackout makes GTM conduct legible, testable, and enforceable—with receipts.

**We don't argue intent. We publish timing and URLs.**

---

## The compliance landscape (and why it falls short)

Nothing in the current compliance landscape touches the behavior of GTM functions the way SOC 2/ISO 27001 cover engineering and security.

**What exists:**

- **SOC 2, ISO 27001, HITRUST, PCI, FedRAMP** – Focus on security and privacy controls for systems and data. GTM tooling is in-scope only when it touches production systems, not for marketing behavior or vendor usage.

- **GDPR, CCPA/CPRA, LGPD, ePrivacy, CASL, CAN-SPAM, TCPA** – Regulate consent, lawful basis, email/SMS outreach, and tracking disclosures. They set legal limits but don't provide a certifiable framework or badge that says, "Your marketing team behaves appropriately."

- **IAB Transparency & Consent Framework, DAA AdChoices, NAI** – Advertising industry self-regulation targeting CMPs and ad-tech consent handling; largely unenforced opt-in systems for programmatic advertising, not comprehensive GTM behavior audits.

- **CMP audits (OneTrust, TrustArc)** – Tools to verify consent banners and ad preferences but do not audit the full stack of vendors or pre-consent behavior.

- **Regulatory settlement agreements (e.g., FTC, CNIL)** – After-the-fact enforcement for egregious tracking, but no proactive framework or ongoing assessment model.

**Net:** No mainstream, certifiable compliance framework currently audits GTM/Sales/Marketing behavior end-to-end (vendor disclosure parity, deanonymization practices, pre-consent tracking, AI SDR outreach). That gap is exactly what Blackout's Trust Standard (BTS) is designed to fill.

---

## What Blackout does

1. **Detect** — Capture post-consent timelines (initiator chains, request URLs, timestamps).
2. **Diff** — Compare runtime vendors to your sub-processor list and policy.
3. **Prove** — Hash the evidence pack and issue (or deny) a BTS badge (Bronze/Silver/Gold).
4. **Enforce** — Critical drift suspends or revokes the badge. Public revocation log.

All verification is performed offline. This site runs no third-party trackers.

---

## The Blackout Trust Standard (BTS)

**BTS:** the evidence-based compliance standard for online GTM behavior.

### Control families (evidence, not opinions):

- **Consent governance** — no identity/replay/ads fire after "Reject All"; GPC honored.
- **Disclosure parity** — your policy & sub-processor list match runtime.
- **De-anonymization** — explicit, verifiable opt-in or it's out.
- **Proof** — initiator chains, request URLs, timestamps; bundle hashed (SHA-256).
- **Attestation** — host `/.well-known/blackout.json`.
- **Enforcement** — badges can be suspended or revoked.

### Badge tiers (objective):

- **BTS-Bronze (≥70):** No identity/replay/ads post-reject; GPC honored; ≥95% sub-processor parity.
- **BTS-Silver (≥80):** Bronze + no de-anon without explicit opt-in; 100% disclosure parity.
- **BTS-Gold (≥90):** Silver + no session replay or fingerprinting; regional consent gating verified.

**Label:** Blackout Trust Standard — {Tier} — Last verified: YYYY-MM-DD

---

## Example controls (excerpt)

**BLK-001** Undisclosed Sub-processor
→ Detected vendor ∉ disclosures → Add & republish with date/version.

**BLK-003** Session Recording Without Consent
→ replay before consent → Gate behind CMP; honor region logic & GPC.

**BLK-005** CNAME Cloak / Shadow Cookies
→ third-party via first-party CNAME → Disable until consent; disclose.

**BLK-007** Consent Timing Violation
→ any identity/replay/ads request < first consent or persists after "Reject All" → Block until known state.

**BLK-021** "Compliant" Claim vs. Reality
→ privacy-first claim, runtime contradicts → Fix runtime or change copy; no absolutes.

**BLK-023** "Cookieless" but Fingerprinting
→ canvas/WebGL or server-side forwarding pre-consent → Disclose or remove; align copy.

**Full library:** [/docs/CONTROLS.md](https://deployblackout.com/docs/CONTROLS.md)

---

## Scoring & certification

**Formula:**
Severity (S) 1–5 × Exposure (E) 1–3 (pages × traffic class) + Remediation (R) 1–3 → Non-Compliance Score.

**Critical:** BLK-001/002 or BLK-007 with identity/replay/ads → **BTS-Denied** until fixed.

- **Score <10 & no Critical** → BTS-Bronze candidate
- **10–19 & no Critical** → BTS-Silver after fixes
- **≥20 or any Critical** → Denied; re-verify after remediation

---

## Minimal UI (week one)

- **Projects:** domain · last scan · score · critical flags · Download Pack
- **Findings:** detections & gaps with evidence chips `{script|network|global|cookie|inline}`
- **Controls:** pass/fail by BLK ID with remediation owners

---

## Manifest (attestation)

Publish `/.well-known/blackout.json`:

```json
{
  "bts_version": "0.1",
  "badge": {
    "tier": "silver",
    "score": 83,
    "last_verified": "2025-11-07"
  },
  "disclosures": {
    "policy_url": "https://example.com/privacy",
    "subprocessors_url": "https://example.com/subprocessors"
  },
  "runtime": {
    "region_gating": true,
    "consent_gpc_honored": true
  },
  "evidence": {
    "pack_sha256": "7b2c...c1a9",
    "report_url": "https://example.com/blackout/report.pdf"
  }
}
```

---

## Responsible disclosure & revocation

- **Private remediation window**; dispute → re-scan → logged outcome.
- **Critical breach:** 72-hour remediation or public suspension.
- **Public revocation log** keeps the badge honest.

**RFP clause:**
"Vendor must maintain BTS-Silver or higher and host a valid `/.well-known/blackout.json`. Buyer may perform independent runtime verification prior to award and quarterly thereafter. Badge suspension is grounds for reassessment."

---

## The Blackout ecosystem

**Blackout for Teams — The Console** (available):
Private audits for Legal/RevOps with counsel-ready exports.

**Blackout Sensor — The Shield** (roadmap):
Opt-in Proof Cards for individuals; correlate outreach to detections.

**BLK — The Ledger** (roadmap):
Evidence-hash registry & attestation APIs; open signature sets; public revocations.

---

**Not a blocker, browser, or on-site widget. No legal advice.**
We provide counsel-ready evidence, not promises.

---

## Get certified / Get involved

- [Founding Cohort](https://deployblackout.com/#waitlist)
- [Enterprise Audit](https://deployblackout.com/#waitlist)
- [Sensor Waitlist](https://deployblackout.com/#waitlist)

**Site:** [deployblackout.com](https://deployblackout.com)
**Email:** hello@deployblackout.com

---

## Proof & Evidence

- [Methodology](https://deployblackout.com/proof/methodology)
- [Verification Matrix](https://deployblackout.com/proof/matrix)
- [Sample Evidence Pack](https://deployblackout.com/proof/sample-evidence)

---

## Promise vs Payload

![Promise vs Payload](https://deployblackout.com/assets/promise-vs-payload.png)

**Left:** Landing page claim — "Privacy-first. We don't track you."
**Right:** HAR capture — `T+84ms → connect.facebook.net/en_US/fbevents.js` (pre-consent)

**Download sample evidence** · **Request audit**
