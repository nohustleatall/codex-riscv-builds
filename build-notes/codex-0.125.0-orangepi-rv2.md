# Codex 0.125.0 on Orange Pi RV2

Target board class: Orange Pi RV2 / SpacemiT K1.

Rust target:

```text
riscv64gc-unknown-linux-gnu
```

## Build inputs

Codex 0.125.0 already includes GPT-5.5 model metadata upstream. The local RISC-V build needs three compatibility changes:

1. Build OpenSSL from source for `riscv64gc-unknown-linux-gnu`.
2. Skip vendored bubblewrap while cross-compiling if target `libcap` is not available through `pkg-config`.
3. Use `seccompiler`'s `riscv64` target architecture when installing the network seccomp filter.

The release binary was built with a local RISC-V `rusty_v8` archive and matching generated source binding file for `v8` crate `146.4.0`.

## Build command shape

```sh
export RUSTY_V8_ARCHIVE=/path/to/librusty_v8_release_riscv64gc-unknown-linux-gnu.a.gz
export RUSTY_V8_SRC_BINDING_PATH=/path/to/src_binding_release_riscv64gc-unknown-linux-gnu.rs
export CARGO_TARGET_RISCV64GC_UNKNOWN_LINUX_GNU_LINKER=/usr/bin/riscv64-linux-gnu-g++
export CC_riscv64gc_unknown_linux_gnu=/usr/bin/riscv64-linux-gnu-gcc
export CXX_riscv64gc_unknown_linux_gnu=/usr/bin/riscv64-linux-gnu-g++

cargo build --release -p codex-cli --bin codex --target riscv64gc-unknown-linux-gnu --offline
```

The release build used `CARGO_PROFILE_RELEASE_LTO=false` and `CARGO_PROFILE_RELEASE_CODEGEN_UNITS=16` to keep link time manageable on the build host.

## Runtime expectations

The binary is dynamically linked for RISC-V Linux and expects the target system to provide:

```text
libgcc_s.so.1
libm.so.6
libc.so.6
ld-linux-riscv64-lp64d.so.1
```

System `bubblewrap` is expected on the target board for the filesystem sandbox path. The RISC-V seccomp architecture selector is included so sandboxed command execution does not panic on the network seccomp filter.
