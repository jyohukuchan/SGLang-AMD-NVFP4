# Contributing

This repository coordinates validation and upstreaming. SGLang implementation
changes should normally be developed against
[`sgl-project/sglang`](https://github.com/sgl-project/sglang) and submitted to
that project as focused pull requests.

## Compatibility reports

Use the compatibility issue template and include exact, immutable versions.
State whether the result is compile-only, kernel execution, or full model
generation. A failure report is useful when it includes the first relevant
error and enough context to reproduce it.

## Performance reports

Follow [docs/benchmarking.md](docs/benchmarking.md). Do not compare results
from different model revisions, environments, graph modes, cache states, or
request shapes without labeling the differences.

## Pull requests to this repository

Pull requests may update the support matrix, validation tooling, result
summaries, and project documentation. Keep hardware-specific conclusions
scoped to the hardware that actually ran them.

Before submitting:

- remove credentials, hostnames, private prompts, and machine-local paths;
- do not add model weights, caches, compiled objects, wheels, or raw profiles;
- link the relevant SGLang commit or pull request;
- separate verified facts from expectations and planned work;
- confirm Markdown links and run `git diff --check`.

By contributing, you agree that your contribution is licensed under Apache-2.0.

