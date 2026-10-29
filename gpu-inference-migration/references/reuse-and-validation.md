# Validate reuse and hand off target tuning

Read while adapting mechanisms and accepting the target baseline.

Keep a short mechanism inventory: source design/result, prerequisites, target disposition and evidence. Relevant negative source results remain conditional; changed hardware, backend or execution shapes may invalidate their reason for rejection. Do not replay every old experiment.

Check affected assumptions together: state representation and ownership, buffer extents, indexing, valid lengths, captures, masks, completion events, cancellation and slot reuse. Independent request state is required even when weights are shared. Worker topology, slot capacity, batch limits and queue budgets are distinct and must have a coherent resource budget.

Use matched target inputs and agreed correctness criteria. A minimal legal call is followed by a representative application check covering affected stateful/streaming behavior. Validate required output and state updates, not just API success. Source outputs cannot always be sliced into a target reference when randomness or padding changes semantics.

For asynchronous execution, verify actual streams, complete fork/join and timing boundaries. Avoid adding overlapping waits and execution as independent costs. A correctness check does not prove a scheduling benefit; source performance does not prove target performance. Document backend/kernel coverage and traffic differences before attributing an observed change to batch or concurrency.

After migration passes, hand the target record to gpu-inference-optimization: objective and SLO, load protocol, semantic reference, target baseline and commands, mechanism inventory, known regressions, target-dependent parameters, and remaining budget. In particular, defer searches over worker/stream counts, P/D allocation, L2-sensitive group sizes, operator algorithms and compiler tuning to that phase.

Do not silently relax quality, precision or timing boundaries to complete migration. If the user requested migration only, stop; otherwise the main skill's handoff continues optimization within the same authorization and budget.
