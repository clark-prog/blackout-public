![Blackout Logo](2.svg)

# BLACKOUT — GTM behavior you can verify

**Blackout is a GTM Compliance platform** (RegTech × MarTech) that verifies what actually runs in the browser after **“Reject All”** and certifies it against the **Blackout Trust Standard (BTS)**.  
We don’t grade influence. **We verify behavior.**

---

## What is Ƀłⱥȼҟꝋᵾⱦ?

**Continuous, disclosure-grade verification** for hidden tracking and white-label surveillance.  
Detect what’s really running, diff it against what’s disclosed, and **auto-generate the receipts**.

---

## Why Blackout exists

- Everyone understands **SOC2/ISO**. Security earned its standard.  
- **Sales & marketing never did.** Vendors hid behind cookie banners and pay-to-play rankings while identity tech, session replay, and ad pixels still fire **after “Reject All.”**  
- Blackout makes GTM conduct **legible, testable, and enforceable**—with receipts.

> We don’t argue intent. **We publish timing and URLs.**

---

## What Blackout does (at a glance)

1. **Detect** — Capture post-consent timelines (initiator chains, request URLs, timestamps).  
2. **Diff** — Compare runtime vendors to your **subprocessor list** and stated policy.  
3. **Prove** — Hash the evidence pack and issue (or deny) a **BTS badge** (Bronze/Silver/Gold).  
4. **Enforce** — Badges can be **suspended or revoked** on critical drift. Public log.

All verification is performed **offline**. This site runs **no third-party trackers**.

---

## The Blackout Trust Standard (BTS)

**BTS is the evidence-based compliance standard for go-to-market behavior online.**

**Controls (evidence, not opinions):**  
- **Consent governance** — no identity/replay/ads fire post-reject  
- **Disclosure parity** — your policy ↔ your runtime  
- **De-anonymization** — explicit, verifiable opt-in or it’s out  
- **Proof** — initiator chains, request URLs, timestamps  
- **Attestation** — host a manifest at `/.well-known/blackout.json`  
- **Enforcement** — badge can be **suspended or revoked**

**Badge tiers:**  
- **BTS-Bronze (≥70)** — No identity/replay/ads post-reject; GPC honored; substantial subprocessor parity  
- **BTS-Silver (≥80)** — Bronze + no de-anon without explicit opt-in; full disclosure parity  
- **BTS-Gold (≥90)** — Silver + no session replay or fingerprinting; regional consent gating verified

**Badge label (alt):**  
`Blackout Trust Standard — {Tier} — Last verified: YYYY-MM-DD`

---

# BLK — The Blackout Compliance Framework (v0.1)

Operational controls, scoring, and schemas for verifying GTM runtime behavior against the **Blackout Trust Standard (BTS)**.

---

## Control Library (v0.1)

IDs → check → suggested remediation.

- **BLK-001 Undisclosed Subprocessor**  
  **Check:** vendor in `detections` ∉ `disclosures`.  
  **Remediate:** add vendor to subprocessor list; republish policy with version/date.

- **BLK-002 De-anonymization Without Notice**  
  **Check:** `category = "deanonymization"` detected; no explicit identity-resolution notice/basis in policy.  
  **Remediate:** add clear notice, lawful basis (opt-in/opt-out), retention, DPA references.

- **BLK-003 Session Recording Without Consent**  
  **Check:** `category = "session-replay"` loads before recorded consent.  
  **Remediate:** gate behind CMP; honor region logic and GPC.

- **BLK-004 Enrichment on PII Without Basis**  
  **Check:** enrichment calls after form submit; disclosures omit enrichment vendors/uses.  
  **Remediate:** disclose enrichment purpose, vendors, retention; update DPA/ROPA.

- **BLK-005 Shadow Cookies / CNAME Cloak**  
  **Check:** third-party tracking via first-party CNAME; cookies set pre-consent.  
  **Remediate:** disable until consent; document vendor + purpose; adjust DNS/CSP.

- **BLK-006 “Instant Outreach” from Web Events**  
  **Check:** webhook to SDR/LLM using visit-level signals; no disclosure of automated decisioning.  
  **Remediate:** disclose automated processing; provide opt-out and escalation path.

- **BLK-007 Consent Timing Violation**  
  **Check:** any identity/replay/ads request timestamp < first consent accept; or persists after **Reject All**.  
  **Remediate:** enforce true prior consent; block scripts until state is known.

- **BLK-008 GPC / DNT Not Honored**  
  **Check:** `Global Privacy Control` or browser DNT ignored in regions where honored/claimed.  
  **Remediate:** respect signals consistently; update policy to match behavior.

- **BLK-009 Region Gating Failure**  
  **Check:** EU/UK/CA visitors receive identity/replay/ads despite regional gating claims.  
  **Remediate:** fix geo logic; add region tests to CI; update manifests.

- **BLK-010 Fingerprinting / Evasion**  
  **Check:** canvas/audio/font fingerprinting or **S3/CDN alias** evasion (e.g., `b2bjsstore` S3).  
  **Remediate:** remove non-essential fingerprinting; stop alias evasion; disclose unavoidable signals.

- **BLK-011 Policy–Runtime Mismatch**  
  **Check:** policy states “no X” but runtime shows X (or stale subprocessor revision).  
  **Remediate:** bring runtime into compliance or update policy; date/version the change.

- **BLK-012 Unattributed Pixel / Unknown Vendor**  
  **Check:** network host not listed in disclosures or vendor registry.  
  **Remediate:** identify owner; disclose or remove; add to vendor inventory.

