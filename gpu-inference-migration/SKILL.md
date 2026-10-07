---
name: gpu-inference-migration
description: "Migrate optimized NVIDIA inference to a new batch size, shape or sequence length on the same model, hardware, backend and quantization recipe. Establish the target baseline, transfer applicable optimizations, validate and hand off."
---

# GPU inference migration

Transfer the optimized computation and its applicable mechanisms, validating them under the target workload. Source performance is evidence about source conditions.

## Establish source and target

Read the source whiteboard and relevant code, effective configuration and experiment records. Establish the requested shapes, inputs, objective, semantic reference and agreed correctness criteria. Recover project facts before asking for missing information essential to proceed; reuse existing authorization.

Before building, read the matching [GPU profile](../gpu_parameters/README.md) and record its link and relevant conditions in the target whiteboard.

Keep the model/checkpoint, actual hardware, backend/version, precision and quantization recipe fixed. Migration alone does not authorize recalibration, a new quantization method or changed acceptance criteria. Resolve broader changes to these assumptions before treating the task as this migration. Preserve source code, artifacts and caches; put target changes and writable cache copies in separate locations, respecting project resource limits.

Judge target schemes by correctness and the agreed performance objective: increased power is not a penalty, and reduced watts alone are not a gain.

## Transfer in dependency order

1. Summarize consequential source mechanisms, including relevant rejected or deferred candidates: their implementation, prerequisites or rejection reason, and target disposition. Include graph/fusion/custom coverage as well as application scheduling; correct outputs alone cannot reveal missing optimization coverage.
2. Establish a strong target baseline from the validated source representation and compute mechanisms. Adapt shape-dependent graph, plugin/kernel interfaces and build inputs; restore applicable inherited coverage. Verify through a minimal correct invocation before transplanting source application scheduling. See [Target baseline](references/target-baseline.md).
3. Adapt the existing buffers, captures, reuse, chunking and stream behavior whose assumptions change. Check target execution and compare affected choices selectively; an integrated check can cover mechanisms whose prerequisites still hold. See [Reuse and validation](references/reuse-and-validation.md).
4. Validate the retained target artifact and actual route against the agreed reference/criteria, then measure matched unprofiled target E2E. Resolve consequential omissions and migration regressions before accepting the result.

Adapting inherited kernel code, launch geometry or fusion interfaces is migration. After the target baseline passes, an existing rejected candidate may receive a focused recheck when changed prerequisites invalidate its source conclusion. New mechanisms or execution-domain designs belong in the handoff. If adaptation changes the graph or engine interface, rebuild and revalidate the affected baseline.

## Record, deliver and stop

Keep source records intact and create or resume an independent target whiteboard before building. Follow project conventions, otherwise use `WHITEBOARD.md` and `history/`. Keep the board near 1,000 tokens: source/target conditions, constraints, reference/baseline links, a brief mechanism/prerequisite/disposition summary, current best and reproduction command, unresolved questions and next action. Archive detailed experiments and preserve necessary links; read only relevant history on resumption. Source conclusions retain their source conditions until target evidence supports them.

Complete migration when the target baseline and adapted stack pass validation, important inherited coverage is accounted for, and consequential adaptation issues are resolved. An optimization may be adjusted or removed on target evidence; unexplained omission is not a completed transfer. Report unresolved correctness, execution or material regression as incomplete, preserving usable artifacts.

Deliver target results and build/run commands, the mechanism inventory with target decisions, evidence limits and further leads. Then stop. Newly visible opportunities do not extend migration; a separately requested `gpu-inference-optimization` run can continue from the target record. This skill works independently of that skill's installation. The [flowchart](FLOWCHART.svg) summarizes the workflow.
