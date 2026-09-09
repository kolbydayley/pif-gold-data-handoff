# PIF / Signal Desk — incoming agent handoff

Prepared for Kolby Dayley on September 8, 2026.

## Your objective

Take over investigation and planning for Signal Desk's unfinished clean-corpus/gold-data project. Kolby wants trustworthy, useful podcast-industry intelligence, not another indefinite sequence of labeling experiments. First establish the actual quality state and propose a bounded path to finish. Do not treat authored gold, valid JSON, successful provider calls, or process exits as accepted gold.

The original checkout is to remain untouched. Work in a separate clone. This handoff supplies code and a private data snapshot; it does not by itself authorize paid calls, production changes, wider access to sealed answers, or changes to the benchmark/gates.

## 1. Where everything is

### Public code

- Repository: https://github.com/kolbydayley/pif-factory
- Handoff branch: https://github.com/kolbydayley/pif-factory/tree/codex/signal-desk-agent-handoff
- Handoff branch commit at creation: `552be1ef11dfd388d724d0a79e426a16b3e93ecf`.
- Original frozen code baseline: `7f72e6bf44bfc1fcdfae93a4f033fb119bb1bd48`.
- The branch adds isolation guidance in `AGENTS.md` on top of that baseline.

Read the comprehensive 7,700-word history first:

https://github.com/kolbydayley/pif-factory/blob/codex/signal-desk-agent-handoff/docs/signal-desk/comprehensive-chat-handoff-2026-09-08.md

Also read `docs/signal-desk/repository-handoff-snapshot-2026-09-08.md` and the diagnostic documents it references. These distinguish historical claims, verified results, requirements, and unapproved proposals.

### Private data — now uploaded

- Private repository: https://github.com/kolbydayley/pif-gold-data-handoff
- Release: https://github.com/kolbydayley/pif-gold-data-handoff/releases/tag/gold-snapshot-2026-09-08
- Archive asset: `pif-gold-private-snapshot-2026-09-08.tar.gz`.
- Supporting assets: `manifest.json` and `SHA256SUMS`.

The archive contains **22,320 files**, compressed to **229,789,174 bytes** (approximately 230 MB). All archived file hashes were checked after packaging. GitHub reports the uploaded archive digest as:

```text
32342c6a90ef41f2516e9bff4c74f182e2806aba5e39d2eb6d4887627cb499a2
```

The manifest digest is:

```text
500a0659677a16f0bf88ee826385a0d4b1b4ccf343ef3f3c39a4f621be0a2181
```

The repo is PRIVATE. An agent without authenticated access will not be able to download it; that is expected, not proof the files are missing. Ask Kolby to grant the agent's GitHub integration/account access. Do not request tokens in chat or make this repository public as a workaround.

### Local locations, if working on Kolby's Mac

- Original checkout — do not mutate: `/Users/kolbydayley/pif-factory`.
- Separate working clone: `/Users/kolbydayley/pif-factory-agent`.
- Original gold root: `/Users/kolbydayley/pif-factory/work/signal-desk-rebuild/gold-authoring-v2`.
- Original benchmark root: `/Users/kolbydayley/pif-factory/work/signal-desk-rebuild/benchmark`.

Those directories are not shared merely because you clone the public code. Many scripts hard-code the original path or use `Path.home() / "pif-factory"`. Audit path resolution before running anything that can write or dispatch work.

## 2. Download and verify

Use a fresh directory, not the original checkout:

```sh
git clone --branch codex/signal-desk-agent-handoff \
  https://github.com/kolbydayley/pif-factory.git pif-factory-agent

gh release download gold-snapshot-2026-09-08 \
  --repo kolbydayley/pif-gold-data-handoff \
  --dir pif-gold-download

cd pif-gold-download
shasum -a 256 -c SHA256SUMS
```

On Linux, `sha256sum -c SHA256SUMS` is an equivalent checksum check.

**Do not immediately unpack the entire archive into an agent-readable development workspace.** It contains sealed validation/holdout answers as well as development material. An authorized evaluation custodian must isolate the sealed paths and expose only permitted development material to a prompt-tuning agent. Do not search, preview, summarize, or load sealed answers into a prompt author's context.

