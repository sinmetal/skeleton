# skeleton 

skeleton creates skeleton codes for a modularized static analysis tool with [x/tools/go/analysis](https://golang.org/x/tools/go/analysis) package.

## x/tools/go/analysis pacakge

[x/tools/go/analysis](https://golang.org/x/tools/go/analysis) package provides a type `analysis.Analyzer` which is unit of analyzers in modularized static analysis tool.

If you want to create new analyzer, you should provide a package variable which type is `*analysis.Analyzer`.
`skeleton` creates skeleton codes of the package and directories including test codes and main.go.

## Insall

```
$ go get -u github.com/gostaticanalysis/skeleton
```

## How to use

### Create skeleton codes in GOPATH

```
$ skeleton pkgname
pkgname
├── cmd
│   └── pkgname
│       └── main.go
├── plugin
│   └── pkgname
│       └── main.go
├── pkgname.go
├── pkgname_test.go
└── testdata
    └── src
        └── a
            └── a.go
```

### Create skeleton codes with import path

```
$ skeleton -path="github.com/gostaticanalysis/pkgname"
pkgname
├── cmd
│   └── pkgname
│       └── main.go
├── plugin
│   └── pkgname
│       └── main.go
├── pkgname.go
├── pkgname_test.go
└── testdata
    └── src
        └── a
            └── a.go
```

### Create skeleton codes without cmd directory

```
$ skeleton -cmd=false pkgname
pkgname
├── plugin
│   └── pkgname
│       └── main.go
├── pkgname.go
├── pkgname_test.go
└── testdata
    └── src
        └── a
            └── a.go
```

### Create skeleton codes without plugin directory

```
$ skeleton -plugin=false pkgname
pkgname
├── cmd
│   └── pkgname
│       └── main.go
├── pkgname.go
├── pkgname_test.go
└── testdata
    └── src
        └── a
            └── a.go
```

## Build as a plugin for golangci-lint

`skeleton` generates plugin directory which has main.go.
The main.go can be built as a plugin for [golangci-lint](https://golangci-lint.run/contributing/new-linters/#how-to-add-a-private-linter-to-golangci-lint).

```
$ skeleton pkgname
$ go build -buildmode=plugin -o path_to_plugin_dir importpath
```

If you would like to specify flags for your plugin, you can put them via `ldflags` as below.

```
$ skeleton pkgname
$ go build -buildmode=plugin -ldflags "-X 'main.flags=-funcs log.Fatal'" -o path_to_plugin_dir github.com/gostaticanalysis/called/plugin/called
```
