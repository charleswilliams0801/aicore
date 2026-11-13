# 3. TaiShan V200M CPU: name and related specifications

## Finding

The exact CPU-core name is **TAISHANV200M**, usually written **TaiShan V200M**. Huawei describes it as a processor **core** integrated into the Atlas 200I A2 platform. The containing processor in the matching board white paper is Ascend 310B. [Huawei user guide][S01] [Board-vendor white paper][S03]

No independently packaged CPU product with an ordering code simply called “TaiShan V200M” was established. For a chip database, store the core name separately from the SoC name and board/module product.

Huawei's user guide documents four CPU cores, with 1.6 GHz in the 20-TOPS module and 1.0 GHz in the 8-TOPS module. In the main-processor / RC application mode these cores can run the embedded system and application software. [User guide, sections 2.3 and 3.1][S01]

The software is supplied for AArch64, and the toolchain examples use an AArch64 target. This supports identifying the software environment as 64-bit Arm. The precise Arm ISA revision and enabled optional extensions should be verified from the target CPU/OS or a CPU-specific reference manual. [Huawei driver guide][S04]

## Related datasheets

- [Huawei Atlas 200I A2 User Guide][S01]: exact core name and module configuration.
- [Advantech MIC-ATL2S datasheet][S10]: a board-vendor specification with four TaiShan V200M cores at 1.6 GHz and Atlas 200I A2 module integration. It documents the board rather than the CPU core implementation.
- [All Love Technology technical white paper][S03]: identifies the containing Ascend 310B processor.
- [QA200A2 supplier brochure][S11]: useful supplementary product material, but it lists a 1.8 GHz CPU figure. Do not apply that supplier figure to every Atlas module. Its context differs from Huawei's 1.0/1.6 GHz module table; the discrepancy was not resolved.

## What remains unknown

A dedicated public TaiShan V200M CPU technical reference manual was not located. The available sources do not establish enough detail to report a definitive pipeline width, reorder-buffer size, cache configuration, instruction latency, CPU-only power or exact ISA revision.

The name also does not establish that the CPU is an Arm Cortex-A76 or Cortex-A53 implementation. Such equivalences found in third-party material were not used as evidence. For analysis, mark those fields **unverified**, rather than filling them from another CPU or another Ascend product.

On target hardware, `lscpu` and `/proc/cpuinfo` can provide corroborating runtime information, but firmware/kernel naming may still be less precise than a vendor technical reference.

**Confidence:** High for core designation and documented module clocks; incomplete for internal CPU architecture.

[S01]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/24.1.0/intro/userguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%20%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97.pdf
[S03]: https://www.hiascend.com/s/ascendstatic/lst/files/pdf/All_Love_Technology_Atlas200I_Technical_White_Paper.pdf
[S04]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/23.0.0/RC/driverdevelopmentguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%2023.0.x(23.0.3%E5%8F%8A%E5%85%B6%E7%B3%BB%E5%88%97%E7%89%88%E6%9C%AC)%20%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%2007.pdf
[S10]: https://advdownload.advantech.com.cn/productfile/PIS/MIC-ATL2S/file/MIC-ATL2S%E7%B0%A1%E4%B8%AD_DS%28013024%29%281%2920240412182703.pdf
[S11]: https://www.hiascend.com/s/ascendstatic/lst/as3.0/pba20250414/apn/12/pdf_1.pdf
