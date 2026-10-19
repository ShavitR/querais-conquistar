# TypeScript, JavaScript, Python, Rust and Go beta workflows

Conquistar 0.5 adds an explicitly selected schema 3 project workflow. It can
create, edit and delete named source files and check declared local package
graphs. Existing schema 1/2 Work remains on its original contract and runtime;
upgrading does not migrate it or grant fresh authority.

For explicitly prepared public locks, see [the dependency beta contract](DEPENDENCIES.md).
The dependency-free defaults below remain available.

Open Conquistar, select a language and choose **Prepare starter**. Each language
gets a separate isolated starter. Preparation downloads public Docker toolchain
packages and may require more than 1 GB for Rust or Go. Docker Desktop must be running
with Linux containers. No model request starts during preparation. Source checks
run in fresh offline containers without host project mounts or credentials.

The original small TypeScript workflow remains available through `conq onboard`.
The language selector uses `conq onboard --language typescript` (or `javascript`, `python`, `rust` or `go`). Project-local Codex settings are created only in the owned starter;
existing foreign configuration is never replaced. CLI users can explicitly run
`conq prepare-toolchain LANGUAGE` to obtain the exact local image ID.

## Admit an existing project

Create a JSON cases file, for example:

```json
[{"id":"negative","args":[-3],"expected":-6},
 {"id":"positive","args":[21],"expected":42}]
```

CLI cases and signed profile metadata support only finite JSON integer number
tokens. Fractional tokens such as `1.25`, including whole-valued notation such
as `1.0`, are rejected during CLI admission. This does not enable a general
floating-point cases contract. For JSON-function workflows, use integer units
such as cents, decimal strings, or a serialized JSON string as the declared
argument/result; the checked function must accept and return that representation.
For example, a decimal-text function can use `args: ["1.25"]` and
`expected: "2.50"`. Rust's initial function protocol remains i64-only.

After preparing the language toolchain, use its returned `image` digest:

```text
conq native init-language C:\Conq\work --language python --source C:\MyProject --file component.py --entry component.py --function twice --cases C:\Conq\cases.json --image sha256:EXACT_LOCAL_IMAGE_ID --intent "Return twice the supplied integer."
conq connect C:\Conq\work --project C:\MyProject
```

List every required source module with repeated `--file`. Select `.ts`, `.js`/`.cjs`/`.mjs`, `.py`, `.rs` or `.go` modules; the entry is the only writable module. This admits the original
project, not a copy. Generated verification drivers are virtual, read-only files:
they do not get added to your checkout. Existing collisions with their reserved
names refuse admission or installation. Python package-relative imports work
when all required package modules are selected.

TypeScript uses strict fixed compiler options and the bundled TypeScript 5.9.3,
not project scripts or tsconfig. TypeScript and JavaScript functions may return
Promises; the driver awaits each call in order. JavaScript supports explicit
CommonJS (`.js`/`.cjs`) or ES modules (`.mjs`) and selected local imports.
Only plain JSON values pass: undefined, NaN, Infinity, sparse arrays, cycles,
custom serialization and unsafe JavaScript integer cases are refused. Finite
whole-valued JSON numbers compare using the JavaScript wire representation.
No package.json interpretation or npm dependency installation is performed.

Python supports standard-library modules, selected local packages, proper
`__init__.py` entries and async functions. The imported entry must resolve to
exactly the selected source file; cached standard-library modules cannot stand
in for it. No pip dependencies are installed.

Rust functions use dependency-free `pub fn(i64) -> i64`, with overflow checks.
For an ordinary Cargo library use `--language rust --cargo`, select root
`Cargo.toml`, `Cargo.lock` and every required Rust module with `--file`, and name
the public function in the library root. The entry remains the one writable
file. For example:

```text
conq native init-language C:\Conq\work --language rust --cargo --source C:\MyCrate --file Cargo.toml --file Cargo.lock --file src/lib.rs --file src/helper.rs --entry src/lib.rs --function twice --cases C:\Conq\cases.json --image sha256:EXACT_RUST_IMAGE_ID --intent "Return twice the supplied integer."
```

The preset builds the actual library using `cargo build --frozen --lib`, then
links the read-only driver to its compiled rlib. Dependency-free lock versions
3/4 and editions 2015/2018/2021/2024 are supported. Metadata bytes are bound at
admission. Workspaces, dependencies, features, build scripts, procedural macros,
custom profiles and general Rust JSON types are refused by this preset.

Go supports explicitly selected source files in one ordinary package, with the
standard library only. Use `--language go --go-package mathops` for a package
named `mathops`; `main` is the default. Name the actual Go function (for example,
`Twice`). The driver compiles the package using `go test -c` and calls the
function with JSON-decoded typed arguments. It accepts one JSON result or
`(result, error)`; a non-nil error fails the check. Multi-file same-directory
packages, structs and exact int64 arguments are supported. Null for a
non-nullable argument, unknown struct fields and signature mismatches fail.
Modules, remote dependencies, cgo, subpackages and candidate test files are
outside this preset. A public standard-library build cache is copied into each
fresh container; candidate outputs and caches are never shared between checks.

