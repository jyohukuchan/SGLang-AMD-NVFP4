# Support matrix

This matrix distinguishes a locally observed result from upstream support.
Entries apply only to the listed hardware, format, model, and execution mode.

## Status definitions

- **Planned**: work is scoped, but no target-device execution is claimed.
- **Prototype**: an implementation has executed locally, but its public patch
  or reproducibility package is incomplete.
- **Validated locally**: the target GPU executed the intended path, numerical
  checks passed, and at least one model loaded and generated.
- **Upstream PR**: a public SGLang pull request exists; this does not imply it
  has been merged or is supported by a release.
- **Upstream**: the change is merged into SGLang. Release availability must
  still be stated separately.

Compilation, import success, model loading without generation, a skipped test,
or an unintended fallback never counts as target-device validation.

## Hardware and model matrix

| Hardware | Architecture | Checkpoint / format | Execution scope | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| Radeon AI PRO R9700 | `gfx1201` | `nvidia/Llama-3.1-8B-Instruct-NVFP4` at `bdb54e24298451af785c0ac63c1b485e9b7400a2` | Dense W4A16, BF16/FP16 activation, single GPU, decode and prefill | Upstream PR | Locally validated on the real target; [SGLang PR #36788](https://github.com/sgl-project/sglang/pull/36788) is open |
| Radeon AI PRO R9700 | `gfx1201` | `unsloth/Qwen3.8-27B-NVFP4` local tree at `9e3d73c76edd` | Mixed compressed-tensors NVFP4/FP8, single GPU | Prototype | Packed NVFP4 MLP weights execute as W4A16; this is not native W4A4 |
| MI300-class GPU | `gfx942` | ModelOpt/Petit NVFP4 | Dense execution through Petit | Planned | The expected CDNA3 path has not yet been validated by this project |
| Radeon AI PRO R9700 | `gfx1201` | NVFP4 MoE or tensor-parallel checkpoints | MoE, TP, or EP | Planned | Outside the current single-GPU dense proof |

## Known boundaries

- RDNA4 validation is currently exact to `gfx1201`; it must not be generalized
  to other RDNA targets without execution evidence.
- The first RDNA4 backend consumes canonical packed NVFP4 weights and
  BF16/FP16 activations (W4A16).
- The Qwen3.8 checkpoint also contains FP8 linears. Compatibility requires
  both the packed-weight path and a supported FP8 activation/GEMM route.
- MI300/CDNA3 uses a materially different wave64/MFMA execution family. RDNA4
  wave32/WMMA results do not establish MI300 performance or correctness.
- Multi-GPU, MoE, online conversion, FP4 KV cache, and generic fallback are not
  supported by the current proof.

