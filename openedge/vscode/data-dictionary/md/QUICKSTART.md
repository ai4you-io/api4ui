# OpenEdge Data Administration — Quick Start

**Edit your OpenEdge database schema without leaving VS Code.** Browse and modify tables, fields, indexes and sequences — the modern equivalent of the classic Progress Data Administration tool.

---

## Prerequisites

| Requirement       | Details                                                                                                                |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **VS Code**       | 1.96 or newer                                                                                                          |
| **Node.js**       | v18 or newer — required to run the Data Administration backend server                                                  |
| **OpenEdge**      | Any supported Progress OpenEdge installation                                                                           |
| **ABL extension** | The OpenEdge ABL VS Code extension must be installed and `abl.configuration.runtimes` must point to your DLC directory |

---

## Install

Install **OpenEdge Data Administration** from the VS Code Marketplace or from the `.vsix` file provided by your team.

---

## Configure a database connection

Add database connections in your `openedge-project.json` at the project root:

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

Connections can also be managed through VS Code workspace or user settings.

---

## Open Data Administration

Three ways to launch it:

1. Click the **Data Administration icon** (book) in the Activity Bar.
2. Right-click any file in the Explorer → **📖 Dictionary Editor**.
3. Run `Ctrl+Shift+P` → **📖 Dictionary Editor**.

> The backend starts automatically. The first launch may take a few seconds while OpenEdge initialises.

---

## What you can do

- **Browse** tables, fields, indexes and sequences across connected databases.
- **Create, edit and delete** tables, fields, indexes and sequences.
- **Dump and load** schema definitions (`.df` files).
- **Dump and load** data (`.d` files).
- **Refresh** the schema tree at any time from the sidebar.

---

## Troubleshooting

| Symptom                          | Fix                                                                                            |
| -------------------------------- | ---------------------------------------------------------------------------------------------- |
| Backend fails to start           | Check the **Dictionary Backend** output channel                                                |
| "No OpenEdge runtime configured" | Set `abl.configuration.runtimes` in VS Code settings                                           |
| Port conflicts                   | Change `dictionary.httpPort` (default `23005`) or `dictionary.ablSocketPort` (default `23002`) |

---

> See [USERGUIDE.md](https://github.com/ai4you-io/api4ui/blob/main/openedge/vscode/data-dictionary/md/USERGUIDE.md) for a full feature reference.
