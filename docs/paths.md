# Paths & lenses

This page walks the engine's capabilities. Each is complete unless explicitly marked as a documented deferral.

## Configuration tree

An ordered tree of labelled nodes with values, built by `New()`; every entry addressable by path, with `Root`, `Label` and node insertion/removal preserving order.

## Path language

Absolute and relative paths, `*` name wildcard, `//` descendant axis, `.` / `..`, positional `[n]` / `[last()]`, value `[sub = 'v']`, regexp `[sub =~ 're']` (RE2), existence predicates, union `|`, and `$var` bindings.

## Editing API

`Get` / `Exists` / `Set` / `SetMultiple` / `Insert` / `Remove` / `Move` / `Match` / `Label` / `DefineVariable` / `DefineNode` — the full tree-mutation surface over path expressions.

## Lenses & the FileSystem seam

`Hosts`, `Fstab`, `Shellvars` / `Simplevars` and `Ini` / `Keyvalue` round-trip via `TextStore` / `TextRetrieve`; `Load` / `Save` run through an injectable `FileSystem` seam, and load failures surface under `/augeas//error`.

## Wider lens catalogue & the `.aug` DSL _( planned )_

Upstream ships ~200 lenses; this engine ships four hand-written ones. Interpreting the Augeas `.aug` lens DSL, byte-offset `Span` tracking and blank-line preservation are documented follow-ons.
