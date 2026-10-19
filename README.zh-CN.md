# Rosper Tap to Pay

用于初步检查商米设备的 Stripe Tap to Pay 条件，并通过 Stripe 模拟读卡器演示支付流程。

**0.1.0 为测试预览版。本次发布尚未完成任何商米设备的独立实机验证。** 本地检查通过或模拟支付成功，都不能作为设备兼容认证。

[下载 APK](https://github.com/RosperTech/stripe-tap-to-pay-demo/releases/download/v0.1.0/Rosper-Tap-to-Pay-0.1.0-release.apk) · [版本与附件](https://github.com/RosperTech/stripe-tap-to-pay-demo/releases/tag/v0.1.0) · [English](README.md) · [详细验证步骤](docs/TESTING.md)

## 如何理解结果

| 验证阶段 | 可以说明什么 | 需要什么 |
| --- | --- | --- |
| 本地条件检查 | App 检测到了所需的基础条件 | 安装 APK；联网也是检查项之一 |
| 模拟支付演示 | 测试配置下的模拟支付流程可以运行 | 满足条件的实机、测试后端、Demo mode 开启 |
| 真实读卡器连接 | Stripe 在测试当时接受这台具体设备及固件的非模拟连接 | 测试后端、Demo mode 关闭、设备权限 |

连接成功仍不等于刷卡、扣款确认、退款都已通过。后续每一项都要单独记录测试结果。

## 安装并检查

1. 在设备上打开“下载 APK”，安装 **Rosper Pay**。如进入 Releases 页面，请在 **Assets** 中下载 `.apk`；自动生成的 Source code 压缩包只包含本仓库的发布文档。
2. 按 Android 提示允许浏览器或文件管理器安装应用。
3. 开启 NFC 和网络，关闭开发者选项。
4. 打开 App。如果出现 **This device can't take Tap to Pay payments**，查看未通过项，并打开 **Diagnostics**。进入金额页只代表本地检查通过。
5. 记录准确型号、SKU、GMS 版本、固件、Android 版本和安全补丁日期，再按[验证指南](docs/TESTING.md)进行后续测试。

APK 最低可安装系统为 Android 8.0；Tap to Pay 的本地检查要求 **Android 13 或以上**。请同时核对 [Stripe 当前设备要求](https://docs.stripe.com/terminal/payments/setup-reader/tap-to-pay?platform=android#supported-devices)。同一型号不同地区、GMS 和固件版本的结果可能不同。

## 配置模拟演示

**APK 未预置服务器地址、设备 API key 或 Terminal Location；此次发布也未提供公共演示后端。** 安装后可做本地检查，完整支付演示需要由测试负责人提供与此 App 匹配的测试后端。

本地检查通过后，进入 **⋮ → Settings**：

1. 填写 **Rosper server address**（测试服务器地址）和 **Your payment key**（测试负责人提供的设备访问凭据）。这里不是填写 Stripe secret key。
2. 点击 **Find your store**，选择测试 Terminal Location，并设置商户名称和币种（USD/CAD）。
3. 演示时先开启 **Use a simulated card reader**，再保存。**首次安装时这个开关默认关闭。**
4. 后端必须使用 Stripe 测试模式。开始演示前，确认界面显示 **SIMULATED**，Diagnostics 中的读卡器也是模拟状态。

Demo mode 只控制读卡器是否模拟，不会自动切换后端的 Stripe 测试/正式环境。Stripe secret key 只能保存在服务器端，不能放入 App 或公开 issue。此 App 在相应配置下具备真实收款能力；本预览版用于评估，不用于客户正式收银。

## 已知限制

- APK 使用 **Android Debug 测试签名证书**，但应用本身为不可调试的 release 构建。将来改用正式签名时，可能需要卸载预览版；卸载会删除本地数据。
- 内置 Stripe Terminal SDK **5.8.1**，不表示已覆盖当前及未来所有要求。
- APK 没有显式声明 Google Play Store/Services 的包查询可见性，部分固件上的 GMS 本地检查可能误报。遇到失败，应先确认实际固件与服务状态，不能仅凭这一行判断硬件不支持。
- PCI 设备类别检查按型号前缀判断，Root/完整性检查也只是本地规则，不是权威认证。最终仍要以 Stripe 实机连接和设备校验结果为依据。
- 模拟演示也需要先通过设备条件检查，不能用 Demo mode 绕过不符合条件的设备。

## 反馈测试结果

通过 [New issue → Device evaluation report](https://github.com/RosperTech/stripe-tap-to-pay-demo/issues/new/choose) 提交型号、固件、测试日期、Demo mode 状态、检查结果和 Stripe 错误码。附件应去除密钥、客户信息和唯一设备标识。

[Rosper 官网](https://www.rospertech.com) · [GitHub 组织](https://github.com/RosperTech) · 联系邮箱：sales@rospertech.com

此仓库发布 APK 和使用文档；应用源码、后端源码和内部开发记录未公开。检查范围见[发布验证记录](docs/RELEASE-VERIFICATION.md)。
