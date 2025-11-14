# Railway Deployment Guide

## 🚂 Railway Pe Bot Deploy Kaise Kare

### Step 1: GitHub Personal Access Token Banao

1. GitHub pe jao: [https://github.com/settings/tokens](https://github.com/settings/tokens)
2. **"Generate new token"** → **"Generate new token (classic)"** click karo
3. Token ko naam do: `Railway Bot Backup`
4. **Expiration**: "No expiration" select karo (ya apni choice)
5. **Permissions** select karo:
   - ✅ `repo` (Full control of private repositories) - **IMPORTANT**
6. **"Generate token"** click karo
7. Token **copy karke safe rakho** (ye sirf ek baar dikhega!)

### Step 2: Railway Pe Project Setup

1. [Railway.app](https://railway.app) pe jao aur login karo
2. **"New Project"** click karo
3. **"Deploy from GitHub repo"** select karo
4. Apna `host-bot` repository select karo
5. Railway automatically detect karega aur deploy karega

### Step 3: Environment Variables Set Karo

Railway dashboard mein:

1. Apne project pe click karo
2. **"Variables"** tab pe jao
3. Ye variables add karo:

```
BACKUP_METHOD=api
GITHUB_TOKEN=ghp_your_token_here_paste_karo
GITHUB_REPO=akbhai/host-bot
```

**Important**: `GITHUB_TOKEN` mein apna actual token paste karo jo Step 1 mein banaya tha!

### Step 4: Deploy Karo

1. Variables save karne ke baad Railway automatically redeploy karega
2. Ya manually **"Deploy"** button click karo
3. Logs check karo deployment status ke liye

## ✅ Backup System Kaise Kaam Karega

### Automatic Backup (Railway pe)

Railway pe bot run hone ke baad:

1. **Har 1 ghante mein** automatic backup hoga
2. Database file GitHub repository mein save hogi
3. Location: `backups/bot_data_YYYYMMDD_HHMMSS.db`
4. Commit message: `Auto-backup: 2024-11-14 21:30:00`

### Manual Backup

Admin commands:
- `/backup` - Instant backup trigger karo
- Admin Panel → "💾 Backup to GitHub" button

### Backup Files Location

GitHub repository mein ek naya folder banega:
```
host-bot/
├── backups/
│   ├── bot_data_20241114_213000.db
│   ├── bot_data_20241114_223000.db
│   └── bot_data_20241114_233000.db
├── main.py
└── ...
```

## 🔧 Configuration Options

### Backup Interval Change Karna

`main.py` mein edit karo:
```python
BACKUP_INTERVAL = 3600  # 1 hour (seconds)
```

Options:
- `1800` = 30 minutes
- `3600` = 1 hour (default)
- `7200` = 2 hours
- `21600` = 6 hours
- `86400` = 24 hours

### Backup Disable Karna

Railway variables mein:
```
GITHUB_BACKUP_ENABLED=False
```

Ya `main.py` mein:
```python
GITHUB_BACKUP_ENABLED = False
```

## 📊 Logs Check Karna

Railway dashboard mein:
1. **"Deployments"** tab pe jao
2. Latest deployment click karo
3. **"View Logs"** click karo

Backup logs dikhenge:
```
🔄 Auto-backup system started (interval: 3600s)
Starting GitHub API backup...
✅ Database backup successful via API: 2024-11-14 21:30:00
```

## 🔍 Troubleshooting

### Backup Nahi Ho Raha

**Check karo:**
1. `GITHUB_TOKEN` sahi set hai?
2. Token mein `repo` permission hai?
3. `BACKUP_METHOD=api` set hai?
4. `GITHUB_REPO` format sahi hai? (`username/repo`)

**Logs mein dekho:**
```
❌ GITHUB_TOKEN not set. Cannot backup via API.
```
→ Token add karo Railway variables mein

```
❌ API backup failed: 401
```
→ Token invalid hai, naya token banao

```
❌ API backup failed: 404
```
→ Repository name check karo

### Database File Nahi Mil Raha

Railway pe database file `inf/` folder mein save hoti hai. Agar folder nahi hai to automatically ban jayega.

### Token Expire Ho Gaya

1. Naya token banao (Step 1 repeat karo)
2. Railway variables mein update karo
3. Redeploy karo

## 🎯 Best Practices

### 1. Token Security
- Token ko kabhi code mein hardcode mat karo
- Sirf Railway environment variables mein rakho
- Token ko regularly rotate karo (har 6 months)

### 2. Backup Monitoring
- Regular logs check karo
- Backup files GitHub pe verify karo
- Agar backup fail ho to turant fix karo

### 3. Storage Management
- Purane backups manually delete kar sakte ho
- Ya GitHub Actions se automatic cleanup setup karo

## 📱 Local Testing (Optional)

Agar local pe test karna hai:

1. `.env` file banao:
```bash
BACKUP_METHOD=git
```

2. Bot run karo:
```bash
python main.py
```

Local pe Git method use hoga, Railway pe API method.

## 🆘 Support

Agar koi problem ho to:
1. Railway logs check karo
2. GitHub token permissions verify karo
3. Repository access check karo

## 📝 Summary

Railway pe deploy karne ke liye:
1. ✅ GitHub token banao (repo permission ke saath)
2. ✅ Railway pe project deploy karo
3. ✅ Environment variables set karo
4. ✅ Automatic backup start ho jayega!

**Backup location**: `https://github.com/akbhai/host-bot/tree/main/backups`
