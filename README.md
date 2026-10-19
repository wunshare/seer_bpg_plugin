# BPG Viewer for Seer

[![Version](https://img.shields.io/badge/version-1.1.2-blue)]() [![Seer](https://img.shields.io/badge/Seer-%E2%89%A54.1.3-green)]()

按空格即可预览 `.bpg` 图片的 [Seer](https://www.1218.io/) 插件（Convert 型）。

> 作者：wunshare (739514761@qq.com)

## 特性

- 解码：libbpg 0.9.8（WPP 波前多线程 + PGO 优化；输出与单线程解码逐字节一致）
- 编码：libjpeg-turbo (SIMD) → JPG q90（视觉无损：vs 无损解码 PSNR 45.25 dB / SSIM 1.0000）
- 支持：4:2:0 / 4:2:2 / 4:4:4 / CMYK、8-12bit（降 8bit 输出）、alpha 透明度
- 动画 BPG 取第一帧
- Unicode 路径可用（emoji 目录、罕见 CJK 文件名）
- 单文件分发，**不需要任何 DLL**
- 转换结果由 Seer 缓存，同一文件仅转换一次

## 安装

1. 下载 [`bpg-viewer-1.1.2.zip`](https://github.com/wunshare/seer_bpg_plugin/releases/download/v1.1.2/bpg-viewer-1.1.2.zip)（也可直接在本仓库下载）
2. Seer 设置 → Viewers → Local 标签 → 点 "＋" 选择该 zip
3. 资源管理器中选中任意 `.bpg`，按空格预览

## 性能（9950X 实测，含解码端到端）

| 图片 | v1.1.1（单线程解码） | **v1.1.2（WPP 多线程 + PGO）** | 提速 |
|---|---|---|---|
| 6MP / 2.3 MB | 226 ms | **66 ms** | 3.4× |
| 8.3MP / 0.1 MB（4K 截图） | 101 ms | **56 ms** | 1.8× |
| 90MP / 21 MB | 2452 ms | **605 ms** | 4.0× |
| 小图（clock.bpg） | 10.6 ms | **10.9 ms** | 1.0× |

v1.1.2 的 JPG 输出与 v1.1.1 **逐字节相同**（解码位精确），所以已经缓存的预览不会失效。

## 版本

- **v1.1.2**（2026-10-19）：解码换成 WPP 波前多线程（默认 1 job / 逻辑核，上限 32）+ 修复版 PGO。
  同时修掉 v1.1.1 的两个缺陷：进程无 UTF-8 清单（emoji / 罕见 CJK 路径预览直接失败）、
  动态依赖 `libwinpthread-1.dll`（旧 zip 并未附带）。旧版是单线程解码（没有 `-DUSE_WPP`）。
- v1.1.1（2026-10-01）：元数据（作者 / 描述 / 主页）。
- v1.1.0：PNG 输出改为 JPG（q90，libjpeg-turbo），转换提速 2.1~2.5 倍。
- v1.0.x：`bpg2png` + PNG 输出。

## 说明

- Windows x64 二进制分发，静态链接 libbpg / libjpeg-turbo / zlib，**仅依赖系统 UCRT**
- 遵循 libbpg / libjpeg-turbo / zlib 各自的开源许可
- 校验值：`bpgconv.exe` MD5 `3070E9B1CB259149C9395B901B3328DD`；`bpg-viewer-1.1.2.zip` MD5 `253D5E5E1A3569BB7935714ED035320F`
