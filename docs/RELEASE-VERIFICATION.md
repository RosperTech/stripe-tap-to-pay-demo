# Release verification: position settings preview

Inspected and tested on 2026-10-23. This record covers the supplied APK and the checks below; it is not a device compatibility certification. [Original v0.1.0 record](RELEASE-VERIFICATION-v0.1.0.md).

## APK identity

| Item | Verified value |
| --- | --- |
| Release tag | `v0.1.0-position-settings.20261021` |
| Asset | `Rosper-Pay-5.8.1-position-settings.apk` |
| Size | 49,687,095 bytes |
| Package / display name | `com.rosper.taptopay` / Rosper Pay |
| App version / code | 0.1.0 / 1 |
| Stripe Terminal SDK | 5.8.1 |
| Minimum / target API | 26 / 35 |
| Build / debuggable | release / false |
| Signature verification | Passed, APK Signature Scheme v2 |
| Signing identity | Android Debug certificate |

The APK supplied separately and the APK inside the update archive are byte-identical. The installed APK on Samsung SM-T733 also matched the checksum. No rebuild or binary modification was performed.

APK SHA-256:

```text
fe878cd93fedb376b08149d865c8c414caba80f43cfabddfaa63133a83aa181d
```

Signing certificate SHA-256:

```text
9fc6402f658e474f2eb95acf0f46ad13a0c9d8094496607b088926893827d811
```

This certificate differs from the original v0.1.0 certificate (`209bf83ca3a92afcad64b1ac5d5afcddbb560356ac550c454a247b6a4d99fed3`). An in-place upgrade from that APK is not supported. Uninstalling removes local data and settings; resolve pending transactions and preserve required records first.

The dated release tag identifies the distribution revision. The app's internal version is still 0.1.0 / code 1; `5.8.1` in the filename identifies the Stripe Terminal SDK.

## Configuration

- Backend, device credential and Terminal Location defaults are present. A fresh installation displayed these values without manual entry. Credential values and private endpoint addresses are omitted from this record.
- Demo mode defaults to OFF. It selects the reader type and does not establish the backend's Stripe test/live mode.
- A read-only Location request succeeded and included the configured Location. No payment, capture or refund request was sent during verification. The read-only response did not establish Stripe test/live mode.
- On 2026-10-23, the maintainer confirmed that the configured service is for testing only. This is a maintainer statement, separate from the read-only verification above.
- The current Settings screen does not expose editable backend, device credential or Location fields. Merchant display name, currency, Demo mode, appearance and tap-position controls remain available.
- Application and backend source were inspected locally and are excluded from the public distribution repository and release assets.

## Samsung SM-T733 test

| Check | Observed result |
| --- | --- |
| System | Android 14 / API 34; security patch 2025-06-01 |
| Fresh install / launch | Passed |
| Preset payment configuration | Displayed; no manual configuration entered |
| Location permission | Granted while the app is in use |
| Local eligibility | Blocked: no NFC, hardware keystore version 4 below app threshold 100, old security patch, Developer options enabled |
| Other local checks | Android, ARM, GMS, local integrity, device class and internet passed |
| Custom position | Horizontal 30%, vertical 70% saved and retained after cold restart |
| Reset position | Restored device default, saved and retained after another cold restart |
| Final position mode | SDK default, no custom coordinates |
| Reader connection | Not tested; eligibility gate blocked |
| Simulated or physical card payment | Not tested |
| Capture / refund / reconciliation | Not tested |

SUNMI CPAD installation, hardware checks, real-reader connection and payments have not been independently tested for this APK. Observations on the Samsung tablet do not establish SUNMI compatibility. Position settings were verified in settings and diagnostics; their appearance during a live payment prompt was not verified.

## Interpretation limits

The APK retains local model-name and integrity heuristics and lacks explicit package queries for Google Play Store/Services. A local pass or failure does not replace Stripe's device checks. See the [testing guide](TESTING.md) for separate eligibility, simulated-flow and real-reader test stages.

## 中文摘要

已验证 APK 一致性和签名、三星 SM-T733 全新安装启动、预置配置、自定义位置保存及冷启动保留、恢复默认。三星平板没有 NFC，且其他部分本地条件未通过，因此未测试读卡器连接、模拟支付、实体卡支付、扣款确认或退款。CPAD 尚未完成独立实机验证。

本版签名与旧包不同，不能覆盖升级；卸载旧版会删除本地数据。App 内部版本仍为 0.1.0，文件名中的 5.8.1 指 Stripe Terminal SDK 版本。
