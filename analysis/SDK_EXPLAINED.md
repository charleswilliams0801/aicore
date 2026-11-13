# SDK explained: Ascend 310B / Hi1910B

Prepared: 2026-11-12 UTC.

**For this platform, the board SDK and the AI application toolkit serve different purposes.** The board SDK supports system and peripheral development; CANN supplies the AI development and execution software. A board image may already include parts of both software environments.

## 1. What “SDK” means here

SDK means **Software Development Kit**: tools, libraries, examples and development resources supplied for a platform.

The relevant Huawei board SDK archive is:

```text
Ascend-hdk-310b-sdk-soc_<version>.zip
```

Huawei lists these components inside it:

| Component | Purpose |
| --- | --- |
| `Ascend310B-source.tar.gz` | Platform source/build resources, including the device-tree development material |
| `toolchain.tar.gz` | Compiler toolchain |
| `sdtool.tar.gz` | SD-card preparation tools |
| `emmc_burn_tool.tar.gz` | eMMC image preparation tools |
| `hdmi_sample.tar.gz`, `audio_sample.tar.gz` | Interface examples |
| Other utilities | Release-specific upgrade and provisioning tools |

The guide separately lists `Ascend-hdk-310b-hboot2-sdk-soc_<version>.zip` for Hboot2 bootloader source. These package names are documented patterns; replace `<version>` with a real release selected from the official download service. [Huawei driver development guide, section 4.1][BOARD]

## 2. How CANN differs from the board SDK

CANN is the Ascend AI software layer. Its packages have different roles:

| Package | Main use |
| --- | --- |
| **Toolkit** | Application/operator development, compilation, model conversion and debugging |
| **NNRT** | Runtime for offline model inference |
| **NNAE** | Broader AI execution engine; supported functions depend on the hardware and release |
| **Kernels** | Prebuilt AI operator implementations for the selected processor |

Huawei's installation documentation describes choosing the appropriate development/runtime package and adding operator packages as required. A CANN “kernel” is an AI compute implementation; it is separate from the **Linux operating-system kernel**. Toolkit features listed for the whole Ascend product family do not establish that every feature works on Ascend 310B. [CANN package roles][ROLES] [CANN package selection][CANN]

Example filename patterns:

```text
Ascend-cann-toolkit_<version>_linux-<arch>.run
Ascend-cann-nnrt_<version>_linux-<arch>.run
Ascend-cann-nnae_<version>_linux-<arch>.run
```

The architecture refers to the machine where the software runs. Select an AArch64 build for a supported Arm board environment, or the appropriate host build when developing on a PC. Check the selected release's actual hardware/OS support. [CANN package selection][CANN]

## 3. Drivers, firmware and the OS image

These are additional parts of the working system:

- **NPU driver:** provides the operating-system interface used to control and manage the accelerator.
- **NPU firmware:** device software needed for the processor's operation.
- **OS image:** the bootable board system, with its Linux kernel, filesystem and board configuration.

The board-specific guide lists driver and firmware packages separately from the SDK ZIP. Its RC driver naming includes `Ascend-hdk-310b-npu-driver-soc_<version>_linux-aarch64.run`. This is a naming example, not an instruction to install an arbitrary release. [Board software packages][BOARD]

For OrangePi AIpro, the manufacturer's setup guide distinguishes a **desktop image**, which includes CANN and examples, from a **minimal image**, which omits them. [OrangePi environment guide][ORANGE]

## 4. Which material fits your task?

The following is a practical selection guide based on those package roles:

| Your task | Starting point |
| --- | --- |
| Study chip specifications | Hardware manuals and datasheets |
| Run a supplied AI demonstration | Board-vendor image and its matched runtime |
| Convert models or develop an AI application | Compatible CANN Toolkit and examples |
| Deploy a prepared offline inference application | Compatible runtime and required operator packages |
| Modify peripheral support, DTS or kernel configuration | Board SDK, toolchain and board documentation |
| Modify the bootloader | Matching Hboot2 SDK and boot documentation |

