# zhangming-kimi-claw-packages-20260330
Private delivery assets for Kimi Claw skills and backup package

## 2026-04-30 refresh

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
8ef22ac583817610640beae93d3cff9178de65a8f553c4b6f644bd8514d9e0e2  rizaoli-kimi-claw-code-20260430.zip
7659d68d527dea8f8f5ae489a1133fd1c3609aac389324a19ad3227f8fc7cef2  rizaoli-kimi-claw-data-20260430.zip
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
