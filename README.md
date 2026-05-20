# z-bites 🍖

A collection of personal Ubuntu utility scripts for productivity, browser management, and media downloading.

## 📋 Table of Contents
- [Prerequisites](#-prerequisites)
- [Chrome Alt Management](#-chrome-alt-management)
- [Web App Management](#-web-app-management)
- [YouTube Utilities](#-youtube-utilities)
- [Manhwa Scraping](#-manhwa-scraping)
- [System Tools](#-system-tools)
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
- **Python 3 + img2pdf**: Required for PDF generation in `manhwa-scrape` (`pip install img2pdf`).

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

## 📖 Manhwa Scraping

Download manhwa chapters from supported platforms as PDFs.

### `manhwa-scrape`
Scrapes all chapters of a manhwa series and converts them to PDF files.
- **Usage**: `./manhwa-scrape <platform> <url> <output_directory>`
- **Platforms**: `omegascans`, `asurascans`
- **Examples**:
  - `./manhwa-scrape omegascans https://omegascans.org/series/new-town-massage /data/downloads`
  - `./manhwa-scrape asurascans https://asurascans.com/comics/immortals-way-of-life-9a7a1ac5 /data/downloads`
- **Output**: Creates `<output>/<Manhwa Title>/Chapter_<N>.pdf` for each chapter.
- **How it works**: Fetches chapter lists via API (Omega) or HTML parsing (Asura), extracts images from each chapter page, downloads in parallel, and assembles into PDFs via `img2pdf`.

### `build_manhwa_index`
Builds a searchable semantic index from scraped manhwa PDFs using a local Ollama vision model.
- **Usage**: `./build_manhwa_index <manhwa_folder> <cache_folder>`
- **Example**: `./build_manhwa_index /data/downloads/My-Manhwa ./cache`
- **How it works**: Extracts pages from PDFs via `pdftoppm`, samples every 3rd page, sends each to a local Ollama instance (`qwen3-vl:4b-instruct`) for scene description, and saves per-chapter JSON index files.

### `query_manhwa`
Semantically searches the index built by `build_manhwa_index` using sentence embeddings.
- **Usage**: `./query_manhwa <cache_folder> "<query>"`
- **Example**: `./query_manhwa ./cache "fight scene with restraints"`
- **Prerequisites**: `pip install sentence-transformers scikit-learn`
- **How it works**: Encodes the query and all indexed descriptions with `all-MiniLM-L6-v2`, ranks by cosine similarity, and shows the top results (one per chapter).

---

## ⚙️ System Tools

### `set-editor`
Interactively set the default system editor.
- **Usage**: `./set-editor`
- **What it does**:
  - Uses `update-alternatives` to set the system default.
  - Updates `EDITOR` and `VISUAL` variables in `~/.bashrc`.

### `opencode-setup-big-pickle`
Install and configure the OpenCode CLI to work with the Big Pickle ("pig pickle") model.
- **Usage**: `./opencode-setup [API_KEY]`
- **What it does**:
  - Automatically installs the OpenCode CLI if not present.
  - Configures the `OPENCODE_API_KEY` in environment profiles (`~/.bashrc`, `~/.zshrc`).
  - Sets up global and project-level configs to use the `opencode/big-pickle` model.

---

## 🚀 Installation

1. Clone the repository.
2. Make scripts executable: `chmod +x *`
3. (Optional) Add the directory to your `PATH`.

## 📄 Agents Documentation

For a comprehensive list of all supported CLI agents, their trigger commands, and brief descriptions, see the agents documentation file:

[agents.md](file:///home/zhran/mypc/projects/z-bites/agents.md)

## 🛠 Development Workflow

Whenever you modify any script or documentation in this repository:

1. Stage the changes:
   ```bash
   git add .
   ```
2. Commit with a descriptive message:
   ```bash
   git commit -m "Describe your change"
   ```
3. Push to the remote repository:
   ```bash
   git push
   ```

The `install-cli-agents` script also includes a helper function `git_sync` that can be invoked manually to automatically add, commit, and push after any change.