For your current chip/kernel research, the driver development guide is the best starting document. You need the SDK itself when you want to inspect or build the actual platform source.

## 5. RC versus EP mode matters

Huawei documents two deployment modes:

- **RC (Root Complex):** the module's Arm CPU runs the embedded system and applications.
- **EP (Endpoint):** the accelerator connects to a separate host through PCIe.

Choose documentation and packages for the mode you actually use. A PC host's Linux kernel and an embedded module's Linux kernel are separate version fields. [Huawei application modes][MODES]

## 6. How to obtain a compatible set

1. Identify the board/module and whether it uses RC or EP mode.
2. Record its chip, OS, kernel, driver and firmware versions.
3. Open the [Ascend developer portal][PORTAL] and navigate to the applicable product's software downloads. The [legacy firmware/driver selector][DOWNLOADS] also identifies Atlas 200I A2.
4. Sign in if required, select the intended release, and consult its HDK/CANN compatibility information.
5. Obtain the matching SDK/toolchain or application packages needed for your task.

Huawei explicitly requires compatible driver and firmware versions and links a release-specific HDK compatibility table. Its CANN installation guidance also requires compatible CANN, driver and firmware versions. Package version numbers need not be numerically identical. [Upgrade preparation][COMPAT] [CANN compatibility guidance][UPGRADE]

No exact release is prescribed here because the physical board and installed versions have not been supplied. A stock upstream Linux kernel, a different carrier-board image, or the newest CANN package cannot be assumed to match the existing installation.

Useful read-only commands on the target:

```bash
uname -r
uname -m
cat /etc/os-release
npu-smi info
cat /etc/sys_version.conf
```

The last file is documented for the Atlas module and may be absent from a customized image. Firmware-version inspection is described in the [upgrade preparation guide][COMPAT].

## 7. What was obtained in this research

The package identities and explanations above were checked against public manufacturer documentation. **No SDK archive was downloaded or installed.** This Markdown file explains what to request and how the pieces fit together; it is not an SDK archive or a source-code inspection report.

All **11 previously listed PDFs were retried**. Every local attempt failed at hostname resolution with `[Errno -2] Name or service not known`; no PDF bytes were saved. That error does not establish that a source URL is dead or requires an account. See [the retry report](DOWNLOAD_RETRY_STATUS.md) and [machine-readable attempt log](logs/download_attempts.json).

[BOARD]: https://www.hiascend.com/doc_center/source/zh/Atlas%20200I%20A2/23.0.0/RC/driverdevelopmentguide/Atlas%20200I%20A2%20%E5%8A%A0%E9%80%9F%E6%A8%A1%E5%9D%97%2023.0.x(23.0.3%E5%8F%8A%E5%85%B6%E7%B3%BB%E5%88%97%E7%89%88%E6%9C%AC)%20%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97%2007.pdf
[ORANGE]: https://public-download.obs.cn-east-2.myhuaweicloud.com/%E4%BC%99%E4%BC%B4%E6%96%87%E6%A1%A3/OrangePi_AI_Pro_20T%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97_v1.0.pdf
[ROLES]: https://www.hiascend.com/document/detail/zh/Pytorch/600/configandinstg/instg/insg_0002.html
[CANN]: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/softwareinst/instg/instg_0003.html
[MODES]: https://www.hiascend.com/document/detail/zh/Atlas%20200I%20A2/250RC1/har/hardwareguide/hardware_005.html
[PORTAL]: https://www.hiascend.com/developer
[DOWNLOADS]: https://www.hiascend.com/hardware/firmware-drivers/old/commercial
[COMPAT]: https://www.hiascend.com/document/detail/zh/Atlas%20200I%20A2/24.1.RC3/RC/driverdevelopmentguide/atlasdg_11_0130.html
[UPGRADE]: https://www.hiascend.com/doc_center/source/zh/CANNCommunityEdition/80RC1alpha003/softwareinst/instg/CANN%208.0.RC1.alpha003%20%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97%2001.pdf
