# Usage & API

```go
import "github.com/go-augeas/augeas"
```

```go
a := augeas.New()
lens, _ := augeas.LensByName("Hosts")
_ = a.TextStore(lens, "/files/etc/hosts", "127.0.0.1 localhost\n")

v, _ := a.Get("/files/etc/hosts/1/canonical") // "localhost"
_ = a.Set("/files/etc/hosts/1/alias", "loopback")
out, _ := a.TextRetrieve(lens, "/files/etc/hosts", nil)
```

`New` returns an empty tree. Tree mutation and query go through path expressions: `Get`, `Exists`, `Set`, `SetMultiple`, `Insert`, `Remove`, `Move`, `Match`, `Label`, `DefineVariable`, `DefineNode`. `TextStore` / `TextRetrieve` parse and serialise text through a lens, while `Load` / `Save` read and write files through the injectable `FileSystem` seam (`ReadFile`, `WriteFile`, `Glob`); load failures are recorded under `/augeas/files/<name>/error` and reachable via `/augeas//error`.

## Command line & builds

The library is `CGO_ENABLED=0` pure Go. Cross-compile it anywhere:

```sh
GOOS=linux   GOARCH=arm64    go build ./...
GOOS=js      GOARCH=wasm     go build ./...
```

It builds and tests on all six 64-bit Go targets (amd64, arm64, riscv64, loong64, ppc64le, s390x).
