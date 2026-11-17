# TaNi Audio Leveler — FFmpeg LGPLv3 Compliance & Replacement Guide

**Application:** TaNi Audio Leveler (Windows 10/11 Desktop)  
**Publisher:** TaNi Digital Labs  
**Repository:** `https://github.com/anhtu2163-dev/tani-audio-leveler-lgpl-source`  
**Release Tag:** `ffmpeg-lgpl-9.0-d838f9f9ae`

---

## 1. Binary Identification, Provenance & PE Import Dependencies

| Field | Verified Value |
| :--- | :--- |
| **Upstream Build System** | `FFmpeg-Builds/FFmpeg-Builds` (formerly `BtbN/FFmpeg-Builds`) |
| **GitHub Actions Build Run** | Run ID `43712307594` (`2026-11-15T12:59:41Z`) |
| **Exact Build Scripts Commit** | `c9fe5114060e507409f7ee07edfd82efaf25d767` |
| **Release Asset Name** | `ffmpeg-n9.0-latest-win64-lgpl-shared-9.0.zip` |
| **Release Archive SHA-256** | `67e32c16f8c5632bdb03ec3cc296b63743e3ff69194c773274632a3378fccccb` |
| **FFmpeg Version & Commit** | `n9.0.2-57-gd838f9f9ae-20261115` (Branch `release/9.0`, Commit `d838f9f9ae`) |
| **Compiler Toolchain** | `gcc 16.2.0 (crosstool-NG 1.29.0.36_fbb6372)` (`x86_64-w64-mingw32`) |
| **Governing License** | GNU Lesser General Public License Version 3 (`LGPLv3`, `--enable-version3`; no `--enable-gpl`, no `--enable-nonfree`) |

### Distributed Runtime Files (8 Files)

| File Name | Size (KB) | SHA-256 Digest | PE Import Dependencies (Non-OS) |
| :--- | :---: | :--- | :--- |
| `ffmpeg.exe` | `538.5` | `41e9de1dbca838a9c41b4af5fcef7f60edec1e4d9d8ddd3c8eb01aa623c72ff5` | `avcodec-63.dll`, `avdevice-63.dll`, `avfilter-12.dll`, `avformat-63.dll`, `avutil-61.dll`, `swresample-7.dll`, `swscale-10.dll` |
| `avcodec-63.dll` | `89,527.0` | `b1b96733b56bb6435ed8b344cb5301d1a944439718b7feea6eb0f72003f668be` | `avutil-61.dll`, `swresample-7.dll` |
| `avfilter-12.dll` | `31,129.0` | `9708d120fcff749953f8cb668cfd5b02c718f7ca058e033cb6bac201500ae2f1` | `avcodec-63.dll`, `avformat-63.dll`, `avutil-61.dll`, `swresample-7.dll`, `swscale-10.dll` |
| `avformat-63.dll` | `19,422.0` | `5d17e25d12c3d1c397d13920ee5695bae1bbd6123f1fe2fd7fed87e154138256` | `avcodec-63.dll`, `avutil-61.dll` |
| `avdevice-63.dll` | `4,891.0` | `1ec7d2d4a1edeb11d49e5f5867690dd6852b4ae813fa5a0f5ef29dcf105433cb` | `avcodec-63.dll`, `avfilter-12.dll`, `avformat-63.dll`, `avutil-61.dll` |
| `avutil-61.dll` | `2,954.5` | `35f633502141df491ce18a8386209e03208bcb7f494c3b9a23956f3bb744afd3` | *(Windows OS DLLs only)* |
| `swscale-10.dll` | `2,289.0` | `ed85b16e49d51a946d3b5cd67bbaf7b7ff9f2516f319c41aced93f38a7b5d735` | `avutil-61.dll` |
| `swresample-7.dll` | `729.5` | `00f21199f02a5a2c4137d51286833c4fb4082529301761804a24c073f8526d5b` | `avutil-61.dll` |

*(Note: `ffplay.exe` and `ffprobe.exe` are not used or distributed by TaNi Audio Leveler.)*

---

## 2. How to Replace or Use a Custom FFmpeg Build

1. **In-App Setting (Recommended):**
   - Open **TaNi Audio Leveler** $\rightarrow$ **Settings** $\rightarrow$ **Custom FFmpeg Executable Path** $\rightarrow$ browse to your custom `ffmpeg.exe`.
2. **Direct Shared Library Replacement:**
   - Replace the 7 shared DLLs (`avcodec-63.dll`, `avdevice-63.dll`, `avfilter-12.dll`, `avformat-63.dll`, `avutil-61.dll`, `swresample-7.dll`, `swscale-10.dll`) and/or `ffmpeg.exe` with ABI-compatible builds compiled from the Corresponding Source archives in Release `ffmpeg-lgpl-9.0-d838f9f9ae`.

---

## 3. Corresponding Source & Reproducibility

All **24 Corresponding Source `.zip` archives (`139.83 MB` total)** and their SHA-256 digests are cataloged in [CORRESPONDING_SOURCE_MANIFEST.json](CORRESPONDING_SOURCE_MANIFEST.json) and [RELEASE_ASSETS_PLAN.md](RELEASE_ASSETS_PLAN.md). Build instructions and submodule/Cargo dependency details are documented in [BUILD_AND_REPRODUCIBILITY.md](BUILD_AND_REPRODUCIBILITY.md).
