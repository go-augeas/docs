# go-augeas

**Augeas configuration-tree editing in pure Go — parse, query and edit config files via lenses.**

go-augeas is a pure-Go (CGO_ENABLED=0) implementation of the core of Augeas, the configuration-editing tool from the Puppet ecosystem. It models configuration files as an ordered tree, exposes an XPath-like path language to query and edit that tree, and uses lenses to translate between the tree and concrete file syntax. A from-scratch pure-Go interpreter for the Augeas `.aug` lens DSL reads the entire embedded upstream lens corpus (232 modules — `/etc/hosts`, `/etc/fstab`, shell vars, INI and everything else upstream ships) plus five original contrib lenses (Wireguard, Rclone, Caddyfile, Nftables, Unbound); writing back through those lenses is verified correct internally but not yet exposed via the public API (see [Paths & lenses](paths.md)). Load and save go through an injectable FileSystem seam, so parsing and error branches are covered deterministically without touching the disk. It imports only the Go standard library, holds 100% test coverage, and cross-compiles to the six 64-bit Go targets and WebAssembly.

- **[Why pure Go](why.md)** — a static, cgo-free engine for the Puppet stack.
- **[Paths & lenses](paths.md)** — the capabilities in detail.
- **[Usage & API](api.md)** — the Go API and how to call it.
- **[Roadmap](roadmap.md)** — what is done and what is next.

## Guarantees

- **Pure Go, zero cgo.** Imports the Go standard library only; cross-compiles to the six 64-bit Go targets (amd64, arm64, riscv64, loong64, ppc64le, s390x) and WebAssembly, linking into a static binary.
- **Faithful to the Augeas tree / path / lens model.**
- **100% test coverage** including error branches, enforced as a CI gate.
