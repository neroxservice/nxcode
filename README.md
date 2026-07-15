<div align="center">

![nxCode Banner](.github/assets/banner_title.png)

[![Platform](https://img.shields.io/badge/platform-Windows-0d0d1a?style=for-the-badge&logo=windows11&logoColor=00e5ff)](#-building)
[![Electron](https://img.shields.io/badge/Electron-31-0d0d1a?style=for-the-badge&logo=electron&logoColor=ff2d95)](#-tech-stack)
[![License: MIT](https://img.shields.io/badge/license-MIT-0d0d1a?style=for-the-badge&logo=opensourceinitiative&logoColor=b967ff)](LICENSE)
[![Made with Monaco](https://img.shields.io/badge/editor-Monaco-0d0d1a?style=for-the-badge&logo=visualstudiocode&logoColor=00e5ff)](#-tech-stack)

</div>

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="About" src=".github/assets/banner_about.png" height="56"/>

**nxCode** is a desktop code editor with an anime/neon look, built on the same
editor core as VS Code itself ([Monaco](https://microsoft.github.io/monaco-editor/)).
It's tailored for **FiveM/Lua scripting** and general **web development**,
wrapped in a fully custom, neon pink/cyan (or Cyber-Purple, or Toxic-Green)
UI shell.

Split-view editing, a real integrated terminal, format-on-save, a full
FiveM/ESX natives database with autocomplete, and a self-updating Windows
installer — all in one lightweight Electron app.

> ⚠️ **FiveM/React IntelliSense is static, not a language server.**<br/>
> Autocomplete for GTA5 natives, CFX/ESX functions, and React/JSX hooks works
> out of the box — but nxCode doesn't read your project's own
> `node_modules`/`tsconfig.json`, so it won't know about your own local
> functions across files. Great for looking up native signatures, not a
> replacement for a full language server.
>
> ⚠️ **Windows-first.** The integrated terminal (`node-pty`), the installer,
> and the auto-updater are all built and tested for Windows. It *may* run
> elsewhere via `pnpm dev`, but that's not the primary target.

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="Features" src=".github/assets/banner_features.png" height="56"/>

- 🪟 **Split-view editing** — drag a tab to the right edge to open a second
  pane, exactly like VS Code. Both halves share the same live Monaco model,
  so edits sync instantly and undo history is shared too.
- 🧠 **FiveM/Lua IntelliSense** — autocomplete + hover docs for ~6,700 real
  GTA5 natives, plus hand-curated CFX (`TriggerEvent`, `RegisterNetEvent`, …)
  and ESX Legacy (`ESX.*`, `xPlayer.*`) functions. Known API calls even get
  their own accent color, since Monaco's stock Lua tokenizer doesn't know
  them.
- 🎨 **React/JSX IntelliSense** — real `@types/react`/`@types/react-dom`
  preloaded, so hooks, props, and events autocomplete even without a local
  `node_modules`.
- 💅 **Format-on-save** — Prettier for TS/TSX/JS/JSX/JSON/CSS/SCSS/LESS/HTML/
  Markdown/YAML, plus a custom re-indenting formatter for `.lua` (Prettier
  has no official Lua support).
- 🩺 **Problems panel** — real diagnostics for TS/JS/JSON/CSS/HTML via
  Monaco's language services; for Lua, a custom checker catches
  missing/mismatched `end`/`until`/brackets. Generic bracket checking for
  everything else (Python, PHP, Go, Rust, C/C++/C#, Java, …).
- 🖥️ **Integrated terminal** — a real `cmd.exe` session via `xterm.js` +
  `node-pty`.
- 🗂️ **Full file management** — open/create/rename/delete/move files and
  folders (drag & drop in the tree, or drag in from Windows Explorer),
  multi-tab editing with dirty indicators.
- 🌍 **Multi-language UI** — German, English, French, and Turkish, switchable
  live from Settings.
- 🎛️ **Settings that stick** — theme, font size, format-on-save, keybindings,
  and your whole workspace (open folder, tabs, split state) persist across
  restarts.
- 🌈 **3 accent themes** — Neon Pink/Cyan, Cyber-Purple, Toxic-Green — live
  switchable, affects both the UI chrome and the editor's syntax colors.
- 🚀 **Self-updating** — checks GitHub Releases on launch and installs
  updates via `electron-updater`.
- ⌨️ **A real VS-Code-style menu bar** — File/Edit/Selection/View/Go/
  Terminal/Help, with working Undo/Redo, multi-cursor, comment toggling,
  go-to-line, and more.

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="Tech Stack" src=".github/assets/banner_techstack.png" height="56"/>

<div align="center">

![Electron](https://img.shields.io/badge/Electron-2B2E3A?style=flat-square&logo=electron&logoColor=9FEAF9)
![React](https://img.shields.io/badge/React-2B2E3A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-2B2E3A?style=flat-square&logo=typescript&logoColor=3178C6)
![Vite](https://img.shields.io/badge/Vite-2B2E3A?style=flat-square&logo=vite&logoColor=BD93F9)
![Monaco Editor](https://img.shields.io/badge/Monaco_Editor-2B2E3A?style=flat-square&logo=visualstudiocode&logoColor=00E5FF)
![Zustand](https://img.shields.io/badge/Zustand-2B2E3A?style=flat-square&logoColor=FF2D95)
![Prettier](https://img.shields.io/badge/Prettier-2B2E3A?style=flat-square&logo=prettier&logoColor=F7B93E)

</div>

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="Media" src=".github/assets/banner_media.png" height="56"/><br/>

<img alt="Split view" src=".github/assets/screenshot_splitview.png" width="720"/><br/>
Split-view editing with live-synced Monaco models<br/><br/>
<img alt="Menu bar and explorer" src=".github/assets/screenshot_menu.png" width="720"/><br/>
The full VS-Code-style menu bar, explorer, and bracket-pair colorization in action

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="FAQ" src=".github/assets/banner_faq.png" height="56"/>

### Is this a VS Code extension?

No — nxCode is a **standalone Electron app**, not a VS Code extension. It just
uses the same Monaco editor core under the hood.

### Does the FiveM/React autocomplete understand my own project?

Not fully. It's static autocomplete over known APIs (GTA5 natives, CFX/ESX,
React), not a project-aware language server — see the callout above.

### Does it work on macOS/Linux?

The renderer/editor itself is plain Electron and should run anywhere, but the
integrated terminal (`node-pty`), the installer, and the auto-updater are all
Windows-focused and untested elsewhere.

### Why Lua and not [my framework]?

nxCode's Lua tooling is built specifically around **FiveM + ESX Legacy**,
since that's what it was built for. Other Lua frameworks will still get
syntax highlighting and the generic bracket checker, just not the
autocomplete/hover database.

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="Building" src=".github/assets/banner_building.png" height="56"/>

1. Clone the repository:
   ```bash
   git clone https://github.com/neroxservice/nxcode.git
   ```
2. `cd` into the project directory:
   ```bash
   cd nxcode
   ```
3. Install dependencies (also rebuilds `node-pty` against Electron's ABI):
   ```bash
   pnpm install
   ```
4. Run in development mode (Vite + Electron with hot reload):
   ```bash
   pnpm dev
   ```
5. Build the Windows installer:
   ```bash
   pnpm dist:win
   ```

The installer (NSIS) and a portable `.exe` are output to `release/`.

> If `node-pty` fails to rebuild on Windows with an `MSB8040` error, install
> the **Spectre-mitigated libraries** for your MSVC toolset via the Visual
> Studio Installer (Individual Components → search "Spectre"), then run
> `pnpm run rebuild`.

<img alt="separator" src=".github/assets/separator.png" width="100%"/>

<img alt="License" src=".github/assets/banner_license.png" height="56"/>

This project is licensed under the MIT license. See [LICENSE](LICENSE) for
more details.

<div align="center">

Made with ❤️ by **nxService & Streams**

</div>
