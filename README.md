# Conquistar — free public beta

Give Codex a bounded TypeScript, JavaScript, Python, Rust or Go task, check proposed changes, and review what gets installed.

This repository distributes releases, documentation and corresponding public dependency sources. Proprietary source remains private. GitHub-generated source archives here contain documentation, not the implementation.

## Install

[Install for Windows 11 x64](https://github.com/ShavitR/querais-conquistar/releases/download/v0.5.0-beta.1/Conquistar_0.5.0-beta.1_x64-setup.exe) · [Checksums](https://github.com/ShavitR/querais-conquistar/releases/download/v0.5.0-beta.1/SHA256SUMS.txt)

Free beta **0.5.0-beta.1**, 130,249,540 bytes. No payment details or Conquistar account. Model access and Docker Desktop terms and charges remain separate.

Installer SHA-256: `5b0a01c079eb989d53970ceab2a8ddd2e8c94ee5e6fadbbdc895db31a58e3666`

1. Install Docker Desktop with Linux containers, and Codex. Sign in to Codex using your own eligible access. Setup does not install prerequisites, start model calls, change PATH or request administrator access.
2. Compare the download using `Get-FileHash -Algorithm SHA256 .\Conquistar_0.5.0-beta.1_x64-setup.exe` and SHA256SUMS.txt. Setup is unsigned; checksums confirm bytes, not publisher identity.
3. Run setup, then open **Start > Conquistar > Conquistar**. Check or locate your tools, select a language and choose **Prepare starter**. Preparation downloads public verifier packages; Rust/Go may require over 1 GB. Candidate checks run offline.
4. Use **Open project folder** and **Copy first request**. Open that exact folder in Codex, accept its normal trust prompt, and paste the request. Preparation checks installed Codex tool discovery without a model request or global configuration changes.
5. Review accepted changes. From the runtime folder, explicitly run `conq.cmd native deliver "WORK-PATH"` and `conq.cmd native install "WORK-PATH"`. The MCP worker tools cannot install; installation is an explicit operator CLI step. Conquistar does not confine an assistant with separate unrestricted host access.

The starter defaults to `%LOCALAPPDATA%\Conquistar\Starters\start-LANGUAGE`. Choose a short local path in the window. Tools and guides are in `%LOCALAPPDATA%\Programs\Conquistar\versions\0.5.0-beta.1`. Keep extra files outside the runtime except private mutable state under `.conq`.

## Existing projects and dependencies

[LANGUAGE-WORKFLOWS.md](LANGUAGE-WORKFLOWS.md) covers selected function interfaces, range edits and admission. [DEPENDENCIES.md](DEPENDENCIES.md) explains explicit locked public npm, hash-pinned Python universal wheel, crates.io Cargo and public Go module preparation. Networked preparation uses selected metadata and generated placeholders; project source files and separate private package-manager configuration files do not enter its context. Selected metadata can contain identifiers or script text; review it for secrets. Package lifecycle scripts do not run. Keep customer-local dependency images private. Verification uses the exact admitted image in fresh offline containers. Metadata stays read-only.

Private registry packages, undeclared or unsupported workspace shapes, Python source distributions/native wheels, dependency installation scripts, Cargo build scripts/procedural macros and general whole-app verification are outside these presets. For large source selections, use the exact four-list `--selection PATH` JSON instead of thousands of command arguments. Candidate-bound manifest pages and bounded reads keep the initial task compact. Explicit declared local graphs cover private CommonJS npm workspaces, ordinary Cargo library workspaces, one Go module and unambiguous Python source roots within the documented restrictions. Old Work remains on its original runtime; new admission needs fresh verification and explicit dependency preparation with the new helper fingerprint.

The 512 MiB / 50,000-file dependency limits apply to final artifacts after download, not network or transient disk use. Failed/cancelled builds do not activate readiness. A dispatched Docker daemon build may continue after its owned client is cancelled.

## Multi-file installation and recovery

[MULTI-FILE-INSTALL.md](MULTI-FILE-INSTALL.md) explains schema 3 creation, editing and deletion of 1–64 exact admitted source paths under one accepted candidate and fresh authority debit. Creation requires an absent target and existing ordinary parent directories; metadata stays read-only. Each operation checks current acceptance and the expected entire checkout. The live attempt conditionally compensates exact owned bytes; independent edits are preserved. Operations are sequential, so other applications can observe an intermediate tree. No directory creation/rename, filesystem-wide atomicity or power-loss guarantee is added. Schema 1/2 retain their earlier contracts.

`conq native install-status WORK` reports validated original/result artifacts and current hashes. `conq native install-reconcile WORK` may settle an exact complete candidate or restored baseline; both leave checkout source untouched. Mixed/conflicted crash states require manual restoration from hash-checked artifacts. Repeating install never replays writes under an old debit. Shared cross-Work blocking starts when the transaction marker is persisted; no installation writes have dispatched before that marker. Close editors/builds while installing and keep backups.

Limits remain 8 MiB per file and 64 MiB aggregate. Schema 3 admits at most 8,192 paths and 900,000 serialized bytes per manifest/profile; long paths can bind the byte limit sooner. Metadata, virtual support and declared absence count toward the path universe. Schema 1/2 retain their earlier limits. Compiler/runtime complexity matters: the earlier 8 MiB typed-table repair passed, while a separate large exported-function stress case failed Node module loading. Finite cases establish the supplied checks, not general correctness, customer value or economic savings.

## Reinstall and uninstall

Setup shows live output and elapsed time, offers a short starter folder and cooperative cancellation, and retains logs. It reuses healthy same-version files and preserves work, while refusing modified/incomplete runtimes. Versions live side by side so old Codex connections retain their paths. This installer refuses selecting an older version over a newer installation. There is no automatic updater or Work migration.

Uninstall through Windows Settings or the Start Menu. Runtimes containing `.conq` work are retained in full. Changed/unexpected files, external projects and Docker images are preserved. Review work and disconnect its Codex connections before manually removing a runtime. Cleanup details: `%LOCALAPPDATA%\Conquistar\uninstall.log`.

## Verification and sources

Canonical integration run: 405 tests, 1 explicit skips, no failures. The runtime qualification record binds the exact archive SHA-256 to the maintained source inventory and packaged workflow observations. Its recorded scope is: Actual embedded CLI/MCP quotation workflow across12 packages with five serialized report cases and create/edit/delete; actual4096-source/4111-path graph with paged reads, wrong-output refusal, correction, verification, operator delivery/install and read-only replay; five public-dependency/schema2 multi-file workflows, five native language starters and the original schema1 starter, plus installed Codex tool discovery without account/model requests.. Finite behavior cases establish only their declared outcomes; they do not prove universal correctness, customer value or economic savings. Setup timings may use warm Docker caches; network bytes were not independently measured.

This exact installer passed the offline non-administrator Windows Sandbox check set, including published 0.4.0-beta.1 upgrade retention, reinstall/refusal/uninstall, missing prerequisites and native layout assertions. Native controls were exercised offscreen. Font/geometry scaling does not change physical monitor DPI. Full prerequisite installation and first desktop model interaction on a separate clean machine remain unobserved.

[Corresponding bundled verifier sources](https://github.com/ShavitR/querais-conquistar/releases/download/v0.5.0-beta.1/conq-verifier-source-4c2f5097be1ee269.zip) are supplied free. Embedded native binaries, Python and the bundled TypeScript image are unchanged from the qualified base. Public Rust dependency sources/notices are inside the runtime. Optional toolchains build locally; dependency preparation additionally copies selected lock metadata. Upstream licenses retain their terms. NSIS notices are in NSIS-COPYING.txt.

## License and support

[BETA-LICENSE.txt](BETA-LICENSE.txt) grants no-charge use, including your own commercial work, with no expiry or automatic paid conversion.

Support: contact@querais.xyz. Include the version and a redacted description; do not send credentials or private Work stores. No response-time commitment.
