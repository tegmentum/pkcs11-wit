# PKCS#11 WIT Definitions

WebAssembly Interface Type (WIT) definitions for PKCS#11 cryptographic token interface standard.

## Overview

This repository contains WIT interface definitions that model the PKCS#11 (Cryptoki) API for use with WebAssembly Component Model. These definitions enable WebAssembly components to interact with cryptographic tokens, HSMs, and smart cards through a standardized interface.

## Structure

- `pkcs11-core/` - Core PKCS#11 types and error codes
- `pkcs11-buffer/` - Buffer management utilities
- `pkcs11-crypto/` - Cryptographic operations (encrypt, decrypt, sign, verify, digest)
- `pkcs11-object/` - Object management (create, destroy, find, get/set attributes)
- `pkcs11-session/` - Session management
- `pkcs11-token/` - Slot and token management
- `pkcs11-util/` - Utility functions
- `pkcs11-registry/` - Provider registry
- `worlds/` - WIT world definitions
- `guest-smoke/` - Example guest interface for testing

## Usage

### As a Git Dependency

Reference these WIT definitions in your project's `Cargo.toml`:

```toml
[dependencies]
# Your other dependencies...

[build-dependencies]
wit-bindgen = "0.46"
```

In your `build.rs`:

```rust
use std::path::PathBuf;

fn main() {
    let wit_dir = PathBuf::from(env!("CARGO_MANIFEST_DIR"))
        .join("path/to/pkcs11-wit");

    println!("cargo:rerun-if-changed={}", wit_dir.display());
    std::env::set_var("PKCS11_WIT_ROOT", wit_dir);
}
```

### With Git Submodules

Add as a submodule to your project:

```bash
git submodule add https://github.com/your-org/pkcs11-wit.git wit/pkcs11
git submodule update --init --recursive
```

## License

Apache-2.0

## Related Projects

- [wasm-pkcs11](https://github.com/your-org/wasm-pkcs11) - Host adapter implementation
