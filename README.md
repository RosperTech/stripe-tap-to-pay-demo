<img src="assets/rosper.png" alt="Rosper" width="96">

# Rosper Tap to Pay

Evaluate a SUNMI device's readiness for Stripe Tap to Pay on Android and demonstrate the payment flow with Stripe's simulated reader.

**0.1.0 is an evaluation preview. No SUNMI device has been independently validated for this release.** A successful local check or simulated payment is not a compatibility certification.

[Download APK](https://github.com/RosperTech/stripe-tap-to-pay-demo/releases/download/v0.1.0/Rosper-Tap-to-Pay-0.1.0-release.apk) · [Release notes](https://github.com/RosperTech/stripe-tap-to-pay-demo/releases/tag/v0.1.0) · [中文说明](README.zh-CN.md) · [Testing guide](docs/TESTING.md)

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

**The APK contains no backend address, device API key or Terminal Location. There is no public demo backend included in this release.** Installation alone provides the local checks; payment demonstrations require an operator-provided test backend compatible with this app.

After the local checks pass, open **⋮ → Settings**:

- Enter the **Rosper server address** and **Your payment key** supplied by the evaluation operator. The payment key is a device credential for the backend, **not a Stripe secret key**.
- Select **Find your store**, then choose the test Terminal Location. Choose the business name and currency (USD or CAD).
- For a simulated demonstration, turn **Use a simulated card reader** ON before saving. **This switch defaults to OFF on a fresh install.**
- Use a backend connected only to Stripe test mode. Confirm the app shows **SIMULATED** and Diagnostics identifies the reader as simulated before demonstrating a payment.

Stripe secret keys belong on the backend, never in the APK, app settings or public issues. Demo mode selects the reader type; it does not configure the backend's Stripe account mode. The app is capable of real payments when configured accordingly; this release is intended for evaluation, not customer checkout.

## Preview limitations

- The release uses an **Android Debug signing certificate**, while the application itself is **not debuggable**. A future release signed with a different key may require uninstalling this preview, which removes its local data.
- The bundled Stripe Terminal SDK is **5.8.1**. This release is not a claim that all current or future Stripe requirements are covered.
- The local Google Play check can be affected by Android package visibility: the APK does not explicitly declare Google Play Store/Services in its package queries. A reported GMS failure needs confirmation against the actual firmware and installed services.
- Device-class and integrity checks use local heuristics. In particular, a model beginning with `P` followed by a digit is treated as a PCI payment terminal; this is not an authoritative certification lookup. Root/bootloader checks are also incomplete. Stripe's device attestation remains necessary.
- The eligibility gate also runs before simulated demonstrations. Demo mode does not bypass unsupported hardware or firmware.
- No production-readiness, payment-network certification or support for every SUNMI model is implied. See the [verification record](docs/RELEASE-VERIFICATION.md) for the scope of the release checks.

## Report a result

Use [New issue → Device evaluation report](https://github.com/RosperTech/stripe-tap-to-pay-demo/issues/new/choose). Include the hardware and firmware details, test date, Demo mode state, local results and exact Stripe error code. Remove credentials, customer data and unique device identifiers from attachments. Reports are observations for a specific configuration, not certification.

[Rosper website](https://www.rospertech.com) · [Rosper GitHub organization](https://github.com/RosperTech) · Contact: sales@rospertech.com

This repository distributes the evaluation APK and documentation. Application/backend source code and internal development documents are not included. Stripe and SUNMI are trademarks of their respective owners; this is a Rosper evaluation project.
