# GPU 硬件参考

按实际型号、架构和资源选择对应画像；`gpu_parameters/` 与两个技能目录保持同级。默认只读匹配的短表，复现或解释异常时再打开详细记录。

| GPU | 画像 |
|---|---|
| 本机 RTX 4090 / SM89 / 约 48 GiB | [4090](rtx4090-sm89-48g.md) |
| RTX 6000D / SM120 | [6000D](rtx6000d-sm120.md) |

口径：dense，MAC=2 operations；Roof 为 TFLOP/s、Ridge 为 FLOP/Byte（INT8 为 TOPS、OP/Byte）。Ridge=1000×Roof÷本卡 Triad 带宽（GB/s）；功耗取独立 ≥30 s 负载末约 20 s 的板卡均值。

带宽为有效读写字节数/时间：Triad `A=B+C×D` 三读一写、16 Byte/FP32 元素；Copy 一读一写、8 Byte/元素，每数组 512 MiB。吞吐不含输入准备、量化或传输成本。

实测 Roof 用于估算，业务判断须匹配精度语义和工作量，并验证 E2E；功耗、SM 参与及管线活跃率不等同于有效利用率。
