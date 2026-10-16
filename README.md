# Flowchart Builder

**Flowchart Builder** is a two-way editor between source code and flowcharts. Paste or load C++ / Python code and instantly see its logical structure — or build a flowchart by hand and let the app generate clean, runnable code back. Built for anyone who wants to *see* what their program actually does.

![Version](https://img.shields.io/badge/version-v1.6-blue)
![Languages](https://img.shields.io/badge/languages-C%2B%2B%2C%20Python%2C%20Auto-green)
![Interface](https://img.shields.io/badge/interface-Russian%2C%20English-orange)
![Themes](https://img.shields.io/badge/themes-12-purple)
![Export](https://img.shields.io/badge/export-PNG%20%7C%20PDF%20%7C%20SVG-pink)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)

> Free to use. **Not** open source. See [LICENSE](LICENSE).

---

## 📸 Screenshots

*(screenshots will be added soon)*

---

## 📥 Installation

### Option 1: Ready-to-use application (recommended)

1. Go to the **Releases** section of this repository.
2. Download the latest `FlowchartBuilder-vX.X-win64.zip`.
3. **Extract the whole archive** into a dedicated, empty folder of your choice (e.g. `C:\Tools\Flowchart Builder\`). The archive already contains the `.exe` and its companion `_internal/` folder — they must stay together.
4. Run `Flowchart Builder.exe` from inside that folder.
5. On first launch the app creates its working files (`config.json`, `blueprints/`, `exports/`, `recovery.json`) in the same folder. Everything stays self-contained — nothing is written to the registry or your user profile. You can move the folder to a USB stick at any time.

> ⚠️ Do not extract only the `.exe` — the app will not launch without `_internal/`.

### Option 2: Running from source code (authorized use only)

> The source code is **private**. This option is for the author and licensed collaborators only.

Required files:

- `main.py` — entry point
- `gui.py` — the PySide6 interface
- `logic.py` — tree model, parsers, layout, generators
- `logic_langs.py` — language detection tables
- `error_checks.py` — auto-fix engine (Qt-free)
- `requirements.txt`

Then:

```bash
pip install -r requirements.txt
python main.py
```

`blueprints/` and `exports/` are created automatically next to `main.py` on first run.

> 💡 `logic.py`, `logic_langs.py` and `error_checks.py` do **not** import PySide6, so the parser / generator / auto-fix pipeline can be imported and tested headlessly.

---

## 🎮 Controls

### Mouse

| Action | Control |
|---|---|
| Pan flowchart | Left mouse button (drag) |
| Zoom in / out | Mouse wheel |
| Fit to window | Middle mouse button |
| Edit block | Double-click a block |
| Structural menu | Right-click a block |
| Collapse / expand branch | Click the `−` / `+` dot on the block |
| Resize text in editor | `Ctrl` + wheel over the editor |

### Keyboard

| Shortcut | Action |
|---|---|
| `F5` | Code → Flowchart |
| `F6` | Flowchart → Code |
| `Ctrl+S` / `Ctrl+Shift+S` | Save / Save As |
| `Ctrl+O` | Open source file |
| `Ctrl+N` | New schema |
| `Ctrl+E` | Export diagram (PNG / PDF / SVG) |
| `Ctrl+Z` / `Ctrl+Y` | Undo / Redo |
| `Ctrl+F` | Search in editor |
| `Ctrl+C` / `Ctrl+V` | Copy / paste block subtree |
| `Ctrl+↑` / `Ctrl+↓` | Previous / next saved schema |
| `Ctrl+=` / `Ctrl+-` / `Ctrl+0` | Interface font size |
| `Delete` | Delete selected block |
| `F1` | Help |
| `Ctrl+Shift+D` | Developer console (if enabled) |

---

## ✨ Features

### Two-way editing

- **Code → Flowchart**: paste or load code, press `F5`, get a clean, colored diagram with proper yes/no branches, back-arrows for loops and multi-column layout for large programs.
- **Flowchart → Code**: build or edit blocks by hand, press `F6`, get idiomatic, runnable Python or C++ — with automatic type inference, `#include` collection and `using namespace std;`.

### Languages

- **Python** and **C++** with full round-trip fidelity: a line parsed from code in the same language is reused verbatim. Switching languages translates constructs (`print` ↔ `cout`, `sum` ↔ `accumulate`, `len` ↔ `.size()`, …).
- **Auto-detect** mode: leave the dropdown on `Auto` and the app picks Python or C++ from the code itself.

### Auto-fix engine

Before building the diagram the app scans your code and offers one-click fixes:

- **Python**: missing `:`, wrong indentation, `print x` (Python 2 style), `::` after a header, `=` instead of `==`, unclosed brackets and quotes, tabs in indentation, and more.
- **C++**: missing `;`, missing `#include`, missing `using namespace std;`, wrong I/O direction (`cin <<` / `cout >>`), conditions without parentheses, two statements glued on one line, missing `return 0;`, and more.
- Optional **undeclared variable** check (reads before declarations). For C++ the dialog can insert `int x;` declarations automatically.

### Diagram

- Full block palette: **Start / End**, **Process**, **Input / Output**, **Condition (if / elif / else)**, **While loop**, **For loop**, **Comment** (with a folded corner).
- **Collapse / expand** any condition or loop — the branch disappears on the diagram *and* its code is folded in the editor. Both stay in sync.
- **Copy / paste** entire block subtrees.
- **Undo / redo** for both text and tree edits.
- **Click a line in the editor** — the matching block highlights and glows on the diagram. **Click a block** — the editor jumps to its first line.
- **Comment blocks** attached to conditions and loops are drawn as small sticky notes off to the side.

### Editor

- Python and C++ syntax highlighting, theme-aware.
- Line numbers with error marks, fold indicators, current-line highlight.
- **Auto-completion**: keywords, builtins, plus all identifiers extracted from your code (variables, function params, ranges, `cin >>` targets).
- **Search bar** (`Ctrl+F`) with match counter and next / previous navigation.
- **Fold** loops and conditions directly from the gutter.

### Themes

- **12 built-in themes**: dark neon (`Cyberpunk`, `Red Neon`, `Midnight Blue`, `Emerald`, `Sunset`, `Graphite`, `True Black`), light (`Solarized Light`, `GitHub Light`, `Paper`) and two customizable ones.
- **Custom accent colors** per theme: accent, border, arrow — with a live color picker.
- **Uniform block color** mode — one color for every block, handy for printing.
- Optional **grid** on the diagram canvas.

### Sessions & files

- **Autosave** with configurable interval.
- **Crash recovery**: on the next launch after an unexpected close, a dialog offers to restore unsaved work.
- **Unsaved changes guard** on close.
- **Save mismatch guard**: if editor code and diagram disagree, saving is blocked.
- **Schemas list** with search, sort by date or name, inline rename, delete, double-click to load, `Ctrl+↑` / `Ctrl+↓` to cycle.

### Export

- **PNG** (color or black & white with optional inversion), **PDF** (A4, orientation chosen automatically), **SVG** (vector, color).
- Grid is hidden on export; generous margins so nothing is clipped.

### Developer mode

Off by default, toggled in Settings. Adds a log console (filterable by category), a sandbox for running internal operations, and a test runner that streams output from `tests/run_all.py`.

---

## 🆕 What's in v1.6

This is the first public release of the rebuilt Flowchart Builder. Everything below is what the app ships with today:

- ✅ **Two-way editor** between source code and flowchart for **Python** and **C++**.
- ✅ **Auto-fix engine** for both languages (`error_checks.py`, Qt-free).
- ✅ **Undeclared variable** check with optional C++ declaration insertion.
- ✅ **Full block palette**: Start/End, Process, I/O, Condition, While loop, **For loop**, **Comment** blocks.
- ✅ **Collapse / expand** for conditions and loops, mirrored between diagram and editor.
- ✅ **Copy / paste** of whole block subtrees, **undo / redo** for text and tree.
- ✅ **Autosave** + **crash recovery** + **unsaved changes guard** + **save mismatch guard**.
- ✅ **Multi-column layout**: large programs split into 1–4 columns with wrap connectors.
- ✅ **12 themes** including three light ones, plus **custom accent colors** and a **uniform color mode**.
- ✅ **Export** to PNG (color / B&W / inverted), **PDF** and SVG.
- ✅ **Search & sort** in the schemas list, **auto-detect language** (`Auto`).
- ✅ **Editor**: line numbers, fold gutter, current-line highlight, syntax-aware auto-completion, `Ctrl+F` search bar.
- ✅ **Schema storage**: each schema is a folder `blueprints/<name>/` with `chart.json` and a ready-to-run `main.py` / `main.cpp`.
- ✅ **Developer mode** with console, sandbox and test runner.
- ✅ **Modular core**: `logic.py`, `logic_langs.py` and `error_checks.py` are Qt-free and headlessly testable.

> **Version naming.** The public release line starts at **v1.6** as a small nod to a favourite game. Once the roadmap below is significantly complete, the project will graduate to **v2.0**.

---

## 🗺️ Roadmap to v2.0

- 🤖 **AI assistant** — explain a diagram in plain language, suggest refactorings, generate code from a text description, highlight likely bugs.
- 🎓 **Learning mode** for classrooms:
  - built-in tasks with automatic checking of the student's solution,
  - a **teacher role** for authoring tasks and monitoring progress,
  - **local network (school LAN)** mode for classroom use without internet.
- ▶️ **Code simulation** — step through the flowchart, watch variable values change, see which branch is taken and why.
- 🎨 **Visual and animation upgrades** — smoother rebuild transitions, animated arrows, drag-and-drop block editing, a minimap.
- 🌐 **More languages** — Java, C#, Pascal, JavaScript, and possibly Russian-style pseudocode.
- 🧱 **More block types and functions** — switch/case, try/except, arrays, dictionaries, file I/O, custom subroutines.
- 🖐️ **Free-form diagram building** — place and connect blocks by hand without being tied to a strict tree.
- 📚 **PDF / DOCX worksheet export** — printable assignments straight from the app.

---

## 📁 How your work is stored

Everything lives next to the executable (or next to `main.py` when running from source):

```
<app folder>/
├── Flowchart Builder.exe   ← the app
├── _internal/              ← companion folder (required)
├── config.json             ← your settings
├── recovery.json           ← auto-written when there are unsaved changes
├── blueprints/             ← saved schemas
│   └── My task/
│       ├── chart.json      ← tree + metadata
│       └── main.py         ← mirror of the current code (or main.cpp)
└── exports/                ← default folder for exported diagrams
```

On first launch all of these are created automatically. Nothing goes to the Windows registry or your user profile — you can move the whole folder to a USB stick and it will keep working.

---

## 🧭 Project layout

```
README.md          — this file
LICENSE            — usage terms
requirements.txt   — PySide6
docs/              — screenshots and assets
```

The application source (`.py` files) is kept in a private repository and is not distributed with this one.

---

## 💬 Feedback

Bug reports, feature requests and general feedback are welcome via the **Issues** tab. Please include:

- your OS and version,
- the app version (shown in the title bar),
- the code that caused the problem (if applicable),
- a short description of what you expected vs. what happened.

---

## 📜 License

**Flowchart Builder v1.6 — © 2026. All rights reserved.**

Free to use, **not** open source. See the [LICENSE](LICENSE) file for the full text.

In short:

- ✅ Use it free of charge, personally, in classrooms, or inside a company.
- ✅ Share a link to this repository and the official releases.
- ❌ Do not redistribute, modify, reverse-engineer or repackage the app.
- ❌ Do not redistribute the source code (`.py` files).
- ❌ Do not sell, sublicense or bundle it into another product.

For commercial licensing, OEM bundling or acquisition inquiries, please contact the author.

---

*Made in collaboration with AI.*
