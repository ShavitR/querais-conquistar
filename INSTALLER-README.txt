Conquistar - free public beta 0.3.0-beta.1
Runtime build: 0.3.0-beta.1

INSTALL
Run Conquistar_0.3.0-beta.1_x64-setup.exe on Windows 11 x64.
Setup installs for your Windows account without administrator access in:
%LOCALAPPDATA%\Programs\Conquistar
Open Start > Conquistar > Conquistar for the get-started window.
Check your tools, select TypeScript, JavaScript, Python, Rust or Go, then choose Prepare starter.
Preparation explicitly downloads public verifier packages; Rust/Go may need over
1 GB. Actual candidate checks run offline. Preparation shows live build output,
elapsed time and a Cancel button; local logs and your work are retained on cancel. When ready, use Open project
folder and Copy first request to continue in Codex. Choose Codex.exe if automatic
discovery cannot find your installation. Command-line first run is also in Start.
The first run requires Docker Desktop running Linux containers and Codex
installed, signed in and eligible for your chosen model. Setup does not install
these prerequisites, change PATH, start model calls or add an automatic updater.
The installer is unsigned. Compare its SHA-256 with the published checksum.

This beta is free, requires no Conquistar account or payment details, and has
no automatic conversion to a paid plan. Your Codex/model and Docker terms and
any applicable charges remain separate. See BETA-LICENSE.txt.

USING THE BETA
Open the exact starter project printed by first run in Codex, complete its
trust prompt, and use the printed first request. Review the accepted change.
Installing a proposed code change is explicit; setup does not approve changes.
Tools and detailed documentation live in versions\0.3.0-beta.1.
The get-started window lets you choose a short local starter folder, defaulting to
%LOCALAPPDATA%\Conquistar\Starters\start-LANGUAGE. Keep that folder private.
LANGUAGE-WORKFLOWS.md explains existing-project admission and range edits.
Keep extra files and source downloads outside the runtime: its integrity check
refuses unexpected files outside .conq.

REINSTALL / UPDATE
Running setup again verifies and reuses the same runtime without overwriting
work. Modified or incomplete runtimes are preserved and setup refuses to replace
them: move the complete folder somewhere safe before retrying. New runtime
versions use separate folders so existing absolute Codex connections keep their
paths. Existing portable ZIP installations are left untouched; keep using their
original paths for existing work. There is no automatic migration or updater.

UNINSTALL
Use Windows Settings > Apps > Installed apps > Conquistar, or Start > Conquistar
> Uninstall. Clean, unused runtime files are removed. A version containing .conq
work is retained in full to preserve its Codex connections. Changed and unexpected
files are also retained. External projects and Docker images are not removed.
Review retained work and disconnect its Codex connections before manually deleting
its complete runtime folder. Cleanup details: %LOCALAPPDATA%\Conquistar\uninstall.log.

SCOPE / SOURCES
Bounded TypeScript JSON functions (range edits up to the 8 MiB file ceiling),
async TypeScript/JavaScript/Python JSON functions, standard-library Go packages,
and dependency-free Rust i64 functions/Cargo libraries with explicit finite
behavior cases. No remote project dependency setup or whole-project verification. Local installation changes one accepted file.
The original small TypeScript workflow remains available via conq onboard.
No whole-app correctness or
economic savings are promised. Review changes and keep backups.
Corresponding third-party verifier sources and checksums:
https://github.com/ShavitR/querais-conquistar/releases/tag/v0.3.0-beta.1
The runtime is proprietary; third-party licenses retain their own terms.
NSIS setup engine: https://nsis.sourceforge.io/ (see NSIS-COPYING.txt).
Support: contact@querais.xyz. Include the version and a redacted description;
do not send credentials or private work stores. No response-time commitment.
