---
name: gpu-inference-migration
description: "Migrate portable inference scheduling and state-management mechanisms for the same model to a new GPU, backend or workload. Validate a target baseline, then hand off to gpu-inference-optimization within the task budget."
---

# GPU inference migration

Transfer applicable logic first, establish a correct target baseline, then optimize for the target. No framework is preferred. Portability of a design does not establish implementation compatibility or target performance.

## Establish source and target

Read source records and effective code/configuration. Freeze the requested model/checkpoint, source and target hardware/backend/workload, semantic reference, quality criteria, test protocol, remaining budget and authorization. New GPU/backend/shape are supported migration targets; changes to precision, quantization or calibration require task authorization. A different model needs fresh semantic validation, not transplantation of model state.

Read relevant available [GPU profiles](../gpu_parameters/README.md). Preserve source artifacts and create an independent target record. Do not repeat unrelated historical experiments or modify the source to make the target easier.

## Transfer by portability and dependency

Inventory consequential source mechanisms and classify them:

- **Reusable logic:** request lifecycle, deadlines, admission, logical P/D, state ownership, invalidation and streaming boundaries. Adapt APIs and dependencies first; reuse the design, not assumptions about its benefit.
- **Environment-dependent parameters:** worker/stream counts, batch/slot limits, length buckets, partition sizes and queue budgets. Establish safe legal values; leave performance tuning to optimization.
- **Hardware/backend-bound implementations:** kernels, engines, captures, layouts, IPC and synchronization primitives. Reuse only when compatible. Adapt or rebuild what is necessary for correctness, or use an authorized fallback; document lost coverage and its cost.

Follow actual dependencies rather than insisting on engines before scheduling or scheduling before every required compute adapter. See [Target baseline](references/target-baseline.md). Do not turn migration into an exhaustive tactic, backend or topology search.

Validate complete target behavior, including state handoff, cancellation/reuse, long-input boundaries and streaming termination where affected. Use a minimal correct invocation followed by a representative application check; record matched target timing and resources. Source timing is context, not a target baseline. See [Reuse and validation](references/reuse-and-validation.md).

## Accept and hand off

Migration passes when the target runs correctly, the actual route is known, reusable logic has been accounted for, and unsupported mechanisms or regressions are explained. An unexplained omission or correctness failure remains incomplete; do not optimize around it as though migration passed.

Then invoke [gpu-inference-optimization](../gpu-inference-optimization/SKILL.md) with the target objective/SLO, frozen workload, reference, measured baseline, mechanism inventory, pending questions and remaining test/time/resource budget. Continue under the same task authorization and budget; do not reset the clock or create a new goal without an explicit request. Optimization does not recursively invoke migration as a mandatory step.

If the user requested migration only, stop after delivery. If the budget is exhausted or the optimization skill is unavailable, report the unexecuted handoff explicitly rather than claiming optimization occurred.

Keep a concise target whiteboard and linked history. Deliver reproduction commands, correctness/performance evidence, retained/adapted/unsupported source mechanisms, target-specific tuning needs and rollback. Do not deploy unless authorized. The [flowchart](FLOWCHART.svg) summarizes the handoff.
