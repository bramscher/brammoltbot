# HEARTBEAT.md

## Periodic Tasks

### 🧠 Brain Backup (every few hours of use)
Check if there are uncommitted changes in the workspace. If so, commit locally.
```bash
git add -A
git diff --cached --quiet || git commit -m "Auto-backup $(date +%Y-%m-%d\ %H:%M)"
```
Only commit if there are actual changes. Track last backup in memory/heartbeat-state.json.

Note: Pushes to GitHub are manual. Bram syncs when needed.
