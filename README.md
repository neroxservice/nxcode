# nxCode

Ein VS-Code-artiger Desktop-Code-Editor im Anime/Neon-Pink-&-Cyan-Look, gebaut mit
Electron + React + TypeScript + Vite + Monaco Editor (der Editor, der auch VS Code
selbst antreibt).

## Features

- **Alles persistent**: Theme, Schriftgröße, Format-on-Save, Minimap, Sidebar-Sichtbarkeit, Terminal-Höhe – UND der komplette Workspace (zuletzt geöffneter Ordner, offene Tabs je Gruppe, aufgeklappte Ordner, Split-Zustand) wird automatisch gespeichert und beim nächsten Start wiederhergestellt. Liegt als JSON in Electrons `userData`-Ordner
- **FiveM/Lua-Funktions-Hervorhebung**: GTA5-Natives, CFX-Funktionen (`TriggerEvent`, `RegisterNetEvent`, ...) und ESX-API (`ESX.*`, `xPlayer.*`) werden in einer eigenen Akzentfarbe hervorgehoben – Monacos eingebauter Lua-Tokenizer kennt diese sonst nicht und stellt sie wie normale Variablen dar
- **Ordner schließen**: über Datei-Menü, Explorer-Header-Icon oder Befehlspalette – schließt Ordner, alle Tabs und Split-Gruppen sauber (inkl. Aufräumen der Monaco-Modelle)
- **Theme-Varianten**: 3 Akzentfarben-Presets (Neon Pink/Cyan, Cyber-Lila, Toxic-Grün), live umschaltbar über Ansicht-Menü – wirkt sich sowohl auf die UI-Farben als auch auf die Editor-Syntax-Highlighting-Farben aus
- **Über nxCode & Tastenkürzel** als richtiges Modal (Hilfe-Menü): Branding mit Versionen (App/Electron/Chromium/Node), Tech-Stack-Badges, plus ein durchsuchbares Tastenkürzel-Cheatsheet
- **Branded Splash-Screen** beim Start statt leerem Fenster, bis React/Monaco geladen sind
- **VS-Code-artige Menüleiste**: Datei/Bearbeiten/Auswahl/Ansicht/Gehe-zu/Terminal/Hilfe mit Icons, echten Tastenkürzeln und funktionierenden Befehlen (Undo/Redo, Ausschneiden/Kopieren/Einfügen, Kommentar umschalten, Mehrfach-Cursor, Zeilen verschieben, Gehe-zu-Zeile, ...)
- **Split-View**: Editor teilen (Ctrl+\, Button in der Tab-Leiste, oder **einen Tab/eine Explorer-Datei an den rechten Rand ziehen** – wie in VS Code) zeigt zwei Dateien nebeneinander, jede mit eigener Tab-Leiste. Beide Hälften nutzen ein zentral verwaltetes Monaco-Modell pro Datei – dieselbe Datei in beiden Hälften bleibt dadurch live synchron (inkl. Undo-Verlauf), jeder Tab merkt sich außerdem Cursor-Position/Scroll-Stand einzeln
- **Datei-Explorer** mit Ordner öffnen, einzelne Datei öffnen, neue Datei/Ordner anlegen (Toolbar-Buttons oder Rechtsklick), umbenennen, **verschieben per Drag & Drop innerhalb des Baums**, löschen – Umbenennen/Verschieben hält offene Tabs & aufgeklappte Unterordner in allen Editor-Gruppen korrekt synchron
- **Drag & Drop von außen**: Ordner oder Datei direkt aus dem Windows-Explorer ins Fenster ziehen zum Öffnen
- **Format-on-Save**: beim Speichern wird automatisch formatiert – Prettier für TS/TSX/JS/JSX/JSON/CSS/SCSS/LESS/HTML/Markdown/YAML, ein eigener Lua-Reindent-Formatter für `.lua` (Prettier hat keinen offiziellen Lua-Support). Ein-/ausschaltbar über die Befehlspalette ("Format-on-Save")
- **Erweiterte Syntax-Prüfung**: TS/JS/JSON/CSS/HTML nutzen Monacos eingebauten Sprachdienst; für **Lua** gibt es zusätzlich einen eigenen Checker, der fehlende/vertauschte `end`/`until` zu `function`/`if`/`for`/`while`/`repeat` sowie unbalancierte Klammern erkennt; für alle anderen Sprachen (Python, PHP, Go, Rust, C/C++/C#/Java, ...) läuft ein genereller Klammer-Balance-Check mit
- **Auto-Close-Tag & Auto-Rename-Tag** für HTML/JSX/TSX/XML: `<div>` tippen ergänzt automatisch `</div>`; den Tag-Namen nachträglich ändern aktualisiert automatisch auch das Gegenstück
- **Probleme-Panel** (wie VS Codes „Problems"-Tab): listet alle Fehler/Warnungen mit Datei, Zeile, Spalte und Meldung auf, Klick springt direkt zur Stelle; Zähler in der Statusleiste (`Ctrl+Shift+M`); Quick-Fix-Glühbirne (Ctrl+.) für TS/JS-Vorschläge
- **FiveM/Lua-IntelliSense**: Autocomplete + Hover-Doku für ~6.700 echte GTA5-Natives (aus der öffentlichen `alloc8or/gta5-nativedb-data`-Datenbank) plus handkuratierte CFX-Framework- (Events, Threads, Ressourcen, Commands) und ESX-Legacy-Funktionen (`ESX.*`, `xPlayer.*`)
- **React/JSX-IntelliSense**: echte `@types/react` + `@types/react-dom` Definitionen vorab geladen – Autocomplete/Hover für Hooks, JSX-Props, Events etc. auch ohne eigenes `node_modules` im geöffneten Ordner
- **Integriertes Terminal**: echte `cmd.exe`-Session (xterm.js + node-pty)
- **Tabs** mit Dirty-Indikator (ungespeicherte Änderungen)
- **Befehlspalette** (`Ctrl+Shift+P`) mit Fuzzy-Suche
- **Farbige Klammer-Ebenen** (Bracket Pair Colorization) im `nxNeon`-Theme – 6 unterscheidbare Neon-Farben inkl. aktivem Klammer-Paar-Highlight und vertikalen Guide-Linien
- **Minimap**, Klammer-Matching, Multi-Cursor, Find & Replace (`Ctrl+F` / `Ctrl+H`) – alles nativ von Monaco
- **Speichern / Speichern unter**, „Untitled"-Dateien wie in VS Code
- Eigene, frameless Titlebar im neon-anime Stil, Statusleiste mit Cursor-Position & Sprache

### Grenzen der IntelliSense (wichtig zu wissen)

Sowohl das FiveM/Lua- als auch das React/TS-IntelliSense sind **statisches,
projekt-unabhängiges Autocomplete** – kein echter Language-Server-Prozess pro
Projekt (das wäre wie VS Codes `tsserver` bzw. eine Lua-Language-Server-
Instanz, die eigene `node_modules`/`tsconfig.json` bzw. lokale Lua-Module
mitliest). Es kennt also:
- ✅ Alle GTA5-Natives, CFX-Funktionen, ESX-Legacy-API, React/JSX-Grundlagen
- ❌ Keine eigenen lokalen Funktionen/Variablen aus anderen Dateien deines Projekts
- ❌ Keine Typen aus dem tatsächlichen `node_modules`-Ordner deines geöffneten Projekts

Für den Alltag (Natives-Signaturen nachschlagen, ESX-Funktionen finden, React-
Hooks-Autocomplete) ist das trotzdem ein sehr praktisches Sprungbrett.

Das **Probleme-Panel** zeigt echte semantische Fehler/Warnungen für
TypeScript/JavaScript/JSON/CSS/HTML (Monacos eingebauter Sprach-Checker) plus
Klammer-/Block-Fehler für Lua und generische Klammer-Fehler für alle anderen
Sprachen (eigene, einfache Checker – kein vollständiger Parser, erkennt aber
zuverlässig vergessene/vertauschte Klammern und `end`/`until`).

## Tastenkürzel

| Aktion                  | Shortcut           |
|--------------------------|--------------------|
| Ordner öffnen            | `Ctrl+O`           |
| Datei öffnen             | `Ctrl+Shift+O`     |
| Neue Datei               | `Ctrl+N`           |
| Speichern                | `Ctrl+S`           |
| Speichern unter          | `Ctrl+Shift+S`     |
| Tab schließen            | `Ctrl+W`           |
| Editor teilen            | `Ctrl+\`           |
| Explorer ein/ausblenden  | `Ctrl+B`           |
| Terminal ein/ausblenden  | `` Ctrl+` ``       |
| Probleme ein/ausblenden  | `Ctrl+Shift+M`     |
| Befehlspalette           | `Ctrl+Shift+P`     |
| Suchen / Ersetzen        | `Ctrl+F` / `Ctrl+H`|

## Voraussetzungen

- Node.js 20 LTS oder neuer
- pnpm (`npm i -g pnpm`)
- Auf Windows: Build-Tools für native Module (werden meist automatisch über
  `node-gyp` nachinstalliert; falls nicht, `npm i -g windows-build-tools` bzw.
  die "Desktop development with C++" Workload in Visual Studio Build Tools)

## Installation

```bash
pnpm install
```

Der `postinstall`-Hook ruft `electron-rebuild` auf und baut `node-pty` damit
automatisch gegen die Electron-ABI neu – dafür ist Internetzugriff beim ersten
Install nötig. Falls das fehlschlägt, startet nxCode trotzdem: das Terminal-Panel
meldet dann nur "nicht verfügbar", der Rest der App funktioniert normal.

Falls der Rebuild-Schritt manuell nachgeholt werden muss (z. B. nach einem
Node- oder Electron-Update), einfach erneut ausführen:

```bash
pnpm run rebuild
```

## Entwicklung

```bash
pnpm dev
```

Startet Vite-Dev-Server + Electron gemeinsam mit Hot Reload für den Renderer.

## Windows-.exe bauen

```bash
pnpm dist:win
```

Erzeugt in `release/` sowohl einen NSIS-Installer als auch eine portable `.exe`.
Das App-Icon liegt unter `build/icon.ico` (kann jederzeit gegen ein eigenes
ausgetauscht werden – 256×256, mehrere Auflösungen eingebettet).

## Projektstruktur

```
nxCode/
├─ electron/           # Main-Prozess (Fenster, IPC, Dateisystem, PTY)
│  ├─ main.ts
│  ├─ preload.ts
│  └─ shared/types.ts  # gemeinsamer IPC-Contract
├─ src/                # React-Renderer
│  ├─ components/
│  │  ├─ Editor/       # Monaco-Wrapper, nxNeon-Theme, React-Typen, Lua/FiveM-Support,
│  │  │                # Tag-Editing, Format-on-Save, Syntax-Checks
│  │  │  ├─ formatters/   # Prettier-Anbindung + eigener Lua-Formatter
│  │  │  └─ checkers/     # Lua-Block-Checker + generischer Klammer-Checker
│  │  ├─ Sidebar/      # Datei-Explorer (inkl. Drag&Drop zum Verschieben)
│  │  ├─ Terminal/     # xterm.js Panel (cmd.exe)
│  │  ├─ BottomPanel.tsx    # Terminal/Probleme-Tabs
│  │  └─ ProblemsPanel.tsx  # Fehler/Warnungen-Liste
│  ├─ data/
│  │  ├─ lua/          # GTA5-Natives-DB + kuratierte CFX/ESX-Funktionen
│  │  └─ react-types/  # echte @types/react .d.ts Dateien für JSX-IntelliSense
│  ├─ hooks/           # Keybindings, Diagnostics-Hook
│  ├─ store/           # zustand State (Tabs, offene Dateien, UI-Zustand)
│  └─ styles/          # Design-Tokens + Komponenten-CSS
└─ package.json
```

## Nächste sinnvolle Ausbaustufen

- Mehrere Editor-Splits (Side-by-Side)
- Git-Integration (Status-Icons im Explorer, Diff-View)
- Einstellungen-Panel (Theme-Varianten, Tastenkürzel anpassen)
- Extension-artige Snippet-Verwaltung
