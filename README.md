# Conquistar — free public beta

Give Codex a bounded TypeScript, Python or Rust task, check proposed changes, and review what gets installed.

This repository distributes packaged releases, documentation and corresponding public dependency sources. Proprietary Conquistar source remains private. GitHub-generated source archives for this repository contain documentation, not the implementation.

## Install

[Install for Windows 11 x64](https://github.com/ShavitR/querais-conquistar/releases/download/v0.2.0-beta.1/Conquistar_0.2.0-beta.1_x64-setup.exe) · [Checksums](https://github.com/ShavitR/querais-conquistar/releases/download/v0.2.0-beta.1/SHA256SUMS.txt)

Free beta **0.2.0-beta.1**, 130,199,931 bytes. No payment details or Conquistar account. Model access and Docker Desktop terms and any applicable charges remain separate.

Installer SHA-256: `92897ec3c241c5913b09333a8f3f7f36a8bb6c638ef4dfc7209f4410eae90940`

1. Install Docker Desktop with Linux containers, and Codex. Sign in to Codex using your own eligible access. Conquistar setup does not install prerequisites, start model calls, change PATH or request administrator access.
2. Compare the download with SHA256SUMS.txt using `Get-FileHash -Algorithm SHA256 .\Conquistar_0.2.0-beta.1_x64-setup.exe`. Setup is unsigned; checksums confirm bytes, not publisher identity.
3. Run setup, then open **Start > Conquistar > Conquistar**. Check or locate your tools, select TypeScript, Python or Rust, and choose **Prepare starter**. This explicit preparation downloads public verifier packages; Rust may require over 1 GB. Actual candidate checks run offline.
4. Use **Open project folder** and **Copy first request**. Open that exact folder in Codex, accept its normal trust prompt, and paste the request. Preparation checks installed Codex tool discovery without starting a model request or changing global settings.
5. Review the accepted change. From the runtime folder, explicitly run `conq.cmd native deliver "WORK-PATH"` and `conq.cmd native install "WORK-PATH"`. Workers cannot call install.

Tools and guides are in `%LOCALAPPDATA%\Programs\Conquistar\versions\0.2.0-beta.1`. [LANGUAGE-WORKFLOWS.md](LANGUAGE-WORKFLOWS.md) explains existing-project admission, exact byte edits and supported interfaces. The original small TypeScript workflow remains available through `conq.cmd onboard` and `conq.cmd work`. Keep extra files outside the runtime, except private mutable state under `.conq`.

## Scope

TypeScript JSON functions with fixed strict compiler settings, Python synchronous standard-library JSON functions (including explicit package modules), and dependency-free Rust `pub fn(i64) -> i64`. No Cargo/pip/npm dependency setup, whole-app verification, deployment, atomic multi-file installation or economic savings are promised. Checks cover the finite cases supplied by the operator. Review changes and keep backups.

Version 2 range edits bind exact candidates, whole-file hashes and old byte-range hashes. Engineering ceilings are 8 MiB per file, 64 MiB aggregate and 4,096 admitted files. The boundary control uses comment padding; it does not establish compiler performance on arbitrary large ASTs. Installation atomically replaces one accepted writable file and refuses conflicting local edits or stale/revoked evidence.

## Reinstall and uninstall

Setup reuses a healthy same-version runtime and preserves saved work. It refuses to overwrite modified/incomplete runtimes. New versions live side by side so older Codex connections keep their paths. There is no automatic updater or migration.

Uninstall through Windows Settings or the Start Menu. A runtime containing `.conq` work is retained in full. Changed and unexpected files, external projects and Docker images are preserved. Review retained work and disconnect its Codex connections before removing a runtime manually. Cleanup details: `%LOCALAPPDATA%\Conquistar\uninstall.log`.

## Verification and sources

317 integration tests, additional range/native installation checks and a real Docker language/size matrix passed. The packaged runtime passed real Codex discovery and MCP repair → verification → delivery → explicit installation → replay in all three languages, with zero model calls. Revocation, receipt/blob corruption, concurrent edits and process crashes before/after replacement were checked.

This installer passed 45 offline clean-user Windows guest checks, including actual beta.3 upgrade across runtime folders, work preservation, reinstall/refusal/uninstall, missing prerequisites, the three-language selector and small-screen scrolling. Native controls were exercised off-screen in the disposable guest. Host checks used already installed Docker/Codex; full prerequisite installation and desktop interaction on a separate clean machine remain unobserved.

[Corresponding bundled verifier sources](https://github.com/ShavitR/querais-conquistar/releases/download/v0.2.0-beta.1/conq-verifier-source-4c2f5097be1ee269.zip) are supplied at no charge. The embedded native binaries, Python and bundled TypeScript image are unchanged from the qualified base. Exact public Rust dependency sources/notices are inside the runtime. Optional language toolchains are built locally from pinned public bases using a generated-Dockerfile-only context; no private project source enters image layers. Upstream licenses retain their terms. NSIS engine notices are in NSIS-COPYING.txt.

## License and support

[BETA-LICENSE.txt](BETA-LICENSE.txt) grants no-charge use of this delivered beta, including your own commercial work, with no expiry or automatic paid conversion.

Support: contact@querais.xyz. Include the version and a redacted description; do not send credentials or private Work stores. No response-time commitment.
