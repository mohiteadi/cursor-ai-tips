# Troubleshooting Common Cursor Issues

> Solutions from Reddit and forum community.

---

## 1. "Connection Failed" Error

### Root Cause
NOT a network issue! Serialization bugs with large data packets.

### Fix
```
1. Open new chat (Cmd+L)
2. Settings → Disable HTTP/2
3. Keep conversations < 20 messages
```

---

## 2. "Stuck Generating" / Infinite Loading

### Root Cause
Model fails to send termination signal, context too large.

### Fix
```
1. Press Escape
2. Cmd+N for new Composer
3. Use "Single Purpose Composer" pattern - one task per window
```

---

## 3. Agent Deleting Files

### Root Cause
Agent decides recreate is easier than edit.

### Fix
```bash
# Always commit before Agent mode
git add -A && git commit -m "checkpoint"

# Use explicit instructions
"Edit src/UserService.ts - do NOT delete and recreate"
```

---

## 4. AI Ignoring .cursorrules

### Fix
```
1. File must be in project root
2. Restart Cursor after changes
3. Start new chat
4. Consider migrating to .mdc files
```

---

## 5. Slow/Stuck Indexing

### Fix
```
# Add .cursorignore
node_modules/
dist/
.git/
*.log
coverage/

# Reset index
Cmd+Shift+P → "Cursor: Clear Codebase Index"
```

---

## 6. High Token Usage

### Fix
```
1. Set spending limits in API dashboard
2. Use "Auto" model selection
3. Start fresh chats (old messages use tokens)
4. Use Kimi k2 for routine tasks
```

---

## 7. Diff View Empty

### Fix
```
1. Click away and back
2. Check git status for actual changes
3. Restart Cursor if persists
```

---

## Quick Fixes

| Problem | Fix |
|---------|-----|
| Connection Failed | New chat |
| Stuck Generating | Cmd+N |
| Files Deleted | Checkpoint restore |
| Rules Ignored | Restart Cursor |
| Slow Indexing | Add .cursorignore |
| High Usage | Set limits |

---

## Prevention Checklist

- [ ] Commit before Agent mode
- [ ] Keep chats < 20 messages
- [ ] Use .cursorignore
- [ ] Set API spending limits
- [ ] Restart after config changes
