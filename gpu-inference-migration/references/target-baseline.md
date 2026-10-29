# Establish the portable target baseline

Read before target adaptation or when compatibility is uncertain.

Inventory source logic, its prerequisites and evidence. Prioritize request/state lifecycle, scheduling policies, logical stage separation, reuse and streaming semantics. Model-specific KV, recurrent state and termination rules remain model-specific even when the scheduling design is reusable.

Separate policy from parameters and implementation. A deadline policy may transfer; its waiting budget, worker count and batch sizes need target evidence. A shared-state design may transfer; IPC handles, addresses, events, layouts and execution-context thread safety may not.

Keep an inventory of directly reused, minimally adapted, unsupported and deferred mechanisms. Preserve compatible existing compute; do not remove fused/custom paths merely to obtain a supposedly portable baseline. If source kernels or engines are incompatible, use a correct supported target implementation or perform the minimum required adaptation/build under the task's constraints. Disclose coverage and resource changes. Never force the source backend or introduce a compiler prerequisite for a target that does not need it.

Preserve the agreed model semantics and precision rules. Cross-GPU/backend migration does not itself authorize recalibration or a different quantization recipe. If such a change is necessary, resolve it under the existing task authorization before accepting the target.

Validate legal shapes, buffers, state ownership, cancellation/reuse and complete output at the actual target entrypoint. Recreate invalid captures and bindings. Record target application latency, resources and actual execution shapes using the frozen protocol; do not require target speedup as proof of basic migration correctness. Performance regressions must be explained and passed to optimization, not hidden. An unusable target or failed quality gate is not a valid optimization starting point.
