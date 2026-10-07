# Adapt inherited execution and validate

Read after the target baseline passes. Use source implementations and relevant history as candidates with explicit conditions.

Keep the consequential entries in the target whiteboard as a short inventory, linking full details in history:

| Source mechanism and result | Prerequisite or rejection reason | Target disposition and evidence |
|---|---|---|
| Brief implementation and source outcome, including relevant rejection or deferral | Conditions that made it useful or unsuccessful | Carry forward, adapt, recheck or hand off, with a result or next action link |

## Inspect affected assumptions

Target shapes can change buffer extents, addresses, captures, padding, masks and cache lifetimes. They also change ready work, CTA count, per-SM resource demand and stage duration, so streams or chunking that were legal and fast at the source may behave differently. Neither low utilization nor a source rejection settles the target decision.

Inspect relevant negative source results, not just retained changes. Reuse a rejection conditionally when its reason still applies; otherwise give the existing candidate a targeted recheck or an explicit follow-up entry. Rechecks requiring only adaptation of an existing implementation belong to migration after the baseline; new mechanisms or deeper exploratory work go to subsequent optimization. Do not replay unrelated history or silently discard a changed prerequisite.

Adapt dependent mechanisms together. Existing bounded-grid or persistent parameters may need adjustment; verify actual work allocation rather than assuming fixed SM partitioning. Repairing inherited fusion/kernel coverage and recreating shape-bound artifacts belong here or in [baseline preparation](target-baseline.md), as their dependencies require. New execution-domain designs go into subsequent optimization.

## Compare only what the evidence questions

Inspect target execution using suitable traces, events or focused instrumentation. Compare an inherited option or parameter when its changed prerequisites or observed target behavior make its benefit uncertain. Keep a legal current best; disabling one member of a dependent group may create an invalid control. Do not require an individual ablation for every unchanged mechanism.

Use the same target request work, precision, correctness reference, timing boundary and warmup policy. Verify the intervention executes and required outputs/state update. For concurrent or captured paths, check actual capture streams, complete fork/join and timing coverage, including buffering and movement. Account for component slowdowns caused by the proposed resource allocation relative to the best legal target control.

Before attributing a difference to shape, chunking or concurrency, account for engine partitions, fusion/custom coverage, fallback and intermediates. Restore applicable inherited omissions. A combined scheme gain remains valid, but identifying one cause requires matching other consequential differences or a focused control. Kernel layouts and tactics need not be identical. A slower concurrent run alone does not prove cache contention or rule out the mechanism under other conditions.

## Accept the target deployment

Validate the final artifact, actual application route and required stateful behavior under the agreed correctness criteria. Measure repeatable, unprofiled target E2E; add sampling when noise could change the decision and check relevant memory/tail regressions. Use a valid target control or preceding target candidate. Source-batch timing is context; framework-only timing is a separate boundary. An integrated pass does not establish an independent benefit for every inherited optimization.

Update the short mechanism inventory with target decisions, conditional rejections and explicit follow-ups; explain unsupported coverage and unresolved regressions. Report observations separately from causal hypotheses, including tool/metric limitations. Follow the main skill's [delivery and stopping rules](../SKILL.md#record-deliver-and-stop), handing off new opportunities without starting a fresh optimization search.
