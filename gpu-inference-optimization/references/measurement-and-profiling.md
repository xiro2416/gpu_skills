# Measurement, correctness and attribution

Read when comparing candidates, locating costs or deciding what an experiment establishes.

## Match the task and the comparator

Record the workload, representative inputs, backend/precision, shapes, batch/concurrency, timing boundary, artifact and reproduction command. Keep the fixed semantic reference, original performance and current best separate. Determine correctness criteria before judging results: preserve required operations, dependencies, masks, state ownership, sampling, termination and streaming behavior; apply numerical/statistical tests or report-only audits as the task requires. Do not silently change the precision recipe or acceptance criteria to retain a gain.

Measure matched, unprofiled application E2E using the agreed statistic. Account consistently for compilation, warmup, capture, caches, transfers and delivery. Control drift with adjacent comparisons or alternating order when useful; add samples or statistical analysis only to resolve uncertainty. Confirm the selected artifact after any final rebuild, including relevant memory and tail behavior.

## Separate scheme gains from causal claims

Before attributing a gain to batch size, scheduling or another factor, inspect consequential differences in engine partitions, fusion/custom coverage, fallback, intermediates and total work. Repair omissions of applicable established optimizations when needed for the comparison. Equivalent coverage does not require identical tactics or kernel traces.

A compound candidate may be retained on sound E2E evidence. Describe that as a scheme gain until other important differences are controlled. Add a focused control when attributing the cause would affect a decision; do not demand every possible ablation. Explain deliberate work elimination and investigate unexplained route or work-count changes.

## Interpret profiling within its limits

Use application/runtime traces to locate costs and dependencies, engine inspection to identify actual execution, and kernel profiling for a specific residual question. Diagnostic timing includes instrumentation/capture effects and is not production E2E. Follow completion dependencies: a consumer's wait can include producer execution; overlapping spans and waits cannot be added as independent costs.

For decisive counters, record the exact metric, scope, window and normalization. Pipeline-active percentages, achieved throughput, occupancy and warp-stall fractions describe different quantities; their difference does not measure free SM capacity. Treat unavailable metrics as unknown. Check support for the actual SKU and tool version: CUDA activity tracing and GPU performance-counter support are distinct. See [NVIDIA SKU support](https://developer.nvidia.com/err_nvgpu/) and the [Nsight Compute profiling guide](https://docs.nvidia.com/nsight-compute/ProfilingGuide/index.html).

Attach important conclusions to an observation or controlled probe. Distinguish observed behavior, a plausible explanation and established causality. A slower concurrent run alone does not identify cache competition. If a tool is unavailable, seek another observation that answers the question; inadequate coverage remains uncertainty.

## Verify complete concurrent work

For asynchronous, graph or persistent probes, verify the actual capture/execution streams, legal fork/join, complete timing boundary and all required output/state updates. Sentinel outputs or work counters can expose stale results and omitted branches. Consider whether the profiler serializes the execution being studied.

Compare against the current best legal serial path with the same total work. Also measure each component under the proposed resource limits, then the combined run including synchronization, buffering and movement. Savings versus a deliberately constrained, slower serial variant are not the net gain over the current best. Confirm production dependencies permit the measured overlap before integrating it for E2E validation.

A negative result is informative only if the intervention executed and the probe could detect its prediction. Revisit attribution when retained changes alter the execution structure; a failed variant does not exclude every implementation of its mechanism.
