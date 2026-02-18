# log.os()

A single-file, browser-based daily productivity tool combining a task list and a running text log.

> *The name is a nod to **Logos** — the Greek philosophical principle of reason and judgment as the controlling force of the universe — rendered in the style of a function call.*

**Created by [Kevin Guyer](https://github.com/kevinguyer)**
**Latest release:** [github.com/kevinguyer/logos](https://github.com/kevinguyer/logos)

---

## What is log.os()?

log.os() is a lightweight daily planner that lives entirely in a single `.html` file. Open it in your browser, keep it pinned in a tab, and use it to track tasks and capture a running log throughout your day. All data is stored locally via `localStorage` — no server, no account, no sync, no internet required after the initial load.

---

## Getting Started

1. Download `index.html` from this repository
2. Open it in Chrome, Firefox, or Edge (via `File > Open` or drag it into the browser)
3. Start typing in the log panel and adding tasks on the right
4. That's it — your data persists automatically in your browser's local storage

---

## Design Goals

log.os() was built around a clear set of design principles drawn from a product requirements document written before a single line of code existed. These goals shape every decision in the app.

### The Day as the Primary Unit

Everything in log.os() is organized around **the day**. Each day has exactly one task list and one log entry. There is always one active (editable) day; all prior days are read-only archives. Days with no activity simply don't exist — no empty placeholders, no filler.

Day transitions are **strictly manual**. The app never auto-advances or nags you. When you're ready to start a new day, you initiate it. Completed tasks stay with the day they were finished; open tasks carry forward automatically.

### Radical Simplicity

Tasks have no priorities, no subtasks, no dependencies, no tags, no due dates, no time estimates. A task has a title and a status: open or complete. This is intentional. The goal is a friction-free capture tool, not a project management system.

The log is a single block of plain text per day. The only markup supported is triple-backtick code blocks for display purposes. No rich text, no markdown rendering, no formatting toolbar.

### Local-First, Single-File Architecture

The entire application — HTML, CSS, JavaScript, fonts — is self-contained in one `.html` file. You can:

- Save it anywhere on your machine
- Open it via `file://` with no web server
- Back it up by copying a single file
- Share it with anyone who has a browser

All data lives in your browser's `localStorage`. Nothing leaves your machine.

### Retro Terminal Aesthetic

The visual design is inspired by early-90s CRT monitors and the Pip-Boy interface from Fallout. All UI elements render in a **single foreground color** against a dark background. No gradients, no multicolor icons, no decorative imagery. Visual depth comes from phosphor glow effects, CRT scanline overlays, and subtle vignetting.

Nine themes are included — each a different take on the monochrome terminal palette:

| Theme | Inspiration |
|---|---|
| Green Screen (default) | VT100 / Pip-Boy phosphor green |
| Amber | Amber monochrome CRT monitors |
| IBM 5151 / Sepia | IBM PC monochrome display |
| Cool Blue | Blue-phosphor CRT and LCD displays |
| Wyse 60 | Wyse terminal white-on-black |
| Commodore 64 | C64 blue/purple palette |
| Apple II | Apple II green phosphor |
| Paper White | High-contrast e-ink light mode |
| Kindle | Warm e-ink light mode |

### Keyboard-Driven Workflow

The app is designed to be operated primarily from the keyboard. All major actions have hotkeys, and all hotkeys are **user-rebindable** from the hotkey reference dialog. Default bindings:

| Action | Default Hotkey |
|---|---|
| Focus Log Panel | `Ctrl+1` |
| Focus Task Panel | `Ctrl+2` |
| Add New Task | `Ctrl+Shift+N` |
| Complete First Task | `Ctrl+Shift+D` |
| Initiate New Day | `Ctrl+Shift+Enter` |
| Search Logs | `Ctrl+Shift+F` |
| History Browser | `Ctrl+Shift+H` |
| Settings | `Ctrl+,` |
| Cycle Theme | `Ctrl+Shift+T` |
| Export | `Ctrl+Shift+E` |

---

## Features

### Task List
- Add, complete, uncomplete, edit, and delete tasks for the current day
- Open tasks carry forward automatically when a new day is initiated
- Completed tasks stay archived with the day they were finished
- Prior-day task lists are visible (read-only) in the history sections and history browser

### Log
- A freely editable plain-text area for the current day
- Autosaves to `localStorage` on a short debounce (configurable: 500ms–2s)
- Tab key inserts a tab character or 4 spaces (configurable)
- Triple-backtick code blocks render as visually distinct blocks in read-only view
- Prior-day logs are readable (and text-selectable) but not editable

### Scratchpad
- A persistent quick-notes area at the bottom of the task panel
- Resets daily by default; can be **pinned** to persist across day transitions
- Can be **expanded** to show more content when needed, then collapsed back to normal height

### History Browser
- The last 7 active days are accessible as collapsible sections within the main panels
- The full history browser (via `[History]` button or `Ctrl+Shift+H`) lets you browse all past days
- Click any date to see its tasks and log content

### Log Search
- Full-text search across all stored log entries (no time limit)
- Shows date and context snippet for each match, with the search term highlighted
- Click a result to view that day's full log

### Export / Backup
- Exports all data as a single Markdown file (most recent day first)
- Choose a cleanup option after export: keep all data, purge entries older than 90 days, or purge entries older than 30 days
- Cleanup only runs after the export file has been successfully generated

### Settings
- Theme selection and live preview
- Toggle CRT scanlines and vignette effects
- Configure tab key behavior and autosave delay
- All settings persist in `localStorage`

---

## Data Storage

All data is stored under `localStorage` keys prefixed with `logos:`:

| Key | Contents |
|---|---|
| `logos:currentDay` | ISO date string of the active day |
| `logos:log:<date>` | Log content for a given date |
| `logos:tasks:<date>` | JSON array of tasks for a given date |
| `logos:settings` | User preferences (theme, hotkeys, etc.) |
| `logos:scratchpad` | Scratchpad content |

`localStorage` is browser- and origin-scoped. Data does not sync across browsers or machines. For backup, use the Export function.

---

## Out of Scope

The following are intentionally **not** part of log.os():

- Multi-device sync or cloud storage
- User authentication or multi-user support
- Import/restore from exported files
- Mobile or tablet layouts
- Task priorities, dependencies, tags, or hierarchy
- Markdown rendering beyond triple-backtick code blocks
- Rich text editing
- Notifications or reminders
- Recurring tasks or time tracking
- Integration with external services

---

## Browser Compatibility

- **Supported:** Latest Chrome, Firefox, Edge
- **Nice-to-have:** Safari
- **Requirement:** Must work via `file://` protocol (no HTTP server needed)

---

## License

See [LICENSE](LICENSE).
