# HEARTBEAT.md

## Periodic Tasks

### 🧠 Brain Backup (every few hours of use)
Check if there are uncommitted changes in the workspace. If so, commit and push to GitHub.
```bash
git add -A
git diff --cached --quiet || git commit -m "Auto-backup $(date +%Y-%m-%d\ %H:%M)"
git push
```
Only push if there are actual changes. Track last backup in memory/heartbeat-state.json.
