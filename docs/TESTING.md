# Device evaluation guide / 设备验证指南

Use an operator-controlled Stripe **test-mode** backend for this preview. The position-settings APK includes backend, device credential and Location presets; the maintainer confirms that this preset backend is for Stripe testing only. Never put a Stripe secret key in the app. Demo mode does not select the backend's Stripe test/live mode.

本预览版使用测试负责人管理的 Stripe **测试模式**后端。拍卡位置设置版已预置服务器、设备凭据和门店；维护方确认该预置后台仅用于 Stripe 测试。不要把 Stripe secret key 放入 App。Demo mode 不会切换后台的测试/正式环境。

The signing certificate differs from the original `v0.1.0`. Prefer a fresh test device. Resolve pending transactions and preserve required records before uninstalling an old version; uninstalling deletes local data.

本版与原 `v0.1.0` 签名不同。优先使用新测试设备；卸载旧版前先处理未完成交易并保存所需记录，卸载会删除本地数据。

## 1. Identify the exact device / 确认设备版本

Record the manufacturer, marketing model, Android model identifier, SKU/region, GMS variant, firmware build, Android version, security patch date, release tag, app version and test date. The new APK still reports app version 0.1.0; its release tag and SHA-256 identify this build. Keep unique serial numbers out of public reports.

记录厂商、商品型号、系统型号、SKU/地区、GMS 版本、固件版本、Android 版本、安全补丁日期、App 版本和测试日期。公开报告不要包含设备唯一序列号。

Consult [Stripe's current requirements](https://docs.stripe.com/terminal/payments/setup-reader/tap-to-pay?platform=android#supported-devices) and the [reader connection guide](https://docs.stripe.com/terminal/payments/connect-reader?reader-type=tap-to-pay&terminal-sdk-platform=android). Exact firmware and configuration matter even when a model family is listed. The device must meet Stripe's current conditions; local app checks cover only part of them.

核对 Stripe 官方要求和连接指南。即使商品系列出现在官方列表中，也要验证实际固件与配置。本地检查仅覆盖部分条件。

## 2. Run the local checks / 本地条件检查

- Install the release APK, enable NFC and network access, and disable Developer options.
- Open Rosper Pay, then **Diagnostics**. If blocked, address the listed items and use **Check again**.
- Record each failure or the fact that the amount screen is reachable.
- Do not treat either result as definitive certification: the GMS visibility and model heuristics described in the README can affect the result. Do not reflash a device solely because of a local message; confirm the supported firmware with the device supplier.

安装 APK，开启 NFC 和网络，关闭开发者选项。查看 Diagnostics 中的条件检查，处理失败项后点击 Check again。记录失败原因或已进入金额页。GMS 可见性和型号规则可能影响结果；不要仅凭本地提示给设备刷机，应先向设备供应方确认适配固件。

## 3. Demonstrate the simulated flow / 模拟演示

1. Once the local gate passes, open **⋮ → Settings**.
2. Confirm USD/CAD and the display name. The backend, device credential and Location are preset and cannot be edited in this Settings screen; contact the evaluation operator if they need changing.
3. Turn **Use a simulated card reader** ON **before Save**. It is OFF by default on a fresh install.
4. Grant requested permissions. Confirm **SIMULATED** on screen and **Card reader: SIMULATED — payments are not real** in Diagnostics.
5. Run the agreed sample amount through the simulated payment flow. Verify the transaction in Stripe's test environment; record capture/refund results separately if tested.

通过本地检查后进入设置，确认显示名称和币种。本版设置页不能编辑预置服务器、凭据或门店，需要更换时联系测试负责人。先打开模拟读卡器开关再保存。授予所需权限，确认页面和 Diagnostics 均显示模拟状态，然后演示测试金额。支付、确认、退款等结果分别记录，并在 Stripe 测试环境核对。

**This stage tests the integration flow; no physical card-read result is established.** The app's eligibility gate still applies. For current simulated-reader behavior, see [Stripe's testing guide](https://docs.stripe.com/terminal/references/testing?terminal-sdk-platform=android).

此阶段验证模拟流程，不能证明实体卡或设备 NFC 读取成功。模拟模式仍受设备条件检查限制。

## 4. Check the non-simulated reader / 验证真实读卡器连接

1. Keep the backend in **Stripe test mode**. Confirm the selected Location belongs to that test setup.
2. Turn **Use a simulated card reader** OFF and save. Enable the device's Location service, grant the app's requested location permission and keep Developer options OFF.
3. Return to the amount screen. The app attempts to connect automatically after configuration; a separate payment is not required just to observe connection status.
4. Open **Diagnostics**. Record **Real reader**, **Not connected**, or the exact failure. If **Card reader isn't ready** appears, record its **Details**, including the Stripe error code.
5. A real reader connection is evidence for this particular configuration at this time. If a card-payment exercise is required, follow Stripe's current testing procedure with appropriate test media; record card collection, confirmation, capture and refund outcomes separately. Do not label a connection-only result as a successful payment test.

保持后端为 Stripe 测试模式，关闭模拟读卡器并保存。开启系统定位、授予应用定位权限、关闭开发者选项。返回金额页后会自动尝试连接；只观察连接状态不需要发起付款。到 Diagnostics 记录 Real reader / Not connected 或错误详情。连接通过只证明当前设备与配置在当时通过了这一步；实体卡测试、支付确认、扣款确认和退款需要另行验证。

## 5. Share a reproducible result / 提交可复查结果

Use the repository's device evaluation issue form. Include exact errors and the test stage. Review exported logs before sharing; remove credentials, customer/payment data, device serials and private endpoints. Send sensitive diagnostics privately to the evaluation operator instead of a public issue.

通过仓库的设备反馈表提交准确错误码与测试阶段。公开日志前去除凭据、客户/支付信息、序列号和内部服务地址；敏感诊断信息请交给测试负责人私下处理。
