<h1 align="center">⚡ FilezToLinkX Bot - Premium Edition</h1>

<p align="center">
  <img src="logo.png" alt="FilezToLinkX Logo" width="250" style="border-radius: 20px; box-shadow: 0 0 20px rgba(59,130,246,0.3);">
</p>

<p align="center">
  <b>A state-of-the-art highly concurrent Telegram File Streaming backend featuring real-time bandwidth analytics, a beautiful glassmorphic administrative dashboard, and a multi-cloning network architecture for blazing-fast downloads.</b>
</p>

<p align="center">
  <a href="https://github.com/Monster-ZeroX/FilezToLinkXBot/issues"><img src="https://img.shields.io/badge/Report%20Bug-red?style=for-the-badge&logo=github"></a>
  <a href="https://github.com/Monster-ZeroX/FilezToLinkXBot/issues"><img src="https://img.shields.io/badge/Request%20Feature-blue?style=for-the-badge&logo=github"></a>
  <img src="https://img.shields.io/badge/Python-3.11+-yellow?style=for-the-badge&logo=python">
  <img src="https://img.shields.io/badge/MongoDB-Optimized-green?style=for-the-badge&logo=mongodb">
</p>

---

## 🌟 Premium Features

- **🚀 Highly Concurrent Multi-Client Architecture**: Seamlessly scales payload deliveries across 40+ proxy bot-tokens instantly bypassing Telegram's aggressive 1469s `FloodWait` bans! (New Auto-Healing implementation ignores dead tokens gracefully).
- **📊 Real-Time Analytics Dashboard**: Monitor every byte of network traffic securely via the built-in HTTP basic-auth dashboard located at `/admin`. Includes Daily, Weekly, and Monthly traffic windows!
- **🌐 Zero-Waiting Streaming Access**: Automatically generates static download routes `/watch/` and `/dl/` for massive Telegram files bridging VLC/IDM straight to the cloud seamlessly.
- **🛡️ Integrated User Management Engine**: Admins can securely `Warn`, `Ban`, and `Unban` users natively straight from the web dashboard. Banned users stay logged for lifetime network oversight.
- **📈 Advanced Download Counters**: Every stream is wrapped locally forcing MongoDB to track live byte-exchange counts per user and per file to accurately trace "most requested" data allocations.

---

## 💻 How It Works

**FilezToLinkX** uses `Pyrogram` and `aiohttp` under the hood. When a user forwards or uploads a file chunk to the Bot inside Telegram, the system indexes the MTProto ID directly into MongoDB. In return, the user automatically gets an HTTP URL!

When an external browser clicks that URL, the internal Dockerized `aiohttp` python server rapidly connects to Telegram's Core MTProto framework utilizing its **Multi-Client Pool**, instantly streaming the exact bitstreams straight out of Telegram's physical data-centers and piping them synchronously to the Web downloader! All while seamlessly logging bandwidth metrics natively on the VPS.

---

## ⚙️ Environment Variables

Set these properties inside your server's `.env` or Heroku Config panel.

### 📝 Mandatory Details

| Variable | Type | Description |
|---|---|---|
| `API_ID` | `int` | Telegram API App ID from [My Telegram](https://my.telegram.org). |
| `API_HASH` | `str` | Telegram API Hash from [My Telegram](https://my.telegram.org). |
| `BOT_TOKEN` | `str` | Your Primary Bot Token from [@BotFather](https://t.me/BotFather). |
| `OWNER_ID` | `int` | Your personal Telegram User ID. |
| `DATABASE_URL` | `str` | MongoDB URI String (Required for bandwidth tracking). |
| `FLOG_CHANNEL` | `int` | ID of the Channel where all internal bot actions & links are logged (-100...). |
| `ULOG_CHANNEL` | `int` | ID of the Channel to trace completely new registering users. |
| `ADMIN_USERNAME` | `str` | Secure Username for `/admin` web dashboard. |
| `ADMIN_PASSWORD` | `str` | Secure Password for `/admin` web dashboard. |
| `PORT` | `int` | HTTP Web server port. Highly recommend `8080`. | 

### 🗼 Multi-Client / Load Balancing
*Add these strictly to bypass native MTProto Flood limits by separating chunk downloads:*
| Variable | Description |
|---|---|
| `MULTI_TOKEN1` ... `MULTI_TOKEN40` | Up to 40 additional unique Bot Tokens. The engine natively balances the load dynamically! |

### 🪐 Optional Optimizations
| Variable | Description |
|---|---|
| `FQDN` | A Custom Domain mapped to your VPS `(e.g., example.com)`. |
| `HAS_SSL` | Set `True` if you serve Nginx Proxy Manager securely with HTTPS. |
| `FORCE_SUB` & `FORCE_SUB_ID` | Set to `True` and list the native channel ID to force user joining. |
| `BOT_WORKERS` | Async execution max limits. Defaults to `20`. |

---

## 🚀 Deployment Guides

<details>
  <summary><b>1. Deploy using Docker (Recommended ⭐️)</b></summary>
<br>

Perfect for NGINX Proxy Manager and highly robust 24/7 VPS uptime.
```bash
# 1. Clone the repository
git clone https://github.com/Monster-ZeroX/FilezToLink.git
cd FilezToLink

# 2. Build the Docker Image securely
docker build -t file-stream .

# 3. Spin up the Core Engine matching your .env mapped PORT
docker run -d --restart unless-stopped --name fsb \
  -v $(pwd)/.env:/app/.env \
  -p 8080:8080 \
  file-stream
```

*To seamlessly reset or apply new environment configs:*
```bash
docker restart fsb
```
</details>

<details>
  <summary><b>2. Deploy Completely Locally</b></summary>
<br>

For local PC environments or classic VPS configurations.
```bash
git clone https://github.com/Monster-ZeroX/FilezToLink.git
cd FilezToLink

# Create & Enter highly isolated virtual env
python3 -m venv ./venv
source ./venv/bin/activate

# Install dependencies rapidly
pip install -r requirements.txt

# Boot the Bot!
python3 -m FileStream
```
</details>

<details>
  <summary><b>3. Deploy on Heroku</b></summary>
<br>

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)
- Simply Fork the repository and press the Deploy Button above.
- Configure the variables cleanly in the deployment GUI natively!
</details>

---

## 📟 Telegram Commands

**⚠️ Critical**: Ensure your Primary Bot represents an `Admin` precisely inside your `FLOG_CHANNEL` or it will critically panic (`[400 CHANNEL_PRIVATE]`).

| Command | Status | Description |
|---|---|---|
| `/start` | User | Verify connection & initiate Database User schema. |
| `/help` / `/about` | User | Get dynamic instructional responses. |
| `/files` | User | Obtain completely interactive index of all historically processed files! |
| `/del` | Admin | Delete a mapped target File natively using the provided FileID. |
| `/ban` / `/unban` | Admin | Manually blacklist dangerous users from MTProto integration natively. |
| `/status` | Admin | Realtime hardware loads and internal client connections count. |
| `/broadcast` | Admin | Propagate messaging completely to every indexed user in MongoDB! |

---
<p align="center"><b>© 2026 Developed explicitly by MonsterZeroX</b></p>
