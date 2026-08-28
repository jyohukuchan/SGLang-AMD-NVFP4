# Benchmarking protocol

Performance is reported only after numerical and model-level correctness has
been established on the same implementation.

## Required separation

- Compile and first-run latency versus warmed execution.
- Operator microbenchmarks versus end-to-end serving.
- Prefill versus decode.
- Kernel GPU time versus wall-clock latency.
- Single request versus concurrent serving.
- Baseline and candidate using the same environment and model revision.

## Operator measurements

Report the exact `M`, `N`, `K`, activation dtype, packed-weight layout, warmup
count, sample count, summary statistic, and numerical tolerance. Include model
shapes and boundary shapes. Synchronization used solely for timing must be
stated and kept outside the hot path under test.

## End-to-end measurements

At minimum, record:

- input and requested output token counts;
- time to first token or prefill throughput;
- inter-token latency or decode throughput;
- total wall time;
- concurrency and batch settings;
- CUDA Graph or eager mode;
- prefix/radix cache state;
- peak and resident device memory.

Use sufficiently large input and output lengths to expose steady-state
behavior. A short smoke generation is correctness evidence, not a throughput
result.

## Reporting rejected candidates

Record optimizations that were measured and rejected when they are likely to
be rediscovered. Include the tested shapes and the reason: regression,
workspace cost, lack of dispatch coverage, numerical failure, or excessive
complexity.

