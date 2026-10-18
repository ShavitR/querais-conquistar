# Bounded multi-file installation and recovery

Native schema 2 can replace 2–64 existing admitted writable UTF-8 files after exact receiver acceptance. The existing single-file installer and legacy adapter retain their existing semantics. No file creation, deletion, rename, directory replacement, worker installation tool or filesystem-wide atomicity is added.

The operator reviews `conq native deliver WORK`, then runs `conq native install WORK`. The transaction binds a sorted replacement set, every original/result file hash, the complete admitted source hashes, exact candidate and receiver decision to one native effect and one fresh authority debit. Every replacement is preceded by fresh acceptance and a full expected-checkout comparison. All replacement and original-byte stages are prepared and flushed before the first replacement. Other applications can observe the intermediate tree; close editors/builds while installing.

The shared checkout coordinator lock serializes cooperating installers. Its durable `.conq/install/transaction.json` marker blocks other Conq Works, including the legacy/single-file path, until an active transaction is reconciled. A process can stop after recording its Work intent or native effect but before persisting this shared marker. No checkout source bytes have changed and no installation dispatch has occurred at that point; a separately authorized Work may proceed until the marker exists. Cross-Work blocking starts when the marker is persisted. Existing pre-upgrade pending single-file effects without this marker must be reconciled using their original runtime before starting another Work against the checkout. Path checks reject links/reparse points; they do not establish a filesystem compare-and-swap against a hostile local account.

## Failure during the live attempt

The original running operation can conditionally roll back files already replaced. Each rollback requires current acceptance and the exact expected entire admitted checkout. An external edit to any admitted file, authority revocation, expired evidence, changed stages or an unreadable path stops compensation. Unexpected bytes are never overwritten or silently deleted. A sharing/replace failure followed by complete restoration records `failed_settled`. An incomplete/conflicting tree retains a pending effect and recovery artifacts.

## Process crash and explicit reconciliation

Run:

```text
conq native install-status WORK
conq native install-reconcile WORK
```

Both commands leave checkout source bytes untouched. Status validates the stored manifest and every original/result recovery blob, reports exact per-file current hashes and artifact paths, and indicates `original`, `candidate`, `mixed`, `conflict` or `unreadable`. Reconciliation may record native/journal metadata; it never executes a previous debit or finishes/restores a file.

For a still-pending native effect, an exact complete result settles `succeeded`; an exact restored baseline settles `failed_settled`. A mixed/conflicted/unreadable tree remains pending and blocks another operation. Preserve the Work, recovery manifest and blobs under `WORK/installations/OPERATION/`. Review the per-file status, manually restore the intended original files using the named hash-checked original blobs, then reconcile. Do not overwrite independent edits: preserve them separately and resolve them deliberately before restoration.

Repeating `install` after a crash performs only this reconciliation. It never replays mutation. A changed candidate or new decision cannot bypass the old pending intent. An already recorded native `indeterminate` outcome is immutable; manual restoration cannot rewrite it to success. Such a Work remains blocked and requires operator investigation. Historical success remains historical if the checkout is later edited; status reports the current state separately.

`failed_settled` also consumes the recorded operation: repeating the same candidate/decision is a read-only replay, not a retry. After resolving the original cause and restoring the intended baseline, admit a new Work for a new installation attempt. Losing a settlement response never triggers rollback after a potentially recorded native success; the next invocation inspects and reconciles exact state.

Preparation writes durable recovery data before native intent recording. A crash between native preparation and its local checkpoint can leave an unrecorded effect identifier but no modified source. Reconciliation rebinds the exact operation request to discover/record that intent; this is metadata-only and does not authorize dispatch. Interrupted stages and recovery artifacts are preserved; remove them only after reviewing their ownership and hashes.

## Durability and evidence limits

Stages use exclusive creation, readback hashes, `flush` and `os.fsync`; journals use SQLite synchronous FULL. These mechanisms support the tested process-crash semantics. They do not establish whole-tree power-loss durability, distributed exactly-once execution, isolation from arbitrary editors, ACL/alternate-stream preservation or filesystem-wide atomic visibility. Windows sharing violations and permission failures are reported and conditionally compensated as described above.

Focused regression: `python -B -m unittest integrations.repository_native.tests.test_multi_install integrations.repository_native.tests.test_install_v2 integrations.repository.tests.test_install -v`. The multi-file suite uses real receiver decisions, real child-process termination at individual transaction checkpoints, multi-Work exclusion, conflicts, revocation, changed recovery blobs/stages, conditional rollback and immutable indeterminate outcomes. A symbolic-link test explicitly skips if the local Windows account lacks that facility; the skip is not evidence of Windows reparse-path qualification.
