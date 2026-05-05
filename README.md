# Codex RISC-V Builds

Build notes, patches, checksums, and release metadata for running the Rust-based Codex CLI on RISC-V Linux boards.

The current focus is the Orange Pi RV2 / SpacemiT K1 class of boards using the `riscv64gc-unknown-linux-gnu` Rust target.

## Current release

| Version | Target | Notes |
| --- | --- | --- |
| 0.128.0 | Orange Pi RV2 / `riscv64gc-unknown-linux-gnu` | V8-enabled build with RISC-V seccomp support |

Large binaries are published as GitHub Release assets, not committed to this repository.

## Verify a downloaded binary

```sh
sha256sum codex-0.128.0-orangepi-rv2-riscv64gc-v8
chmod +x codex-0.128.0-orangepi-rv2-riscv64gc-v8
./codex-0.128.0-orangepi-rv2-riscv64gc-v8 --version
```

Expected version:

```text
codex-cli 0.128.0
```
