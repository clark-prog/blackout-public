# ZoomInfo GTM Studio: Technical Findings

**Target:** https://www.zoominfo.com/products/gtm-studio  
**Date:** November 25, 2025  
**Methodology:** Live browser reconnaissance via Chrome DevTools  
**Total Requests Analyzed:** 234  
**Unique Domains Contacted:** 118

---

## 1. Consent Timing Analysis

### Request Sequence (Pre-Consent Violations)

| Request # | Category | URL | Status |
|-----------|----------|-----|--------|
| 41 | Analytics | `googletagmanager.com/gtm.js?id=GTM-PHWTRTJ` | **PRE-CONSENT** |
| 47 | Consent SDK | `cdn.cookielaw.org/scripttemplates/otSDKStub.js` | Loading |
| 48 | Fingerprint | `zoominfo.com/osx7m0dx/init.js` (PerimeterX) | **PRE-CONSENT** |
| 62 | Geolocation | `geolocation.onetrust.com/.../geo/location` | Determining |
| **79** | **Fingerprint** | `collector-pxosx7m0dx.px-cloud.net/api/v2/collector` | **VIOLATION** |
| **87** | **Identity** | `gw-app.zoominfo.com/gw/ziapi/fraud-detection/api/v1/sessions` | **VIOLATION** |
| 90 | Consent SDK | `cdn.cookielaw.org/.../otBannerSdk.js` | SDK Loads |
| **119** | **Biometrics** | `frapi.zoominfo.com/assets/collector.min.d4021d2.html` | **VIOLATION** |
| **155** | **Fingerprint** | `*.d.sardine.ai/bg.png` | **VIOLATION** |

### Timeline

```
0ms     - Page load begins
~100ms  - GTM fires (PRE-CONSENT)
~150ms  - PerimeterX init loads (PRE-CONSENT)
~300ms  - OneTrust SDK starts loading
~400ms  - PerimeterX collector POST fires (VIOLATION)
~450ms  - Fraud detection session created (VIOLATION)
~500ms  - Consent banner SDK loads
~600ms  - Sardine.ai biometrics collector loads (VIOLATION)
~800ms  - Sardine fingerprint pixels fire (VIOLATION)
???     - User sees consent banner (IF EVER)
```

**Key Finding:** Tracking fires 400-800ms BEFORE consent SDK fully loads.

---

## 2. Sardine.ai Biometrics Collection

### Configuration (Decoded from Base64)

The collector iframe at `frapi.zoominfo.com/assets/collector.min.d4021d2.html` contains a base64-encoded configuration:

```json
{
  "loaderInitTime": 1764084620894,
  "enableBiometrics": true,
  "enableDNS": true,
  "revision": "2025-10-28-d4021d2",
  "origin": "https://www.zoominfo.com",
  "collectorDomain": "frapi.zoominfo.com",
  "pixelURL": "https://p.zoominfo.com/v1/b.png",
  "dBaseDomain": "d.sardine.ai",
  "location": "https://www.zoominfo.com/products/gtm-studio",
  "sessionKey": "9c8821ba-030e-4169-832e-79d5f88036e8",
  "environment": "production",
  "partnerId": "zoominfo"
}
```

### Critical Fields Explained

| Field | Value | Implication |
|-------|-------|-------------|
| `enableBiometrics` | `true` | Mouse movements, typing patterns, scroll behavior collected |
| `enableDNS` | `true` | DNS fingerprinting enabled |
| `dBaseDomain` | `d.sardine.ai` | Sardine.ai fingerprinting infrastructure |
| `partnerId` | `zoominfo` | ZoomInfo has formal partnership with Sardine.ai |
| `environment` | `production` | Live production deployment |

### Sardine Fingerprint Pixels

Multiple hashed subdomain requests observed:

```
ntbjkuss0tbhk250k9m39j8w2vr79jke.d.sardine.ai/bg.png
hujehbun7m3axhey43rwnwws64qorro1.d.sardine.ai/bg.png
3j1ly3e46x5zvzekyvvv2w9q1mia4uji.d.sardine.ai/bg.png
61vzbdkdore0uxg9wp0e31pug7yblt15.d.sardine.ai/bg.png
cwel4b8n9i9yiax7z7szhqm1oq9i68me.d.sardine.ai/bg.png
```

**Pattern:** 32-character hashed subdomains indicate multi-vector fingerprinting.

---

## 3. PerimeterX Bot Detection

### Infrastructure

- **App ID:** `PXosx7m0dx`
- **Collector:** `collector-pxosx7m0dx.px-cloud.net/api/v2/collector`
- **Network Sensor:** `tzm.px-cloud.net/ns`

### Timing

- **Request #48:** PerimeterX init script loads
- **Request #79:** First collector POST fires
- **Request #156:** Additional collector POST

**Verdict:** PerimeterX fingerprinting fires BEFORE consent SDK loads.

---

## 4. Fraud Detection API

### Endpoint

```
POST https://gw-app.zoominfo.com/gw/ziapi/fraud-detection/api/v1/sessions
```

### Response

```json
{
  "sessionKey": "9c8821ba-030e-4169-832e-79d5f88036e8"
}
```

### Correlation

The `sessionKey` from this response matches the `sessionKey` in the Sardine.ai config, proving these systems are linked for cross-vendor fingerprint correlation.

---

## 5. Complete Domain List (118 Unique)

### Identity & Fingerprinting (4)
- *.d.sardine.ai (Sardine - behavioral biometrics)
- collector-pxosx7m0dx.px-cloud.net (PerimeterX)
- tzm.px-cloud.net (PerimeterX)
- api.identitymatrix.ai (IdentityMatrix)

### Advertising (15+)
- bat.bing.com / bat.bing.net (Microsoft)
- analytics.tiktok.com
- tr.snapchat.com
- insight.adsrvr.org (Trade Desk)
- tags.srv.stackadapt.com
- aorta.clickagy.com (ZoomInfo subsidiary)
- px.ads.linkedin.com
- a.quora.com
- www.redditstatic.com

### Data Sync/Exchange (10+)
- ib.adnxs.com (AppNexus/Xandr)
- sync.crwdcntrl.net (Lotame)
- ei.rlcdn.com (LiveRamp)
- i.liadm.com (LiveIntent)

---

## 6. The Irony

### ZoomInfo's Product Claim
> "Identify Person-Level Website Visits"

### ZoomInfo's Actual Behavior

Uses **3 external identity/fingerprinting vendors** on their own site:
1. **Sardine.ai** - Behavioral biometrics
2. **PerimeterX** - Bot detection/fingerprinting
3. **IdentityMatrix.ai** - Identity resolution

**Translation:** Even the visitor identification vendor doesn't trust their own product for visitor identification.

---

**Investigation Conducted By:** Blackout Security Research  
**Date:** November 25, 2025
