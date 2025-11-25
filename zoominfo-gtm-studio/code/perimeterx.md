# PerimeterX Infrastructure on ZoomInfo

## App Configuration

| Field | Value |
|-------|-------|
| App ID | `PXosx7m0dx` |
| Init Script | `zoominfo.com/osx7m0dx/init.js` |
| Collector | `collector-pxosx7m0dx.px-cloud.net` |
| Network Sensor | `tzm.px-cloud.net` |

## Endpoints Observed

### 1. Initialization Script
```
GET https://www.zoominfo.com/osx7m0dx/init.js
```
Loads PerimeterX bot detection framework.

### 2. Collector API
```
POST https://collector-pxosx7m0dx.px-cloud.net/api/v2/collector
```

**Request Body Parameters:**
- `payload` - Encoded fingerprint data
- `appId` - PXosx7m0dx
- `tag` - Session tag
- `uuid` - Unique visitor ID
- `ft` - Fingerprint type
- `seq` - Sequence number
- `pxhd` - Encrypted fingerprint header

### 3. Network Sensor
```
GET https://tzm.px-cloud.net/ns?c=[session_id]
```
Network-level fingerprinting and monitoring.

## Timing Analysis

| Request # | Endpoint | Relative Timing |
|-----------|----------|-----------------|
| 48 | Init script loads | ~150ms |
| 78 | Network sensor | ~350ms |
| 79 | First collector POST | ~400ms |
| 156 | Second collector POST | ~900ms |

**Note:** All PerimeterX requests fire BEFORE the OneTrust consent banner SDK fully loads (Request #90).

## What PerimeterX Collects

1. **Device Fingerprint**
   - Browser type and version
   - Operating system
   - Screen resolution
   - Canvas fingerprint
   - WebGL fingerprint

2. **Behavioral Signals**
   - Mouse movements
   - Keyboard patterns
   - Touch gestures
   - Scroll behavior

3. **Network Signals**
   - IP address
   - Connection type
   - Network latency
   - DNS characteristics

## Compliance Implications

PerimeterX is deployed for "bot detection" but:
- Fires before consent is obtained
- Collects behavioral data by default
- Creates persistent device fingerprints
- May constitute "tracking" under GDPR/ePrivacy