Preserve the archived relative layout when restoring authorized files. Do not overwrite an existing workspace or production database. The manifest lists every included path, size, hash, and backup method; read metadata first, not sealed item contents.

## 3. What the data package includes and excludes

Included source trees:

```text
work/signal-desk-rebuild/gold-authoring-v2/
work/signal-desk-rebuild/benchmark/
```

Plus the comprehensive handoff and repository snapshot documentation.

Important gold subdirectories:

- `results/development/A`, `B`, `C`, `AUDIT`: authored development passes.
- `results/development/C`: 189 JSON files were counted in the latest location check.
- `sealed-gold-results/validation` and `sealed-gold-results/sealed_holdout`: protected answers.
- `development-source-reauthor-v1/`: later repair and diagnostic families.
- `artifacts/`: audits, provenance, operational handoff, and process-exit receipts.
- `inputs/` and benchmark private-input directories: source fixtures with their original isolation boundaries.

The snapshot preserves experiment outputs, failed attempts, source revisions, provider receipts, and audit history. Included SQLite databases were copied through SQLite's backup API rather than relying on inconsistent live-file copies. Thirteen runtime lock files were excluded. The bounded credential-pattern screen did not find credential matches in included files; do not treat that as a universal secret-detection guarantee.

This is **not** a full production backup. It does not include `data/factory.sqlite`, credentials, all external corpus material, every referenced external audit database, or a live synchronization. Absolute references may point outside the package. Report missing dependencies precisely; do not silently fall back to the original machine or upload private data publicly.

## 4. Current substantive status

### Product goal

Signal Desk should answer: what changed, why it matters, where credible people disagree, and what evidence/coverage limitations deserve trust. Research paths should support issue → proposition/claim → voice → excerpt → context → original source, on mobile and desktop.

The public product has a documented evidence-first presentation release, but that release explicitly did not approve or replace the corpus. Public UI improvements and accepted data are separate milestones.

### Benchmark and model roles

- Frozen benchmark: 804 windows, 57 current shows plus 10 OOD/non-tech shows.
- Original intended roles: GLM workhorse; GPT-5.6-sol medium gold author; GPT-5.5 independent final approval.
- A/B independent authors; C adjudicates A/B; AUDIT reads source without author answers.
- Do not substitute models, shrink populations, open holdout answers, or extend grants without authority.

### Gold is NOT accepted

The retained dev reliability checkpoint covered 59 windows / 1,909 consequential events and recorded 151 critical errors: about 7.91%, with an approximately 8.99% one-sided error upper bound against a below-1% target. Agreement was about 92.09%, below the requested 95% gate. Zero confirmed catastrophes at that checkpoint did not make the dataset pass.

These are historical recorded results, not a newly recalculated score from this export. Later repairs and diagnostics did not establish full-benchmark acceptance.

### Latest bounded experiment

Family: `question-v1-recovery-rule-clarification-v1`, under:

```text
development-source-reauthor-v1/shared-rubric-qualification-v1/
  question-v1-recovery-rule-clarification-v1/
```

It changes only the source-recovery clarification, retaining 16 development windows and 64 A/B/C/AUDIT role slots. A separate question-boundary amendment is not included.

The 2026-09-08 15:25:40 UTC snapshot recorded:

- 14 raw returns; four structurally valid/authored-not-accepted; ten held.
- 35 not-started slots and 15 waiting for verified parents.
- One complete four-role window, a webpage-chrome negative control.
- `qualified: false`, `gold_accepted: false`.

Read-only counts can be checked after isolated restoration with:

```sh
python3 -B scripts/pif_signal_desk_question_status.py --family recovery
python3 -B scripts/pif_signal_desk_question_status.py --family recovery --calls
```

Verify that the script resolves to YOUR restored workspace before running it. It does not check process liveness or establish semantic approval.

The last checked worker (PID 61818, wrapper 61810) exited code 2 at 15:09:51 UTC and was absent at 15:25:40. Those are historical process IDs, not runnable instructions. Hook dispatch acceptance did not prove an idle autonomous wake. Do not restart copied hooks or assume the original machine is still idle now.

## 5. The actual blockers

