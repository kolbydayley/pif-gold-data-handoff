# PIF gold data — private handoff

This private repository holds a September 8, 2026 data snapshot as a release asset.
The public code is at https://github.com/kolbydayley/pif-factory/tree/codex/signal-desk-agent-handoff .

## Download

Authenticate as Kolby or as a GitHub user explicitly granted access, then:

```sh
gh release download gold-snapshot-2026-09-08 --repo kolbydayley/pif-gold-data-handoff --dir pif-gold-download
cd pif-gold-download
shasum -a 256 -c SHA256SUMS
```

The archive contains the original relative `work/signal-desk-rebuild/` layout,
the benchmark fixtures, authored gold, revisions and experiments, audit outputs,
provider/exit receipts, and consistent backups of included SQLite databases.
The comprehensive project handoff is included in `docs/signal-desk/`.

## Required handling

- PRIVATE research material. Never commit or upload this archive to the public code repository.
- Contains validation/holdout answers and sealed-source text. Keep those paths inaccessible
  to any agent or person tuning prompts. An authorized evaluation custodian should extract
  the archive into private storage and provide development-only inputs to prompt authors.
- All existing seal rules remain binding; private GitHub access is not permission to read
  holdout answers during development. No sealed item text is printed in this README.
- Authored output is NOT accepted gold. The reliability gates described in the handoff
  have not passed. Preserve failed outputs, source hashes, and original denominators.
- This is a snapshot, not a live synchronization or full production system backup.
- Do not execute copied hooks, old process IDs, stop/resume commands, or paid workers
  automatically. Audit absolute paths before running code in a different checkout.
- Credentials and excluded runtime files are not supplied. `manifest.json` lists included
  files, hashes, backup method, and exclusions. The credential scan is bounded, not a
  guarantee that all possible secret formats have been recognized.
- Preserve copyright: transcripts are private analysis fixtures, not public redistribution.

Read the manifest before assuming any referenced external production source is present.
This export covers the gold campaign and benchmark directories, not `data/factory.sqlite`
or the entire external transcript corpus. A remote continuation may need additional
scoped inputs, but should never silently access the original machine or weaken seals.
