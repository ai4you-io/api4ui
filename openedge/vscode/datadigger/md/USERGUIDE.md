# OpenEdge DataDigger — User Guide

**OpenEdge DataDigger** is a VS Code extension that lets you browse, query and edit your OpenEdge (Progress 4GL) databases from inside the editor. It is inspired by the classic DataDigger tool by [Patrick Tingen](https://github.com/patrickTingen).

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Installation](#2-installation)
3. [Configuration](#3-configuration)
   - [OpenEdge runtime](#31-openedge-runtime)
   - [Database connections](#32-database-connections)
   - [Extension settings](#33-extension-settings)
4. [Opening DataDigger](#4-opening-datadigger)
5. [User interface overview](#5-user-interface-overview)
6. [Working with databases](#6-working-with-databases)
7. [Working with tables](#7-working-with-tables)
8. [Querying data](#8-querying-data)
9. [Editing records](#9-editing-records)
10. [Export & Import](#10-export--import)
11. [Connection scopes](#11-connection-scopes)
12. [Multi-project workspaces](#12-multi-project-workspaces)
13. [Troubleshooting](#13-troubleshooting)

---

## 1. Prerequisites

| Requirement | Version / Notes |
|---|---|
| **VS Code** | 1.96 or newer |
| **Node.js** | v20 or newer — required to run the DataDigger backend server |
| **OpenEdge** | Any supported Progress OpenEdge installation |
| **ABL extension** | The OpenEdge ABL VS Code extension must be installed and `abl.configuration.runtimes` must point to your DLC directory |

---

## 2. Installation

### From the Marketplace
Search for **OpenEdge DataDigger** in the Extensions panel and click *Install*.

### From a `.vsix` file
```
Extensions panel → ⋯ menu → Install from VSIX…
```
Select the `.vsix` file provided by your team.

---

## 3. Configuration

### 3.1 OpenEdge runtime

DataDigger delegates the ABL runtime path to the existing ABL extension configuration. Make sure **`abl.configuration.runtimes`** is set:

```json
// settings.json
{
  "abl.configuration.runtimes": [
    { "name": "12.2", "path": "C:/Progress/OpenEdge" }
  ],
  "abl.configuration.defaultRuntime": "12.2"
}
```

If `defaultRuntime` is not set, the first entry in `runtimes` is used.

### 3.2 Database connections

Connections can be configured in three places (see [Connection scopes](#11-connection-scopes)):

**Project scope** — `openedge-project.json` at the root of your project:

```json
{
  "dbConnections": [
    {
      "name": "sports2020",
      "connect": "-db sports2020 -H localhost -S 10001"
    },
    {
      "name": "mydb",
      "connect": "-db mydb -H dbserver -S 20001",
      "aliases": []
    }
  ]
}
```

**User / Workspace scope** — managed through the **Settings → Connections** dialog inside DataDigger (stored in VS Code settings, not in your project files).

### 3.3 Extension settings

| Setting | Default | Description |
|---|---|---|
| `datadigger.httpPort` | `23004` | HTTP port used by the DataDigger backend server |
| `datadigger.ablSocketPort` | `23001` | Socket port for ABL communication |

Change these if the default ports conflict with other services on your machine.

---

## 4. Opening DataDigger

### Activity Bar icon
Click the DataDigger icon (magnifying glass) in the left Activity Bar. DataDigger opens as a full editor tab and the backend starts automatically.

### Right-click from Explorer
Right-click any file in the Explorer panel → **🔍 DataDigger**. DataDigger opens in the context of the project that file belongs to. This is the recommended way to work in a multi-project workspace.

### Command palette
`Ctrl+Shift+P` → type `DataDigger` → select **🔍 DataDigger**.

> **First launch note:** The backend spawns an OpenEdge ABL process and connects to your databases. This can take 5–15 seconds depending on your environment.

---

## 5. User interface overview

```
┌─────────────────────────────────────────────────────────────────┐
│  Database selector ──────────────────────────────── [Settings]  │
├──────────────┬──────────────────────────────────────────────────┤
│ Tables panel │  Fields / Indexes tabs                           │
│              │                                                  │
│  (filtered   │  Field name │ Type │ Format │ Label │ …         │
│   list of    │                                                  │
│   tables)    ├──────────────────────────────────────────────────┤
│              │  WHERE clause input  ▶ Run  ◀▶ History          │
│              ├──────────────────────────────────────────────────┤
│              │  Data grid  (paginated, sortable, selectable)    │
│              │                                                  │
│              │  [Add] [Edit] [Delete] [Export] [Import]         │
└──────────────┴──────────────────────────────────────────────────┘
```

- **Tables panel** — resizable left panel listing all tables in the selected database. Supports text filtering and favorites (⭐).
- **Fields tab** — shows all fields for the selected table: name, data type, format, label, and more.
- **Indexes tab** — shows all indexes for the selected table.
- **Data grid** — paginated, sortable view of the table data. Rows are loaded 100 at a time; scroll down to load more.

---

## 6. Working with databases

### Selecting a database
Use the **database selector** drop-down at the top of the screen to switch between connected databases.

### Refreshing
Clicking the same database again reloads the table list.

---

## 7. Working with tables

### Finding a table
Type in the filter box above the tables list. The list filters in real time.

### Favorites
Click ⭐ next to a table name to pin it to the top of the list. Favorites are persisted between sessions.

### Fields
Select a table to load its field list in the **Fields** tab. Columns shown: name, data type, format, label, description, mandatory flag.

### Indexes
The **Indexes** tab shows all indexes, their fields, whether the index is unique/primary, and the active flag.

### Column visibility
Right-click a column header in the data grid (or use the column visibility toggle) to show/hide individual columns. Your preferences are remembered per table.

---

## 8. Querying data

### WHERE clause
Type a standard OpenEdge WHERE clause in the input box above the data grid (without the `WHERE` keyword):

```
custnum > 100 AND country = "US"
```

Press **Enter** or click ▶ to run the query. The data grid reloads with matching records.

### Query history
Use the ◀ ▶ arrows beside the input to navigate through your last queries. Click the history icon to see the full list.

### Sorting
Click any column header in the data grid to sort ascending; click again to sort descending.

### Pagination
The first 100 records are loaded automatically. Scroll to the bottom of the grid to load the next 100.

---

## 9. Editing records

### Viewing a record
Double-click a row or select it and click **View** to open the record detail dialog showing all field values.

### Adding a record
Click **Add** to open the add-record form. Fill in the field values and confirm.

### Editing a record
Select one or more rows and click **Edit** to modify field values. All selected rows are updated.

### Deleting a record
Select one or more rows and click **Delete**. A confirmation dialog is shown before the operation runs. **This cannot be undone.**

---

## 10. Export & Import

### Export
1. (Optional) Select specific rows to export only those; otherwise all loaded rows are exported.
2. Click **Export**.
3. Choose the destination file path and export format (`.d` dump or other supported formats).
4. Additional options:
   - **Open folder** after export — reveals the file in the Explorer.
   - **Open file** after export — opens the dump file as a text document in VS Code.
   - **Copy to clipboard** — copies the data as tab-separated values.

### Import
1. Click **Import**.
2. Select or paste the path to a `.d` dump file.
3. Confirm — records are inserted into the current table.

---

## 11. Connection scopes

DataDigger supports three connection scopes, selectable from the top drop-down:

| Scope | Where connections come from | Who can change them |
|---|---|---|
| **Project** | `openedge-project.json` in your project root | Commit to source control |
| **Workspace** | VS Code workspace settings | Shared across the current `.code-workspace` |
| **User** | VS Code user settings | Personal / machine-specific |

Switch scope using the drop-down next to the database selector. Open **Settings → Connections** to add, edit or remove connections for any scope.

Connections support:
- A **display name** (shown in the drop-down) separate from the physical database name.
- An optional **username** and **password** (password stored in VS Code SecretStorage).

---

## 12. Multi-project workspaces

When you have multiple folders open in a VS Code workspace, DataDigger detects all of them. Use the **project switcher** drop-down (visible in workspace mode) to select which project's databases to browse.

Alternatively, right-click any file in the Explorer to open DataDigger pre-selected on that file's project.

---

## 13. Troubleshooting

### Backend fails to start
Open the **DataDigger Backend** output channel (*View → Output → DataDigger Backend*) for detailed logs.

Common causes:
- OpenEdge runtime path (`abl.configuration.runtimes`) is not configured or the path does not exist.
- The configured ports (`datadigger.httpPort` / `datadigger.ablSocketPort`) are already in use.
- The `.pl` procedure library was not built — run `npm run build-datadigger-pl` from the extension source.

### "No OpenEdge runtime configured"
Set `abl.configuration.runtimes` in your VS Code settings (user or workspace level). Example:

```json
"abl.configuration.runtimes": [
  { "name": "12.2", "path": "/usr/dlc" }
]
```

### "No `openedge-project.json` found"
Create `openedge-project.json` in the root of your project folder with at least one valid `dbConnections` entry (see [Database connections](#32-database-connections)).

### Extension not loading / blank screen
1. Reload the window: `Ctrl+Shift+P` → *Developer: Reload Window*.
2. Check the **OpenEdge DataDigger** output channel for errors.
3. Rebuild the extension if running from source: `npm run compile`.

### Port conflicts
Change the ports in your VS Code settings:
```json
"datadigger.httpPort": 24000,
"datadigger.ablSocketPort": 24001
```

---

> For a concise quick start, see [`docs/QUICKSTART.md`](QUICKSTART.md).