1. **Contract contradictions:** assertion versus endorsement; actual transcript voice versus quoted proposition owner; source-supported versus strategically useful; questions versus asserted premises.
2. **Representation loss:** `asr_diarized` acquisition did not guarantee speaker-labeled model input. Closing host self-identification does not identify every preceding utterance.
3. **Exact-offset failures:** many role outputs are held for inexact spans. These are mechanical failures, but some of the same outputs also contain semantic errors.
4. **Adjudication duplication:** preserving every A/B input ID previously encouraged retaining duplicate semantic records. Explicit input-to-output merge/split/rejection lineage is required.
5. **Reviewer errors:** GPT-5.5 sometimes proposes unsupported or rubric-inconsistent corrections. Review proposals must be source-checked, not blindly adopted.
6. **Strategic contamination:** announcements, community invitations, show schedules, incidental biography, and sponsors can be source-grounded but useless as industry evidence.
7. **Overfitting and scope drift:** the 16 dev windows have been heavily inspected. They are regression diagnostics, not a representative untouched quality estimate. Repeated small runs became too open-ended.
8. **Unfinished acceptance dependencies:** independent per-split reliability, measured A1 gates, qualified A2 matching, and the GLM tournament remain prerequisite-bound.

Current scorer source was observed as v6, although earlier user requirements mention v5. Bind every score to the actual scorer/spec hash. Never combine scores from changed schemas, prompts, matching rules, or source representations as if they were comparable.

## 6. Recommended first actions

1. Read the comprehensive history and diagnostic documents before touching artifacts.
2. Verify the code commit, archive checksum, manifest scope, and sealed-data access boundary.
3. Inventory development outputs without running provider calls or mutating existing results.
4. Inspect the latest held development records with full permitted source context; distinguish mechanical, semantic, source-quality, and rubric defects.
5. Produce a concise decision memo: reuse versus reauthor scope, contract simplification, measurable qualification criteria, bounded iteration budget, cost/time estimate, and stop/escalation conditions.
6. Agree on that bounded plan with Kolby before another paid campaign or architectural expansion.

One previously discussed proposal is to have models select verbatim evidence and let deterministic code locate it, rejecting ambiguous matches. It could remove repeated manual-offset errors, but it is **not implemented or automatically approved**. Any trial must preserve raw outputs, exact source revisions, repeated-text ambiguity, voice/context boundaries, and independently measured semantic quality. Do not fuzzy-match fabricated evidence into something plausible.

## 7. What completion would require

- A qualified, frozen contract and source representation.
- Provenance-based reuse/reauthor strategy for the complete 804 population.
- Independent per-split audit gates with original denominators and uncertainty bounds.
- Correct handling of unknown voices, quoted owners, unsupported attributions, empty windows, ASR variants, and OOD source shapes.
- A1 measured reference ceilings with frozen derived gates; A2 qualification of the actual scorer version.
- GLM optimization and transfer checks only after prerequisites are valid.
- Shadow evaluation, final approval, coverage reconciliation, source-grounded public citations, and separate production release verification.

Do not promise an ETA from throughput alone while a quality gate remains unresolved. Report accepted-data progress, not just running jobs or returned envelopes.

## 8. Operational boundaries

- Preserve original sources, raw failed outputs, hashes, and lineage. No silent repairs or retries until a label passes.
- Do not weaken or retroactively lower gates to declare completion.
- Never guess speakers to improve apparent completeness.
- Do not restart Codex/ChatGPT hosts or kill unrelated processes.
- No changes to OpenClaw, Finance, or the original checkout.
- The copied code contains gold-exclusion integrations from shared work. Their presence does not authorize shrinking frozen benchmark denominators; review governing rules and receipts before use.
- Local historical grants and monitoring instructions are not transferable blanket spending authority.
- The original task used exit hooks plus one authorized backstop. Do not clone that live control loop into a second competing worker.

## Message from Kolby in practical terms

The user wants this finished, is frustrated with the long gold-labeling cycle, and expects an honest account of what is accepted versus merely generated. Preserve the investigation's useful findings, but do not continue the same unbounded pattern. Make the next phase measurable, finite, and clearly tied to trustworthy data that improves the product.
