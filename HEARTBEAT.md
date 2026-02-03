# HEARTBEAT.md

## Periodic Tasks

### 🧠 Brain Backup (every 12 hours or on-demand)
Check if there are uncommitted changes in the workspace. If so, commit and push to GitHub.

**Schedule:** Only check during heartbeat polls (every 12 hours), not every poll.

**On-Demand:** User can say "backup workspace" or "commit changes" anytime.

```bash
git add -A
git diff --cached --quiet || git commit -m "Auto-backup $(date +%Y-%m-%d\ %H:%M)"
git push
```

Track last backup in memory/heartbeat-state.json. Only backup if:
- 12+ hours since last backup, OR
- User explicitly requests it

**Cost Optimization:** Reduced from every 10min to 12hr saves ~99% of heartbeat token usage.
