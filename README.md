# Conquistar — free public beta

Conquistar gives Codex a bounded TypeScript task, checks proposed changes, and leaves local installation in your hands.

This repository distributes packaged releases, documentation and corresponding public dependency sources. The proprietary Conquistar source repository is private. GitHub-generated “Source code” archives for this repository contain documentation, not the Conquistar implementation.

## Download

[Download the Windows x64 ZIP](https://github.com/ShavitR/querais-conquistar/releases/download/v0.1.0-beta.1/conq-0.1.0-rc.1-windows-x64.zip) · [Checksums](https://github.com/ShavitR/querais-conquistar/releases/download/v0.1.0-beta.1/SHA256SUMS.txt)

Free public beta, build **0.1.0-rc.1**, 130,010,533 bytes. No payment or Conquistar account. Codex/model usage and Docker Desktop requirements or charges are separate.

[Corresponding third-party verifier sources](https://github.com/ShavitR/querais-conquistar/releases/download/v0.1.0-beta.1/conq-verifier-source-4c2f5097be1ee269.zip) are available at no charge beside this exact binary. Public Rust dependency sources and notices are included in the product ZIP. This does not grant an open-source license to proprietary Conquistar files.

## Install

1. Use Windows 11 x64 with Docker Desktop running Linux containers and Codex installed, signed in and eligible for your chosen model.
2. Compare the ZIP's SHA-256 with `SHA256SUMS.txt`, using `Get-FileHash -Algorithm SHA256`. The package is unsigned; a matching checksum confirms bytes, not a publisher signature.
3. Extract the complete ZIP into a new, short local folder you own. Do not extract over an old version. Keep documentation/source downloads outside the extracted runtime folder: its integrity check refuses extra files.
4. Run `START-CONQ.cmd`, or run `./conq.cmd onboard` from that folder.
5. Open the exact starter project printed by onboarding in Codex, complete its trust prompt, and use the printed first request.
6. Review the accepted change. Installation is explicit: `./conq.cmd work install "WORK-PATH"`, using the actual printed path.

See `INSTALLATION.md`, `TASK-PROFILE.md`, `DATA-HANDLING.md` and `SUPPORT.md` inside the ZIP. Older candidate-distribution statements in packaged documentation are superseded by this public beta release and BETA-LICENSE.txt. All runtime bytes remain those of the tested candidate.

## Scope

Selected existing TypeScript modules, explicit finite behavior cases, and local installation of one accepted file. This beta does not verify whole applications, perform atomic multi-file installation, deploy applications, guarantee correctness or promise economic savings. There is no automatic updater. Review changes and keep backups.

The package has source/build regression checks, clean Windows portable startup checks and actual Docker workflow/boundary checks. Codex desktop interaction in an independent clean Windows guest remains unobserved.

## License and support

[BETA-LICENSE.txt](BETA-LICENSE.txt) grants no-charge use of this delivered beta, including your own commercial work. No automatic conversion to a paid plan. Third-party licenses retain their own terms.

Support: contact@querais.xyz. Include the version and a redacted description; do not send credentials or private task stores. No response-time commitment is made.
