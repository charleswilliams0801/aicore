# 1. DaVinci V300 AI Core

**Identification:** DaVinci V300 is the AI accelerator core name. Ascend 310B is the SoC family identified in the board literature. A standalone orderable V300 chip or core datasheet was not located.

The [Ascend-hosted QA200A2 brochure](https://www.hiascend.com/s/ascendstatic/lst/as3.0/pba20250414/apn/12/pdf_1.pdf) lists DaVinci V300 and 8/20 INT8 TOPS. Those are product configurations. The [board database](https://www.findboard.cn/chips/ascend310b/) lists one V300 AI Core. A [20T kit procurement listing](https://www.qianlima.com/bid-632754683.html) specifies 1.224 GHz and 10 FP16 TFLOPS. Treat clock as configuration-specific, and advertised throughput as peak.

Core-local memory, instruction encoding, and a V300-specific pipeline reference were not verified. The general DaVinci paper in the original link list provides architecture background only.
