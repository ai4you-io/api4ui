# OpenEdge HCK — Quick Start

**Monitor the health of your OpenEdge databases without leaving VS Code.** The Health Check Kit provides a real-time dashboard for buffer usage, locks, transactions, replication, I/O statistics and more.

---

## Prerequisites

| Requirement | Details |
|---|---|
| **VS Code** | 1.96 or newer |
| **Node.js** | v18 or newer — required to run the HCK backend server |
| **OpenEdge** | Any supported Progress OpenEdge installation |
| **ABL extension** | The OpenEdge ABL VS Code extension must be installed and `abl.configuration.runtimes` must point to your DLC directory |

---

## Install

Install **OpenEdge HCK - Health Check Kit** from the VS Code Marketplace or from the `.vsix` file provided by your team.

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

## Open HCK

Three ways to launch it:

1. Click the **HCK icon** (pulse / heartbeat) in the Activity Bar.
2. Right-click any file in the Explorer → **🏥 HCK - Health Check Kit**.
3. Run the command palette command `Ctrl+Shift+P` → **🏥 HCK - Health Check Kit**.

> The backend starts automatically. The first launch may take a few seconds while OpenEdge initialises.

---

## What you can do

- **Activity monitoring** — buffer usage, lock analysis, page writers, server activity.
- **Database status** — area status, buffer status, checkpoints, connections, files, locks, transactions.
- **Replication monitoring** — replication agents and servers.
- **Statistics** — table/index statistics and user I/O patterns.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Backend fails to start | Check the **HCK Backend** output channel |
| "No OpenEdge runtime configured" | Set `abl.configuration.runtimes` in VS Code settings |
| Port conflicts | Change `hck.httpPort` (default `23003`) or `hck.ablSocketPort` (default `23000`) in settings |

---

> See [USERGUIDE.md](https://github.com/ai4you-io/api4ui/blob/main/openedge/vscode/hck/md/USERGUIDE.md) for a full feature reference.
