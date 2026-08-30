# RJTOOL — iOS

iOS port of RJTOOL `v1.0.59` — PUBG Mobile asset path index browser.  
163,833 game file paths, searchable and filterable by category.

---

## What's inside

| File | Purpose |
|------|---------|
| `RJTOOL/RJTOOLApp.swift` | App entry point (`@main`) |
| `RJTOOL/IndexStore.swift` | Loads + filters `index.csv` off main thread |
| `RJTOOL/ContentView.swift` | Tab controller (Search / Browse / About) |
| `RJTOOL/SearchView.swift` | Full-text search across all 163k paths |
| `RJTOOL/BrowseView.swift` | Category-tree browser |
| `RJTOOL/AboutView.swift` | App info screen |
| `RJTOOL/Resources/index.csv` | Full PUBG Mobile asset index (16 MB) |
| `.github/workflows/build-ipa.yml` | GitHub Actions — produces IPA |

---

## Build locally

Requirements: macOS 13+, Xcode 15+

```bash
git clone <your-repo>
cd RJTOOL-iOS
open RJTOOL.xcodeproj
```

Select your team in **Signing & Capabilities**, then ⌘R.

---

## GitHub Actions — unsigned IPA (no certs needed)

1. Push to `main` / `master`  
2. Actions → **Build RJTOOL IPA** → wait ~5 min  
3. Download `RJTOOL-1.0.59-ipa` artifact  
4. Install via **AltStore**, **Sideloadly**, or **TrollStore**

---

## GitHub Actions — signed IPA (ad-hoc / TestFlight)

Add these repository secrets (`Settings → Secrets → Actions`):

| Secret | Value |
|--------|-------|
| `BUILD_CERTIFICATE_BASE64` | `base64 -i Certificates.p12` |
| `P12_PASSWORD` | p12 export password |
| `BUILD_PROVISION_PROFILE_BASE64` | `base64 -i profile.mobileprovision` |
| `KEYCHAIN_PASSWORD` | any string |
| `DEVELOPMENT_TEAM` | 10-char Apple Team ID |

Re-run the workflow — it auto-detects the secrets and produces a signed IPA.

### Export your p12

```bash
# In Keychain Access:
# 1. Find your "Apple Development: ..." cert
# 2. Right-click → Export
# 3. Save as Certificates.p12
base64 -i Certificates.p12 | pbcopy   # paste into secret
```

### Export your provisioning profile

```bash
# Download .mobileprovision from developer.apple.com
base64 -i profile.mobileprovision | pbcopy   # paste into secret
```

---

## Install unsigned IPA

### AltStore (free, requires PC/Mac once)
1. Install AltStore on your iPhone  
2. Open AltStore → `+` → pick `RJTOOL-unsigned.ipa`

### Sideloadly (free, requires PC/Mac)
1. [sideloadly.io](https://sideloadly.io) → drag IPA → install

### TrollStore (jailbreak-free, A12–A17 iOS 14–17)
1. Open TrollStore → `+` → pick IPA  
2. No resigning needed — permanent install

---

## Notes

- Minimum iOS: **16.0**  
- Supports iPhone + iPad  
- Dark mode only (matches original RJTOOL aesthetic)  
- Bundle ID kept as `cn.rjtool.mobile` to match original  
- Tap any path row to copy it to clipboard  
- Swipe left on a row → **Copy** button
