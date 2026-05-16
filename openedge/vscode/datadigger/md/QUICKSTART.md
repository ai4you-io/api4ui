# OpenEdge DataDigger — Quick Start

**Browse, query and edit your OpenEdge databases without leaving VS Code.** <br/>
It is inspired by the classic DataDigger tool by [Patrick Tingen](https://github.com/patrickTingen).

---

## Prerequisites

| Requirement | Details |
|---|---|
| **VS Code** | 1.96 or newer |
| **Node.js** | v20 or newer — required to run the DataDigger backend server |
| **OpenEdge** | Any supported Progress OpenEdge installation |
| **ABL extension** | The OpenEdge ABL VS Code extension must be installed and `abl.configuration.runtimes` must point to your DLC directory |

---

## Install

Install **OpenEdge DataDigger** from the VS Code Marketplace or from the `.vsix` file provided by your team.

---

## Configure a database connection

Connections can be set up in three scopes:

| Scope | Where | Use case |
|---|---|---|
| **Project** | `openedge-project.json` in your project root | Shared with the team via source control |
| **Workspace** | VS Code workspace settings | Shared across all folders in a `.code-workspace` |
| **User** | VS Code user settings | Personal / machine-specific connections |
| **Folder** | Per-folder VS Code settings | Per-project overrides inside a multi-folder workspace |

**Project scope example** — add to `openedge-project.json`:

```json
{
  "dbConnections": [
    {
      "name": "sports2020",
      "connect": "-db sports2020 -H localhost -S 10001"
    }
  ]
}
```

**User / Workspace / Folder scope** — manage connections directly inside DataDigger via **Settings → Connections** (no file editing required).

> For full details on connection scopes see [`docs/USERGUIDE.md` → Connection scopes](USERGUIDE.md#11-connection-scopes).

---

## Open DataDigger

Three ways to launch it:

1. Click the **DataDigger icon** in the Activity Bar (left sidebar).
2. Right-click any `.p` / `.cls` file in the Explorer → **🔍 DataDigger**.
3. Run the command palette command `DataDigger`.

> The backend starts automatically. The first launch may take a few seconds while OpenEdge initialises.

---

## What you can do

- **Browse** tables and fields across all connected databases.
- **Query** data with a custom WHERE clause and navigate results.
- **Add / Edit / Delete** records directly from the data grid.
- **Export** data to a `.d` dump file or copy it to the clipboard.
- **Import** `.d` dump files back into a table.
- **Favorite** tables for quick access.
- Switch between **project**, **workspace** and **user-level** connection scopes.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Backend fails to start | Check the **DataDigger Backend** output channel |
| "No OpenEdge runtime configured" | Set `abl.configuration.runtimes` in VS Code settings |
| "No `openedge-project.json` found" | Create the file with a valid `dbConnections` entry |

---

> See [`docs/USERGUIDE.md`](USERGUIDE.md) for a full feature reference.
