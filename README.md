<div align="center">
  <img src="docs/icon.png" alt="LinerNotes icon" width="120" />
  
  # 🎧 LinerNotes
  "Write it on the sleeve, right in your browser."
  
  **A single-file, browser-based MP3 ID3 tag editor.**
  *Drop in one track or a whole album, edit the metadata, preview the audio, and export — all client-side, with nothing ever uploaded anywhere.*
  
  **No build step. No dependencies to install. No server. Open the HTML file and it works.**
  
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
  [![HTML](https://img.shields.io/badge/HTML-%23E34F26.svg?logo=html5&logoColor=white)](#)
  [![CSS](https://img.shields.io/badge/CSS-639?logo=css&logoColor=fff)](#)
  [![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=000)](#)

  [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/L3G824WA0P)
  
  <br />
</div>

## 📖 Table of Contents
- [🚀 Getting Started](#-getting-started)
- [🌐 Browser Support](#-browser-support)
- [✨ Features](#-features)
- [💻 Desktop Versions](#-desktop-versions)
- [🛠️ Technical Notes](#️-technical-notes)

---

## 🚀 Getting Started

Just open `linernotes.html` in any modern browser (Chrome, Firefox, Edge, Safari). That's it — no installation, no server, no account.

1. **Drop** one or more `.mp3` files onto the tray (or click it to browse).
2. **Click** a track to edit its tags in the panel on the right, or check multiple tracks to batch-edit them together.
3. **Preview** using the player bar at the bottom to hear whatever's selected.
4. **Click** "Export tagged MP3" for a single file, or "Export all/selected (.zip)" for a batch.

---

## 🌐 Browser Support

Any modern browser with support for the File API, Blob/`URL.createObjectURL`, and the HTML5 `<audio>` element — i.e. current Chrome, Firefox, Edge, and Safari.

---

## ✨ Features

### 🏷️ Tag Editing
*   Reads and writes **ID3v2.3** tags with a hand-rolled parser/writer (no external tagging library). Handles title, artist, album, album artist, genre, year, track number, comment, and embedded cover art.
*   Falls back gracefully for files with no existing tag, or tags in ID3v2.4.
*   A genre field with autocomplete against the standard ID3v1 genre list.

### 📦 Batch Editing for Albums
*   Check two or more tracks in the tray to edit them all at once.
*   Shared fields **pre-populate automatically**: if every checked track already agrees on a value (e.g. the same artist), that value shows up ready to go. If they disagree, the field shows a **"Various"** placeholder instead of guessing — and leaving it as "Various" never overwrites the tracks' existing (differing) values.
*   Only fields you actually type into (or deliberately clear) get written to the selected tracks — everything else is left untouched.
*   **Auto-numbering**: reorder the selected tracks with up/down controls and stamp sequential track numbers (`3/12`, `4/12`, …) across the whole selection in one click.
*   **Batch artwork**: upload or remove cover art across every selected track at once. The preview shows the shared artwork when all selected tracks match, "No artwork" when none of them have any, or "Various" when they differ.

### 🎵 Built-In Audio Player
*   A persistent player bar at the bottom of the editor shows the album art, title, artist, and album of whichever track is active in the tray.
*   Transport controls: **restart**, **play/pause** (a single toggle button that swaps icons with playback state), and **stop**.
*   A seekable progress bar with live elapsed/duration timestamps.
*   Playback is **sticky**: once a track is playing, clicking around the tray (switching tracks, checking boxes for batch mode, removing other tracks) never interrupts it. The player only loads whatever's newly selected once playback is explicitly paused or stopped.

### 💾 Exporting
*   Export a single tagged file, rebuilt with a fresh ID3v2.3 tag.
*   **Export all** (or **export selected**, if you've checked specific tracks) bundles everything into a `.zip`, automatically named from the tags:
    *   Multiple tracks → `Artist-Album.zip` (falls back to `Various Artists-…` for mixed-artist compilations).
    *   A single track → `Artist-Title.zip`.
    *   Missing tags or characters invalid in filenames are handled gracefully.

### 🎛️ Interface & Tray Management
*   Drag-and-drop or click to load any number of MP3s.
*   Per-track remove, or **Clear tray** to wipe everything at once (with a confirmation prompt).
*   A dirty-state indicator shows which tracks have unsaved edits.
*   Distinct **cassette-deck / analog-console** visual theme — not a generic admin-panel look.
*   **Light and dark themes**, toggleable at any time (resets each session).
*   Fully responsive: the two-column desktop layout collapses to a stacked, scrollable layout on mobile.

### 🔒 Privacy
*   Runs **entirely in the browser**. No files are ever uploaded or sent anywhere. Tag parsing, editing, audio playback, and zip export all happen locally using the File, Blob, and Web Audio APIs.

---

## 💻 Desktop Versions

This project can also be packaged as:

| Format | Description |
| :--- | :--- |
| **Electron App** | A native app (Windows `.exe`, Mac `.dmg`/`.app`, Linux `.AppImage`/`.deb`) for a chromeless window experience, with JSZip vendored locally for fully offline use. |

*(It's built from the same underlying HTML/CSS/JS — see the respective project folders for build instructions).*

---

## 🛠️ Technical Notes

*   **No frameworks.** Vanilla HTML, CSS, and JavaScript in a single file.
*   **No tagging library.** ID3v2 reading and writing (synchsafe integers, frame parsing, text encodings including UTF-16 and UTF-8, `APIC` embedded art, `COMM` comments) is implemented directly.
*   The only external dependency is [JSZip](https://stuk.github.io/jszip/), used solely for the "export as zip" feature.
*   Audio playback uses a native `<audio>` element backed by an in-memory `Blob` built from the original file bytes, so tag edits never affect the audio stream itself.

---

<div align="center">
  <i>Distributed under the MIT License.</i>
</div>
