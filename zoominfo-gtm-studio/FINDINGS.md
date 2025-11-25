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

## 2. FormComplete: Pre-Submission Data Capture (CRITICAL)

### The Evidence

During this capture, the following request was made **without my knowledge or consent**:

```
POST https://ws.zoominfo.com/formcomplete-internal/getNeverbounce
Body: {"email":"clark@deployronin.com","formId":"79afc4d1-7040-4e49-945c-57ba17399b28"}
```

**Initiator:** `https://ws-assets.zoominfo.com/formcomplete.js`

### Let Me Be Crystal Clear

Yes, that's my email. `clark@deployronin.com`. I'm not hiding it.

**Here's what I did NOT do:**
- ❌ Fill out a form on this page
- ❌ Click any submit button
- ❌ Type my email into any field
- ❌ Give ZoomInfo permission to collect this

**Here's what DID happen:**
- ✅ My browser's autofill populated a field (standard browser behavior)
- ✅ ZoomInfo's `formcomplete.js` detected this
- ✅ ZoomInfo immediately transmitted my email to their servers
- ✅ They validated it against NeverBounce (email verification service)

### Technical Analysis

The call stack from the HAR file shows:

```
formcomplete.js:17509 → t()
formcomplete.js:17712 → s()
formcomplete.js:17771 → anonymous
formcomplete.js:40767 → anonymous
formcomplete.js:31478 → anonymous
formcomplete.js:754   → h()
formcomplete.js:2096  → anonymous
formcomplete.js:1183  → anonymous
```

This is **not** form submission handling. This is an **input field watcher** that:
1. Monitors all `<input>` elements on the page
2. Detects when values appear (typed OR autofilled)
3. Immediately transmits email addresses to ZoomInfo's servers
4. Does this **before any user action**

### The Product This Powers

This is ZoomInfo's **"FormComplete"** product, marketed as:
> "Automatically enrich form submissions with verified contact data"

**Reality:** It captures emails from form fields **before submission**, meaning:
- Users who start filling a form but abandon it get captured
- Browser autofill triggers capture without user knowledge
- The "form submission" ZoomInfo enriches may never have been submitted

### What This Feels Like

I'm not here to speculate on ZoomInfo's intent. I'm here to tell you what it feels like to be on the receiving end of this.

I visited a marketing page. I didn't fill out a form. I didn't click submit. I didn't opt into anything. And yet my email address was transmitted to ZoomInfo's servers and validated against a third-party service.

**That feels violating.**

The technical explanation is probably "we enrich form data to improve lead quality." But from where I'm sitting — as the person whose data was just taken — the experience is:

1. I went to read about a product
2. My browser did normal browser things (autofill)
3. A script watched that happen and immediately sent my email to ZoomInfo
4. I had no idea until I analyzed the network traffic

Users don't consent to this. Users don't expect this. Users are entitled to feel however they feel about discovering their data was captured this way.

I feel like my pocket got picked while I was window shopping.

That's my perception. The HAR file is the evidence. Draw your own conclusions.

---

## 3. Sardine.ai Biometrics Collection

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
  "referrer": "",
  "uuid": "99656dd7-a545-4f6c-8fd4-d0a8288da2bd",
  "clientId": "7fb5c66f-1918-44dd-b6e6-66bc99a271c8",
  "sessionKey": "9c8821ba-030e-4169-832e-79d5f88036e8",
  "userIdHash": "492e69f3-8422-44be-bee1-a49623c0d0e5",
  "flow": "onboarding",
  "environment": "production",
  "partnerId": "zoominfo",
  "apiSubdomain": "frapi.zoominfo.com",
  "pixelSubdomain": "p.zoominfo.com"
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
nq9hb24r7ol1j9hnli6c6e2lwziofz33.d.sardine.ai/bg.png
fz22n8o3rsbhm5k834a5kpw5dv9arehw.d.sardine.ai/bg.png
```

**Pattern:** 32-character hashed subdomains indicate multi-vector fingerprinting.

---

## 4. PerimeterX Bot Detection

### Infrastructure

- **App ID:** `PXosx7m0dx`
- **Collector:** `collector-pxosx7m0dx.px-cloud.net/api/v2/collector`
- **Network Sensor:** `tzm.px-cloud.net/ns`

### Request Payload Sample

```
payload=[encoded fingerprint data]
appId=PXosx7m0dx
tag=ZjgXeyhNGRB/
uuid=a6fd1a80-ca13-11f0-aea5-bbeb5dcb2245
ft=369
seq=0
en=NTA
pc=0061410833470998
pxhd=[encrypted fingerprint data]
rsc=1
```

### Timing

- **Request #48:** PerimeterX init script loads
- **Request #79:** First collector POST fires
- **Request #156:** Additional collector POST

**Verdict:** PerimeterX fingerprinting fires BEFORE consent SDK loads.

---

## 5. Fraud Detection API

### Endpoint

```
POST https://gw-app.zoominfo.com/gw/ziapi/fraud-detection/api/v1/sessions
```

### Request

```json
{
  "customerId": "492e69f3-8422-44be-bee1-a49623c0d0e5",
  "origin": "CWS",
  "platform": "zoominfo"
}
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

## 6. Complete Domain List (118 Unique)

### ZoomInfo Infrastructure (8)
- frapi.zoominfo.com
- js.zi-scripts.com
- ws.zoominfo.com
- wss.zoominfo.com
- p.zoominfo.com
- schedule.zoominfo.com
- ws-assets.zoominfo.com
- gw-app.zoominfo.com