An exact finite behavior check is required; exit zero alone cannot pass it.
Passing cases do not establish whole-project correctness.

## Refactor a declared project (schema 3)

Declare every source input and exact creation/deletion permission. For example,
with existing `src/shop` directories and a `twice` entry in `total.py`:

```text
conq native init-language C:\Conq\work --language python --source C:\MyProject --python-root src --file src/shop/__init__.py --file src/shop/total.py --file src/shop/legacy.py --entry src/shop/total.py --function twice --cases C:\Conq\cases.json --image sha256:EXACT_PYTHON_IMAGE --writable src/shop/total.py --create-path src/shop/adjust.py --delete-path src/shop/legacy.py --intent "Move the helper into adjust.py, update total.py and remove the obsolete legacy module. Preserve the supplied behavior."
conq connect C:\Conq\work --project C:\MyProject
```

`--create-path` adds an initially absent source path to the fixed admitted
universe; its parent directory must already exist and be ordinary. `--delete-path`
names an existing selected source file. These grants also make those paths
writable. Repeat `--writable` for other existing edit targets; the entry must
remain writable. Metadata and generated drivers stay read-only. No directories,
renames, file/directory substitutions, symlinks or arbitrary new paths are granted.

In Codex, call `conq_brief` for the compact exact-candidate task. Schema 3 returns
`repository_summary` rather than the complete file manifest. Call
`conq_list_files` with the task's `candidate_id`, `offset: 0`, `limit: 128`, then
follow `next_offset` until it is null. Each row has `path` and `sha256`; null means
admitted absence, not an empty file. Every page names its candidate and complete
manifest hash. A changed candidate refuses the old page/read request. Read the
needed present file ranges with `conq_read_file`; do not read the whole tree just
because it is admitted.

Schema 3 proposals use the issued assignment/candidate bindings and a `files`
array of explicit operations:

| Operation | Required file fields |
| --- | --- |
| `edit` | `op`, `path`, exact present `base_sha256`, and the existing ordered byte `edits` |
| `create` | `op`, exact granted `path`, `base_sha256: null`, UTF-8 `content` |
| `delete` | `op`, exact granted `path`, exact present `base_sha256` |

Creation, editing and deletion are proposals only. Call `conq_verify`; acceptance
still requires the exact receiver-owned finite behavior checks. Then the operator
reviews the delivery operation list and explicitly installs it.

### Select many files without a long command

For large projects, save an exact selection JSON file outside the checkout.
Windows command lines cannot safely carry thousands of repeated file arguments.
The four keys are required; paths are project-relative and case-sensitive.

```json
{
  "files": ["src/shop/__init__.py", "src/shop/total.py", "src/shop/legacy.py", "src/shop/adjust.py"],
  "writable": ["src/shop/total.py", "src/shop/legacy.py", "src/shop/adjust.py"],
  "create_paths": ["src/shop/adjust.py"],
  "delete_paths": ["src/shop/legacy.py"]
}
```

Use `--selection C:\Conq\selection.json` instead of the repeated `--file`,
`--writable`, `--create-path` and `--delete-path` arguments in the example above.
Do not combine these forms. Selection always admits schema 3, even when both
source-operation lists are empty. Writable paths must belong to `files`; create
and delete grants must belong to `writable`. A helper-only repair can leave the
entry read-only. Declare package members, Python roots, entry, behavior cases and
the pinned image separately. Graph metadata is still added and bound read-only.
The selection file does not grant access to unlisted source paths, and the same
profile, path-count, byte and operation limits apply.

## Local package graphs

For TypeScript/JavaScript, declare every workspace member and its source entry.
Prepare the exact root/member manifests and root lock first:

```text
conq prepare-dependencies typescript --source C:\MyProject --image sha256:EXACT_TOOLCHAIN_IMAGE --output C:\Conq\workspace-deps.json --member packages/base --member packages/report
conq native init-language C:\Conq\work --language typescript --source C:\MyProject --member packages/base:@demo/base:src/index.ts --member packages/report:@demo/report:src/index.ts --file packages/base/src/index.ts --file packages/report/src/index.ts --entry packages/report/src/index.ts --function twice --cases C:\Conq\cases.json --image sha256:EXACT_DEPENDENCY_IMAGE --dependencies C:\Conq\workspace-deps.json --writable packages/report/src/index.ts --intent "Preserve the declared report behavior."
```

Member entries are relative to their member path; `--entry` is relative to the
project root. The CLI binds the selected graph metadata read-only. npm workspace
roots must be private, with explicit member paths, a v3 lock and supported
CommonJS member interfaces. Local dependency references accept the exact member
version or `*`. The receiver creates confined aliases and one strict CommonJS
source build from the currently present selected TypeScript files. This does not
implement general `tsc -b`, project references, package exports/imports, arbitrary
tsconfig, lifecycle scripts or build plugins.

