# z-bites 🍖

A collection of personal Ubuntu utility scripts for productivity, browser management, and media downloading.

## 📋 Table of Contents
- [Prerequisites](#-prerequisites)
- [Chrome Alt Management](#-chrome-alt-management)
- [Web App Management](#-web-app-management)
- [YouTube Utilities](#-youtube-utilities)
- [Manhwa Scraping](#-manhwa-scraping)
- [System Tools](#-system-tools)
- [OCX Profile Management](#-ocx-profile-management)
- [Installation](#-installation)
- [AI Agents Management](#-ai-agents-management)

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
- **OpenCode CLI**: Required for `clone-ocx-profile`, `publish-ocx-profile`, and `unpublish-ocx-profile`. Install via `curl -fsSL https://opencode.ai/install | bash`.

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

### `opencode-setup`
Install and configure the OpenCode CLI to work with the Big Pickle ("pig pickle") model.
- **Usage**: `./opencode-setup [API_KEY]`
- **What it does**:
  - Automatically installs the OpenCode CLI if not present.
  - Configures the `OPENCODE_API_KEY` in environment profiles (`~/.bashrc`, `~/.zshrc`).
  - Sets up global and project-level configs to use the `opencode/big-pickle` model.

---

## 📦 OCX Profile Management

Publish, clone, and manage OpenCode profiles on the zhran GitHub Pages registry.

### `clone-ocx-profile`
Clones a profile from the personal zhran OCX registry to your local machine.
- **Usage**: `./clone-ocx-profile <name> [source-name]`
- **Examples**:
  - `./clone-ocx-profile z-ws` — install `zhran/z-ws` as local profile `z-ws`
  - `./clone-ocx-profile my-ws ws` — install `zhran/ws` as local profile `my-ws`
- **What it does**: Runs `ocx profile add` under the hood, then updates `parent-tree.json` with the cloned name for provenance tracking.

### `publish-ocx-profile`
Publishes a local OpenCode profile to the zhran GitHub Pages registry.
- **Usage**: `./publish-ocx-profile [options] <source-name> [publish-name]`
- **Options**:
  - `--skip-readme` — Skip AI-powered README generation for the published profile
- **Examples**:
  - `./publish-ocx-profile ws` — publish local `ws` profile as component `ws`
  - `./publish-ocx-profile ws z-ws` — publish local `ws` as component `z-ws`
- **What it does**: Snapshots all files from the source profile, builds a provenance chain in `parent-tree.json`, regenerates `registry.jsonc`, and pushes to GitHub Pages. Optionally generates a README via AI from the profile contents.

### `unpublish-ocx-profile`
Removes a published profile component from the zhran OCX registry.
- **Usage**: `./unpublish-ocx-profile <profile-name>`
- **Example**: `./unpublish-ocx-profile z-ws` — removes component `z-ws` from the registry
- **What it does**: Deletes the profile files from the registry repo, regenerates `registry.jsonc`, rebuilds the packument, and pushes the updated registry to GitHub Pages.

---

## 🚀 Installation

1. Clone the repository.
2. Make scripts executable: `chmod +x *`
3. (Optional) Add the directory to your `PATH`.

## 🤖 AI Agents Management

Scripts to install and manage the 15 AI CLI agents supported by this repository.

### `install-cli-agents`
Installs required dependencies (Node, Rust, Go, Python) and the 15 CLI agents.
- **Usage**: `./install-cli-agents`
- **What it does**:
  - Installs Node.js, Rust, Go, and Python system dependencies.
  - Dynamically installs 15 different AI agents including OpenCode, Goose, Crush, Claude Code, and Gemini.

### `list-cli-agents`
Checks the installation status and version of all 15 supported AI CLI agents.
- **Usage**: `./list-cli-agents`
- **What it does**: Outputs a formatted status table of all agents and required runtimes (node, cargo, go, python).