### Identity & Fingerprinting (4)
- *.d.sardine.ai (Sardine - behavioral biometrics)
- collector-pxosx7m0dx.px-cloud.net (PerimeterX)
- tzm.px-cloud.net (PerimeterX)
- api.identitymatrix.ai (IdentityMatrix)

### Google (8)
- www.googletagmanager.com
- analytics.google.com
- googleads.g.doubleclick.net
- stats.g.doubleclick.net
- cm.g.doubleclick.net
- www.google.com
- fcmatch.google.com
- fcmatch.youtube.com

### Advertising (15+)
- bat.bing.com / bat.bing.net (Microsoft)
- analytics.tiktok.com
- tr.snapchat.com / tr6.snapchat.com
- insight.adsrvr.org / js.adsrvr.org (Trade Desk)
- tags.srv.stackadapt.com
- aorta.clickagy.com / hemsync.clickagy.com / tags.clickagy.com
- px.ads.linkedin.com
- a.quora.com / q.quora.com
- www.redditstatic.com / alb.reddit.com
- pixel.tapad.com

### Marketing/Analytics (10+)
- cdn.cookielaw.org (OneTrust)
- geolocation.onetrust.com
- events.launchdarkly.com
- api2.amplitude.com
- munchkin.marketo.net
- js.navattic.com / app.navattic.com
- zoominfo.widget.insent.ai
- js.partnerstack.com

### Data Sync/Exchange (10+)
- ib.adnxs.com (AppNexus/Xandr)
- sync.crwdcntrl.net (Lotame)
- ei.rlcdn.com / idsync.rlcdn.com (LiveRamp)
- i.liadm.com (LiveIntent)
- sync.graph.bluecava.com
- sync.ipredictive.com

---

## 7. Initiator Chain

```
www.zoominfo.com/products/gtm-studio (document)
    │
    ├─► GTM-PHWTRTJ (Google Tag Manager)
    │   ├─► Google Analytics (G-PP03JV8JP3)
    │   ├─► Google Ads (AW-1014544981)
    │   ├─► Google Ads (AW-11081837180)
    │   ├─► Google Ads (AW-11085496201)
    │   ├─► Bing Ads (ti=5991834)
    │   ├─► TikTok Pixel
    │   ├─► Snapchat Pixel
    │   └─► Trade Desk, StackAdapt, Clickagy...
    │
    ├─► frapi.zoominfo.com/assets/loader.min.js
    │   └─► frapi.zoominfo.com/assets/collector.min.*.html
    │       └─► *.d.sardine.ai/bg.png (fingerprints)
    │
    ├─► js.zi-scripts.com/zi-tag.js
    │   ├─► ws.zoominfo.com/pixel/*
    │   └─► zi-script-telemetry-dev.clickagydev.io
    │
    └─► zoominfo.com/osx7m0dx/init.js (PerimeterX)
        └─► collector-pxosx7m0dx.px-cloud.net
```

---

## 8. The Irony

### ZoomInfo's Product Claim
> "Identify Person-Level Website Visits"

### ZoomInfo's Actual Behavior

Uses **3 external identity/fingerprinting vendors** on their own site:
1. **Sardine.ai** - Behavioral biometrics
2. **PerimeterX** - Bot detection/fingerprinting
3. **IdentityMatrix.ai** - Identity resolution

**Translation:** Even the visitor identification vendor doesn't trust their own product for visitor identification.

---

## 9. Raw Evidence

### Base64 Encoded Sardine Config

```
eyJsb2FkZXJJbml0VGltZSI6MTc2NDA4NDYyMDg5NCwiZW5hYmxlQmlvbWV0cmljcyI6dHJ1ZSwiZW5hYmxlRE5TIjp0cnVlLCJyZXZpc2lvbiI6IjIwMjUtMTAtMjgtZDQwMjFkMiIsIm9yaWdpbiI6Imh0dHBzOi8vd3d3Lnpvb21pbmZvLmNvbSIsImNvbGxlY3RvckRvbWFpbiI6ImZyYXBpLnpvb21pbmZvLmNvbSIsInBpeGVsVVJMIjoiaHR0cHM6Ly9wLnpvb21pbmZvLmNvbS92MS9iLnBuZyIsImRCYXNlRG9tYWluIjoiZC5zYXJkaW5lLmFpIiwibG9jYXRpb24iOiJodHRwczovL3d3dy56b29taW5mby5jb20vcHJvZHVjdHMvZ3RtLXN0dWRpbyIsInJlZmVycmVyIjoiIiwidXVpZCI6Ijk5NjU2ZGQ3LWE1NDUtNGY2Yy04ZmQ0LWQwYTgyODhkYTJiZCIsImNsaWVudElkIjoiN2ZiNWM2NmYtMTkxOC00NGRkLWI2ZTYtNjZiYzk5YTI3MWM4Iiwic2Vzc2lvbktleSI6IjljODgyMWJhLTAzMGUtNDE2OS04MzJlLTc5ZDVmODgwMzZlOCIsInVzZXJJZEhhc2giOiI0OTJlNjlmMy04NDIyLTQ0YmUtYmVlMS1hNDk2MjNjMGQwZTUiLCJmbG93Ijoib25ib2FyZGluZyIsImVudmlyb25tZW50IjoicHJvZHVjdGlvbiIsInBhcnRuZXJJZCI6Inpvb21pbmZvIiwiYXBpU3ViZG9tYWluIjoiZnJhcGkuem9vbWluZm8uY29tIiwicGl4ZWxTdWJkb21haW4iOiJwLnpvb21pbmZvLmNvbSJ9
```

### Decode Command

```bash
echo "[base64 string]" | base64 -d | jq .
```

---

**Investigation Conducted By:** Blackout Security Research
**Date:** November 25, 2025
