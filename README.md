# zhangming-kimi-claw-packages-20260330
Private delivery assets for Kimi Claw skills and backup package

## 2026-04-30 refresh

Updated again after diagnosing the Feishu document backfill stall:
- Daily 00:30 sync intentionally writes local backup/Bitable first and queues doc writes.
- Daily doc backfill now prioritizes newest pending videos and moves failed/rate-limited items behind normal pending items, so one old failed video no longer blocks newer entries.
- Dry-run backfill no longer writes the daily dedupe stamp.

Baseline:
- Original delivery tag: `v2026-03-30` / commit `c2093d3`
- Original local packages: `zhangming-kimi-claw-skills.zip` and `zhangming-kimi-claw-backups.zip`

New packages:
- `rizaoli-kimi-claw-code-20260430.zip`
  - Current source for `douyin-transcribe-to-feishu`
  - Query/write skills: `knowledge-writer`, `video-knowledge-query`, `knowledge-base-query`, `knowledge-grounded-writer`
  - Ingest skill: `douyin-knowledge-ingest`
  - `knowledge-bases/rizaoli-douyin` profile
  - Douyin daily sync prompts
- `rizaoli-kimi-claw-data-20260430.zip`
  - `skills/douyin-transcribe-to-feishu/.local-backups`
  - required checkpoint/run/dedupe state
  - `daily-sync.env`
  - `douyin-storage-state.json`
  - `knowledge-bases/rizaoli-douyin`

Checksums:

```text
d34f934aa1c2fb09dae2ea8daeed511ab1ee7accad987e14c8b0fa1de64d2923  rizaoli-kimi-claw-code-20260430.zip
c8dffb6791c1998fb3a9e762e53cf6080e19061fe5cdd70c342d335395465b10  rizaoli-kimi-claw-data-20260430.zip
```

Kimi Linux restore outline:

```bash
cd ~/.openclaw/workspace
unzip -o /path/to/rizaoli-kimi-claw-code-20260430.zip
unzip -o /path/to/rizaoli-kimi-claw-data-20260430.zip
cd skills/douyin-transcribe-to-feishu
npm install
python3 -m pip install -r requirements.txt
bash scripts/install_scheduler_linux.sh
```

Daily runner:

```bash
cd ~/.openclaw/workspace/skills/douyin-transcribe-to-feishu
DOUYIN_SYNC_PIPELINE_MODE=skip_doc_write OPENCLAW_SKIP_NOTIFY=1 ./scripts/run_douyin_daily_sync.sh
```
