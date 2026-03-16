# easemesh-api

`easemesh-api` contains the versioned Protocol Buffers schemas and generated artifacts for EaseMesh API resources.

This repository is the schema package, not the full EaseMesh runtime. It keeps the `.proto` source, generated Go types, and rendered reference documentation in one place so other projects can import the API definitions directly.

## What is included

- Versioned API definitions for EaseMesh resources such as `Tenant`, `Service`, `Ingress`, `Resilience`, `TrafficTarget`, and `CustomResourceKind`
- Generated Go bindings for each API version
- Generated Markdown, HTML, and JSON documentation for each API version

## Repository layout

```text
.
├── v1alpha1/
│   ├── meshmodel.proto
│   ├── meshmodel.pb.go
│   ├── meshmodel.md
│   ├── meshmodel.html
│   └── meshmodel.json
├── v2alpha1/
│   ├── meshmodel.proto
│   ├── meshmodel.pb.go
│   ├── meshmodel.md
│   ├── meshmodel.html
│   └── meshmodel.json
├── Makefile
├── go.mod
└── LICENSE
```

## API versions

- `v1alpha1`: early alpha API definitions
- `v2alpha1`: newer alpha API definitions and the default generation target in the `Makefile`

Each version directory is self-contained and includes:

- `meshmodel.proto`: source schema
- `meshmodel.pb.go`: generated Go code
- `meshmodel.md`: generated reference documentation
- `meshmodel.html`: generated HTML documentation
- `meshmodel.json`: generated machine-readable documentation

## Using from Go

The module path in `go.mod` is:

```go
github.com/megaease/easemesh-api
```

Install the module:

```bash
go get github.com/megaease/easemesh-api
```

Import the API version you need:

```go
package main

import v2alpha1 "github.com/megaease/easemesh-api/v2alpha1"

func main() {
	_ = &v2alpha1.Service{
		Name:           "orders",
		RegisterTenant: "default",
	}
}
```

## Regenerating artifacts

The repository uses `protoc`, `protoc-gen-go`, and `protoc-gen-doc` to regenerate committed artifacts.

### Requirements

- Go 1.17 or later
- `protoc`
- `protoc-gen-go`
- `protoc-gen-doc`

The helper target below checks for required tools and attempts to install missing ones:

```bash
make pre-check
```

### Common commands

Generate all outputs for the default version (`v2alpha1`):

```bash
make all
```

Generate all outputs for a specific version:

```bash
make RELEASE=v1alpha1 all
make RELEASE=v2alpha1 all
```

Generate specific artifact types:

```bash
make RELEASE=v2alpha1 go
make RELEASE=v2alpha1 md
make RELEASE=v2alpha1 html
make RELEASE=v2alpha1 json
```

Remove generated files for a version:

```bash
make RELEASE=v2alpha1 clean
```

## Updating the API

1. Edit the versioned `meshmodel.proto` file.
2. Regenerate the artifacts with `make`.
3. Review the generated `.pb.go`, `.md`, `.html`, and `.json` outputs.
4. Commit the source and generated files together.

## Reference docs

- [v1alpha1 Markdown reference](./v1alpha1/meshmodel.md)
- [v2alpha1 Markdown reference](./v2alpha1/meshmodel.md)
- [v1alpha1 HTML reference](./v1alpha1/meshmodel.html)
- [v2alpha1 HTML reference](./v2alpha1/meshmodel.html)

## License

Apache License 2.0. See [LICENSE](./LICENSE).
