# BPG Viewer for Seer

[![Version](https://img.shields.io/badge/version-1.1.1-blue)]() [![Seer](https://img.shields.io/badge/Seer-%E2%89%A54.1.3-green)]()

按空格即可预览 `.bpg` 图片的 [Seer](https://www.1218.io/) 插件（Convert 型）。

> 作者：wunshare (739514761@qq.com)

## 特性

- 解码：libbpg 0.9.8（PGO 优化构建，比官方解码快 25~30%）
- 编码：libjpeg-turbo (SIMD) → JPG q90（视觉无损：vs 无损解码 PSNR 45.25 dB / SSIM 1.0000）
- 支持：4:2:0 / 4:2:2 / 4:4:4 / CMYK、8-12bit（降 8bit 输出）、alpha 透明度
- 动画 BPG 取第一帧
- 转换结果由 Seer 缓存，同一文件仅转换一次

## 安装

1. 下载 [`bpg-viewer-1.1.1.zip`](./bpg-viewer-1.1.1.zip)
2. Seer 设置 → Viewers → Local 标签 → 点 "＋" 选择该 zip
3. 资源管理器中选中任意 `.bpg`，按空格预览

## 性能（9950X 实测，含解码端到端）

| 图片 | PNG 时代 (v1.0) | 当前 JPG (v1.1.x) |
|---|---|---|
| 8MP | 389 ms | **158 ms** |
| 4K | 727 ms | **340 ms** |
| 8K | 2951 ms | **1337 ms** |

## 说明

- Windows x64 二进制分发，静态链接，仅依赖包内 zlib1.dll
- 遵循 libbpg / libjpeg-turbo / zlib 各自的开源许可
