# z-bites 🍖

A collection of personal Ubuntu utility scripts for productivity, browser management, and media downloading.

## 📋 Table of Contents
- [Prerequisites](#-prerequisites)
- [Chrome Alt Management](#-chrome-alt-management)
- [Web App Management](#-web-app-management)
- [YouTube Utilities](#-youtube-utilities)
- [System Tools](#-system-tools)

---

## 🛠 Prerequisites

Ensure you have the following tools installed:
- **Google Chrome**: Required for `chrome-alt-*` scripts.
- **Nativefier**: Required for `webapp-create`. (`npm install -g nativefier`)
- **yt-dlp**: Required for `yta` and `ytv`.
- **FFmpeg**: Required for audio conversion in `yta`.
- **ImageMagick**: Required for icon processing in `webapp-create`.
- **xprop**: Required for window detection in `webapp-create`.

---

## 🌐 Chrome Alt Management

Manage isolated Google Chrome instances with separate profiles and desktop entries.

### `chrome-alt-create`
Creates a new Chrome profile instance.
- **Usage**: Run the script and follow the interactive prompts.
- **Modes**:
  1. **Full Browser**: Standard Chrome window.
  2. **App Mode**: Minimal window for a specific URL.

### `chrome-alt-list`
Lists all current `chrome-alt` instances, their user directories, icons, and desktop entries.
- **Usage**: `./chrome-alt-list`

### `chrome-alt-delete`
Deletes the **most recently created** `chrome-alt` instance (removes profile, icon, and desktop entry).
- **Usage**: `./chrome-alt-delete`

---

## 📦 Web App Management

Convert any website into a standalone desktop application.

### `webapp-create`
Uses Nativefier to build an Electron-based app from a URL.
- **Usage**: `./webapp-create "App Name" "URL" [--icon PATH] [--user-agent UA]`
- **Flags**:
  - `--icon`: Path to a PNG icon.
  - `--user-agent`: Specify a custom user agent string.

### `webapp-remove`
Removes a web app created by `webapp-create`.
- **Usage**: `./webapp-remove "App Name"`

---

## 🎥 YouTube Utilities

Simple scripts for downloading media from YouTube.

### `yta` (YouTube Audio)
Downloads audio from a URL and converts it to MP3.
- **Usage**: `./yta "URL"`
- **Save Path**: `/data/yami/Music/ytv`

### `ytv` (YouTube Video)
Downloads the best quality video from a URL.
- **Usage**: `./ytv "URL"`
- **Save Path**: `/data/yami/Videos/ytv`

---

## ⚙️ System Tools

### `set-editor`
Interactively set the default system editor.
- **Usage**: `./set-editor`
- **What it does**:
  - Uses `update-alternatives` to set the system default.
  - Updates `EDITOR` and `VISUAL` variables in `~/.bashrc`.

---

## 🚀 Installation

1. Clone the repository.
2. Make scripts executable: `chmod +x *`
3. (Optional) Add the directory to your `PATH`.

