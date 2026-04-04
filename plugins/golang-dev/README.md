# golang-dev

Go development intelligence for Claude Code: 36 skills covering idiomatic Go plus gopls LSP integration.

## Install

```
/plugin install golang-dev@jylhis-plugins
```

## Features

### gopls LSP

Provides Go language intelligence (diagnostics, type checking, go-to-definition) via [gopls](https://pkg.go.dev/golang.org/x/tools/gopls) run from nixpkgs:

```
nix run nixpkgs#gopls -- serve
```

Requires [Nix](https://nixos.org/) installed.

### Skills

| Skill | Description |
|-------|-------------|
| `golang-benchmark` | Benchmarking, profiling, pprof, benchstat |
| `golang-cli` | CLI development with Cobra/Viper |
| `golang-code-style` | Formatting and conventions |
| `golang-concurrency` | Goroutines, channels, sync primitives, errgroup |
| `golang-context` | context.Context creation, propagation, cancellation |
| `golang-continuous-integration` | GitHub Actions CI/CD, linting, GoReleaser |
| `golang-data-structures` | Slices, maps, generics, pointers |
| `golang-database` | SQL, transactions, connection pools, migrations |
| `golang-dependency-injection` | Manual DI, wire, dig/fx, samber/do |
| `golang-dependency-management` | go.mod, versioning, vulnerability scanning |
| `golang-design-patterns` | Functional options, constructors, architecture |
| `golang-documentation` | Godoc, README, CHANGELOG |
| `golang-error-handling` | Error wrapping, errors.Is/As, samber/oops |
| `golang-grpc` | gRPC servers/clients, protobuf, interceptors |
| `golang-linter` | golangci-lint configuration and linter selection |
| `golang-modern-syntax` | Version-aware modern Go syntax (Go 1.0-1.26) with auto-detection |
| `golang-modernize` | Go 1.21-1.26 migration and deprecated package replacement |
| `golang-naming` | Package, interface, constant, and variable naming |
| `golang-observability` | slog, Prometheus, OpenTelemetry, pprof |
| `golang-performance` | Allocation reduction, CPU efficiency, GC tuning |
| `golang-popular-libraries` | Vetted library recommendations by category |
| `golang-project-layout` | Project structure, module naming, workspaces |
| `golang-safety` | Nil safety, slice aliasing, numeric truncation |
| `golang-samber-do` | samber/do v2 dependency injection |
| `golang-samber-hot` | samber/hot in-memory caching |
| `golang-samber-lo` | samber/lo functional utilities |
| `golang-samber-mo` | samber/mo monads (Option, Result, Either, Future) |
| `golang-samber-oops` | samber/oops structured error handling |
| `golang-samber-ro` | samber/ro reactive streams |
| `golang-samber-slog` | samber/slog-* logging pipeline |
| `golang-security` | Injection, crypto, secrets, threat modeling |
| `golang-stay-updated` | Go news, communities, newsletters |
| `golang-stretchr-testify` | assert/require, mock, suite packages |
| `golang-structs-interfaces` | Composition, embedding, type assertions |
| `golang-testing` | Table-driven tests, fuzzing, coverage |
| `golang-troubleshooting` | Debugging, common bugs, Delve, race detection |

## Sources

Skills are aggregated from:

- [samber/cc-skills-golang](https://github.com/samber/cc-skills-golang) — 35 skills by Samuel Berthe (MIT)
- [JetBrains/go-modern-guidelines](https://github.com/JetBrains/go-modern-guidelines) — `golang-modern-syntax` skill by JetBrains (Apache-2.0)

## License

Skills retain the licenses of their original sources. See the repositories above.
