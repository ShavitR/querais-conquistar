# TypeScript, Python and Rust beta workflows

Open Conquistar, select a language and choose **Prepare starter**. Each language
gets a separate isolated starter. Preparation downloads public Docker toolchain
packages and may require more than 1 GB for Rust. Docker Desktop must be running
with Linux containers. No model request starts during preparation. Source checks
run in fresh offline containers without host project mounts or credentials.

The original small TypeScript workflow remains available through `conq onboard`.
The language selector uses `conq onboard --language typescript` (or `python` /
`rust`). Project-local Codex settings are created only in the owned starter;
existing foreign configuration is never replaced. CLI users can explicitly run
`conq prepare-toolchain LANGUAGE` to obtain the exact local image ID.

## Admit an existing project

Create a JSON cases file, for example:

```json
[{"id":"negative","args":[-3],"expected":-6},
 {"id":"positive","args":[21],"expected":42}]
```

After preparing the language toolchain, use its returned `image` digest:

```text
conq native init-language C:\Conq\work --language python --source C:\MyProject --file component.py --entry component.py --function twice --cases C:\Conq\cases.json --image sha256:EXACT_LOCAL_IMAGE_ID --intent "Return twice the supplied integer."
conq connect C:\Conq\work --project C:\MyProject
```

List every required source module with repeated `--file`. Select `.ts`, `.py` or
`.rs` modules; the entry is the only writable module. This admits the original
project, not a copy. Generated verification drivers are virtual, read-only files:
they do not get added to your checkout. Existing collisions with their reserved
names refuse admission or installation. Python package-relative imports work
when all required package modules are selected.

TypeScript uses strict fixed compiler options and the bundled TypeScript 5.9.3,
not project scripts or tsconfig. Python supports synchronous JSON functions and
standard-library modules. Rust initially supports dependency-free
`pub fn(i64) -> i64`, compiled with overflow checks. Cargo workspaces, pip/npm
dependency installation, async functions and general Rust JSON types are outside
this beta. An exact finite behavior check is required; exit zero alone cannot
pass it. Passing cases do not establish whole-project correctness.

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

After `conq_verify` accepts the exact candidate, the operator reviews a delivery:

```text
conq native deliver C:\Conq\work
conq native install C:\Conq\work
```

Delivery produces a small JSON manifest and exact hash-named source blobs under
the Work's `delivery` folder. Keep the manifest with its `blobs` directory.
Installation requires current acceptance and an unchanged admitted checkout;
it atomically replaces exactly one admitted writable file. Workers cannot call
install. Concurrent edits, revoked/expired authority, altered receipts and
ambiguous interrupted effects are refused. A second successful install reports
a replay without writing again. Multi-file transactional installation is not
implemented. Preserve the original package and Work together for recovery.

Optional toolchains derive from digest-pinned public official Python/Rust images
or the exact bundled public TypeScript image. Only a generated Dockerfile enters
their build contexts. Project/private repository bytes never enter image layers.
Public image references: https://hub.docker.com/_/python and
https://hub.docker.com/_/rust . Build logs and exact image IDs remain locally in
`.conq/toolchains`. Checks use the admitted local image with `--pull=never`.
