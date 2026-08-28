# Validation protocol

Support claims are fail-closed and divided into independent evidence levels.

## Evidence levels

1. **Host checks**: formatting, lint, CPU-safe unit tests, and dispatch tests.
2. **Target compilation**: the kernel is compiled for the exact GPU target.
3. **Small numerical execution**: the exact target GPU executes the intended
   kernel and matches an independent FP32-dequantized oracle.
4. **Model execution**: a pinned checkpoint loads, generates, and preserves the
   packed-weight memory advantage.
5. **Quality and performance**: deterministic output checks and warmup-aware
   latency/throughput measurements pass after correctness is established.

Passing a lower level does not imply a higher one. Timeouts, crashes, skips,
zero collected tests, CPU fallback, or a different kernel path are failures at
the relevant level.

## Minimum numerical coverage

- BF16 and FP16 activation types where supported.
- Decode and prefill as separate execution classes.
- Aligned and non-aligned dimensions.
- Values on both sides of every dispatch boundary.
- Representative small and model-realistic `M`, `N`, and `K` shapes.
- Format checks for nibble order, block size, FP8 scale encoding, and global
  scale convention.
- Negative tests for unsupported architectures, layouts, and dimensions.

## Minimum model record

Every model-level result must include:

- GPU product and exact architecture identifier.
- SGLang commit and patch/PR identifier.
- Container digest or immutable package versions, including ROCm and PyTorch.
- Model repository and immutable revision.
- Launch command and relevant environment variables.
- Confirmation of the selected quantization and kernel paths.
- Resident weight memory and any explicit workspace allocation.
- A deterministic output or quality check.
- Known limitations and unsupported execution modes.

Credentials, machine-local paths, model weights, full prompts containing
private data, and raw environment dumps must not be published.

