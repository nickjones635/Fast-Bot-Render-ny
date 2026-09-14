# Fast-Bot-Render

⚡ A high-speed Telegram bot for extracting and downloading course content from educational platforms (AppX, ClassPlus, and others) with automated upload to Telegram using fast MTProto protocol.

## 🎯 Features

- **Multi-Platform Support**: Extract content from AppX, ClassPlus, Adda247, Physics Wallah, and 10+ other platforms
- **Fast Uploads**: Uses Telethon MTProto client for high-speed file uploads to Telegram (supports files up to 2GB)
- **Batch Processing**: Download and upload multiple videos/PDFs in batch from a single TXT file
- **Encrypted Content Handling**: Automatically decrypts encrypted MKV files and PDFs
- **Progress Tracking**: Real-time upload progress with speed, ETA, and file size indicators
- **Quality Selection**: Automatically selects optimal video quality (360p/480p preferred to avoid size limits)
- **Docker Support**: Easy deployment with included Dockerfile
- **Error Handling**: Robust error recovery with detailed logging and notifications

## 📋 Prerequisites

- Python 3.11+
- Telegram Bot Token
- Telegram API credentials (API_ID, API_HASH)
- System dependencies: `ffmpeg`, `curl`, `yt-dlp`

## 🚀 Installation

### Local Setup

```bash
# Clone the repository
git clone https://github.com/adityass07/Fast-Bot-Render.git
cd Fast-Bot-Render

# Install Python dependencies
pip install -r requirements.txt

# Install system dependencies (Ubuntu/Debian)
apt-get install -y ffmpeg curl

# Install yt-dlp
pip install yt-dlp
