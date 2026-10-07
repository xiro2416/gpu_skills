# Establish the target baseline

Read before adapting application scheduling, or when a target build or inherited compute path needs repair.

## Preserve the optimized representation

Start with the validated source computation and its graph transformations, fused operators/plugins and custom implementations. Record which semantic regions each covers and the assumptions affected by the target shape. Distinguish compute representation needed for the baseline from application scheduling adapted afterwards.

Repair target-specific loss of applicable inherited coverage. Adjust static constants, masks, indexing, layouts, kernel geometry and plugin interfaces as required; transfer the existing mechanism rather than assuming a source launch or serialized capture is reusable. New algorithms or additional optimization mechanisms are separate work. Label any custom compute honestly instead of calling the resulting baseline framework-only.

Preserve the quantization algorithm, calibration policy and scale rules. Input-dependent scales from the original dynamic algorithm may change without changing the recipe. Apply the task's agreed correctness criteria; a migration does not silently relax them.

## Build for the target and hardware conditions

An incompatible static source engine requires a target build. A dynamic engine accepting the shape establishes legality, not performance suitability: check every input/profile and shape-tensor constraint. Prefer static dimensions or exact MIN=OPT=MAX for a fixed target where applicable. Follow the installed TensorRT/TensorRT-LLM backend's supported preparation path.

Use the highest supported, applicable framework search effort, discovering builder, tiling/code-generation and build-route capabilities. Respect actual hardware and task limits without artificial tactic restrictions or blindly maximizing stream counts/capacity. Reuse compatible caches with provenance and target search coverage; allow target search rather than freezing source tactics. See version-matched [shape guidance](https://docs.nvidia.com/deeplearning/tensorrt/latest/inference-library/dynamic-shapes-basics.html) and [build guidance](https://docs.nvidia.com/deeplearning/tensorrt/latest/performance/optimization.html).

Use the shared GPU profile selected at task entry; source and target shapes may attain different fractions of its measured performance. Keep this shape-specific interpretation with the target evidence.

## Validate the target baseline

Use a minimal correct invocation: legal buffers, intended profile, required state and fresh captures where needed. Verify backend, precision, fallback and inherited compute coverage. Compare with the original semantic reference evaluated at the target under the agreed criteria; slicing source outputs is insufficient when padding, randomness or state changes semantics.

Record repeatable framework timing, boundary and artifact separately from application E2E. Resolve material baseline omissions before judging inherited scheduling. If valid source evidence covers a region, do not redo every historical optimization; if required coverage cannot be restored, document the consequence instead of silently declaring equivalence. Continue with [Reuse and validation](reuse-and-validation.md) after the baseline is valid.
