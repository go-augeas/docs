# Paths & lenses

This page walks the engine's capabilities. Each is complete unless explicitly marked as a documented deferral.

## Configuration tree

An ordered tree of labelled nodes with values, built by `New()`; every entry addressable by path, with `Root`, `Label` and node insertion/removal preserving order.

## Path language

Absolute and relative paths, `*` name wildcard, `//` descendant axis, `.` / `..`, positional `[n]` / `[last()]`, value `[sub = 'v']`, regexp `[sub =~ 're']` (RE2), existence predicates, union `|`, and `$var` bindings.

## Editing API

`Get` / `Exists` / `Set` / `SetMultiple` / `Insert` / `Remove` / `Move` / `Match` / `Label` / `DefineVariable` / `DefineNode` — the full tree-mutation surface over path expressions.

## The embedded `.aug` corpus interpreter

A from-scratch, pure-Go interpreter for the Augeas lens DSL (`internal/interp`) reads the **entire embedded upstream Augeas 1.14.1 lens corpus** — all 232 modules, verbatim `.aug` sources under `lenses/dist/` — plus five original contrib lenses (`Wireguard`, `Rclone`, `Caddyfile`, `Nftables`, `Unbound`) under `lenses/contrib/`. `NewEngine().Lens(module, binding)` (e.g. `Lens("Hosts", "lns")`) returns a `Lens` usable with `TextStore` / `Get` / `Set` / `Match`; `Load` / `Save` run through an injectable `FileSystem` seam, and load failures surface under `/augeas//error`. The interpreter's own get **and** put are verified correct against the corpus's inline test assertions (1791/1791, 100%), but the public `Lens.Build` for these interpreted lenses is not yet wired up — see "Deferred" in the README for what that means for `TextRetrieve`/`Save` today.

## Writing your own lens

`Register`/`LensByName` are a pluggable seam: implement `Lens` (`Parse`/`Build`) in hand-written Go and register it under a name for full get+put round-trip control outside the interpreted corpus. No lens ships pre-registered.
