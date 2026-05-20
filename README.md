# 🧠 CortexSec OS

**AI-augmented operating system for cybersecurity professionals and everyday users. Built on Kali Linux. Fully open-source, privacy-first.**

![CortexSec OS](artwork/cortexsec-logo.png)

## 🚀 What is CortexSec OS?

CortexSec OS is a dual-mode Linux distribution offering two separate experiences during installation:

1. **Cybersecurity Mode** – 100% Kali Linux (every tool preserved) + AI security enhancements.
2. **AI Desktop Mode** – Full Kali tools (hidden) + Ubuntu-style GNOME desktop + local AI assistant + office suite.

Both modes are privacy-respecting: all AI runs offline, no telemetry.

## ✨ Key Features

- 🔐 **Full Kali Linux Toolkit** (`kali-linux-everything`) pre-installed in both editions.
- 🧠 **Deep AI Integration**:
  - *Cybersecurity Mode*: AI shell (`cotx shell`), AI threat analyzer, Metasploit AI plugin.
  - *AI Desktop Mode*: Local LLM assistant (voice + text), semantic file search, AI app launcher.
- 🖥️ **Dual Installation Choice**: Choose between Xfce (Cyber) and GNOME (AI Desktop) at boot.
- 🛡️ **Privacy by Design**: All AI models run on-device. No cloud, no data collection. OneDrive is optional and user-installed.
- 📦 **Pre-installed Productivity (AI Desktop)**:
  - **LibreOffice** (Writer, Calc, Impress) – mandatory MS Office alternative.
  - GIMP, VLC, Thunderbird.
- 🌐 **Optimized Browsers**:
  - Cybersecurity Mode: **Firefox** (hardened with uBlock, privacy tweaks).
  - AI Desktop Mode: **Golden Chrome** – a privacy-hardened Chromium fork (ungoogled-chromium based).
- ⚙️ **Open Source & Customizable**: Every component (UI, AI, tools) can be modified; GPLv3.
- 🔧 **Live ISO with Custom Installer**: Dual boot entries for easy selection.

## 📥 Installation

1. Download the ISO from [Releases](https://github.com/Agri-Codex/cortexsec-os/releases).
2. Write to USB (e.g., `sudo dd if=cortexsec-os-*.iso of=/dev/sdX bs=4M status=progress`).
3. Boot from USB. In GRUB menu, select:
   - **CortexSec OS (Cybersecurity Mode)** – installs Kali look + AI security.
   - **CortexSec OS (AI Desktop Mode)** – installs GNOME + AI assistant + office.
4. Follow the guided installer.

## 🤖 AI Integration Architecture

- **Cortex AI Daemon (`cotxd`)**: System service that loads local LLM (Llama 3, Mistral) and exposes skills via dbus.
- **Cybersecurity modules**: `cotx-shell` (natural language terminal), `cotx-threat` (log/traffic anomaly detection), `cotx-vuln` (AI vulnerability ranker).
- **Desktop modules**: `cotx-assist` (chat interface), `cotx-voice` (Whisper + Coqui TTS), `cotx-search` (semantic file search).

All AI components live in `/opt/cotx/` and can be swapped or extended.

## 🔏 Privacy & Security

- No data sent to any cloud service.
- Default firewall rules restrict AI daemon to localhost.
- Golden Chrome is built from ungoogled-chromium (Google telemetry stripped).
- OneDrive integration is **not pre-installed**; an optional script is provided (`/opt/cotx/optional/install-onedrive.sh`).

## 🛠️ Building the ISO from Source

```bash
git clone https://github.com/Agri-Codex/cortexsec-os.git
cd cortexsec-os
sudo ./build.sh