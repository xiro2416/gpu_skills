# Choose a remedy from execution evidence

Read when an observed cost needs a discriminating experiment or implementation change.

## Start with the exposed cost

Select the simplest plausible remedy for a consequential cost. Check basic representation and implementation quality early, including inherited custom code; a high-effort engine build is not evidence that these opportunities were addressed.

| Observed mechanism | Useful investigation |
|---|---|
| Missing fusion or redundant computation | Inspect the graph and actual fused path; test canonicalization, existing fused operators/plugins or permitted local fusion. |
| Conversion, copies or intermediates | Trace production, storage and consumption; test layout, reuse or fusion that removes measured traffic. |
| Large live state or poor work distribution | Examine tile decomposition, register/shared-memory use, spill and available parallel work. |
| Exposed submission, synchronization or transfer cost | Test capture/replay, submission granularity, residency or GPU-side control with the same request semantics. |

Trace influence on retained outputs before removing, narrowing or caching work. Preserve complete neighborhoods, masks, state ownership and cache lifetimes. Discarding an output region does not establish that its upstream computation is irrelevant.

## Decide whether overlap is useful

Find work that is ready and independent in the target interval: across tiles, heads, branches or requests. Different instruction types alone do not make operations independent; an epilogue consuming an unfinished accumulator must wait for it.

Distinguish insufficient work from work separated by execution boundaries or coarse scheduling. Persistence does not create parallelism. Check grid CTA count, per-SM resident blocks/warps, register/shared-memory demands and the pipelines actually exercised. More CTAs can improve residency or work distribution without activating additional SMs. Low Tensor activity or low board power does not establish spare execution capacity.

When one pipeline is limited, use the GPU profile and current execution evidence to consider overlapping useful work or redistributing existing computation between supported Tensor and SIMT/CUDA-core paths. Preserve the precision recipe and required semantics, and include conversion, shared issue, register, memory and synchronization costs. Reducing live state or changing decomposition may make coexistence possible. Favor low-cost probes of graph/submission changes or local fusion where appropriate; use bounded static schedules, warp specialization, cross-operation pipelines or dynamic queues when the observed mechanism justifies their added cost. These are choices, not a mandatory technique sequence.

## Verify the tradeoff

Check architecture support and compiled behavior: instruction path, producer/consumer roles, tile geometry, registers, shared memory, spill and barriers. Setting a warp-specialization or fusion flag does not prove the intended mechanism executed. Bounded grids constrain work allocation rather than pinning blocks to particular SMs; stream overlap does not by itself prove same-SM residency.

Evaluate launch/materialization savings, locality and extra parallelism against scheduler/synchronization costs, larger live state, lost specialized GEMM/Conv performance and load imbalance. Use [complete-work comparisons](measurement-and-profiling.md#verify-complete-concurrent-work) and the best current E2E comparator. A local win is useful evidence, but production dependencies and downstream effects decide whether to retain it.
