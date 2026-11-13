# 4. Hi1910B: kernel, development kit, and Ebaina verification

## Result and scope

**The ebaina.com-specific answer could not be verified.** Searches for Hi1910B, Hi1910, Ascend 310B and Atlas-related development material did not yield an accessible Ebaina document tying the exact target to a kernel release and development kit.

An [Ebaina category page][S13] lists a discussion asking about Ascend 310B and manufacturer support. Its [linked discussion][S14] could not be fetched. The listing alone is insufficient evidence for a kit model or kernel. Internal search URLs also failed to load through the research browser.

This is a limitation of the accessible evidence, not proof that Ebaina has no relevant material. No Ebaina account, paid download or private support archive was accessed.

## Verified manufacturer alternative

Huawei's documentation supplies the following useful answer outside Ebaina:

| Question | Verified result | Scope |
| --- | --- | --- |
| Kernel family | **Linux 5.10** | Atlas 200I A2 driver documentation |
| Example release string | **5.10.0+** | Driver-guide module paths and OrangePi board specifications |
| Development kit | **Atlas 200I DK A2** | Huawei device-tree mapping |
| 8-TOPS kit device tree | `hi1910B-asic-M100-B51.dts` | Atlas 200I DK A2 |
| 20-TOPS module on kit carrier | `hi1910B-asic-M150-B51.dts` | 20-TOPS Atlas module plus DK A2 carrier |
| Related board | **OrangePi AIpro 20T / 8T** | Huawei developer-board portal; independent board configurations |

Sources: [Huawei kernel introduction][S05], [driver guide, sections 8.2.4–8.2.5][S04], and [developer-board specifications][S06].

The exact patch level and build of a particular shipped image remain unknown. “Ubuntu 22.04” and “openEuler 22.03” are distribution versions, not kernel version numbers. The OrangePi portal lists Ubuntu 22.04.3 LTS and openEuler 22.03 with Linux 5.10.0+. [Board specifications][S06]

## Software development packages

Huawei documents the SDK archive pattern:

`Ascend-hdk-310b-sdk-soc_<version>.zip`

It contains `Ascend310B-source.tar.gz`, `toolchain.tar.gz`, and supporting tools. The same guide lists a separate Hboot2 source SDK, NPU drivers and firmware. These are release-dependent packages; `<version>` is a placeholder, not a usable download filename. [Driver guide, section 4.1][S04]

Use the official product software/download navigation and select a compatible release. The guide directs users to log in to obtain packages. No authenticated SDK package was downloaded, and no guessed binary URLs are supplied.

For OrangePi, the [manufacturer setup guide][S08] points to its [official support/download page][OPI]. Its desktop image includes CANN and examples; the minimal image omits those components. Keep the selected board image, firmware, driver and CANN versions together when reproducing an environment.

## Conflicting kernel clues

A separate Huawei guide contains an example directory named `linux-4.19`. A directory name in one example is not sufficient to override the explicit kernel section or to identify a running board. The inconsistency is recorded rather than silently ignored. [24.1.RC1 guide, printed page 172][S17]

A host PC's kernel is also distinct from the embedded device kernel, particularly when the module runs as a PCIe endpoint.

## Read-only checks on the actual board

```bash
uname -r
uname -a
cat /proc/version
cat /etc/os-release
npu-smi info
tr '\0' '\n' < /proc/device-tree/compatible
tr '\0' '\n' < /proc/device-tree/model
```

These are suggested checks, not results obtained from hardware. The device-tree paths may be unavailable on some systems.

**Confidence:** High for the manufacturer-documented Linux 5.10 family and Atlas kit association; unverified for the requested Ebaina-specific kit and a particular device's exact kernel build.

[S13]: https://www.ebaina.com/channels/20/100
[S14]: https://www.ebaina.com/ask/100000053567
[S05]: https://www.hiascend.com/document/detail/zh/Atlas%20200I%20A2/24.1.0/RC/driverdevelopmentguide/atlasdg_11_0108.html
[S04]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/23.0.0/RC/driverdevelopmentguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%2023.0.x(23.0.3%E5%8F%8A%E5%85%B6%E7%B3%BB%E5%88%97%E7%89%88%E6%9C%AC)%20%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%2007.pdf
[S06]: https://www.hiascend.com/developer/devboard
[S08]: https://public-download.obs.cn-east-2.myhuaweicloud.com/%E4%BC%99%E4%BC%B4%E6%96%87%E6%A1%A3/OrangePi_AI_Pro_20T%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97_v1.0.pdf
[S17]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/24.1.RC1/RC/driverdevelopmentguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%2024.1.RC1%20%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%2005.pdf

[OPI]: http://www.orangepi.cn/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-Pi-AIpro(20T).html
