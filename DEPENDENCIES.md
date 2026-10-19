# Public locked dependency beta

## Declared local graphs in 0.5

Schema 3 can bind explicit local package members in addition to public packages.
Repeat `--member packages/NAME` during dependency preparation; repeat
`--member path:package-name:relative-source-entry` during native admission. Only
selected root/member metadata enters preparation. Source files remain outside the
networked context. Inspect selected metadata for identifiers, script text and
secrets before preparing a customer-local image.

npm graphs require a private root, an exact explicit workspace list and v3 lock.
Local dependencies use the exact declared member version or `*`. Validated local
links are removed before the regular public-artifact inventory and recreated only
inside the confined offline source build. General exports/imports, lifecycle
scripts, arbitrary user configuration and build plugins are outside this contract.
TypeScript uses one fixed strict CommonJS source build, not general `tsc -b` or
project-reference semantics.

Cargo graphs use a virtual workspace with resolver 2/3, explicit ordinary library
members, concrete manifests/root lock and confined local path dependencies. Build
scripts and procedural macros remain refused. Go supports selected subpackages
inside one root module, without cgo or external path replacement. Python uses
explicit nonambiguous source roots; it does not install local editable packages or
execute build backends. The language guide contains concrete admission commands.

Preparation records bind their helper implementation fingerprint. Keep existing
0.4 Work, records and runtime together; installing 0.5 does not migrate them or
establish fresh acceptance. For new 0.5 admission, explicitly reprepare under the
new runtime after selecting its metadata and graph. Do not edit record hashes or
reuse historical acceptance to bypass the new binding.

## Original public-lock contract

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

With repeated `--file` flags, omitting `--writable` makes only the entry writable;
repeated writable flags must include the entry and only admitted source files.
A schema 3 `--selection PATH` can instead select only writable helpers, leaving
the entry read-only. In every form, metadata and generated drivers
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
