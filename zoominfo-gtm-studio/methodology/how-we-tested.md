# Methodology: How We Tested

## Overview

This document describes the methodology used to analyze ZoomInfo's GTM Studio landing page for pre-consent tracking violations.

## Tools Used

| Tool | Purpose |
|------|---------|
| Google Chrome 142 | Browser for testing |
| Chrome DevTools | Network capture & analysis |
| Node.js | Base64 decoding |

## Testing Environment

- **Browser:** Google Chrome 142.0.7444.176 (64-bit)
- **OS:** Windows 10/11
- **Network:** Standard residential connection
- **Location:** United States
- **Date:** November 25, 2025

## Step-by-Step Procedure

### 1. Prepare Browser

```
1. Open Chrome in Incognito mode (Ctrl+Shift+N)
2. Open DevTools (F12)
3. Go to Network tab
4. Enable "Preserve log" checkbox
5. Enable "Disable cache" checkbox
```

### 2. Navigate to Target

```
1. In URL bar, enter: https://www.zoominfo.com/products/gtm-studio
2. Press Enter
3. DO NOT interact with consent banner
4. DO NOT click anywhere on page
5. Wait for page to fully load (~5 seconds)
```

### 3. Capture Evidence

```
1. In Network tab, observe request count
2. Note requests firing before consent interaction
3. Right-click → "Save all as HAR with content"
```

### 4. Decode Sardine Configuration

```bash
# Find request to frapi.zoominfo.com/assets/collector.min.*.html
# Copy the URL fragment (after #)
# Decode base64:
echo "[fragment]" | base64 -d | jq .
```

## Reproduction Instructions

### Quick Test (5 minutes)

1. Open Chrome Incognito
2. Open DevTools → Network tab
3. Enable "Preserve log"
4. Navigate to https://www.zoominfo.com/products/gtm-studio
5. **DO NOT INTERACT WITH PAGE**
6. Count requests that fire before you see consent banner

### What To Search For

- `sardine.ai` - Biometrics fingerprinting
- `px-cloud.net` - PerimeterX bot detection
- `fraud-detection` - Session fingerprinting

## What Constitutes a Violation

Any request that:
1. Fires before consent SDK loads
2. Collects identifying information
3. Sets tracking cookies
4. Creates device fingerprints
5. Collects behavioral data

---

**Testing Conducted By:** Blackout Security Research  
**Date:** November 25, 2025
