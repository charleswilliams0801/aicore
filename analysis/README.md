# AI chip research results

Research date: 2026-11-12 (UTC). Original request: [request.txt](request.txt).

**Update:** All 11 PDF downloads were retried; all failed at hostname resolution. See the [retry report](DOWNLOAD_RETRY_STATUS.md). The requested [SDK explanation](SDK_EXPLAINED.md) is now included.

**Result:** The requested names describe related layers of the Ascend platform. The AI core is **DaVinci V300**, the CPU core is **TaiShan V200M**, and the processor family is **Huawei Ascend 310B**. Huawei identifies **310B1 (20 TOPS)** and **310B4 (8 TOPS)** in its management-tool documentation. [Chip identification reference][S02] [Board-vendor white paper][S03]

For the Hi1910B software target, Huawei documents **Atlas 200I DK A2** development hardware and **Linux 5.10**. Examples use the release string **5.10.0+**. The requested ebaina.com-specific kit/kernel attribution remains **unverified**; see item 4. [Driver development guide][S04]

| Requested item | Report |
| --- | --- |
| 1. DaVinci V300 AI core and related datasheet | [01 — AI core](analysis/01_davinci_v300_ai_core.md) |
| 2. Exact processor name and related datasheet | [02 — Processor identity](analysis/02_davinci_v300_processor.md) |
| 3. TaiShan V200M CPU name and related datasheet | [03 — CPU core](analysis/03_taishan_v200m_cpu.md) |
| 4. Hi1910B kernel and development kit on Ebaina | [04 — Kernel and development kit](analysis/04_hi1910b_kernel_and_development_kit.md) |

## What is actually included

- Four separately cited analyses and a standalone SDK explanation.
- A [source index](sources/INDEX.md), machine-readable [manifest](sources/manifest.json), and CSV source catalog.
- Direct URLs for 11 related PDFs, plus six web sources or access points.
- [Search and access notes](logs/research_method.md).
- A Python downloader, exact failed-attempt log, and file integrity checksums.

**No original PDF or SDK binaries were downloaded into this package.** The browser could inspect several PDF texts, but local HTTP retrieval failed because this environment cannot resolve the source hosts. Browser inspection is recorded separately from successful local download. Some browser fetches also hit size limits or timeouts. The analyses are original research summaries, not copies of the source documents.

To retrieve the 11 PDF files on a machine with internet access:

```bash
python3 tools/fetch_public_docs.py
```

The script checks PDF signatures, records SHA-256 checksums and failures, and saves files into `downloads/`. It does not install software. This does not fetch authenticated SDK packages; see item 4 for their names and access requirements.

The sources establish module/board specifications. A public standalone V300 core datasheet, V200M CPU technical reference manual, and complete Ascend 310B bare-chip electrical datasheet were **not found in this search**. This does not prove they do not exist.

[S02]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/24.1.RC2/re/npu/Atlas%20A2%20%E6%99%BA%E8%83%BD%E8%BE%B9%E7%BC%98%E7%A1%AC%E4%BB%B6%2024.1.RC2%20npu-smi%20%E5%91%BD%E4%BB%A4%E5%8F%82%E8%80%83%2001.pdf
[S03]: https://www.hiascend.com/s/ascendstatic/lst/files/pdf/All_Love_Technology_Atlas200I_Technical_White_Paper.pdf
[S04]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/23.0.0/RC/driverdevelopmentguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%2023.0.x(23.0.3%E5%8F%8A%E5%85%B6%E7%B3%BB%E5%88%97%E7%89%88%E6%9C%AC)%20%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%2007.pdf
