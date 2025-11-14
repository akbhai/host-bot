# ⚡ Quick Setup Guide - Railway

## 3 Simple Steps

### 1️⃣ GitHub Token (2 minutes)
```
1. https://github.com/settings/tokens
2. "Generate new token (classic)"
3. ✅ Check: repo
4. Copy token → Save somewhere safe
```

### 2️⃣ Railway Deploy (1 minute)
```
1. https://railway.app
2. New Project → GitHub repo
3. Select: host-bot
4. Wait for deploy
```

### 3️⃣ Set Variables (1 minute)
Railway dashboard mein Variables tab:
```
BACKUP_METHOD=api
GITHUB_TOKEN=ghp_xxxxxxxxxxxxx
GITHUB_REPO=akbhai/host-bot
```

## ✅ Done!

Bot ab:
- ✅ Railway pe run ho raha hai
- ✅ Har 1 ghante mein automatic backup
- ✅ GitHub pe data safe

## 🔍 Check Karo

**Logs dekho:**
```
🔄 Auto-backup system started (interval: 3600s)
✅ Database backup successful via API
```

**GitHub pe dekho:**
```
https://github.com/akbhai/host-bot/tree/main/backups
```

## 📱 Bot Use Karo

Telegram pe bot ko message karo:
- `/start` - Menu
- `/backup` - Manual backup (admin only)

---

**Total Time: ~5 minutes** ⏱️

Need help? Read: [RAILWAY_DEPLOYMENT.md](RAILWAY_DEPLOYMENT.md)
