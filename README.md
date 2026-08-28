# SGLang AMD NVFP4

Community validation and upstreaming workspace for running NVFP4 checkpoints
with [SGLang](https://github.com/sgl-project/sglang) on AMD CDNA3 and RDNA4
GPUs.

This repository is an independent community project. It is not an official
SGLang or AMD repository, and it is not a downstream distribution of SGLang.
Implementation changes live on focused branches of
[`jyohukuchan/sglang`](https://github.com/jyohukuchan/sglang) and are proposed
upstream as narrowly scoped pull requests. This repository holds the support
matrix, validation protocol, reproducible result summaries, and roadmap.

## Current status

| Track | Target | Status |
| --- | --- | --- |
| Dense ModelOpt-style NVFP4 W4A16 | Radeon AI PRO R9700 (`gfx1201`) | Locally validated; [SGLang PR #36788](https://github.com/sgl-project/sglang/pull/36788) is open |
| Mixed compressed-tensors NVFP4/FP8 | Radeon AI PRO R9700 (`gfx1201`), Qwen3.8 27B | Local prototype validated; upstream patch not yet published |
| Petit-backed NVFP4 | MI300/CDNA3 (`gfx942`) | Planned validation; no result is claimed here yet |

The Qwen3.8 prototype keeps packed NVFP4 weights but currently executes its
NVFP4 MLP linears as W4A16. It is not native W4A4 acceleration. See the
[support matrix](docs/support-matrix.md) for exact boundaries and terminology.

## Project layout

- [ROADMAP.md](ROADMAP.md) describes the intended upstream patch sequence.
- [docs/support-matrix.md](docs/support-matrix.md) records model, format, and
  hardware support without treating compile-only results as execution proof.
- [docs/validation.md](docs/validation.md) defines correctness and model-level
  acceptance criteria.
- [docs/benchmarking.md](docs/benchmarking.md) defines the reporting protocol.
- [results/README.md](results/README.md) provides the result template and index.

## Scope

The initial hardware tracks are deliberately separate:

- RDNA4: exact `gfx1201`, with the Radeon AI PRO R9700 as the proof target.
- CDNA3: `gfx942`, with MI300-class GPUs as the intended validation target.

The architectures have different wave and matrix-instruction paths, so a
result on one track is not evidence for the other. Format/checkpoint handling
should be shared where possible; hardware execution and dispatch should remain
explicit.

## Contributing

Compatibility reports and reproducible benchmark results are welcome. Read
[CONTRIBUTING.md](CONTRIBUTING.md) before opening an issue or pull request.
Do not upload model weights, caches, compiled binaries, or raw profiles.

## License

This repository is licensed under the [Apache License 2.0](LICENSE).
SGLang and third-party model checkpoints retain their own licenses.

