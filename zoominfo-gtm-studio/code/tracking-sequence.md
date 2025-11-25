# ZoomInfo GTM Studio: Tracking Sequence Analysis

## Complete Request Timeline

This document shows the exact sequence of tracking requests on the GTM Studio landing page.

## Phase 1: Document Load (0-100ms)

```
#1  GET https://www.zoominfo.com/products/gtm-studio
    └── Document load begins
```

## Phase 2: Critical Resources (100-300ms)

```
#41     GET https://www.googletagmanager.com/gtm.js?id=GTM-PHWTRTJ
        └── Google Tag Manager loads [PRE-CONSENT]

#47     GET https://cdn.cookielaw.org/scripttemplates/otSDKStub.js
        └── OneTrust consent stub loads

#48     GET https://www.zoominfo.com/osx7m0dx/init.js
        └── PerimeterX init script [PRE-CONSENT]
```

## Phase 3: Pre-Consent Tracking (300-500ms)

```
#78     GET https://tzm.px-cloud.net/ns
        └── PerimeterX network sensor [VIOLATION]

#79     POST https://collector-pxosx7m0dx.px-cloud.net/api/v2/collector
        └── PerimeterX fingerprint collection [VIOLATION]

#87     POST https://gw-app.zoominfo.com/gw/ziapi/fraud-detection/api/v1/sessions
        └── Fraud detection session created [VIOLATION]
        └── Response: {"sessionKey":"9c8821ba-030e-4169-832e-79d5f88036e8"}
```

## Phase 4: Consent SDK Loads (500-600ms)

```
#90     GET https://cdn.cookielaw.org/.../otBannerSdk.js
        └── OneTrust banner SDK finally loads
```

## Phase 5: Post-SDK But Pre-Interaction (600-900ms)

```
#103    POST https://www.google.com/ccm/collect
        └── Google conversion tracking [NO CONSENT]

#105    GET https://bat.bing.com/bat.js
        └── Bing Ads tracking [NO CONSENT]

#107    GET https://analytics.tiktok.com/i18n/pixel/events.js
        └── TikTok pixel [NO CONSENT]

#119    GET https://frapi.zoominfo.com/assets/collector.min.d4021d2.html
        └── Sardine.ai biometrics collector iframe [VIOLATION]
        └── enableBiometrics: true
        └── enableDNS: true
```

## Phase 6: Biometrics & Ad Tech (900ms+)

```
#155    GET https://ntbjkuss0tbhk250k9m39j8w2vr79jke.d.sardine.ai/bg.png
        └── Sardine fingerprint pixel [VIOLATION]
```

## Summary: Pre-Consent Violations

| Request | URL | Type |
|---------|-----|------|
| #41 | googletagmanager.com/gtm.js | Analytics |
| #48 | zoominfo.com/osx7m0dx/init.js | Fingerprinting |
| #79 | collector-pxosx7m0dx.px-cloud.net | Fingerprinting |
| #87 | gw-app.zoominfo.com/fraud-detection | Fingerprinting |
| #119 | frapi.zoominfo.com/collector | Biometrics |
| #155 | *.d.sardine.ai/bg.png | Fingerprinting |

**Total Pre-Consent/No-Consent Tracking Requests:** 50+  
**Consent SDK Load Request #:** 90
