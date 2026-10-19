# Bounded multi-file installation and recovery

Native schema 3 can install 1–64 explicitly granted source operations after exact
receiver acceptance: create an absent file, edit a present file, or delete a
present file. Schema 2 retains its existing-file replacement contract, and the
legacy/single-file adapter retains its previous semantics. No directory creation,
rename, file/directory substitution, worker installation tool or filesystem-wide
atomicity is added.

## Source-file grants and absence

The operator admits a fixed path universe. Each state is an exact SHA-256 digest
or null for absence; an empty file still has a real digest. `--create-path` requires
an initially absent target with existing ordinary parent directories.
`--delete-path` requires a present selected source file. Both are exact grants,
not directory-wide permission. Package metadata, generated drivers and graph
configuration remain read-only. A same-byte foreign occupant at a creation path
is a conflict, not evidence that Conquistar created it.

Creation uses a no-clobber publication primitive. Deletion checks exact bytes and
file identity before unlinking. Each operation checks the complete expected
checkout and current acceptance; external changes stop mutation. Source-file
checks reject symlinks/reparse points and unreadable parents. These checks do not
make the local account or arbitrary editors participate in an atomic filesystem
transaction.

The operator reviews `conq native deliver WORK`, then runs `conq native install WORK`. The transaction binds a sorted operation set, every original/result digest or absence, the complete admitted source state, exact candidate and receiver decision to one native effect and one fresh authority debit. Every mutation is preceded by fresh acceptance and a full expected-checkout comparison. All required original/result byte stages are prepared and flushed before the first mutation; absent states require no byte stage. Other applications can observe the intermediate tree; close editors/builds while installing.

The shared checkout coordinator lock serializes cooperating installers. Its durable `.conq/install/transaction.json` marker blocks other Conq Works, including the legacy/single-file path, until an active transaction is reconciled. A process can stop after recording its Work intent or native effect but before persisting this shared marker. No checkout source bytes have changed and no installation dispatch has occurred at that point; a separately authorized Work may proceed until the marker exists. Cross-Work blocking starts when the marker is persisted. Existing pre-upgrade pending single-file effects without this marker must be reconciled using their original runtime before starting another Work against the checkout. Path checks reject links/reparse points; they do not establish a filesystem compare-and-swap against a hostile local account.

## Failure during the live attempt

The original running operation can conditionally compensate operations already
performed. Creation compensation removes only the exact owned created file;
deletion compensation republishes the original bytes only into the expected
absent target. Edits restore their original bytes. Each compensation requires
current acceptance and the exact expected entire admitted checkout. An external
edit to any admitted file, authority revocation, expired evidence, changed stages
or an unreadable path stops compensation. Unexpected bytes are never overwritten
or silently deleted. A failure followed by complete restoration records
`failed_settled`. An incomplete/conflicting tree retains a pending effect and
recovery artifacts.

## Process crash and explicit reconciliation

Run:

```text
conq native install-status WORK
conq native install-reconcile WORK
```

Both commands leave checkout source bytes untouched. Status validates the stored
manifest and every required recovery blob, reports exact per-file current hashes
or absence, operation types and artifact paths, and indicates `original`,
`candidate`, `mixed`, `conflict` or `unreadable`. Recovery blobs exist only for
states containing bytes: creation has no original blob and deletion has no result
blob. Null is not an instruction to overwrite or delete an unrelated file.
Reconciliation may record native/journal metadata; it never executes a previous
debit or finishes/restores a file.

For a still-pending native effect, an exact complete result settles `succeeded`; an exact restored baseline settles `failed_settled`. A mixed/conflicted/unreadable tree remains pending and blocks another operation. Preserve the Work, recovery manifest and blobs under `WORK/installations/OPERATION/`. Review the per-file status, manually restore the intended original state using the named hash-checked original blobs and explicit absent-path states, then reconcile. An original absence requires deliberate removal of only the reviewed created file; the status command does not remove it. Do not overwrite independent edits: preserve them separately and resolve them deliberately before restoration.

Repeating `install` after a crash performs only this reconciliation. It never replays mutation. A changed candidate or new decision cannot bypass the old pending intent. An already recorded native `indeterminate` outcome is immutable; manual restoration cannot rewrite it to success. Such a Work remains blocked and requires operator investigation. Historical success remains historical if the checkout is later edited; status reports the current state separately.

`failed_settled` also consumes the recorded operation: repeating the same candidate/decision is a read-only replay, not a retry. After resolving the original cause and restoring the intended baseline, admit a new Work for a new installation attempt. Losing a settlement response never triggers rollback after a potentially recorded native success; the next invocation inspects and reconciles exact state.

Preparation writes durable recovery data before native intent recording. A crash between native preparation and its local checkpoint can leave an unrecorded effect identifier but no modified source. Reconciliation rebinds the exact operation request to discover/record that intent; this is metadata-only and does not authorize dispatch. Interrupted stages and recovery artifacts are preserved; remove them only after reviewing their ownership and hashes.

## Durability and evidence limits

Stages use exclusive creation, readback hashes, `flush` and `os.fsync`; journals use SQLite synchronous FULL. These mechanisms support the tested process-crash semantics. They do not establish whole-tree power-loss durability, distributed exactly-once execution, isolation from arbitrary editors, ACL/alternate-stream preservation or filesystem-wide atomic visibility. Windows sharing violations and permission failures are reported and conditionally compensated as described above.

Focused regression: `python -B -m unittest integrations.repository_native.tests.test_multi_install integrations.repository_native.tests.test_install_v2 integrations.repository.tests.test_install -v`. The multi-file suite uses real receiver decisions, real child-process termination at individual transaction checkpoints, multi-Work exclusion, conflicts, revocation, changed recovery blobs/stages, conditional rollback and immutable indeterminate outcomes. A symbolic-link test explicitly skips if the local Windows account lacks that facility; the skip is not evidence of Windows reparse-path qualification.
