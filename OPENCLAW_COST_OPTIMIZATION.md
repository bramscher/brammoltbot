# OpenClaw Cost Optimization Guide

**Goal:** Reduce AI API costs by 70-90% while maintaining quality for complex work.

## Changes Made

### 1. Heartbeat Frequency
- **Before:** Every 10 minutes
- **After:** Every 12 hours or on-demand only
- **Savings:** ~99% reduction in heartbeat token usage

## Recommended Gateway Config Changes

### 2. Model Routing (Most Important)

**Current Setup:**
```yaml
# You're using Sonnet 4.5 for everything
model: anthropic/claude-sonnet-4-5
```

**Optimized Setup:**
```yaml
# Default to Haiku (10x cheaper)
model: anthropic/claude-haiku-4-5

# Use Sonnet only when needed
thinking: off  # Already optimized ✅
```

**When to Override:**
- Building apps → `/model sonnet` or `/model opus`
- Complex architecture → User explicitly asks
- Routine work → Stays on Haiku

### 3. Context Management

**Add to config (if not present):**
```yaml
# Compact context more aggressively
compaction:
  enabled: true
  targetTokens: 50000  # Keep context tighter
  minMessageAge: 10     # Compact older messages faster
```

### 4. Session Timeouts

```yaml
# Clear inactive sessions faster
session:
  timeoutMinutes: 120  # 2 hours instead of indefinite
  maxContextTokens: 100000  # Cap context size
```

### 5. Heartbeat Config

```yaml
# Reduce heartbeat frequency
heartbeat:
  enabled: true
  intervalMs: 43200000  # 12 hours (was ~600000 = 10min)
  prompt: "Read HEARTBEAT.md if it exists..."
```

## How to Apply Changes

### Option 1: Via Gateway Config File

**Find your config:**
```bash
# Usually at:
~/.openclaw/config.yaml
# or
/etc/openclaw/config.yaml
```

**Edit the file:**
```bash
nano ~/.openclaw/config.yaml
```

**Add/modify:**
```yaml
agents:
  main:
    model: anthropic/claude-haiku-4-5  # Change default
    thinking: off
    
heartbeat:
  intervalMs: 43200000  # 12 hours
  
compaction:
  enabled: true
  targetTokens: 50000
```

**Restart gateway:**
```bash
openclaw gateway restart
```

### Option 2: Via Gateway API

**Apply config patch:**
```bash
curl -X POST http://localhost:8181/api/gateway/config/patch \
  -H "Content-Type: application/json" \
  -d '{
    "agents": {
      "main": {
        "model": "anthropic/claude-haiku-4-5"
      }
    },
    "heartbeat": {
      "intervalMs": 43200000
    }
  }'
```

**Then restart:**
```bash
openclaw gateway restart
```

## Model Aliases for Quick Switching

**In conversation, you can always override:**
```
You: "Build me an app (use Sonnet)"
You: "/model sonnet"  → Switches to Sonnet for session
You: "/model opus"    → Premium tier when needed
You: "/model haiku"   → Back to cheap default
```

## Cost Comparison

**Old Setup (Sonnet always):**
- 115k tokens/day × $10/1M avg = **~$1.15/day**
- **~$35/month**

**Optimized (Haiku default, Sonnet when needed):**
- 100k tokens/day × $1/1M (Haiku) = **~$0.10/day**
- 15k tokens/day × $10/1M (Sonnet for building) = **~$0.15/day**
- **Total: ~$0.25/day = $7.50/month**

**Savings: ~78%**

## What Gets Cheaper

✅ **Haiku handles well:**
- File operations (read/write/edit)
- Git commits
- Simple questions
- Code execution
- Heartbeats
- Status checks
- Memory searches

⚠️ **Still use Sonnet/Opus for:**
- Building new apps
- Complex architecture decisions
- Writing documentation
- Strategic planning
- Debugging complex issues

## Monitoring Usage

**Check current usage:**
```
/status
```

**Shows:**
- Current model
- Tokens used this session
- Cost estimate
- Context size

## On-Demand Backup

**Instead of automatic every 10min, just say:**
- "Backup workspace"
- "Commit my changes"
- "Push to GitHub"

I'll do it immediately, no scheduled waste.

## Next Steps

1. **Update gateway config** with model: haiku default
2. **Restart gateway** to apply changes
3. **Test** - I'll still work great for routine stuff
4. **Override when needed** - `/model sonnet` for complex work
5. **Monitor savings** - Check billing next week

---

**Bottom Line:** You'll save ~$25-30/month while keeping full power available when you need it. Haiku is fast and smart for 80% of tasks, Sonnet is there for the heavy lifting.

Let me know if you want help applying the config changes!
