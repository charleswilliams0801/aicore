# 1. DaVinci V300 AI core: identity and characteristics

## Finding

The exact core designation in Huawei's module documentation is **DaVinciV300 AI core**, commonly spaced as **DaVinci V300**. It is an AI compute core inside the processor. Calling it a standalone chip loses the distinction between the core and its containing SoC.

Huawei's Atlas 200I A2 user guide gives the following configurations. [User guide, section 3.1, printed page 9][S01]

| Module configuration | AI cores | AI-core clock | CPU cores | CPU clock |
| --- | --- | --- | --- | --- |
| 20 TOPS configurations | 1 DaVinci V300 | 1.224 GHz | 4 TaiShan V200M | 1.6 GHz |
| 8 TOPS configuration | 1 DaVinci V300 | 0.5 GHz / 500 MHz | 4 TaiShan V200M | 1.0 GHz |

The associated module ratings are **20 TOPS INT8 / 10 TFLOPS FP16** and **8 TOPS INT8 / 4 TFLOPS FP16**. These are configuration-specific advertised compute ratings, not measured application throughput. [Huawei product specification][S12]

The corresponding processor identity is addressed separately in [item 2](02_davinci_v300_processor.md). The most useful datasheet substitute is the official Atlas 200I A2 user guide, followed by the product specification page. Neither is a full V300 microarchitecture or electrical reference.

## Architecture information and its limits

Huawei's 2019 Hot Chips presentation describes the DaVinci architecture through scalar, vector, matrix/cube computation and an explicitly managed memory hierarchy. It is a useful primary-source introduction to how the architecture works. It predates the module documents and does not establish that every illustrated buffer size, bus width, MAC count or configuration applies unchanged to **V300**. [Huawei architecture presentation][S09]

For that reason, this report does not turn the presentation's generic DaVinci diagrams into a claimed V300 technical reference manual. In particular, the exact V300 instruction set, pipeline, SRAM organization, process node, die size and standalone core power were not verified.

## Related documents

1. **Huawei Atlas 200I A2 User Guide**, issue 07, 2025-02-08 — strongest source for the exact core name and installed clocks. [PDF][S01]
2. **Huawei Atlas 200I A2 product specifications** — module throughput and peripheral capabilities. [Web specification][S12]
3. **Huawei DaVinci architecture presentation**, Hot Chips 31, 2019 — background architecture only. [PDF][S09]
4. **All Love Technology Atlas200I DK A2 white paper** — explicitly connects Ascend 310B with the two core names. [PDF][S03]

**Confidence:** High for core identity and the listed Atlas configurations; incomplete for detailed V300 microarchitecture. No standalone public V300 datasheet was located.

[S01]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/24.1.0/intro/userguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%20%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97.pdf
[S12]: https://www.hiascend.com/hardware/accelerator-module-A2
[S09]: https://www.old.hotchips.org/hc31/HC31_1.11_Huawei.Davinci.HengLiao_v4.0.pdf
[S03]: https://www.hiascend.com/s/ascendstatic/lst/files/pdf/All_Love_Technology_Atlas200I_Technical_White_Paper.pdf
