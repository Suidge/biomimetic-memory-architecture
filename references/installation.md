# BMA Installation and Integration

BMA is installed as one integrated memory-evolution skill. It is intended to replace separate OpenCortex and Lesson-Imprint skill folders after verification.

## Preconditions

BMA assumes OpenClaw is installed and the workspace is the current directory.

Recommended companion runtime stack:

- QMD search/indexing
- LCM / lossless-claw for conversation recall
- active-memory for runtime recall
- memory-wiki bridge mode
- memory-core dreaming light/rem enabled and deep promotion disabled

Recommended memory-wiki settings:

```json
{
  "indexDailyNotes": true,
  "indexDreamReports": false,
  "indexMemoryRoot": true,
  "followMemoryEvents": false
}
```

## Install

```bash
bash skills/biomimetic-memory-architecture/scripts/install.sh
```

The installer creates the base directories and initializes Lesson-Imprint state:

```text
memory/projects/
memory/runbooks/
memory/workflows/
memory/contacts/
memory/archive/
memory-archive/reports/
memory/lesson-imprint/
memory-archive/
```

## Verify

```bash
bash skills/biomimetic-memory-architecture/scripts/verify.sh
```

The verifier checks:

- core bootstrap files
- BMA directories
- Lesson-Imprint store/config/bootstrap
- retention audit script
- cron presence when OpenClaw CLI is available
- OpenClaw doctor plugin error status when available

## Daily Distillation Cron

Use `references/daily-distillation.md` as the cron instruction body, or set the cron message to read that BMA reference file.

Daily distillation handles:

- OpenCortex-style promotion into structured memory files
- Lesson-Imprint extraction from failures/corrections
- raw daily log archive into `memory/archive/`

## Weekly Synthesis Cron

Use `references/weekly-synthesis.md` as the weekly instruction body, or set the cron message to read that BMA reference file.

Weekly synthesis handles:

- recent archive review
- structural integrity
- retrieval health
- runbook candidates
- Lesson-Imprint health
- BMA retention report review

## Lesson-Imprint Component

BMA includes Lesson-Imprint as procedural memory. It stores compact safeguards in:

```text
memory/lesson-imprint/lessons.json
memory/lesson-imprint/config.json
memory/lesson-imprint/BOOTSTRAP.md
```

CLI:

```bash
python3 skills/biomimetic-memory-architecture/scripts/lesson_imprint.py init
python3 skills/biomimetic-memory-architecture/scripts/lesson_imprint.py validate
python3 skills/biomimetic-memory-architecture/scripts/lesson_imprint.py promote
```

Raw failures and corrections remain in daily/archive logs until BMA retention metabolizes those source files.

## Retention Audit

```bash
python3 skills/biomimetic-memory-architecture/scripts/bma_retention_audit.py --workspace . --older-than-days 30
```

This writes a read-only report under:

```text
memory-archive/reports/
```

## Replacing Separate Skills

After BMA verify passes and cron messages have been updated to BMA references, the separate folders can be removed or archived:

```text
skills/opencortex/
skills/lesson-imprint/
```

Do not remove them until:

1. `scripts/verify.sh` passes.
2. Daily and weekly cron messages no longer depend on `skills/opencortex/` paths.
3. Any Lesson-Imprint cron/distillation references point to BMA's `scripts/lesson_imprint.py`.
4. You have a backup or git checkpoint.

## Safety Rules

- Do not cold-archive active Lesson-Imprint state files.
- Do not rewrite `MEMORY.md` or `AGENTS.md` for procedural lessons; use `memory/lesson-imprint/BOOTSTRAP.md`.
- Do not scan the full history by default; start with aged candidates only.
- Do not delete source files unless the user explicitly requests deletion.
