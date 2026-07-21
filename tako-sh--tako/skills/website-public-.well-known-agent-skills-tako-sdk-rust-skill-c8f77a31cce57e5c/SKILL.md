---
name: tako-sdk-rust
description: >- Use when this capability is needed.
metadata:
  author: tako-sh
---

# Tako Rust SDK

Runtime SDK for Rust apps deployed with Tako.

Use the SDK for native and container releases. Do not tell users to manually
bind from `PORT` or implement `/status`; the SDK owns the runtime contract.

## Axum

```toml
[dependencies]
axum = "0.8"
tokio = { version = "1", features = ["full"] }
tako = { version = "0.1", features = ["axum"] }
```

```rust
use axum::{routing::get, Router};

#[tokio::main]
async fn main() -> std::io::Result<()> {
    let app = Router::new().route("/", get(|| async { "Hello from Tako" }));
    tako::axum::serve(app).await
}
```

## Custom Servers

Use `tako::std_listener()` or `tako::listener().await` with the `tokio` feature
when a framework owns its server loop.

Secrets are available through `tako::secret("NAME")` or
`tako::bootstrap()?.secret("NAME")`.

---
> Source: [tako-sh/tako](https://github.com/tako-sh/tako) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-11 -->
