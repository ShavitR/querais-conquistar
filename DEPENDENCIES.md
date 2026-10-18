# Public locked dependency beta

Prepare a language toolchain first. Dependency preparation is an explicit
networked operation producing a customer-local Docker image. Only selected
metadata and receiver-generated placeholders enter its context. Selected metadata
can include project identifiers and package script text; review it for secrets
before preparation. Project source files, separate private configuration files
and credential files are excluded. Package lifecycle scripts are disabled. Do not
publish these customer-local images: their metadata can identify your project.
Candidate checks remain fresh offline containers using an exact admitted image,
without host project mounts.

```text
conq prepare-dependencies typescript --source C:\MyProject --image sha256:EXACT_TOOLCHAIN_IMAGE --output C:\Conq\dependencies.json
```

Use the returned dependency image, preparation record and every metadata file:

```text
conq native init-language C:\Conq\work --language typescript --source C:\MyProject --file component.ts --file helper.ts --file package.json --file package-lock.json --entry component.ts --function normalize --cases C:\Conq\cases.json --image sha256:EXACT_DEPENDENCY_IMAGE --dependencies C:\Conq\dependencies.json --writable component.ts --writable helper.ts --intent "Normalize selected inputs."
```

Without `--writable`, only the entry is writable. Repeated selections must
contain the entry and only admitted source files; metadata and generated drivers
remain read-only. Reprepare after changing a lock or dependency declaration.
A record for different metadata, implementation, language or image is refused.
Foreign project/package-manager configuration is never imported.

| Language | Required root metadata | Supported boundary |
| --- | --- | --- |
| TypeScript / JavaScript | `package.json`, `package-lock.json` | npm lock v2/v3; public registry tarballs with SHA-512 integrity; at most 512 packages; no workspaces, aliases, git/file/link dependencies, bundled packages or dependency install scripts |
| Python | `requirements.lock` | 1-128 exact `name==version` requirements with SHA-256 hashes covering the whole transitive closure; universal wheels only; no source distributions, VCS/editable/URL requirements, options or included files |
| Rust with `--cargo` | `Cargo.toml`, `Cargo.lock` | One ordinary library and at most 127 checksummed crates.io dependencies; no workspaces, path/git dependencies, custom root profiles/features, build scripts or procedural macros |
| Go | `go.mod`, `go.sum` | One selected package in a public module; no replacement/exclude/workspace/toolchain directives, private modules or cgo; unchanged existing sums and exact local toolchain |

npm uses `npm ci --ignore-scripts --no-audit --no-fund`; root scripts do not run.
Root and transitive peers follow the same public-registry restrictions. Versions,
ranges and ordinary dist-tags are bound by exact lock entries/integrity; peer
declarations and optional-peer metadata must agree with the lock. Local/archive
shorthand remains outside this contract.
TypeScript keeps its fixed strict compiler configuration. Runtime and compiler
resolve the same readonly packages. JavaScript uses admitted package module
semantics, with explicit `.mjs` / `.cjs` handling.

Python downloads hash-checked universal wheels, installs with `--no-index`, and
adds the readonly dependency path explicitly. The driver retains `-I -S`;
`.pth` startup hooks are not enabled. Every transitive requirement needs a pin
and hash. Source-distribution metadata/build backends are never invoked.

Cargo vendors its locked graph without compiling. The real library compiles
later with `--frozen` and the vendor directory in the offline verifier. Dependency
build scripts/procedural macros are refused after download. The existing
`pub fn(i64) -> i64` function protocol remains.

Go fills a public module cache from copied metadata. If preparation adds missing
sums it fails; generate complete metadata outside Conquistar and retry. Offline
compilation uses `-mod=readonly`, `GOTOOLCHAIN=local`, `GOPROXY=off`, `GOWORK=off`
and `CGO_ENABLED=0`.
Private/proxy-bypass/insecure module environment overrides are explicitly cleared.

Logs and exact metadata/artifact bindings remain under `.conq/dependencies`.
Successful identical preparation replays without rebuilding. Failed/cancelled
builds never activate readiness. Cancellation stops the owned Docker client,
not Docker Desktop/shared build services; a dispatched daemon build may continue
without activating a record. Keep evidence for recovery.

Metadata is limited to 512,000 aggregate bytes. Final inventories admit at most
50,000 regular files / 512 MiB and reject links. These are post-download artifact
ceilings, not hard network, download or transient disk quotas. Package managers
may consume more transient space before inventory. Preparation has a 20-minute
client timeout. Keep enough free space and inspect retained logs on failure.

Finite cases establish only those observations for the exact source/dependencies.
Hashes bind bytes, not dependency safety or product value. The conventional
comparison is the same native locked package-manager commands inside Docker;
successful preparation alone does not demonstrate performance/economic advantage.

References: [npm ci](https://docs.npmjs.com/cli/v10/commands/npm-ci/),
[lockfile](https://docs.npmjs.com/cli/v10/configuring-npm/package-lock-json/),
[pip secure installs](https://pip.pypa.io/en/stable/topics/secure-installs/),
[pip download](https://pip.pypa.io/en/stable/cli/pip_download/),
[Cargo vendor](https://doc.rust-lang.org/cargo/commands/cargo-vendor.html),
[source replacement](https://doc.rust-lang.org/cargo/reference/source-replacement.html),
[Go modules](https://go.dev/ref/mod).
