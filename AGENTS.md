# AGENTS.md

## Purpose

- This repository is the public coordination and evidence hub for SGLang
  NVFP4 support on AMD RDNA4 and CDNA3.
- It is not a downstream SGLang source fork. Keep implementation patches in a
  SGLang fork and link them here.
- Keep RDNA4 (`gfx1201`) and CDNA3 (`gfx942`) execution claims separate.

## Evidence rules

- Target-GPU PASS requires real execution on the exact architecture, intended
  kernel dispatch, and a numerical oracle.
- Compilation, imports, timeouts, skipped tests, or fallback paths are not
  execution proof.
- Record immutable code, model, container, ROCm, and PyTorch revisions.
- Treat performance as observational until correctness is established.
- State unsupported modes and negative results explicitly.

## Repository hygiene

- Do not commit models, caches, raw traces, compiled objects, wheels, logs, or
  generated model output.
- Do not publish credentials, hostnames, private prompts, or machine-local
  paths.
- Put only small, reviewable summaries under `results/`.
- Preserve upstream and third-party license/provenance information.
- Run `git diff --check` and validate links before publication.

## Change boundaries

- Keep compatibility, optimization, new architecture support, and broad
  refactoring in separate upstream patches.
- Prefer common format semantics with explicit hardware-specific dispatch.
- Do not generalize a result beyond its exact checkpoint recipe, architecture,
  dtype, and execution mode.

