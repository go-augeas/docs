# Roadmap

## Done

- **Configuration tree** — An ordered tree of labelled nodes with values, built by `New()`; every entry addressable by path, with `Root`, `Label` and node insertion/removal preserving order.
- **Path language** — Absolute and relative paths, `*` name wildcard, `//` descendant axis, `.` / `..`, positional `[n]` / `[last()]`, value `[sub = 'v']`, regexp `[sub =~ 're']` (RE2), existence predicates, union `|`, and `$var` bindings.
- **Editing API** — `Get` / `Exists` / `Set` / `SetMultiple` / `Insert` / `Remove` / `Move` / `Match` / `Label` / `DefineVariable` / `DefineNode` — the full tree-mutation surface over path expressions.
- **Lenses & the FileSystem seam** — `Hosts`, `Fstab`, `Shellvars` / `Simplevars` and `Ini` / `Keyvalue` round-trip via `TextStore` / `TextRetrieve`; `Load` / `Save` run through an injectable `FileSystem` seam, and load failures surface under `/augeas//error`.

## Next

- **Wider lens catalogue & the `.aug` DSL** — Upstream ships ~200 lenses; this engine ships four hand-written ones. Interpreting the Augeas `.aug` lens DSL, byte-offset `Span` tracking and blank-line preservation are documented follow-ons.

Quality is a standing gate: 100% coverage including error branches, `gofmt` + `go vet` clean, CI green across the six 64-bit Go targets (amd64, arm64, riscv64, loong64, ppc64le, s390x).
