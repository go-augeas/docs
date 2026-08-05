# Roadmap

## Done

- **Configuration tree** — An ordered tree of labelled nodes with values, built by `New()`; every entry addressable by path, with `Root`, `Label` and node insertion/removal preserving order.
- **Path language** — Absolute and relative paths, `*` name wildcard, `//` descendant axis, `.` / `..`, positional `[n]` / `[last()]`, value `[sub = 'v']`, regexp `[sub =~ 're']` (RE2), existence predicates, union `|`, and `$var` bindings.
- **Editing API** — `Get` / `Exists` / `Set` / `SetMultiple` / `Insert` / `Remove` / `Move` / `Match` / `Label` / `DefineVariable` / `DefineNode` — the full tree-mutation surface over path expressions.
- **Embedded `.aug` corpus interpreter** — a from-scratch pure-Go interpreter reads the entire upstream Augeas 1.14.1 lens corpus (232 modules) plus 5 original contrib lenses (Wireguard, Rclone, Caddyfile, Nftables, Unbound), reachable via `NewEngine().Lens(module, binding)` and usable with `TextStore` / `Get` / `Set` / `Match`; `Load` / `Save` run through an injectable `FileSystem` seam, and load failures surface under `/augeas//error`. Verified 1791/1791 (100%) against the corpus's own inline get+put test assertions.
- **The `Lens` seam** — `Register`/`LensByName` let a hand-written Go type implementing `Lens` be registered under a name for full get+put control; none ship pre-registered.

## Next

- **Public put for interpreted lenses** — the interpreter's put (`Build`) is verified correct internally, but the public `Engine.Lens(...)` adapter only wires up `Parse` (get) today; `TextRetrieve`/`Save` do not yet work on corpus/contrib lenses obtained this way.
- Byte-offset `Span` tracking and non-canonical whitespace/blank-line preservation are documented follow-ons.

Quality is a standing gate: 100% coverage including error branches, `gofmt` + `go vet` clean, CI green across the six 64-bit Go targets (amd64, arm64, riscv64, loong64, ppc64le, s390x).