---

## Risk & Scoring

- **Severity (S):** 1–5 (user harm / regulatory exposure)  
- **Exposure (E):** pages affected × traffic class `{WEBSITE|APP|AUTH}` ⇒ weight `{1|2|3}`  
- **Remediation Difficulty (R):** 1–3 (effort/time/risk)

**Non-Compliance Score = (S × E) + R** (per control, capped by control policy)

**Critical flags:**  
- If **BLK-001** or **BLK-002** present → mark **CRITICAL**.  
- If **BLK-007** present with identity/replay/ads → mark **CRITICAL**.

**Badge guidance (map to BTS):**
- `Score < 10` and **no Critical** → candidate **BTS-Bronze** (if all identity/replay/ads post-reject = none)  
- `10–19` and **no Critical** → candidate **BTS-Silver** after remediation of disclosure gaps  
- `≥20` or **any Critical** → **BTS-Denied** until fixes verified  
- **BTS-Gold** requires **no** session-replay/fingerprinting and clean region gating

---

## Minimal UI (week one)

- **Projects:** domain · last scan · score · critical flags · “Download Pack”  
- **Findings:** detections list & gaps list with evidence chips `{script|network|global|cookie|inline}`  
- **Controls:** pass/fail by BLK ID with remediation copy & owners

---

## Data Model (JSON Schemas)

### Detection
```json
{
  "id": "det_01HZZ7N...",
  "domain": "example.com",
  "vendor_id": "warmly",
  "category": "deanonymization",
  "artifact": { "type": "script", "value": "https://cdn.../warmly.js" },
  "consent_state": "reject", 
  "ts_first_seen": "2025-11-05T03:12:30.120Z",
  "ts_last_seen": "2025-11-05T03:12:30.120Z",
  "confidence": 0.96,
  "signals": ["network", "script", "global"]
}



## The Blackout Ecosystem

**One mission: rebuild trust with evidence—not influence.**

### 🏢 Blackout for Teams — *The Console (available)*
Private audits for Legal/RevOps. Consent timelines, initiator chains, **disclosure-vs-runtime** diffs, and counsel-ready exports. Every vendor called by name in your report.

### 🛡️ Blackout Sensor — *The Shield (roadmap)*
Opt-in **Proof Cards** and alerts so individuals can see who’s watching before the pitch—and correlate outreach to detections they can share.

### 🔗 BLK — *Blackout Ledger (roadmap)*
Evidence-hash registry and attestation APIs for CI/security controls. Public **revocation log** and open signature sets.

> **No on-site scanner.** Verification is offline; evidence packs are shareable with counsel.

---

## How it works (verify & certify, not block)

**Observe** — Capture post-consent timelines: initiator chains, request URLs, timestamps.  
**Compare** — Diff runtime vendors against subprocessor/privacy disclosures.  
**Attest** — Hash the evidence pack (SHA-256); issue **BTS** or remediation.  
**Enforce** — Badges are **revocable**; critical drift triggers suspension & re-verification.

### Detection signals (multi-layer)
- Script hosts & loader patterns (incl. CDN → **S3** fallbacks)  
- Window globals & inline init calls  
- Network patterns (hosts, paths, cache-busting)  
- Consent timing vs first request  
- Fingerprinting/replay surfaces

**Example evidence line:**  
+186 ms post-reject → s3-us-west-2.amazonaws.com/b2bjsstore/.../reb2b.js.gz

---

## What Blackout is **not**

- Not a browser, ad-blocker, or on-site widget  
- Not pay-to-play rankings or “magic shapes”  
- Not a legal opinion—**we provide counsel-ready evidence**, not promises

---

## Manifest (attestation)

Publish a machine-readable manifest so buyers can self-check basics.

`/.well-known/blackout.json`
```json
{
  "bts_version": "0.1",
  "badge": { "tier": "silver", "score": 83, "last_verified": "2025-11-07" },
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
R## Responsible disclosure & revocation

- **Private remediation window** for badged companies  
- **Dispute → re-scan → logged outcome**  
- **Critical breach** (e.g., identity/replay firing post-reject) → **72-hour** remediation or **public suspension**  
- **Public revocation log** keeps the badge honest

---

## RFP clause (copy/paste)

> Vendor must maintain **BTS-Silver or higher** and host a valid `/.well-known/blackout.json`. Buyer may perform independent runtime verification prior to award and quarterly thereafter. Badge suspension is grounds for reassessment.

---

## Roadmap (high-level)

- Public **revocation log**  
- **Open signatures** for vendor detection (PRs welcome)  
- **BLK** attestation & evidence-hash APIs  
- Partner labs for adversarial testing and signature hardening

---

## Contributing

- Propose vendor signatures (host/path regex, function-chain fingerprints, consent-timing rules)  
- Submit redacted **Proof Cards** (URLs + timings only; no PII)  
- File issues with reproducible steps and timestamps

---

## Ethics & privacy posture

- We store **observable runtime facts** (timelines, URLs, initiators).  
- **No PII. No fingerprinting. No cookie planting.**  
- Sensor (when available) will be strictly **opt-in**; users choose what to share.

---

## Get certified / Get involved

- **Founding Cohort** — Priority audits & early steering input  
- **Request an Enterprise Audit** — Legal/RevOps ready  
- **Join the Sensor Waitlist** — Personal Proof Cards & alerts

**Site:** https://www.deployblackout.com  
**Contact:** hello@deployblackout.com
