# Contributing

## Principles

- **Pure Go, zero cgo.** The Go standard library only. Every
  interaction with the outside world goes through an injectable seam.
- **Faithful to the Augeas tree / path / lens model.**
- **100% coverage, including error branches.** New code adds its logic as pure,
  testable functions and wires I/O through seams, so tests cover both the happy
  path and every failure path with fixture injection.

## Working locally

```sh
git clone https://github.com/go-augeas/augeas
cd augeas

go vet ./...
go build ./...

COVERPKG=$(go list ./... | paste -sd, -)
go test -race -coverpkg="$COVERPKG" -coverprofile=cover.out ./...
go tool cover -func=cover.out | tail -1   # must read 100.0%
```

CI builds and tests across the six 64-bit Go targets (amd64, arm64, riscv64, loong64, ppc64le, s390x).

## License

BSD-3-Clause. By contributing you agree your work is licensed under it.
Copyright the go-augeas/augeas authors.
