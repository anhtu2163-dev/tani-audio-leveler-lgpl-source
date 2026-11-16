# Build & Reproducibility Guide (`win64-lgpl-shared-9.0`)

## 1. Binary Provenance & Runtime Inventory

| Field | Verified Value |
| :--- | :--- |
| **Upstream Build System** | `FFmpeg-Builds/FFmpeg-Builds` (formerly `BtbN/FFmpeg-Builds`) |
| **GitHub Actions Build Run** | Run ID `43712307594` (`2026-11-15T12:59:41Z`) |
| **Pinned `FFmpeg-Builds` Commit** | `c9fe5114060e507409f7ee07edfd82efaf25d767` |
| **Release Asset** | `ffmpeg-n9.0-latest-win64-lgpl-shared-9.0.zip` |
| **Release Archive SHA-256** | `67e32c16f8c5632bdb03ec3cc296b63743e3ff69194c773274632a3378fccccb` |
| **FFmpeg Version & Commit** | `n9.0.2-57-gd838f9f9ae-20261115` (`release/9.0`, Commit `d838f9f9ae`) |
| **Compiler Toolchain** | `gcc 16.2.0 (crosstool-NG 1.29.0.36_fbb6372)` (`x86_64-w64-mingw32`) |
| **Governing License** | `LGPLv3` (`--enable-version3`; no `--enable-gpl`, no `--enable-nonfree`) |

### Distributed Runtime Files (8 Files)
- `ffmpeg.exe` (`41e9de1dbca838a9c41b4af5fcef7f60edec1e4d9d8ddd3c8eb01aa623c72ff5`)
- `avcodec-63.dll` (`b1b96733b56bb6435ed8b344cb5301d1a944439718b7feea6eb0f72003f668be`)
- `avfilter-12.dll` (`9708d120fcff749953f8cb668cfd5b02c718f7ca058e033cb6bac201500ae2f1`)
- `avformat-63.dll` (`5d17e25d12c3d1c397d13920ee5695bae1bbd6123f1fe2fd7fed87e154138256`)
- `avdevice-63.dll` (`1ec7d2d4a1edeb11d49e5f5867690dd6852b4ae813fa5a0f5ef29dcf105433cb`)
- `avutil-61.dll` (`35f633502141df491ce18a8386209e03208bcb7f494c3b9a23956f3bb744afd3`)
- `swscale-10.dll` (`ed85b16e49d51a946d3b5cd67bbaf7b7ff9f2516f319c41aced93f38a7b5d735`)
- `swresample-7.dll` (`00f21199f02a5a2c4137d51286833c4fb4082529301761804a24c073f8526d5b`)

---

## 2. Submodule & Dependency Reproducibility Audit

### 2.1. `libplacebo` (`275f7dea27924cdd34ab2e6c20e448b6bc4fab65`) Submodules
In `scripts.d/50-libplacebo.sh`, `-Ddemos=false` disables `demos/3rdparty/nuklear`. The remaining 5 submodules under `3rdparty/` are permissive build/header dependencies pinned to exact commits:
- `3rdparty/glad`: `https://github.com/Dav1dde/glad.git` @ `73db193f853e2ee079bf3ca8a64aa2eaf6459043` (MIT)
- `3rdparty/fast_float`: `https://github.com/fastfloat/fast_float.git` @ `97b54ca9e75f5303507699d27c6b4f4efe4641a1` (Apache-2.0 / MIT)
- `3rdparty/jinja`: `https://github.com/pallets/jinja.git` @ `15206881c006c79667fe5154fe80c01c65410679` (BSD-3-Clause)
- `3rdparty/markupsafe`: `https://github.com/pallets/markupsafe.git` @ `297fc8e356e6836a62087949245d09a28e9f1b13` (BSD-3-Clause)
- `3rdparty/Vulkan-Headers`: `https://github.com/KhronosGroup/Vulkan-Headers.git` @ `74d8a6cb930c68ef617b202c3ff3c59d919e086b` (Apache-2.0; overridden by `-Dvulkan-registry` from `40-vulkan-headers.sh` `v1.4.366`)

### 2.2. `librsvg` (`0c074d0a25adefd65843067306f9bc1fb609f68f`) Rust Cargo Dependencies
- `librsvg-0c074d0a25adefd65843067306f9bc1fb609f68f.zip` includes the verbatim **`Cargo.lock` (`85,370 bytes`)**, pinning **361 total packages** (`352` external `crates.io` crates with SHA-256 checksums + `9` workspace crates).
- During `download.sh` (`99-librsvg.sh`), `cargo vendor --versioned-dirs > .cargo/config.toml` fetches and verifies all 352 crates against `Cargo.lock`, and the build runs offline with `CARGO_NET_OFFLINE=true`.

---

## 3. Step-by-Step Build Reproduction (Linux + Docker BuildKit)

```bash
# 1. Extract the pinned FFmpeg-Builds repository archive
unzip FFmpeg-Builds-c9fe5114060e507409f7ee07edfd82efaf25d767.zip
cd FFmpeg-Builds-c9fe5114060e507409f7ee07edfd82efaf25d767

# 2. Populate .cache/downloads (fetches pinned upstream sources, submodules, and cargo vendor)
./download.sh

# 3. Build the base cross-compiler images (gcc 16.2.0 / crosstool-NG 1.29.0.36_fbb6372)
./makeimage.sh win64 lgpl-shared 9.0

# 4. Compile FFmpeg commit d838f9f9ae
export FFMPEG_REPO="https://github.com/FFmpeg/FFmpeg.git"
export GIT_BRANCH="release/9.0"
./build.sh win64 lgpl-shared 9.0
```

Output is written to `artifacts/ffmpeg-n9.0.2-*-win64-lgpl-shared-9.0.zip`.

---

## 4. Mandatory Legal Requirements vs. Recommended Compliance Measures

| Category | Item | Classification |
| :--- | :--- | :--- |
| **License Texts** | Include `COPYING.LGPLv3`, `COPYING.GPLv3`, `COPYING.LGPLv2.1` | **Mandatory** (LGPLv3 §4(b)) |
| **Copyright & IJG Notices** | Include `THIRD_PARTY_NOTICES.txt` with IJG credit (`jfdctfst.c`, `jfdctint_template.c`, `jrevdct.c`), LAME, and MPL-2.0 §3.2 notice | **Mandatory** (LGPLv3 §4(a), IJG, MPL-2.0 §3.2) |
| **Corresponding Source Access** | Provide exact Corresponding Source & build scripts publicly for >= 3 years | **Mandatory** (LGPLv3 §4(d)(1) / GPLv3 §6(b)) |
| **User Modification & Relinking** | Allow DLL replacement and avoid EULA restrictions on debugging/reverse engineering | **Mandatory** (LGPLv3 §4) |
| **In-App Custom FFmpeg Setting** | UI option `Settings -> Custom FFmpeg Executable Path` | **Recommended** (Strong practical enablement of LGPLv3 §4) |
| **Pre-bundled Submodules / Cargo Vendor Archive** | Optional extra `.zip`/`.tar.xz` for air-gapped builds beyond `Cargo.lock` + `.gitmodules` | **Recommended** (Best practice for long-term air-gapped reproducibility) |
