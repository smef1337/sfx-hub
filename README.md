# hub.wav - Premiere Pro & After Effects Sound Design Extension

hub.wav is a premium sound design extension panel (CEP) built for Adobe After Effects and Adobe Premiere Pro. It streamlines video editing and motion graphics workflows by providing a beautiful, hardware-inspired browser to search, preview, and insert your own local sound libraries directly onto timelines.

---

<img width="816" height="608" alt="With Menu" src="https://github.com/user-attachments/assets/f6616c1a-3051-4576-989e-34c8894f7fde" />
<img width="816" height="611" alt="without menu" src="https://github.com/user-attachments/assets/6155516b-afc6-4596-ab8a-492137b73946" />



## Features

- **Double-Click Import:** Click "Add to Timeline" or double-click any sound to instantly load and place it at your Current Time Indicator (CTI / Playhead) in Premiere or After Effects.
- **Dynamic Categories:** Scans your directories recursively and automatically maps subfolders (e.g. `Whooshes`, `Impacts`, `Drones`) into interactive category tabs!
- **Active Host Detection:** Dynamically detects whether it is running inside Adobe Premiere Pro or Adobe After Effects, showing the active mode directly below the title.
- **Waveform Canvas:** Real-time, responsive audio waveform visualization utilizing the Web Audio API.
- **Speed & Volume Controls:** Dial-in your playback speeds (0.5x to 2x) and volumes before dropping clips on your timeline.
- **Interactive Search:** Filter and search through thousands of sounds instantly.
- **Persisted Favorites:** Star your favorite sound effects for quick recall in a dedicated tab (stored in browser `localStorage`).
- **Custom Local Folders:** Connect your own sound libraries (WAV, MP3, OGG, M4A). The extension recursively scans directories using Node.js and imports them dynamically, persisting across Adobe sessions.

---

## Quick Installation

To install and test the extension on your machine, follow these three steps:

### 1. Enable Adobe PlayerDebugMode
By default, Adobe applications will only load digitally signed extensions. To load this unsigned development panel, you must enable PlayerDebugMode:

- **Windows:** Double-click and run `scripts/setup_debug_mode.bat`, or run `npm run setup-debug` in your terminal.
- **macOS:** Open terminal and run:
  ```bash
  defaults write com.adobe.CSXS.8 PlayerDebugMode 1
  defaults write com.adobe.CSXS.9 PlayerDebugMode 1
  defaults write com.adobe.CSXS.10 PlayerDebugMode 1
  defaults write com.adobe.CSXS.11 PlayerDebugMode 1
  defaults write com.adobe.CSXS.12 PlayerDebugMode 1
  defaults write com.adobe.CSXS.13 PlayerDebugMode 1
  defaults write com.adobe.CSXS.14 PlayerDebugMode 1
  ```

### 2. Copy the Extension Folder to Adobe's CEP Directory
Move or symlink the folder into Adobe's default Extension folder:

- **Windows:**
  Copy the `hub.wav` folder to:
  `C:\Users\<Your-Username>\AppData\Roaming\Adobe\CEP\extensions\hub.wav`
  *(Create the `CEP` and `extensions` folders if they do not exist)*

- **macOS:**
  Copy the folder to:
  `~/Library/Application Support/Adobe/CEP/extensions/hub.wav`

---

## How to Use inside Premiere Pro & After Effects

1. Open Adobe Premiere Pro (v2022+) or After Effects (v2021+).
2. Open a project and ensure you have an **active timeline** open (a sequence in Premiere or a composition in After Effects).
3. Navigate to the top menu: **Window** > **Extensions** > **hub.wav**.
4. In the hub.wav panel:
   - The detected application ("Premiere Pro Mode" or "After Effects Mode") will show below the title logo.
   - Click the **Custom Folders** tab on the left sidebar.
   - Click **Select SFX Folder** and select any local folder containing your audio files.
   - The files will load instantly and be parsed into categories.
   - Switch back to the **Library** tab.
   - Click a sound card to preview it.
   - Adjust the **VOL** (Volume) or **SPD** (Speed) sliders.
   - Click **Loop** if you want continuous playback.
   - Click **Add to Timeline** or **double-click** the card to place the clip directly at the playhead CTI.
5. Star/favorite any sound to add it to your **Favorites** collection for rapid access.

---

## Technical Stack & Architecture

- **Manifest Configuration (`CSXS/manifest.xml`):** Maps CEP bindings, window sizes, target versions, and initializes `--enable-nodejs` and `--mixed-context` CEF flags.
- **Frontend Panel (`client/`):** Implements modern dark-mode styles with glassmorphic elements, Outift/Inter Google typography, and SVG interfaces. Uses Web Audio API for waveform analyser canvas drawing.
- **Host Script (`host/index.jsx`):** Communicates with Adobe's DOM. Coordinates file imports, queries sequence/composition playheads, and inserts clips at frame-accurate times.
