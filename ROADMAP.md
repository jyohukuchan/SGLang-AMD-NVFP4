# Roadmap

The goal is broad, honest NVFP4 model support on AMD RDNA4 and CDNA3 while
keeping changes small enough to review and upstream independently.

## Upstream patch sequence

### 1. RDNA4 dense W4A16 foundation

- Target exact `gfx1201` and a single Radeon AI PRO R9700.
- Support dense ModelOpt-style packed NVFP4 weights with BF16/FP16
  activations.
- Cover decode and prefill with numerical-oracle tests.
- Preserve the existing CUDA and CDNA/Petit paths.

Status: implemented and locally validated; SGLang
[PR #36788](https://github.com/sgl-project/sglang/pull/36788) is open. Project
tracking: [issue #1](https://github.com/jyohukuchan/SGLang-AMD-NVFP4/issues/1).

### 2. Qwen3.8 mixed-format compatibility on RDNA4

- Load the compressed-tensors checkpoint without expanding the full model to
  BF16.
- Execute its packed NVFP4 MLP weights through the RDNA4 W4A16 backend.
- Route unsupported per-token/per-channel FP8 linears through a correct
  `gfx1201` path.
- Keep the limitation explicit: this is compatibility for a W4A4 checkpoint,
  not native W4A4 execution.

Status: local prototype validated; publication is pending a clean patch split.
Project tracking:
[issue #2](https://github.com/jyohukuchan/SGLang-AMD-NVFP4/issues/2).

### 3. RDNA4 performance patches

- Land decode kernel improvements separately from compatibility changes.
- Land prefill tiling changes with bounded shape-based dispatch.
- Land FP8 decode tuning only for measured, cached configurations.
- Require correctness and end-to-end model evidence for each optimization.

Status: local candidates validated; patches are not yet published. Project
tracking: [issue #3](https://github.com/jyohukuchan/SGLang-AMD-NVFP4/issues/3).

### 4. CDNA3/MI300 validation

- Pin a reproducible ROCm, SGLang, and Petit environment for `gfx942`.
- Validate packed layout and scale semantics against an independent oracle.
- Test decode, prefill, model load, generation, and resident weight memory.
- Identify model-level failures separately from Petit/kernel failures.

Status: planned. No MI300 execution result is currently claimed. Project
tracking: [issue #4](https://github.com/jyohukuchan/SGLang-AMD-NVFP4/issues/4).

### 5. Broader model and execution coverage

- Add models one checkpoint recipe at a time.
- Add tensor parallel, expert parallel, and MoE only with dedicated tests.
- Investigate native W4A4 activation paths independently of W4A16 support.
- Track RDNA targets other than exact `gfx1201` as separate enablement work.

## Patch policy

Each upstream pull request should have one primary purpose, a small regression
surface, and target-specific evidence. Model compatibility, kernel
optimization, new architecture support, and broad refactoring should not be
combined merely because they involve NVFP4.
