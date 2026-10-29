# Actual execution baseline

Read when establishing the deployed route or investigating an implementation gap.

Verify what the real entrypoint loads and executes: model assets, precision, preprocessing, runtime settings, caches and fallbacks. A standalone script is not automatically equivalent to the service. Keep correctness and performance timing boundaries explicit.

Reuse a valid deployment baseline. No TensorRT, TensorRT-LLM, ONNX export or other compiler/backend is mandatory. Backend selection should answer an observed limitation and respect the user's constraints; it is not a checklist of frameworks to try.

Inspect expensive repeated regions for missing fusion, conversions, materialization, redundant computation and unsuitable work distribution. Include custom code and boundaries between implementations. Repeated graph passes, maximal build effort or a framework label do not prove implementation quality.

Use the chosen backend's installed-version capabilities when relevant: operator selection, library algorithms, compilation, autotuning, profiles or custom kernels. Use supported export/build paths only when that route is selected. An incompatible serialized artifact may need rebuilding; an accepted dynamic shape proves legality, not suitability. Static specialization is useful only if it matches the real workload and does not create harmful padding or fragmentation.

Screen with inexpensive probes that exercise the mechanism. Spend build/search effort on credible candidates and unresolved questions, within budget; do not require the highest search level by default. Reuse compatible caches with provenance and validate the actual rebuilt or reconfigured application route.
