# Framework and implementation baseline

Read when establishing a baseline or resolving an export, representation, build or backend gap.

## Identify the deployed computation

Inspect the installed backend/version, representative shapes, precision and effective route against the selected GPU profile. TensorRT-LLM backends differ: follow their supported preparation and runtime rather than assuming ONNX export or a TensorRT engine. Consult version-matched [architecture documentation](https://nvidia.github.io/TensorRT-LLM/architecture/overview.html) and source.

For ONNX, use the modern PyTorch exporter and its optimization/verification capabilities where supported. Check their actual coverage using the [installed-release guidance](https://docs.pytorch.org/docs/stable/onnx.html). Export success does not validate the final runtime.

## Inspect costly regions early

Use existing traces, engine inspection and source to review consequential repeated computation before investing heavily in specialization. Establish which semantic regions receive which implementations, including custom paths and boundaries between engines and application code. Check:

- Fusion and reusable computation actually covered, including similar regions that were omitted.
- Layout/precision conversions, intermediate writes and repeated movement or recomputation.
- Work distribution and live state that may limit parallel execution.

Investigate relevant gaps with a focused probe. This is a review of important costs, not an exhaustive operator checklist or a requirement to try every fusion. Framework search optimizes the representation it receives; inherited custom code also needs scrutiny. Choose graph canonicalization, an existing fused operator/plugin, or another permitted implementation when evidence supports it. Repeated GraphSurgeon/constant-folding passes without a hypothesis do not establish a stronger baseline.

## Build for the actual target

Reuse a baseline whose representation, target coverage, search and validation remain adequate. Otherwise use actual static shapes where appropriate and the highest supported, applicable search effort. Discover builder, tiling/code-generation and build-route capabilities without artificial tactic or workspace restrictions; retain real hardware and task limits.

Search effort and runtime choices differ. Evaluate relevant stream, partition and profile choices by execution evidence. Routine sweeps of lower search levels or repeated tactic searches require a concrete unresolved question.

Screen representation changes with local probes or cheaper builds that can exercise the proposed mechanism; compare at matched fidelity. Use strong search for credible finalists, compatible caches with provenance and adequate coverage, and validate the final rebuilt artifact. See [TensorRT build guidance](https://docs.nvidia.com/deeplearning/tensorrt/latest/performance/optimization.html).