Cargo graphs use explicit ordinary library workspace members, their concrete
manifests/root lock, confined local path dependencies and `--cargo-package NAME`.
The declared `--entry` must be the selected Cargo member library, even when only
a helper is writable. The existing i64 function protocol and build-script/proc-macro
refusals remain. Go can select multiple packages inside one root module;
`--go-package` identifies the checked package. A local-only module may have only
`module` and `go` directives/comments and an optional empty `go.sum`; the CLI
automatically binds this metadata. External requirements need locked dependency
preparation. Replacement, toolchain and workspace directives remain refused. Python accepts repeated explicit `--python-root` source
roots with unambiguous module/package ownership, without editable or backend
installation. See DEPENDENCIES.md for exact public-dependency restrictions.

## Edit, review and install

The version 2 profile admits up to 4,096 explicitly selected files, 8 MiB per
file and 64 MiB aggregate. These are engineering ceilings, not a promise about
every compiler input. Workers read at most 32,000 bytes per call through
`conq_read_file`; each read is bound to the current candidate. Large file text is
not included in the initial task. Version 2 proposals bind the assignment,
candidate, whole-file SHA-256, ordered UTF-8 byte ranges and SHA-256 of each old
range. Offsets count bytes, not characters. Edits are bounded independently of
source size (128 edits per file, 200,000 serialized bytes per file, 300,000 per
proposal). Unicode boundaries, CRLF and absent final newlines are preserved.

Schema 3 retains the 8 MiB/file, 64 MiB aggregate source, 64 writable-path and
proposal/range limits. Its engineering ceiling is 8,192 admitted paths and
900,000 serialized bytes for each manifest/profile; long paths can reach the byte
limit sooner. Paths include metadata, virtual support and admitted absent paths.
Manifest pages contain at most 128 rows and 32,000 serialized bytes, so a page may
be shorter than requested. Initial context stays bounded and compiler inputs are
derived from the sealed present/absent manifest instead of duplicated in support
text. Source reads remain at most 32,000 bytes, and Work operation budgets do not
increase automatically.

New schema 3 Codex connections use the sum of admitted check deadlines plus 300
seconds for receiver/acceptance handoff, at most 2,100 seconds. Schema 1/2
connections retain their 240-second setting. A longer client timeout extends no
authority lease and does not alter compiler, resource or acceptance limits.

After `conq_verify` accepts the exact candidate, the operator reviews a delivery:

```text
conq native deliver C:\Conq\work
conq native install C:\Conq\work
```

Delivery produces a small JSON manifest and exact hash-named source blobs under
the Work's `delivery` folder. Keep the manifest with its `blobs` directory.
Installation requires current acceptance and an unchanged admitted checkout.
For schema 3, it stages every required original/result byte blob before changing
the checkout, then performs the granted create/edit/delete operations sequentially
with fresh acceptance and full-checkout conflict checks. Creation cannot overwrite
an occupant; deletion requires the exact existing file. Schema 2 retains its
existing-file replacement contract. Workers cannot call install. Concurrent edits, revoked/expired authority,
altered receipts and ambiguous interrupted effects are refused. A second successful
install reports a replay without writing again. This is not a filesystem-wide
atomic transaction; preserve the original package and Work together for recovery.

Read [MULTI-FILE-INSTALL.md](MULTI-FILE-INSTALL.md), installed beside this guide
in the runtime folder, for the full recovery contract. If installation is
interrupted, inspect before attempting recovery:

```text
conq native install-status C:\Conq\work
conq native install-reconcile C:\Conq\work
```

Status checks exact checkout and recovery-artifact hashes. Reconcile never writes
the checkout: it can settle an exact completed result or exact restored baseline.
A mixed or externally changed checkout stays pending and blocks further installs.
Preserved per-file original blobs and explicit absence states support deliberate
manual restoration. Creation has no original blob and deletion has no result
blob. Never copy recovery bytes over unrelated edits or silently remove an
unreviewed occupant. Conditional rollback is limited to the original
live attempt with current authority and acceptance. Recovery does not replay a
mutation under an old authority debit.
An operation settled as FailedSettled is consumed: invoking install for that same
candidate and decision only replays its outcome. After restoring the exact
baseline, admit a new Work for another attempt. An already terminal Indeterminate
outcome cannot be rewritten by reconcile.

Optional toolchains derive from digest-pinned public official Python/Rust/Go images
or the exact bundled public TypeScript image. Only a generated Dockerfile enters
their build contexts. These base toolchain builds contain no project bytes.
Explicit dependency preparation additionally copies selected lock metadata and
receiver-generated placeholders into customer-local image contexts. Keep those
images private; see [DEPENDENCIES.md](DEPENDENCIES.md).
Public image references: https://hub.docker.com/_/python and
https://hub.docker.com/_/rust and https://hub.docker.com/_/golang . Build logs and exact image IDs remain locally in
`.conq/toolchains`. Checks use the admitted local image with `--pull=never`.
