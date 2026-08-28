# Results

This directory contains small, reviewable summaries. Raw profiles, model
outputs, caches, and generated artifacts stay outside Git.

No public result bundle has been finalized yet. The current project status is
listed in [the support matrix](../docs/support-matrix.md).

## Result template

Each result should contain:

1. Date and status (`draft`, `reproduced`, or `superseded`).
2. Hardware product, architecture, and device count.
3. SGLang commit plus patch, branch, or pull request.
4. Immutable environment and model revisions.
5. Exact commands or a versioned script reference.
6. Dispatch proof and numerical-oracle result.
7. Model correctness or quality result.
8. Warm operator and end-to-end performance tables.
9. Memory usage, limitations, and rejected interpretations.

Do not publish a result as `reproduced` until another clean run has verified
the recorded tuple.

