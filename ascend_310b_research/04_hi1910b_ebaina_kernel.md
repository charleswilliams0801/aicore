# 4. Hi1910B kits and Linux kernel

**Ebaina:** Searches for Hi1910B and 昇腾310B 开发板 内核 yielded no matching kit or kernel documentation. The [Hongying X2 article](https://www.ebaina.com/articles/140000018195) identifies Ascend 310P and dual Hi3403, so it does not establish a Hi1910B kit.

| Hardware | Hi1910B evidence | Kernel evidence |
|---|---|---|
| Orange Pi AIpro 20T | [Vendor manual mirror](https://manuals.plus/m/d16dc322ee7dc9261906a4fe38889401c63ed60b03d86ff914ce65b97a9988af_optim.pdf) documents Ascend310B-source-opi/dtb/dts/hi1910b/hi1910BL/hi1910B-default.dts | [Ascend board spec](https://www.hiascend.com/developer/devboard/spec) lists Linux 5.10.0+ and Ubuntu 22.04.3 LTS / openEuler 22.03. Exact image patch and build suffix depend on the image. |
| Atlas 200I A2 acceleration module | Huawei driver guide linked in item 2 names hi1910B-asic-kernel-rc.dtsi | The DTS filename does not specify the running release. Verify against the selected SDK/image. |
| Orange Pi Kunpeng Pro | [Vendor manual](https://public-download.obs.cn-east-2.myhuaweicloud.com/OrangePi_KunPeng_Pro_%E7%94%A8%E6%88%B7%E6%89%8B%E5%86%8C_v0.3.pdf) shows the same Hi1910B DTS tree | Shared SDK tree is a lead and does not independently confirm the fitted chip or exact kernel. |

On a running kit capture `uname -r`, `cat /etc/os-release`, and `tr '\\0' '\\n' </proc/device-tree/compatible`. Record the image filename and SDK release alongside the output. The OS distribution version and Linux kernel release are separate values.
