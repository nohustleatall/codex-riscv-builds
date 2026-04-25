# RISC-V rusty_v8 Artifact Notes

Codex code mode depends on the Rust `v8` crate, which expects a matching `rusty_v8` static archive and generated source binding for the target architecture.

For the current Codex 0.125.0 build, the relevant `v8` crate version is:

```text
146.4.0
```

The Codex build consumes two target-specific files:

```sh
export RUSTY_V8_ARCHIVE=/path/to/librusty_v8_release_riscv64gc-unknown-linux-gnu.a.gz
export RUSTY_V8_SRC_BINDING_PATH=/path/to/src_binding_release_riscv64gc-unknown-linux-gnu.rs
```

The archive and binding must come from the same `rusty_v8` build and must match the target triple used by Cargo.
