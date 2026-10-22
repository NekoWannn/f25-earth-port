# f25-earth-port

把 earth（Redmi 12C / POCO C55，mt6768，HyperOS A14，4.19.191）的固件移植到
多亲 F25（MT8786/mt6768，640×960 ST7703 面板，Hynitron 66xx 触摸，实体键盘）。

做法：以 Xiaomi 公开的 `earth-s-oss` 4.19.191 内核树为基座，把 F25 的板级驱动补进去，
最终在 F25 上跑 earth 的整套内核 + vendor + system。

- 上游内核：`MiCode/Xiaomi_Kernel_OpenSource` 分支 `earth-s-oss`
- 本仓库只放补丁与 workflow，内核源码由 CI 现拉，不入库

## CI

`.github/workflows/kernel.yml`：

1. 取 AOSP clang `r416183b`（与 earth 内核 banner 中的 clang 12.0.5 对应）
2. 拉 `earth-s-oss` 源码
3. 应用 `patches/*.patch`
4. `earth_defconfig` + `Image.gz-dtb`
5. 上传 `Image.gz-dtb` / `.config`

## 状态

- [x] P1 基线可编译
- [ ] P2 在 F25 上 `fastboot boot` 跑起来
- [ ] P3 ST7703 显示
- [ ] P4 Hynitron 触摸 + 键盘
- [ ] P5 earth super 重建 + 开机进 UI
