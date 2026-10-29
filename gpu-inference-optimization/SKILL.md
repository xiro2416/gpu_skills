---
name: gpu-inference-optimization
description: "Optimize NVIDIA GPU inference latency, throughput, concurrency or resource use from actual execution evidence. Backend-neutral; jointly consider scheduling, operators and hardware costs."
---

# GPU inference optimization

Optimize the agreed user outcome, not a preferred framework or a utilization proxy. Start from the actual deployment; no engine, export format or backend is a prerequisite.

## Establish the objective and baseline

Recover the project whiteboard, effective entrypoint, loaded assets, precision, preprocessing and runtime configuration before experimenting. Keep the semantic reference, original performance and current best distinct. Use the task's quality criteria; do not silently relax semantics or numerical requirements.

Freeze representative input distributions, timing boundaries, SLOs, client behavior and experiment/resource budgets. For concurrency, distinguish clients, in-flight requests, arrival rate, execution batch and goodput. Measure capacity under the chosen closed- or open-loop protocol; do not alter request pacing, chunking or failure accounting to increase the reported capacity. First-output latency and within-request continuity are separate constraints.

Read relevant available [GPU profiles](../gpu_parameters/README.md) for hardware assumptions; measure consequential unknowns rather than treating a source profile as target evidence. See [Execution baseline](references/framework-baseline.md) when the actual route or implementation is uncertain.

## Evidence-driven loop

1. Profile the exposed application cost. Separate queueing, input preparation, CPU submission/locks, GPU queueing, execution and delivery. CPU wait is not automatically GPU idle; overlapping intervals cannot be added independently.
2. Form a falsifiable mechanism and choose the smallest useful probe. Use actual batch/length distributions and stage service curves to jointly consider scheduling and operators. See [Optimization strategies](references/optimization-strategies.md).
3. Make a focused, reversible change; verify the intended route and all output/state updates execute. A backend change is a candidate, not a required first step.
4. Compare matched, unprofiled application results against the current best. Check quality, completion, tails, streaming continuity, memory and fairness as relevant. Compound gains are valid, but do not attribute them to one factor without a control. See [Measurement](references/measurement-and-profiling.md).
5. Retain reproducible improvements and update the remaining bottleneck. A negative probe resolves only the mechanism and conditions actually tested.

Higher power or GPU-Util may suggest more work coverage, but neither proves increased goodput or spare capacity. Do not add dummy work or waiting. Apply energy or memory constraints when they are part of the agreed objective.

## Budget, record and finish

Allocate effort by exposed E2E cost, SLO sensitivity, uncertainty and remaining budget. Small local changes may matter near a capacity boundary; a large kernel speedup may be hidden by dependencies. Avoid fixed gain thresholds that substitute for this assessment.

Prefer component checks and small representative screening runs; confirm finalists independently with enough steady-state samples for the claimed statistic. Avoid repeated full-corpus tests, blanket backend sweeps or high-effort builds without a discriminating question. Preserve failures and consumed attempts.

Keep a concise whiteboard: objective/protocol, baseline/reference, current best and reproduction command, mechanism evidence, budget used and unresolved work. Archive detailed traces/history. Finish with validated artifacts, original-versus-best application metrics, tradeoffs, portability limits and rollback instructions. Honor stop conditions; incomplete evidence or a completed experiment is not a successful optimization. Deployment requires the task's authorization.

The [flowchart](FLOWCHART.svg) summarizes the loop.
