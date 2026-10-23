# Release verification: 0.1.0

Reviewed on 2026-10-19. The supplied APK is published unchanged. This record describes artifact inspection, not an on-device compatibility or production security certification.

## APK identity

| Item | Verified value |
| --- | --- |
| Asset | `Rosper-Tap-to-Pay-0.1.0-release.apk` |
| File size | 49,670,711 bytes |
| Package | `com.rosper.taptopay` |
| Display name | Rosper Pay |
| Version name / code | 0.1.0 / 1 |
| Minimum / target API | 26 / 35 |
| Build type | release |
| Debuggable | false |
| APK signature verification | Passed; APK Signature Scheme v2 |
| Certificate subject | `C=US, O=Android, CN=Android Debug` |

APK SHA-256:

```text
f48341127347da10e925502971343be2c676c4181e3df4df37c1e246d5fe7fc2
```

Signing certificate SHA-256:

```text
209bf83ca3a92afcad64b1ac5d5afcddbb560356ac550c454a247b6a4d99fed3
```

The Android Debug certificate is an evaluation signing identity. It is distinct from the `debuggable` flag; this APK is not debuggable. A different signing key will prevent an in-place update of this installation.

## Configuration and publication checks

- The APK's `BuildConfig` was inspected: default backend URL, device API key, Location, merchant name and currency strings are empty. Runtime currency falls back to USD; Demo mode defaults to OFF on a fresh install.
- Targeted APK scans found no Stripe secret-key or GitHub-token patterns. Private-key matches were header-only parsing strings, not embedded PEM keys. This limited scan does not establish the absence of every possible secret or vulnerability.
- The supplied source was reviewed locally for configuration and eligibility behavior. Secret-scan findings were test fixtures and examples. Source code and internal records are not published in this repository or attached to the release.
- The public distribution files passed a secret scan. Only documentation, branding and the checksum are versioned here; the APK is a Release asset.

## Runtime verification status

| Check | Status for this publication |
| --- | --- |
| SUNMI installation / startup | Not independently performed |
| Local checks on a SUNMI device | Not independently performed |
| Stripe simulated payment | Not independently performed |
| Non-simulated reader connection | Not independently performed |
| Physical card collection / confirmation / capture | Not independently performed |
| Refund / reconciliation against Stripe | Not independently performed |

The original package's build/test report is not a substitute for testing the released APK on the intended hardware. No supported-device list is inferred from unit tests or source comments.

## Interpretation limits

The APK's merged manifest lacks explicit package-visibility declarations for Google Play Store/Services. Depending on system visibility, its local package check can report a false negative; see [Android's package-visibility documentation](https://developer.android.com/training/package-visibility/declaring). The device-class check uses a model-name pattern, while integrity checks use limited local signals. These are preliminary indicators only.

Use the [testing guide](TESTING.md) to record separate local, simulated and real-reader outcomes, and consult [Stripe's current device requirements](https://docs.stripe.com/terminal/payments/setup-reader/tap-to-pay?platform=android#supported-devices).
