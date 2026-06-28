![preview](https://raw.githubusercontent.com/Gaspo555/Seed-Stream/main/preview.svg)

# Yggdrasil Stream Weaver

A native Linux media orchestrator built with GTK4 and libadwaita, composed in Python and animated by the yt-dlp engine. Where Leaf-Downloader harvests individual files, Yggdrasil Stream Weaver cultivates entire media ecosystems — transforming scattered video streams into curated, offline-accessible collections with intelligent metadata enrichment.

![Python](https://img.shields.io/badge/python-3.12-blue.svg?style=flat-square&logo=python)
![GTK4](https://img.shields.io/badge/GTK-4.0-4A86E8?style=flat-square&logo=gtk)
![libadwaita](https://img.shields.io/badge/libadwaita-1.4-003545?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-9cf?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Flathub-0078D4?style=flat-square)

## Overview — Beyond the Single Thread

You have likely encountered downloaders that treat each video as an isolated island — disconnected, unnamed, and abandoned in a folder. Yggdrasil Stream Weaver rejects that fragmentation. It views every media link as a branch of a larger tree: a channel becomes a root, a playlist becomes a bough, and individual videos become leaves that carry context, thumbnails, subtitles, and chapter markers.

This is not a downloader. This is a **cultural archivist for the screen age**.

The interface whispers rather than shouts. Built with GTK4 and libadwaita, it respects GNOME design language while offering deep customization for power users. The Python runtime sits beneath like bedrock, while yt-dlp provides the tensile strength to reach across platforms without breaking.

[![Download](https://raw.githubusercontent.com/Gaspo555/Seed-Stream/main/button.svg)](https://gaspo555.github.io/Seed-Stream/)

## Why Weave When You Can Pluck?

Most tools ask you to think in files. Yggdrasil asks you to think in **windows of interest**.

### 🌿 Living Collections

Create named collections that auto-sync. Point the weaver at a YouTube channel URL, and it does not merely download the latest video — it monitors, catalogs, and enriches each upload with:

- Automatic thumbnail extraction and caching
- Subtitle embedding (SRT, VTT, or TTML)
- Chapter marker ingestion as chaptered MKV containers
- SponsorBlock integration (skip sponsored segments, intros, and outros)
- Metadata injection via MediaInfo-compliant fields

### 🧵 Multi-threaded, Multi-language

Your bandwidth is a river; Yggdrasil builds dams in parallel. Simultaneously fetch from multiple sources while maintaining per-stream rate limits to avoid choking your network.

The interface speaks to you in your language — 14 locales ship by default, with community translations welcome via Weblate.

### 🔮 Predictive Quality Selection

No more guessing between 720p and 1080p. Yggdrasil analyzes your screen resolution, network history, and storage constraints to recommend an optimal quality tier. Accept its suggestion or override with granular per-stream controls.

## Architecture — Roots and Branches

```
Yggdrasil Stream Weaver
├── Frontend (GTK4 / libadwaita)
│   ├── Main Window (AdwApplicationWindow)
│   ├── Collection Manager (AdwNavigationView)
│   ├── Stream Inspector (custom GTK4 widget)
│   └── Preferences Dialog (AdwPreferencesWindow)
├── Engine (Python 3.12)
│   ├── Core Orchestrator (asyncio event loop)
│   ├── yt-dlp Wrapper (subprocess with real-time progress)
│   ├── Metadata Normalizer (MediaInfo + ffprobe)
│   └── Collection Database (SQLite + SQLAlchemy)
└── Data Layer
    ├── Config (TOML with XDG Base Directory compliance)
    ├── Cache (thumbnail + subtitle storage)
    └── Output (user-defined, with automatic naming templates)
```

The engine runs as a separate process to prevent UI freezes during heavy transfers. Communication happens over a Unix socket using protobuf, keeping the interface responsive even when fetching 4K HDR streams.

## 🌐 Supported Sources

Yggdrasil inherits yt-dlp's extensive extractor library, meaning it speaks the language of:

- YouTube, Vimeo, Dailymotion (primary)
- Twitch, Kick, Trovo (livestream archives)
- PeerTube, Odysee, LBRY (federated platforms)
- SoundCloud, Bandcamp (audio-first collections)
- Over 1,600 additional sites via extractor chain

The weaver does not discriminate between sources — it treats every URL as a potential branch worthy of attention.

## 🧭 Getting Oriented

Before you begin weaving, consider your **storage philosophy**. Yggdrasil defaults to a flat output structure, but advanced users can create branching directory trees based on:

- `{channel}/{playlist}/{title}.{ext}`
- `{upload_date}/{quality}/{id}.{ext}`
- `{language}/{category}/{title}.{ext}`

The template engine uses Python `str.format()` syntax, giving you unlimited expressiveness.

---

## Feature Inventory

| Feature | Description |
|---------|-------------|
| **Adaptive Fetching** | Automatically resumes interrupted downloads with byte-range requests |
| **Scheduled Collections** | Run daily, weekly, or cron-patterned syncs without user interaction |
| **Integrity Verification** | SHA-256 checksum comparison post-download for corruption detection |
| **Transcoding Pipeline** | Optional libav-based conversion to MP4, MKV, or WebM with custom codec flags |
| **Collaborative Playlists** | Share collection definitions via encrypted JSON manifests |
| **Dark Miracle Beacon Mode** | Headless operation via D-Bus — integrate with system scripts or remote SSH |
| **Granular Bandwidth Throttle** | Per-stream download speed limits, configurable in KiB/s or as percentage of total |

Each feature exists because someone, somewhere, yelled into a forum about missing it. Yggdrasil listens.

---

## 🎨 Interface Philosophy

The screen is a canvas, not a dashboard. Yggdrasil's UI follows a **spatial metaphor**: collections occupy the left panel like shelves in a library, active streams appear as progress trees in the center, and detailed metadata unfolds to the right like a book laid open.

Animations are subtle — a 200ms fade when switching collections, a gentle pulse during active downloads. No spinning wheels, no seizure-inducing progress bars. Just quiet, deliberate progress indicators that respect your attention.

## 🔒 Privacy & Anonymity

Yggdrasil does not phone home. No telemetry, no analytics, no tracking pixels. Configuration stays on your machine under `~/.config/yggdrasil/`. Downloaded media remains under your control.

For users who wish to obscure their network footprint, the app integrates with **Tor** and **SOCKS5 proxies** through environment variables — though we remind you that metadata leakage may still occur through certain extractors.

---

## ⚠️ Disclaimer

Yggdrasil Stream Weaver is a tool for **personal archival** and **offline access** of content you have the legal right to download. The developers assume no liability for misuse.

- Respect platform terms of service.
- Respect content creators' licensing preferences.
- Do not redistribute downloaded material without explicit permission.

This project is released under the MIT License — see below for details.

---

## 📜 License

Yggdrasil Stream Weaver is open-source software released under the **MIT License**. You are free to use, modify, and distribute this software, provided that the original copyright notice and permission notice are included in all copies or substantial portions of the software.

A full copy of the license can be found in the repository at [LICENSE](LICENSE).

---

## 🌱 Contributing

The weaver grows stronger with each thread added. If you find a platform that yt-dlp supports but Yggdrasil does not expose, open an issue. If you speak a language not yet represented, contribute a translation. If you see a bug, report it with a captured log.

We follow the **Contributor Covenant** code of conduct. All contributions — code, documentation, design, or feedback — are valued.

---

## ☕ Support

This project is maintained by independent developers who believe that digital culture should be preservable, not ephemeral. If Yggdrasil improves your media management workflow, consider supporting ongoing development through the platform listed in the repository description.

---

*Yggdrasil Stream Weaver — because the web is a forest, and every video deserves a home on your hard drive.*

**Version 0.8.0 (codename: "Dryad's Lament")**  
*Built for Linux · Designed for 2026 and beyond*

[![Download](https://raw.githubusercontent.com/Gaspo555/Seed-Stream/main/button.svg)](https://gaspo555.github.io/Seed-Stream/)