# TaNi Audio Leveler — FFmpeg & Third-Party Open Source Compliance

**Publisher:** TaNi Digital Labs  
**Application:** TaNi Audio Leveler (Windows 10/11 Desktop)  
**Microsoft Store ID:** `9PB5VKVTSTQQ`  
**Repository:** `https://github.com/anhtu2163-dev/tani-audio-leveler-lgpl-source`  
**FFmpeg Version:** `n9.0.2-57-gd838f9f9ae-20261115` (Commit `d838f9f9ae`, `win64-lgpl-shared`)  
**Build Scripts:** `FFmpeg-Builds` Commit `c9fe5114060e507409f7ee07edfd82efaf25d767`  
**Governing License:** GNU Lesser General Public License Version 3 (`LGPLv3`)

---

## 1. Purpose of This Repository

This repository provides the **Corresponding Source**, build scripts, license texts, and third-party copyright notices for the open-source FFmpeg shared libraries distributed with **TaNi Audio Leveler**, in compliance with **LGPLv3 Section 4(d)(1)** (incorporating **GPLv3 Section 6(b)/6(d)**) and **MPL-2.0 Section 3.2**.

It is maintained publicly for at least **three (3) years** following the last distribution of the corresponding application version.

---

## 2. Repository Structure

```text
tani-audio-leveler-lgpl-source/
├── README.md                                  # Overview, user rights, and replacement instructions
├── LEGAL_COMPLIANCE_AND_REPLACEMENT_GUIDE.md  # Binary provenance, PE dependencies, and replacement guide
├── BUILD_AND_REPRODUCIBILITY.md               # Build steps, libplacebo submodules, librsvg Cargo.lock audit
├── RELEASE_ASSETS_PLAN.md                     # Inventory & SHA-256 digests of the 19 Corresponding Source archives
├── CORRESPONDING_SOURCE_MANIFEST.json         # Machine-readable SHA-256 manifest (8 runtime binaries + 19 archives)
├── THIRD_PARTY_NOTICES.txt                    # Consolidated notices (FFmpeg, IJG, LAME, LGPL/MPL & permissive libs)
└── licenses/
    ├── COPYING.LGPLv3                         # GNU Lesser General Public License v3.0
    ├── COPYING.GPLv3                          # GNU General Public License v3.0
    ├── COPYING.LGPLv2.1                       # GNU Lesser General Public License v2.1
    └── LICENSE.md                             # Upstream FFmpeg license overview
```

The **19 Corresponding Source `.zip` archives (`72.55 MB` total)** are attached as assets to the GitHub Release tagged **`ffmpeg-lgpl-9.0-d838f9f9ae`** (see [RELEASE_ASSETS_PLAN.md](RELEASE_ASSETS_PLAN.md)).

---

## 3. Your Rights Under LGPLv3 (Modify, Debug, Replace)

In accordance with **Section 4 of the GNU Lesser General Public License v3**:

1. **Right to Modify & Debug:** You may modify any LGPL-covered library distributed with TaNi Audio Leveler and reverse-engineer, decompile, or disassemble for the purpose of debugging your modifications. Nothing in the TaNi Audio Leveler End-User License Agreement restricts this right.
2. **Right to Replace FFmpeg Binaries:**
   - **Option A — In-App Custom FFmpeg Path (Recommended):** Open TaNi Audio Leveler $\rightarrow$ **Settings** $\rightarrow$ **Custom FFmpeg Executable Path** $\rightarrow$ select your own compatible `ffmpeg.exe` build.
   - **Option B — Direct Shared Library Replacement:** Replace the shared libraries (`avcodec-63.dll`, `avdevice-63.dll`, `avfilter-12.dll`, `avformat-63.dll`, `avutil-61.dll`, `swresample-7.dll`, `swscale-10.dll`) alongside `ffmpeg.exe` with ABI-compatible builds compiled from the Corresponding Source.

---

## 4. Reproducing the Build

See [BUILD_AND_REPRODUCIBILITY.md](BUILD_AND_REPRODUCIBILITY.md) and [LEGAL_COMPLIANCE_AND_REPLACEMENT_GUIDE.md](LEGAL_COMPLIANCE_AND_REPLACEMENT_GUIDE.md) for:
- Exact `FFmpeg-Builds` (`c9fe5114060e507409f7ee07edfd82efaf25d767`) Docker build commands (`makeimage.sh` & `build.sh`).
- Verification of **LAME (`SVN r7113`)**, **`libplacebo` (`275f7dea...`)** submodules, and **`librsvg` (`0c074d0a...`)** `Cargo.lock` dependencies.
- SHA-256 verification digests for all 8 runtime binaries and 19 Corresponding Source archives.
