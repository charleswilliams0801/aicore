# 2. Processor containing DaVinci V300: exact name

## Finding

For the platform in the request, the processor family is **Huawei Ascend 310B (昇腾310B)**. The All Love Technology technical white paper explicitly names this processor alongside DaVinci V300 and TaiShan V200M. [White paper, section 2.1, printed page 5][S03]

Huawei's management-tool manual resolves two exact chip names:

| Chip name shown by npu-smi | Compute variant |
| --- | --- |
| **310B1** | **20 TOPS** |
| **310B4** | **8 TOPS** |

This mapping is explicitly documented in table 4-6, rather than inferred from clock speed or a third-party product listing. It applies to the chip names documented in that release; it is not a claim that no other family variants exist. [Huawei npu-smi reference, printed page 11][S02]

The prompt provides no physical board identifier or command output, so it does not determine whether a particular device is 310B1 or 310B4.

## Names to keep separate in a dataset

| Name | Meaning in the evidence |
| --- | --- |
| DaVinci V300 | Integrated AI core designation |
| TaiShan V200M | Integrated CPU core designation |
| Ascend 310B; 310B1 / 310B4 | Processor family and documented chip names |
| Atlas 200I A2 | Acceleration module |
| Atlas 200I DK A2 | Development kit |
| Hi1910B / hi1910b | Hardware/software target identifier found in this platform's device trees |

The Hi1910B association is supported by Huawei's Ascend 310B source-package and device-tree documentation. Treat this as a software-target mapping; the string alone does not determine a purchasable package ordering code or silicon stepping. [Driver development guide][S04]

## How to identify an actual device

Run the read-only command:

```bash
npu-smi info
```

Record the **Name** value and driver version. The manual also documents `npu-smi info -l` for listing devices and `npu-smi info -t board -i ID` for module information. Use the ID actually returned by the device list. These commands were not run on target hardware during this research. [Command reference][S02]

## Datasheet availability

The [official module user guide][S01] is the strongest accessible specification document. The [official technical-white-paper landing page][S15] was also located; it displays a contact-details form and did not expose a retrievable PDF through the browser tool.

A complete bare-chip datasheet specifying package pinout, supply rails, timing and absolute maximum ratings was not verified. The report therefore provides an exact processor-family identification and documented variant mapping, without inventing a component ordering code.

**Confidence:** High for Ascend 310B, 310B1 and 310B4 identification; no determination of the user's particular physical chip.

[S03]: https://www.hiascend.com/s/ascendstatic/lst/files/pdf/All_Love_Technology_Atlas200I_Technical_White_Paper.pdf
[S02]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/24.1.RC2/re/npu/Atlas%20A2%20%E6%99%BA%E8%83%BD%E8%BE%B9%E7%BC%98%E7%A1%AC%E4%BB%B6%2024.1.RC2%20npu-smi%20%E5%91%BD%E4%BB%A4%E5%8F%82%E8%80%83%2001.pdf
[S04]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/23.0.0/RC/driverdevelopmentguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%2023.0.x(23.0.3%E5%8F%8A%E5%85%B6%E7%B3%BB%E5%88%97%E7%89%88%E6%9C%AC)%20%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%2007.pdf
[S01]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/24.1.0/intro/userguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%20%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97.pdf
[S15]: https://e.huawei.com/cn/material/enterprise/8bc139ce5b314db6885c3ccda8bac8cf
