---
name: ferris-native
description: Changes C++ or Rust ownership, unsafe code, FFI, async cancellation, and build configuration. Use when editing those contracts or diagnosing compiler, linker, Cargo, or MSBuild failures. Not for code outside C++ and Rust.
---

# Native Engineering

| Change | Read |
|--------|------|
| C++ | [references/cpp.md](./references/cpp.md) |
| Rust | [references/rust.md](./references/rust.md) |
| Mixed-language boundary | Both, especially ABI, allocation/release, errors, and lifetimes |

House defaults in the references apply only where the repository's compiler or MSRV, standard or edition, build system, and dependency policy leave the choice open. Preserve public ownership, threading, allocation, and failure contracts; do not hide failures behind defaults or ignored results.
