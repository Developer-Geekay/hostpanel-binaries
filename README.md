# hostpanel-binaries

Pre-vetted binaries used by HostPanel packages. Packages pull binaries from here during `on_install()` instead of bundling large files or hitting upstream directly.

## How it works

1. Trigger the **Fetch and Release Binary** workflow (`Actions → fetch-binary.yml → Run workflow`)
2. Enter package name, version, and architectures
3. The workflow downloads the official binary, strips it to the executable only, and publishes it as a GitHub release asset
4. HostPanel packages reference `releases/download/{package}-{version}/{binary}-{arch}`

## Release naming

| Release tag | Asset | Architecture |
|---|---|---|
| `mongodb-8.0.4` | `mongod-aarch64` | ARM64 (Raspberry Pi) |
| `mongodb-8.0.4` | `mongod-x86_64` | x86-64 |
| `nodejs-20.18.0` | `node-aarch64` | ARM64 |
| `nodejs-20.18.0` | `node-x86_64` | x86-64 |

## Adding a new binary

1. Add a fetch step to `.github/workflows/fetch-binary.yml` for the new package
2. Run the workflow
3. Update the package's `lifecycle.py` to reference the new release

## Download URL pattern

```
https://github.com/Developer-Geekay/hostpanel-binaries/releases/download/{package}-{version}/{binary}-{arch}
```

Example:
```
https://github.com/Developer-Geekay/hostpanel-binaries/releases/download/mongodb-8.0.4/mongod-aarch64
```
