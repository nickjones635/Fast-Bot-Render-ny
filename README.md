# ⚡ Fast Bot Render

A high-speed Telegram bot for extracting, downloading, processing, and uploading educational course content.

The bot is designed to automate course-content workflows from supported educational platforms and send the resulting videos/PDFs directly to Telegram using the **Telethon MTProto protocol**.

> **Use this project only with content you are authorized to access and download.**

---

## ✨ Features

* ⚡ **Fast Telegram uploads**

  * Uses Telethon/MTProto for high-speed uploads.
  * Includes a custom `fast_telethon.py` uploader.
  * Supports large-file uploads.

* 🎓 **Educational platform support**

  * AppX
  * ClassPlus
  * Additional platform handlers included in the project

* 📚 **Course extraction**

  * Login/authentication handling
  * Course listing
  * Folder-wise course traversal
  * Video link extraction
  * PDF/file link extraction

* 📦 **Batch processing**

  * Accept a `.txt` file containing links.
  * Process multiple resources automatically.
  * Download → process → upload workflow.

* 🎬 **Video processing**

  * FFmpeg/FFprobe integration.
  * Automatic video metadata detection.
  * Thumbnail generation.
  * Streaming-friendly Telegram video attributes.

* 📊 **Upload progress**

  * Percentage
  * Upload speed
  * File size
  * ETA
  * Live Telegram progress updates

* 🔐 **Encrypted resource handling**

  * Supports processing of encrypted AppX resource links where the implementation provides the required decryption logic.

* 🐳 **Docker support**

  * Python 3.11-based Docker image.
  * FFmpeg and required system packages installed automatically.

---

## 🏗️ Project Structure

```text
Fast-Bot-Render-ny/
│
├── bot.py
│   └── Main Telegram bot
│
├── appx_api.py
│   └── AppX authentication, course extraction
│      and resource-link processing
│
├── classplus_api.py
│   └── ClassPlus-related API functionality
│
├── fast_telethon.py
│   └── Fast Telegram MTProto file uploader
│
├── requirements.txt
│   └── Python dependencies
│
├── Dockerfile
│   └── Docker deployment configuration
│
└── README.md
    └── Documentation
```

---

## ⚙️ Requirements

### Software

* Python **3.11+**
* FFmpeg
* Telegram Bot Token
* Telegram API ID
* Telegram API Hash

The included Dockerfile is based on Python 3.11 and installs FFmpeg automatically.

---

# 🚀 Installation

## 1. Clone the repository

```bash
git clone https://github.com/nickjones635/Fast-Bot-Render-ny.git
cd Fast-Bot-Render-ny
```

---

## 2. Create a virtual environment

### Windows

```cmd
python -m venv venv
venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Install FFmpeg

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install -y ffmpeg
```

Check:

```bash
ffmpeg -version
```

---

# 🔑 Telegram Configuration

Create a Telegram bot using **@BotFather** and obtain your bot token.

You also need Telegram API credentials from:

