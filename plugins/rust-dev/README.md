# rust-dev

Rust development intelligence for Claude Code: 29 skills covering ownership, lifetimes, error handling, concurrency, domain patterns, and LSP tooling plus rust-analyzer integration.

## Install

```
/plugin install rust-dev@jylhis-plugins
```

## Features

### rust-analyzer LSP

Provides Rust language intelligence (diagnostics, type checking, go-to-definition) via [rust-analyzer](https://rust-analyzer.github.io/) run from nixpkgs:

```
nix run nixpkgs#rust-analyzer
```

Requires [Nix](https://nixos.org/) installed.

### Skills

#### Language Mechanics

| Skill | Description |
|-------|-------------|
| `m01-ownership` | Ownership, borrowing, and lifetime issues |
| `m02-resource` | Smart pointers and resource management |
| `m03-mutability` | Mutability and interior mutability patterns |
| `m04-zero-cost` | Generics, traits, zero-cost abstraction |
| `m05-type-driven` | Type-driven design, newtype, type state |
| `m06-error-handling` | Result, Option, thiserror, anyhow |
| `m07-concurrency` | Async/await, Send/Sync, thread safety |

#### Design & Architecture

| Skill | Description |
|-------|-------------|
| `m09-domain` | Domain modeling in Rust |
| `m10-performance` | Performance optimization and benchmarking |
| `m11-ecosystem` | Crate integration and ecosystem guidance |
| `m12-lifecycle` | Resource lifecycle design (RAII, Drop) |
| `m13-domain-error` | Domain error handling strategy |
| `m14-mental-model` | Rust mental models and learning |
| `m15-anti-pattern` | Anti-pattern detection and code review |

#### Domain-Specific

| Skill | Description |
|-------|-------------|
| `domain-cli` | CLI tools with clap, ratatui, indicatif |
| `domain-cloud-native` | Cloud-native apps and microservices |
| `domain-embedded` | Embedded/no_std Rust development |
| `domain-fintech` | Financial technology applications |
| `domain-iot` | IoT applications |
| `domain-ml` | ML/AI applications in Rust |
| `domain-web` | Web services and APIs |

#### LSP Tools

| Skill | Description |
|-------|-------------|
| `rust-code-navigator` | Navigate code using LSP (go-to-definition, references) |
| `rust-refactor-helper` | Safe refactoring with LSP impact analysis |
| `rust-trait-explorer` | Explore trait implementations via LSP |
| `rust-symbol-analyzer` | Analyze project structure using LSP symbols |
| `rust-call-graph` | Visualize function call graphs using LSP |
| `rust-deps-visualizer` | Visualize dependency trees as ASCII art |

#### Core

| Skill | Description |
|-------|-------------|
| `coding-guidelines` | Rust coding style, naming conventions, best practices |
| `unsafe-checker` | Unsafe code review, FFI, raw pointers |

## Sources

Skills are sourced from:

- [actionbook/rust-skills](https://github.com/actionbook/rust-skills) — 29 skills by ZhangHanDong (MIT)

## License

Skills retain the license of their original source (MIT). See the repository above.
