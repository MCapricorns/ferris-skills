---
name: ferris-native
description: C++/Rust contracts. Use when changing ownership, unsafe/FFI, async cancellation, or build behavior, or diagnosing compiler, linker, Cargo, or MSBuild failures.
---

# Native Engineering

| Change | Read |
|--------|------|
| C++ | [references/cpp.md](./references/cpp.md) |
| Rust | [references/rust.md](./references/rust.md) |
| Mixed-language boundary | Both, especially ABI, allocation/release, errors, and lifetimes |

Repository compiler/MSRV, standard/edition, build system, dependency policy, and conventions win. House defaults apply only to unconstrained projects. Check the installed toolchain and current vendor docs when adopting a feature.

Preserve public ownership, threading, allocation, and failure contracts. Do not hide failures behind defaults or ignored results.
