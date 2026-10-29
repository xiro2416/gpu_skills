# Choose a remedy from execution evidence

Read when selecting a probe or implementation change.

## Diagnose before choosing a tool

| Exposed cost | Candidate investigation |
|---|---|
| Ready work blocked by CPU submission, locks or synchronization | Concurrent preparation, shorter critical sections, independent execution contexts, fewer host/device round trips |
| Long preparation/prefill interferes with ongoing generation | Logical P/D isolation, bounded/chunked prefill, deadline-aware admission and scheduling |
| Batch waiting, barriers or long/short interference | Bounded coalescing, completed-subset progress, length grouping and long-request isolation |
| Repeated small operations or launch overhead | Fusion, capture/replay, batched state updates |
| Inefficient compute or excessive traffic | Algorithms, precision when authorized, layout, reuse, decomposition, attention/KV strategy |

These are hypotheses, not a required order or a default architecture. Trace effects on retained outputs before removing work; preserve neighborhoods, masks, sampling, state ownership and lifetimes.

## Couple scheduling and operators

Measure stage cost and resources over the batch/length shapes actually produced by the scheduler. Use this service curve to choose batching waits, admission, chunking and kernel strategies. Operator gains can change the best schedule, and schedule changes can invalidate an operator microbenchmark.

Distinguish resident slots, execution batch limits, admitted requests and clients. Logical P/D does not require a particular process/GPU count. Shared read-only weights do not permit unsafe sharing of mutable state, execution contexts or workspaces.

## Investigate useful overlap

Find independent ready work across branches, stages or requests. More workers may isolate CPU bottlenecks but duplicate weights and traffic; more streams may share weights but still serialize at host submission or workspace locks. MPS does not automatically share weights. Compare controlled execution shapes for attribution, then tune each scheme fairly for its achievable capacity.

Check actual dependencies, CTA count, resident resources, register/shared-memory demand, bandwidth and cache working set. Low power or Tensor activity alone does not show free capacity. Stream overlap does not prove same-SM residency; different instruction types do not establish independence.

Compare overlap, locality and launch savings against copies, synchronization, memory growth, lost specialized-kernel performance and contention. A smaller grouped batch may help one GPU's L2 but hurt another. Use [complete-work measurements](measurement-and-profiling.md#verify-complete-concurrent-work); never infer the cause solely from a faster or slower concurrent run.
