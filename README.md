# Conquistar — free public beta

Conquistar gives Codex a bounded TypeScript task, checks proposed changes, and leaves local installation in your hands.

This repository distributes packaged releases, documentation and corresponding public dependency sources. Proprietary Conquistar source remains private. GitHub-generated “Source code” archives for this repository contain documentation, not the implementation.

## Download

[Download the Windows installer](https://github.com/ShavitR/querais-conquistar/releases/download/v0.1.0-beta.2/Conquistar_0.1.0-beta.2_x64-setup.exe) · [Checksums](https://github.com/ShavitR/querais-conquistar/releases/download/v0.1.0-beta.2/SHA256SUMS.txt)

Free beta setup **0.1.0-beta.2**, 130,170,854 bytes. Runtime **0.1.0-rc.1**, unchanged from beta.1. No payment details or Conquistar account. Your Codex/model and Docker Desktop terms and any applicable charges are separate.

Installer SHA-256: `49d0869eb33aa45d4a21931b09bd4f379ef1395ec8bffca9f88b7d139e84af08`

[Corresponding third-party verifier sources](https://github.com/ShavitR/querais-conquistar/releases/download/v0.1.0-beta.2/conq-verifier-source-4c2f5097be1ee269.zip) are available at no charge beside this exact binary. Public Rust dependency sources and notices are included inside the installed runtime. Third-party licenses retain their own terms; proprietary Conquistar files are not open source. The NSIS setup engine is covered by NSIS-COPYING.txt in the installation folder.

## Install and start

1. Use Windows 11 x64. The workflow needs Docker Desktop running Linux containers, and Codex installed, signed in and eligible for your chosen model. Setup does not install these prerequisites or start model calls.
2. Compare the installer's SHA-256 with SHA256SUMS.txt using `Get-FileHash -Algorithm SHA256 .\Conquistar_0.1.0-beta.2_x64-setup.exe`. Setup is unsigned; the checksum confirms bytes, not a publisher signature.
3. Run setup. It installs for your own Windows account in `%LOCALAPPDATA%\Programs\Conquistar`, without administrator access or PATH changes.
4. Open **Start > Conquistar > Conquistar**. The guided command-line first run checks prerequisites and prepares a starter task.
5. Open the exact starter project printed by onboarding in Codex, complete its trust prompt and use the printed first request.
6. Review the accepted change. Installation of a code change is explicit: `conq.cmd work install "WORK-PATH"` from the runtime folder, using the actual printed path.

The setup guide is also in the Start Menu. Tools and detailed documentation are in `versions\0.1.0-rc.1`. Keep added files and source downloads outside that runtime folder: its integrity check refuses extra files outside `.conq`. Older commercial-candidate statements in bundled documentation are superseded by this free beta release and BETA-LICENSE.txt.

## Reinstall, update and uninstall

Running setup again verifies and reuses a healthy runtime without overwriting saved work. It preserves and refuses a changed or incomplete runtime; move the complete folder somewhere safe before retrying. Future runtime versions use separate folders to preserve absolute Codex connection paths. There is no automatic updater or migration. Existing [portable beta.1 installations](https://github.com/ShavitR/querais-conquistar/releases/tag/v0.1.0-beta.1) remain untouched; keep their original paths for existing work.

Uninstall through Windows Settings > Apps > Installed apps, or Start > Conquistar > Uninstall. Clean, unused runtime files are removed. A runtime containing `.conq` work is kept in full for existing connections. Changed and unexpected files are also retained. Review retained work and disconnect its Codex connections before manually deleting its runtime folder. External projects and Docker images are not removed. Cleanup details are in `%LOCALAPPDATA%\Conquistar\uninstall.log`.

## Scope and checks

Selected existing TypeScript modules, explicit finite behavior cases and local installation of one accepted file. No whole-application correctness, atomic multi-file installation, deployment or economic savings are promised. Review changes and keep backups.

Setup was checked offline in a clean Windows 11 guest under a non-administrator account: installation, package startup, missing-prerequisite guidance, shortcuts, registration, same-version reinstall, changed-runtime refusal, uninstall and work preservation passed. A previous-version fixture's paths survived setup and uninstall. This is not a second-runtime upgrade or a visual wizard test. The unchanged runtime also has source/build checks and actual Docker workflow/boundary checks. Full Docker/Codex desktop integration in an independent clean guest remains unobserved.

## License and support

[BETA-LICENSE.txt](BETA-LICENSE.txt) grants no-charge use of this delivered beta, including your own commercial work, with no automatic paid conversion.

Support: contact@querais.xyz. Include the version and a redacted description; do not send credentials or private task stores. No response-time commitment.
