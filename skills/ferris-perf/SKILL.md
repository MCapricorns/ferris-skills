---
name: ferris-perf
description: Profiles and benchmarks programs, builds, and Windows processes to guide optimization. Use when asked to make something faster or smaller, or before claiming a speedup or memory reduction. Not for correctness failures.
---

# Performance Measurement

## Measure the right build

- Profile optimized builds with symbols. Cargo: a `[profile.profiling]` that `inherits = "release"` with `debug = true` (or `"line-tables-only"`). MSVC: `/Zi` and `/DEBUG`, but `/DEBUG` switches the linker to `/OPT:NOREF`, `/OPT:NOICF`, and incremental linking; restore `/OPT:REF /OPT:ICF /INCREMENTAL:NO` so the measured binary matches the shipped one.
- Keep hardening (`/guard:cf`, `/CETCOMPAT`, overflow checks the project enables) on while measuring; removing it is not an optimization.
- `-C target-cpu=native` and `/arch:` levels above the deployment baseline produce binaries that fault on older CPUs. Use them only for binaries that never leave the build machine.

## Get a trustworthy number

- Fix the workload and the metric (p50/p99 latency, throughput, peak private bytes, build time) before changing code.
- Interleave runs (A B A B) and report median and spread over repeated runs on the same machine. Discard or report the cold first run separately.
- Defender real-time scanning, indexing, power plan, and thermal limits dominate I/O and build timings on Windows. Note them; changing exclusions, power plans, or Dev Drive setup is a machine-wide change that needs approval.
- In microbenchmarks, keep inputs and results opaque to the optimizer (`std::hint::black_box`, `benchmark::DoNotOptimize`). Confirm a microbenchmark win at the user-visible metric.

## Find the cost

- CPU: sample before guessing. ETW-based tools (WPR/WPA, samply) usually need elevation for kernel sampling; ask before elevating.
- Builds: `cargo build --timings`, MSBuild `-bl` binary logs, and `vcperf` for C++ front-end and template cost.
- Memory: working set shrinks under trimming and is not allocation evidence; compare private bytes or commit and heap peaks.

## Change and report

- Change one thing at a time and keep behavior identical; reuse existing regression checks.
- Unchecked indexing, `unsafe` shortcuts, `std::unreachable`, and `[[assume]]` need a profile showing the cost and a proven invariant.
- A performance claim states workload, build configuration, run count, median and spread, before and after.
