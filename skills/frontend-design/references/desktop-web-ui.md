# Track 2: Desktop & Web UI Playbook

Use this playbook when designing SaaS dashboards, admin panels, data-heavy tools, productivity apps, or desktop applications (Tauri, Electron, web-wrapped desktop tools).

---

## 1. Information Architecture & Density

- **Multi-Pane & Splitter Layouts**:
  - Structure complex apps into clean panes: Primary Navigation Rail / Sidebar (collapsible to icon-only), Main Workspace / Canvas, and an optional Contextual Inspector / Right Sidebar.
  - For dense editing environments (like VS Code, Linear, or Notion), support resizable split panes with subtle draggable dividers.
- **High-Density Data Tables**:
  - Sticky table headers with subtle row divider borders or alternating zebra tints.
  - Column alignment rules: text left-aligned, numbers/currencies/metrics right-aligned, status badges/actions centered.
  - Row action menus (hover-revealed or trailing `...` icon button) so secondary actions don't clutter the view.
- **Toolbar & Filter Bars**:
  - Place a unified horizontal toolbar directly above the main view: Global Search (`Cmd+K`), Multi-select Filters, Group-by / Sort dropdowns, and View switchers (Table, Kanban, List).

---

## 2. Desktop Shell & Window Chrome (Tauri / Electron)

When building or styling desktop apps with custom frameless windows:

- **Window Drag & Interactive Areas**:
  - Make the custom titlebar draggable: `-webkit-app-region: drag;`
  - **CRITICAL**: Every clickable element inside the titlebar (search input, buttons, tabs, window controls) **must** have `-webkit-app-region: no-drag;`, otherwise clicks and typing will drag the window instead of interacting.
- **macOS Traffic Light Clearance**:
  - On macOS frameless windows (`titleBarStyle: 'hiddenInset'`), leave at least **72px of left padding** in the titlebar so tabs or buttons do not collide with the native red/yellow/green close/minimize/zoom buttons.
- **Right-Click Context Menus**:
  - Desktop users expect right-clicks. Intercept `onContextMenu` on rows, cards, or canvas items to show custom context menus (Cut, Copy, Duplicate, Rename, Delete).
- **Bottom Status Bar**:
  - Add a slim persistent status bar at the bottom for background sync state, line/column info, word count, zoom level, or keyboard shortcuts help.

---

## 3. Keyboard-First Ergonomics

- **Command Palette (`Cmd+K` / `Ctrl+K`)**:
  - Provide a global search and command palette for rapid navigation, action execution, and switching views.
- **Keyboard Shortcuts**:
  - Standard OS conventions: `Escape` closes active modals, sheets, and menus; `Enter` confirms dialogs; `Cmd+S` saves (preventing default browser save dialog); `Cmd+,` opens Settings/Preferences.
- **Focus Rings & Roving Tabindex**:
  - Ensure high-contrast `:focus-visible` styling on active elements for full keyboard accessibility without distracting mouse users.

---

## 4. Anti-Patterns to Avoid in Desktop & Web UI

- **No "Marketing-Style" Oversized Cards**: Do not use giant 400px cards with 32px padding when users need to compare dozens of items. Use compact lists, tables, or dense cards.
- **No Unconstrained Ultrawide Sprawl**: When full-width tables stretch across 32-inch 4K monitors, keep data rows scannable with structured column widths or max-width constraints.
- **No Unclosable State**: Every modal, drawer, and popover must close cleanly via `Escape` key and backdrop click.
