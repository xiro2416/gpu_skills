# GPU Skills

用于 NVIDIA GPU 推理优化和已优化实现迁移的两套 Agent Skills，共用 GPU 硬件画像。

| Skill | 用途 | 入口 | 流程图 |
|---|---|---|---|
| GPU Inference Optimization | 建立可靠框架基线，以实际执行证据推进端到端优化 | [SKILL.md](gpu-inference-optimization/SKILL.md) | [SVG](gpu-inference-optimization/FLOWCHART.svg) |
| GPU Inference Migration | 在相同模型、硬件、后端和量化配方下迁移 batch、shape 或长度 | [SKILL.md](gpu-inference-migration/SKILL.md) | [SVG](gpu-inference-migration/FLOWCHART.svg) |

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

- 优化以正确性和用户指定的 E2E 延迟或吞吐为依据；性能优先，功耗不作惩罚。
- 开始时读取适用于当前 GPU 的画像，避免套用其他架构或 SKU 的参数。
- 迁移先建立目标框架基线，再适配已有机制；记录旧结论的适用前提及目标处置，验收后由用户另行启动进一步优化。
- 项目记录采用短活动白板和按需读取的历史。迁移保留源记录，并建立独立目标白板。

## GPU 资料

见 [共享资料索引](gpu_parameters/README.md)。目前包含 RTX 6000D / SM120，以及本机约 48 GiB RTX 4090 / SM89 的硬件资源和已有测量资料。4090 采用未观察到温度限频的历史窗口，INT8 Compute Roof 为 635.70 TOPS；功率限频及输入、累加、输出、规模和数值校验边界另行注明。不同 GPU 或配置应提供对应的能力、测试条件与测量来源。
