# GPU Skills

用于 NVIDIA GPU 推理优化和已优化实现迁移的两套 Agent Skills，共用 GPU 硬件画像。

| Skill | 用途 | 入口 | 流程图 |
|---|---|---|---|
| GPU Inference Optimization | 框架无关，依据实际瓶颈联合优化调度、算子、延迟、吞吐与并发 | [SKILL.md](gpu-inference-optimization/SKILL.md) | [SVG](gpu-inference-optimization/FLOWCHART.svg) |
| GPU Inference Migration | 同模型跨 GPU、后端或负载迁移，优先复用通用逻辑，验收后进入优化 | [SKILL.md](gpu-inference-migration/SKILL.md) | [SVG](gpu-inference-migration/FLOWCHART.svg) |

## 目录布局

```text
gpu-inference-optimization/
  SKILL.md
  agents/openai.yaml
  references/
  FLOWCHART.svg
gpu-inference-migration/
  SKILL.md
  agents/openai.yaml
  references/
  FLOWCHART.svg
gpu_parameters/
  README.md
  rtx6000d-sm120.md
  rtx4090-sm89-48g.md
```

使用时保留三个目录的同级关系，两个 Skill 通过相对路径读取共享资料。`gpu_parameters` 是数据目录，并非第三个 Skill。请从对应 `SKILL.md` 开始，按当前问题读取参考文档。

## 工作方式

- 优化以正确性及用户指定的端到端延迟、吞吐、并发或资源目标为依据；功耗和 GPU-Util 不能替代 goodput 与 SLO 验收。
- 按实际硬件读取相关 GPU 画像；不预设 TensorRT 或其他后端，也不照搬源设备的参数。
- 迁移优先复用请求生命周期、逻辑 P/D、deadline、状态所有权和流式边界；区分通用设计、环境参数及绑定实现。目标基线通过后调用 optimization，沿用原授权与剩余预算；用户要求仅迁移时停止。
- 项目记录采用短活动白板和按需读取的历史。迁移保留源记录，并建立独立目标白板。

## GPU 资料

见 [共享资料索引](gpu_parameters/README.md)。目前包含 RTX 6000D / SM120，以及本机约 48 GiB RTX 4090 / SM89 的硬件资源和已有测量资料。4090 采用未观察到温度限频的历史窗口，INT8 Compute Roof 为 635.70 TOPS；功率限频及输入、累加、输出、规模和数值校验边界另行注明。不同 GPU 或配置应提供对应的能力、测试条件与测量来源。
