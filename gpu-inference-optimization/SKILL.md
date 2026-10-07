---
name: gpu-inference-optimization
description: "Optimize NVIDIA GPU inference with a verified TensorRT/TensorRT-LLM baseline and measured end-to-end improvements. Use for latency, throughput, scheduling, transfers, and execution costs."
---

# GPU inference optimization

Choose improvements from actual execution, including the quality of the graph and implementation supplied to the framework.

## Establish the task

Use the agreed objective, correctness requirements and constraints, reusing existing authorization. Ask only for unresolved information that materially changes the work. Keep the semantic reference, original performance and evolving current best distinct. Follow the task's correctness criteria; numerical tolerances are not a universal prerequisite.

Read the workload's existing whiteboard before experimenting. Recover implementation and experiment details from the project as needed.

Before choosing implementations, read the matching [GPU profile](../gpu_parameters/README.md) and record its link and relevant conditions in the whiteboard.

Pursue the agreed performance objective using available GPU resources. Higher power does not penalize a correct faster solution; lower power alone earns no credit. Added dummy computation or waiting is not useful utilization.

## Optimization loop

1. Establish or reuse the actual deployment baseline. Verify backend, precision and applicable framework search. Early in the investigation, review costly or frequently repeated regions for missing fusion, unnecessary materialization or conversion, and unsuitable work distribution or resource use. Highest build effort alone does not establish implementation quality. See [Framework baseline](references/framework-baseline.md).
2. Locate an exposed cost and identify a mechanism. Check dependencies and hardware conditions; choose the smallest probe that can distinguish useful remedies. See [Optimization strategies](references/optimization-strategies.md).
3. Make a focused change, preserve the current best, and verify the intended implementation and complete work actually execute.
4. Validate correctness and compare matched, unprofiled application E2E. Resolve noise only as far as needed to decide. Check important implementation differences before attributing a gain to one factor. See [Measurement and profiling](references/measurement-and-profiling.md).
5. Retain reproducible improvements, update affected execution evidence, and select the next worthwhile opportunity. Repair newly discovered baseline gaps within this loop.

## Invest according to remaining value

For latency, use `100 * (T_before - T_after) / T_before` against the experiment's current-best comparator and agreed statistic. For throughput, use `100 * (Q_after - Q_before) / Q_before` under matched service conditions.

| Remaining net E2E potential | Usual investment |
|---|---|
| At least 1% | Prioritize; deeper work can be worthwhile. |
| 0.1% to below 1% | Favor inexpensive probes and simple improvements. |
| Below 0.1% | Usually end independent pursuit after checking related opportunities. |

Estimate potential from probes, repetition and dependencies, including added costs and downstream effects without double-counting overlap. Probe consequential unknowns before assuming little remains. These guides govern further effort, not acceptance of an already obtained gain or a fixed limit on any technique.

## Record and finish

Keep a workload whiteboard of roughly 1,000 tokens and detailed `history/`, following existing project conventions. The board holds the goal and constraints, reference/baseline links, current best and reproduction command, important conclusions with their conditions, and unresolved work. Update after meaningful progress and before stopping; archive detail while preserving these essentials. On resumption, read only the history relevant to the current question.

Finish after validating the retained artifact and reviewing its execution for remaining worthwhile paths. A milestone or a small gain does not exhaust a direction; one negative probe only resolves the mechanism and conditions it tested. Avoid repeating resolved investigations without new evidence. Missing evidence for a consequential decision means further investigation or an explicitly incomplete outcome. Honor user stop conditions and resource limits while preserving the best result.

Deliver original-versus-best E2E, correctness, retained changes, important residuals and the stopping reason, with links to evidence. The [flowchart](FLOWCHART.svg) summarizes these decisions.
