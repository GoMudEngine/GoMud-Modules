# GoMud-Modules

The official module registry and archive for [GoMud](https://github.com/GoMudEngine/GoMud). This repository hosts the `module-registry.yaml` index and the pre-built `.tar.gz` archives for all official modules.

## Installing Modules

Modules are managed through the GoMud module manager. From your GoMud server directory:

```sh
# List available modules
$ make module
> list
```

## Submitting a Module

To add a new module or update an existing one:

1. Host your module as a `.tar.gz` or `.zip` archive at a stable public URL.
2. Generate a SHA256 checksum of the archive:
   ```sh
   # Linux/macOS
   sha256sum your-module-1.0.0.tar.gz

   # Windows
   Get-FileHash your-module-1.0.0.zip -Algorithm SHA256
   ```
3. Add an entry to `module-registry.yaml` following the existing format.
4. Open a pull request. All entries are reviewed before merging.

### Archive Layout

The archive must contain Go source files at the top level (or inside a single wrapper directory that will be stripped):

```
<module-name>.go        # package declaration and init() registration
files/                  # optional: embedded data files
  datafiles/...
  data-overlays/...
```

The package name must be a valid Go identifier. Module source imports GoMud internals as:

```go
import "github.com/GoMudEngine/GoMud/internal/<package>"
```

## License

MIT - see [LICENSE](LICENSE).
