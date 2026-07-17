# JavTurbo

Release Note
[![Telegram](https://img.shields.io/badge/Telegram-Join_Chat-2CA5E0?style=flat&logo=telegram&logoColor=white)](https://t.me/+1PlPh_PuXFQwMjhh)

Chatroom
[![Telegram](https://img.shields.io/badge/Telegram-Join_Chat-2CA5E0?style=flat&logo=telegram&logoColor=white)](https://t.me/+RSW4IsgpU6A3OGU5)

Language / 语言: [简体中文](./README.zh-CN.md)

JavTurbo is a desktop app for scanning local JAV video files, fetching metadata, downloading assets, and organizing output for media library tools such as Jellyfin, Emby, Kodi, or Plex.

## Features

- Scan local media folders with extension and file size filters
- Parse JAV IDs from filenames automatically
- Support split videos with grouped processing, one metadata request, and one output folder per title
- Concurrent metadata scraping — faster than mdcx, mdcng, and metatube
- High-resolution cover fetching for DMM/Fanza and MGS, with automatic fallback to standard resolution
- Manual cover cropping: crop the downloaded fullcover image and overwrite the frontcover when the automatic crop is not accurate
- Duplicate ID protection for invalid duplicates that are not named as split parts
- Configurable folder, filename, and NFO title naming templates
- Download selected assets: poster, thumb, fanart, trailer, NFO, extrafanart, behind-the-scenes
- Optional `ffmpeg` conversion for behind-the-scenes MP4 output
- Post-scrape cleanup: delete files by extension or size, remove empty folders
- Realtime progress bar and structured runtime logs with per-scrape log files
- Console page with timeline view, by-movie grouping, level filters, and search
- Multi-language UI (`en`, `zh-CN`, `zh-TW`)

## Prerequisites

- Windows uses the Microsoft Edge WebView2 Runtime. The normal setup installs it automatically when it is missing. Before using the portable edition, install the [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) if it is not already available. Most current Windows 10 and Windows 11 systems already include it.
- Optional: `ffmpeg` in PATH — only required for behind-the-scenes MP4 conversion

## Editions

### Normal

The normal Windows setup installs JavTurbo and stores settings and logs in the operating system's application-data directories. It also checks for WebView2 and downloads the runtime when needed.

On macOS, the normal DMG contains the standard `JavTurbo.app` bundle and uses the operating system's application-data directories.

### Portable

The portable edition is a separate build. It does not need a marker file and always stores `settings.json` and `logs/` beside `JavTurbo.exe` on Windows or beside `JavTurbo.app` on macOS. They are created automatically on first use and can be moved together with the application.

The directory containing the portable application must be writable. Do not place the portable edition in a protected or read-only location such as `Program Files`, `/Applications`, or a mounted disk image.

The Windows portable ZIP does not install WebView2. If WebView2 is missing, download and install the [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) before starting JavTurbo.

## Usage

### 1. Settings

Open **Settings** and configure:

- **Media folder** — where your video files are
- **Success output folder** — where processed videos and assets will be moved
- **Failed output folder** — where videos that could not be processed will be moved
- **Download types** — choose which assets to download (poster, thumb, fanart, trailer, NFO, extrafanart, behind-the-scenes)
- **Naming rules** — folder pattern, filename pattern, NFO title pattern
- **Concurrency** — number of parallel download and ffmpeg workers

The media folder, success output folder, and failed output folder must be three separate folder trees. Do not set any of them as a parent or child folder of another one, otherwise scanning, moving, or cleanup can affect the wrong files.

### 2. Scan

Click **Scan** on the main page. JavTurbo will walk your media folder, filter by extension and size, and parse a JAV ID from each filename. Files with an unrecognized ID are shown as failed.

If a movie is split into multiple files, name the parts with a `-cd#` suffix before the extension:

- `ABC-123-cd1.mp4`
- `ABC-123-cd2.mp4`
- `ABC-123-CD3.mkv`

`#` can be `1` to `9`. The suffix is case-insensitive when scanning, but JavTurbo will normalize the final output filename to lowercase such as `-cd1`, `-cd2`.

### 3. Scrape

Click **Scrape** to process all unprocessed videos:

- Fetches metadata from the API
- Moves and renames the video to the success folder
- Writes NFO
- Downloads selected assets (poster, fanart, trailer, etc.)
- Runs post-scrape cleanup if configured

For split videos, JavTurbo treats all `-cd#` parts with the same ID as one movie group:

- Sends only one metadata request
- Places all parts in the same output folder
- Renames each output file with lowercase suffixes like `-cd1`, `-cd2`

The Scan and Scrape buttons are disabled while an operation is in progress.

### 4. Movie Viewer

Click any movie card to open the viewer:

- Fullcover and metadata shown side by side
- Description below
- Trailer (with cover thumbnail and play button), frontcover, and sample images in a grid below
- Click any image or the trailer to open a fullscreen lightbox — use arrow buttons to navigate
- Use **Crop Cover** to manually crop the downloaded fullcover into the frontcover file. This is useful when the automatic frontcover crop is off and you want to overwrite it with a better crop.

### 5. Console

The Console page shows a live log of all scraping activity. Logs can be filtered by level, searched by keyword, and grouped by movie. Each scrape session also writes a log file to the app log folder (`javturbo-scrape-YYYYMMDD-HHMMSS.log`).

## Asset Naming

For Jellyfin/Emby compatibility:

- No prefix mode:
  - `poster.jpg`, `thumb.jpg`, `fanart.jpg`, `movie.nfo`, `trailer.mp4`
- Prefix mode:
  - `<video filename>-poster.jpg`, `<video filename>-thumb.jpg`, `<video filename>-fanart.jpg`, `<video filename>.nfo`, `<video filename>-trailer.mp4`

## License

No explicit license file is currently included.

