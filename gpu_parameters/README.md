# Shared GPU profiles

This directory contains hardware data shared by the inference optimization and migration skills. It is not a third skill. Keep `gpu_parameters/` beside the skill directories when extracting a download; preserve that layout so their relative links work.

| Actual GPU / architecture | Profile |
|---|---|
| NVIDIA RTX 6000D / Blackwell SM120 | [RTX 6000D measurements](rtx6000d-sm120.md) |
| 本机 NVIDIA GeForce RTX 4090 / Ada SM89 / 约 48 GiB | [RTX 4090 resources and measurements without observed thermal throttling](rtx4090-sm89-48g.md) |

At the start of work, select the profile matching the actual SKU, architecture and device resources, read it, and link the relevant conditions and conclusions from the active whiteboard. A name match alone is insufficient if hardware resources or operating conditions differ. The RTX 4090 profile describes the measured approximately 48 GiB device, including power-cap events; absence of observed thermal throttling does not mean unrestricted clocks. Add a separately evidenced profile for another configuration; do not transfer one card's numbers or instruction support.

Distinguish published specifications, sustained throughput achieved within a finite experiment, and unknowns. Match input format, accumulation, output, sparsity, shape, layout, working set and measurement method before applying a number. A measured roof is a useful reference, not a universal limit or attainable target for every shape. Reuse available evidence; fill only gaps that affect the present decision.

Full SM coverage means every enabled SM participated. It does not prove simultaneous saturation. Clock readings, board watts, active-cycle percentages and throttle events measure different things; none alone establishes useful utilization or a particular bottleneck. Use the effective throughput of the real workload to judge improvements. Higher useful utilization is desirable; higher watts alone do not prove faster inference.

Profiles retain provenance and limitations. Original reports and traces remain at their source locations and are not copied into these packages; source paths document provenance and may need remapping after download.
