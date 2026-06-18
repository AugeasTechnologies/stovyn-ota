# Stovyn — app OTA update channel

Public distribution channel for the **Stovyn** Android app (signed release APK +
update manifest). The application **source is private**; this repo holds only the
signed, shipping artifacts so installed apps can self-update over HTTPS.

- `latest.json` — the update manifest the app polls on launch.
- Releases — each `Stovyn-vX.Y.Z.apk` (signed with the Augeas/Stovyn release key).

The app reads `latest.json` and, if a newer `versionCode` is published (and the
device is in `targets`, or `targets` is omitted = all), downloads and installs it.

### `latest.json` schema
```json
{
  "versionCode": 13,
  "versionName": "1.0.13",
  "apkUrl": "https://github.com/AugeasTechnologies/stovyn-ota/releases/download/v1.0.13/Stovyn-v1.0.13.apk",
  "sha256": "<hex>",
  "mandatory": false,
  "notes": "What changed in this build.",
  "targets": ["<optional device-id allow-list for staged rollout>"]
}
```

Releases are published with `scripts/release-ota.sh` in the private app repo.

> The first OTA-enabled build must be installed once (it replaces any earlier
> debug build, which is signed with a different key). From then on the app
> self-updates.

© Stovyn · built by Augeas Technologies.