[my.telegram.org](https://my.telegram.org/?utm_source=chatgpt.com)

You will need:

```text
API_ID
API_HASH
BOT_TOKEN
```

### Recommended configuration

Do **not** place credentials directly inside `bot.py`.

Use environment variables instead:

```env
API_ID=YOUR_API_ID
API_HASH=YOUR_API_HASH
BOT_TOKEN=YOUR_BOT_TOKEN
ADMIN_CHAT_ID=YOUR_ADMIN_CHAT_ID
```

Then load them in Python using environment variables.

> ⚠️ Never commit `.env` files, bot tokens, API hashes, passwords, or session files to GitHub.

---

# ▶️ Run the Bot

Start the bot with:

```bash
python bot.py
```

The Docker configuration also starts the application using:

```bash
python bot.py
```

---

# 🐳 Docker Deployment

Build the image:

```bash
docker build -t fast-bot-render .
```

Run it:

```bash
docker run -d \
  --name fast-bot \
  --restart unless-stopped \
  -e BOT_TOKEN="YOUR_BOT_TOKEN" \
  -e API_ID="YOUR_API_ID" \
  -e API_HASH="YOUR_API_HASH" \
  fast-bot-render
```

Check logs:

```bash
docker logs -f fast-bot
```

---

# ☁️ Render Deployment

This project can also be deployed as a background worker on Render.

### Build Command

```bash
pip install -r requirements.txt
```

### Start Command

```bash
python bot.py
```

### Recommended environment variables

Add these under **Render → Environment**:

```text
BOT_TOKEN
API_ID
API_HASH
ADMIN_CHAT_ID
```

For a Telegram bot that continuously polls Telegram, use a **Background Worker** rather than a normal web service unless the application has been specifically configured with an HTTP health endpoint.

---

# 🤖 How It Works

The general workflow is:

```text
Telegram User
      │
      ▼
  Telegram Bot
      │
      ▼
Select Platform
      │
      ▼
Authentication / Token
      │
      ▼
Course Selection
      │
      ▼
Course / Folder Extraction
      │
      ▼
Video / PDF Links
      │
      ▼
Download / Processing
      │
      ▼
FFmpeg Processing
      │
      ▼
Fast Telethon Upload
      │
      ▼
Telegram
```

The AppX implementation supports login, course retrieval, recursive folder traversal, and extraction of video/PDF resources.

---

# 📁 TXT Batch Processing

The bot can process a `.txt` file containing resources.

The TXT-processing worker runs separately so that downloading and other blocking operations do not block the main Telegram handling loop.

Example:

```text
https://example.com/video1
https://example.com/video2
https://example.com/video3
```

The bot can process the entries and upload the resulting files to Telegram.

---

# 📤 Fast Telegram Upload

The project uses Telethon for MTProto uploads.

Upload progress includes information such as:

```text
⚡ Uploading

Progress: 65.4%
Speed: 8.2 MB/s
Size: 420.5 MB
ETA: 35s
```

The uploader also supports video metadata and thumbnail generation using FFmpeg/FFprobe.

---

# 🎬 Video Processing

For video files, the bot can:

* Detect duration
* Generate a thumbnail
* Set Telegram video attributes
* Enable streaming support
* Upload through the fast Telethon uploader

FFmpeg is used for media inspection and thumbnail generation.

---

# 🛡️ Error Handling

The bot includes handling for common failures such as:

* Invalid credentials
* API errors
* HTTP errors
* Rate limiting
* Failed downloads
* Failed uploads
* Missing media files
* Telegram upload failures

For example, the AppX API implementation detects HTTP `429` responses and reports rate-limit conditions.

---

# ⚠️ Security

**Important:** Never publish secrets in source code.

Before deploying a public fork, check:

```bash
git grep -n "BOT_TOKEN"
git grep -n "API_HASH"
git grep -n "API_ID"
```

Also check for:

```text
*.session
.env
credentials
passwords
tokens
cookies
```

If a Telegram bot token or API credential has already been pushed to GitHub, **revoke/rotate it immediately**.

The current repository contains credentials directly in `bot.py`, including a fallback bot token and API credentials. These should be removed before making the repository public or sharing it with others.

---

# 📜 Legal & Responsible Use

This software is intended for legitimate automation and personal/authorized educational-content workflows.

You are responsible for:

* Having permission to access the content.
* Respecting the platform's Terms of Service.
* Respecting copyright and intellectual-property rights.
* Protecting account credentials and authentication tokens.
* Using downloaded material only in accordance with applicable laws and permissions.

The developers and contributors are not responsible for misuse of the software.

---

# 🧩 Troubleshooting

## Bot does not start

Check:

```bash
python --version
```

Recommended:

```text
Python 3.11+
```

Then reinstall dependencies:

```bash
pip install -r requirements.txt
```

---

## FFmpeg not found

Check:

```bash
ffmpeg -version
```

If it fails, install FFmpeg and make sure it is available in your system `PATH`.

---

## Telegram upload fails

Check:

1. `BOT_TOKEN`
2. `API_ID`
3. `API_HASH`
4. Internet connection
5. Telegram API availability
6. Available disk space
7. File size
8. FFmpeg installation

---

## AppX login fails

Verify:

* Platform/API URL
* Account credentials
* Internet connectivity
* API availability
* Rate-limit status

The AppX implementation uses multiple login endpoint/version strategies because different AppX deployments can expose different API endpoints.

---

# 🔄 Updating

Pull the latest repository changes:

```bash
git pull origin main
```

Update dependencies:

```bash
pip install -r requirements.txt --upgrade
```

Then restart:

```bash
python bot.py
```

---

# ⭐ Credits

Original project:

[adityass07/Fast-Bot-Render](https://github.com/adityass07/Fast-Bot-Render?utm_source=chatgpt.com)

Current repository:

[Fast-Bot-Render-ny](https://github.com/nickjones635/Fast-Bot-Render-ny?utm_source=chatgpt.com)

---

# 📄 License

Add the appropriate license for your project here.

If this repository is a modified fork, review the original project's license and retain any required attribution.

---

## ⭐ Support

If this project is useful to you:

* ⭐ Star the repository
* 🐛 Report reproducible bugs through GitHub Issues
* 💡 Submit improvements through Pull Requests
* 📖 Improve the documentation

**Fast • Automated • Telegram-powered**
::: 

One important thing: **your current GitHub repository exposes a bot token/API credentials in `bot.py`**. I strongly recommend rotating those credentials and moving them to Render environment variables before using this README publicly.
