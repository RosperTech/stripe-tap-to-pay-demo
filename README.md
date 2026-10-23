<img src="assets/rosper.png" alt="Rosper" width="96">

# Rosper Tap to Pay

Evaluate a SUNMI device's readiness for Stripe Tap to Pay on Android and demonstrate the payment flow with Stripe's simulated reader.

**Position settings preview — 2026-10-21.** Fresh installation, preset configuration and position-setting persistence were verified on Samsung SM-T733. No SUNMI device has been independently validated for this release. A successful local check or simulated payment is not a compatibility certification.

[Download APK](https://github.com/RosperTech/stripe-tap-to-pay-demo/releases/download/v0.1.0-position-settings.20261021/Rosper-Pay-5.8.1-position-settings.apk) · [Release notes](https://github.com/RosperTech/stripe-tap-to-pay-demo/releases/tag/v0.1.0-position-settings.20261021) · [中文说明](README.zh-CN.md) · [Testing guide](docs/TESTING.md)

The APK includes backend, device credential and Terminal Location presets. Fresh installs do not require manual entry of these values. Device eligibility and reader connection are still required. The filename's `5.8.1` is the Stripe Terminal SDK version; the Android app version remains `0.1.0` / code `1`. Use the dated release tag and checksum to identify this build.

**Upgrading from the original v0.1.0:** the signing certificate has changed, so this APK cannot be installed over that version. Prefer a fresh test device. Before uninstalling an old installation, resolve pending transactions and preserve required records; uninstalling deletes local data and settings.

## What can I check?

| Stage | What the result establishes | Setup needed |
| --- | --- | --- |
| Local eligibility checks | Whether the app detects its required device conditions | Install the APK; internet is one of the checks |
| Simulated payment demo | Whether the configured test integration completes a simulated payment flow | Compatible physical device, test backend and Demo mode ON |
| Real reader connection | Whether Stripe accepts this particular device and firmware for a non-simulated reader connection at the time of testing | Test backend, Demo mode OFF and on-device permissions |

The app also includes transaction history, reconciliation, refunds, diagnostics and SUNMI peripheral integration. These features need separate testing on the intended device. A connected reader alone does not prove that a card payment, capture or refund succeeds.

## Install and check a device

1. Open the **Download APK** link on the device. On the Releases page, choose the `.apk` under **Assets**; the source archives contain this distribution site's documentation.
2. Allow installation from the browser or file manager when Android asks, then install **Rosper Pay**.
3. Enable NFC and internet access. Turn off Developer options before the eligibility check.
4. Launch the app. If it shows **This device can't take Tap to Pay payments**, read the failed items and open **Diagnostics**. If it reaches the amount screen, the local checks passed.
5. Record the exact model/SKU, GMS variant, firmware, Android version and security patch date. Follow the [testing guide](docs/TESTING.md) before describing the device as validated.

The APK installs on Android 8.0 or later; the app's Tap to Pay checks require **Android 13 or later**. See [Stripe's current requirements](https://docs.stripe.com/terminal/payments/setup-reader/tap-to-pay?platform=android#supported-devices). Models, firmware variants and SDK requirements matter; a product family name by itself is insufficient.

## Configure a demonstration

**The APK supplies preset backend, device credential and Terminal Location values.** Check the selected configuration with the evaluation operator before a payment demonstration. Preset values do not establish that a device supports Tap to Pay or that a payment will succeed.

After the local checks pass, open **⋮ → Settings**:

- Keep the supplied server and Location presets unless the evaluation operator provides a different test setup. The payment key is a device credential for the backend, **not a Stripe secret key**.
- To change test setups, enter the operator's server and device credential, select **Find your store** and choose the matching test Terminal Location. Confirm the display name and currency (USD or CAD).
- For a simulated demonstration, turn **Use a simulated card reader** ON before saving. **This switch defaults to OFF on a fresh install.**
- Use a backend connected only to Stripe test mode. Confirm the app shows **SIMULATED** and Diagnostics identifies the reader as simulated before demonstrating a payment.

Stripe secret keys belong on the backend, never in the APK, app settings or public issues. Demo mode selects the reader type; it does not configure the backend's Stripe account mode. The app is capable of real payments when configured accordingly; this release is intended for evaluation, not customer checkout.

## Adjust the tap prompt position

In **Settings**, use the device default or select a custom position, adjust the horizontal/vertical controls and save. Reset restores the device default. The custom 30% / 70% position and reset were verified across cold restarts on Samsung SM-T733. The effect on a live payment prompt has not been tested.

## Preview limitations

- The release uses an **Android Debug signing certificate**, while the application itself is **not debuggable**. Its certificate differs from the original v0.1.0 download; see the upgrade notice above.
- The bundled Stripe Terminal SDK is **5.8.1**. This release is not a claim that all current or future Stripe requirements are covered.
- The local Google Play check can be affected by Android package visibility: the APK does not explicitly declare Google Play Store/Services in its package queries. A reported GMS failure needs confirmation against the actual firmware and installed services.
- Device-class and integrity checks use local heuristics. In particular, a model beginning with `P` followed by a digit is treated as a PCI payment terminal; this is not an authoritative certification lookup. Root/bootloader checks are also incomplete. Stripe's device attestation remains necessary.
- The eligibility gate also runs before simulated demonstrations. Demo mode does not bypass unsupported hardware or firmware.
- No production-readiness, payment-network certification or support for every SUNMI model is implied. See the [verification record](docs/RELEASE-VERIFICATION.md) for the scope of the release checks.
- Samsung SM-T733 installed and launched this build, but has no NFC and failed other local checks. No simulated payment, real reader connection, physical card payment, capture or refund was tested. SUNMI CPAD remains untested.

## Report a result

Use [New issue → Device evaluation report](https://github.com/RosperTech/stripe-tap-to-pay-demo/issues/new/choose). Include the hardware and firmware details, test date, Demo mode state, local results and exact Stripe error code. Remove credentials, customer data and unique device identifiers from attachments. Reports are observations for a specific configuration, not certification.

[Rosper website](https://www.rospertech.com) · [Rosper GitHub organization](https://github.com/RosperTech) · Contact: sales@rospertech.com

This repository distributes the evaluation APK and documentation. Application/backend source code and internal development documents are not included. Stripe and SUNMI are trademarks of their respective owners; this is a Rosper evaluation project.
