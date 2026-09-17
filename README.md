# MangoPi M28C 定制 OpenWrt 固件

本仓库是 [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede) 的 Fork，为 **Widora MangoPi M28C** 开发板定制编译的 OpenWrt 固件。

## 硬件平台

| 项目 | 参数 |
| --- | --- |
| SoC | Rockchip RK3528（四核 Cortex-A53） |
| 目标架构 | rockchip / armv8 |
| 内核 | 6.12.80 |
| 网络 | 有线网口 + WiFi（AIC8800 SDIO） |
| 其他 | 5G 模组支持 |

## 相对上游的改动

1. **`feeds.conf.default`** 新增三个软件源：
   - `passwall_packages`、`passwall_luci` —— PassWall 科学上网插件
   - `qmodem` —— 新版QModem拨号管理
2. **`configs/mangopi_m28c.config`** —— M28C 的完整编译配置（种子文件，用于复现本固件）

## 下载固件

编译好的固件在 [Releases](../../releases) 页面，包含：

| 文件 | 说明 |
| --- | --- |
| `*-squashfs-sysupgrade.img.gz` | squashfs 根文件系统（**推荐**） |
| `*-ext4-sysupgrade.img.gz` | ext4 根文件系统 |
| `sha256sums` | 固件校验和 |
| `*.manifest` | 已安装软件包清单 |


## 自行编译

```bash
git clone https://github.com/sassalana/lede.git
cd lede
./scripts/feeds update -a
./scripts/feeds install -a
cp configs/mangopi_m28c.config .config
make defconfig
make -j$(nproc) download
make -j$(nproc)
```

编译产物在 `bin/targets/rockchip/armv8/`。

---

上游 lede 的原始说明见 [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)。
