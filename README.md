# Conquistar — free public beta

Give Codex a bounded TypeScript, JavaScript, Python, Rust or Go task, check proposed changes, and review what gets installed.

This repository distributes packaged releases, documentation and corresponding public dependency sources. Proprietary Conquistar source remains private. GitHub-generated source archives for this repository contain documentation, not the implementation.

## Install

[Install for Windows 11 x64](https://github.com/ShavitR/querais-conquistar/releases/download/v0.3.0-beta.1/Conquistar_0.3.0-beta.1_x64-setup.exe) · [Checksums](https://github.com/ShavitR/querais-conquistar/releases/download/v0.3.0-beta.1/SHA256SUMS.txt)

Free beta **0.3.0-beta.1**, 130,212,108 bytes. No payment details or Conquistar account. Model access and Docker Desktop terms and any applicable charges remain separate.

Installer SHA-256: `b383fb236b82634ca90c1f4785f6bf53b182344140c55c608669ee47186b35df`

1. Install Docker Desktop with Linux containers, and Codex. Sign in to Codex using your own eligible access. Conquistar setup does not install prerequisites, start model calls, change PATH or request administrator access.
2. Compare the download with SHA256SUMS.txt using `Get-FileHash -Algorithm SHA256 .\Conquistar_0.3.0-beta.1_x64-setup.exe`. Setup is unsigned; checksums confirm bytes, not publisher identity.
3. Run setup, then open **Start > Conquistar > Conquistar**. Check or locate your tools, select TypeScript, JavaScript, Python, Rust or Go, and choose **Prepare starter**. This explicit preparation downloads public verifier packages; Rust/Go may require over 1 GB. Actual candidate checks run offline.
4. Use **Open project folder** and **Copy first request**. Open that exact folder in Codex, accept its normal trust prompt, and paste the request. Preparation checks installed Codex tool discovery without starting a model request or changing global settings.
5. Review the accepted change. From the runtime folder, explicitly run `conq.cmd native deliver "WORK-PATH"` and `conq.cmd native install "WORK-PATH"`. Workers cannot call install.

The default starter location is `%LOCALAPPDATA%\Conquistar\Starters\start-LANGUAGE`; select another short local folder in the get-started window. Tools and guides are in `%LOCALAPPDATA%\Programs\Conquistar\versions\0.3.0-beta.1`. [LANGUAGE-WORKFLOWS.md](LANGUAGE-WORKFLOWS.md) explains existing-project admission, exact byte edits and supported interfaces. The original small TypeScript workflow remains available through `conq.cmd onboard` and `conq.cmd work`. Keep extra files outside the runtime, except private mutable state under `.conq`.

## Scope

Async TypeScript/JavaScript JSON functions, async Python standard-library functions (including explicit packages), Go standard-library packages, and dependency-free Rust `pub fn(i64) -> i64` functions or Cargo libraries. No remote project dependency setup, whole-app verification, deployment, atomic multi-file installation or economic savings are promised. Checks cover the finite cases supplied by the operator. Review changes and keep backups.

Version 2 range edits bind exact candidates, whole-file hashes and old byte-range hashes. Engineering ceilings are 8 MiB per file, 64 MiB aggregate and 4,096 admitted files. A real 8 MiB typed table with 179,389 records passed repair and exact installation at about 1.3 GB peak container memory. A separate roughly 140,000-export stress case compiled but failed Node module loading with a stack-limit error; that limitation is retained. The byte ceiling does not promise every large program will run. Installation atomically replaces one accepted writable file and refuses conflicting local edits or stale/revoked evidence.

## Reinstall and uninstall

Setup shows live build output and elapsed time, lets you choose a short starter folder, and supports cooperative cancellation with retained logs. Setup reuses a healthy same-version runtime and preserves saved work. This new installer refuses selecting an older version over a newer installation; previously published installers keep their original behavior. It refuses to overwrite modified/incomplete runtimes. New versions live side by side so older Codex connections keep their paths. There is no automatic updater or migration.

Uninstall through Windows Settings or the Start Menu. A runtime containing `.conq` work is retained in full. Changed and unexpected files, external projects and Docker images are preserved. Review retained work and disconnect its Codex connections before removing a runtime manually. Cleanup details: `%LOCALAPPDATA%\Conquistar\uninstall.log`.

## Verification and sources

332 integration tests, strict JSON/import controls, and real Go/Cargo package and language/size controls passed. The packaged runtime passed real Codex discovery and MCP repair → verification → delivery → explicit installation → replay in all five languages, with zero model calls. Revocation, receipt/blob corruption, concurrent edits and process crashes before/after replacement were checked.

This installer passed 50 offline clean-user Windows guest checks, including actual 0.2.0-beta.1 upgrade across runtime folders, work preservation, reinstall/refusal/uninstall, missing prerequisites, the five-language selector, log/folder controls, newer-version refusal, small-screen scrolling and 150/200% geometry scaling. Native controls were exercised off-screen in the disposable guest. Geometry scaling does not change physical monitor DPI. Host checks used already installed Docker/Codex; full prerequisite installation and desktop interaction on a separate clean machine remain unobserved.

[Corresponding bundled verifier sources](https://github.com/ShavitR/querais-conquistar/releases/download/v0.3.0-beta.1/conq-verifier-source-4c2f5097be1ee269.zip) are supplied at no charge. The embedded native binaries, Python and bundled TypeScript image are unchanged from the qualified base. Exact public Rust dependency sources/notices are inside the runtime. Optional language toolchains are built locally from pinned public bases using a generated-Dockerfile-only context; no private project source enters image layers. Upstream licenses retain their terms. NSIS engine notices are in NSIS-COPYING.txt.

## License and support

[BETA-LICENSE.txt](BETA-LICENSE.txt) grants no-charge use of this delivered beta, including your own commercial work, with no expiry or automatic paid conversion.

Support: contact@querais.xyz. Include the version and a redacted description; do not send credentials or private Work stores. No response-time commitment.
