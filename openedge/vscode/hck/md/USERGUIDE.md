# OpenEdge HCK — User Guide

**OpenEdge HCK - Health Check Kit** is a VS Code extension that provides a real-time monitoring and analysis dashboard for OpenEdge databases. It gives you instant visibility into buffer usage, lock contention, transactions, replication status and I/O statistics — all from inside the editor.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Installation](#2-installation)
3. [Configuration](#3-configuration)
   - [OpenEdge runtime](#31-openedge-runtime)
   - [Database connections](#32-database-connections)
   - [Extension settings](#33-extension-settings)
4. [Opening HCK](#4-opening-hck)
5. [User interface overview](#5-user-interface-overview)
6. [Activity monitoring](#6-activity-monitoring)
7. [Database status](#7-database-status)
8. [Replication monitoring](#8-replication-monitoring)
9. [Statistics](#9-statistics)
10. [Multi-project workspaces](#10-multi-project-workspaces)
11. [Troubleshooting](#11-troubleshooting)

---

## 1. Prerequisites

| Requirement | Version / Notes |
|---|---|
| **VS Code** | 1.96 or newer |
| **Node.js** | v18 or newer — required to run the HCK backend server |
| **OpenEdge** | Any supported Progress OpenEdge installation |
| **ABL extension** | The OpenEdge ABL VS Code extension must be installed and `abl.configuration.runtimes` must point to your DLC directory |

---

## 2. Installation

### From the Marketplace
Search for **OpenEdge HCK - Health Check Kit** in the Extensions panel and click *Install*.

### From a `.vsix` file
```
Extensions panel → ⋯ menu → Install from VSIX…
```
Select the `.vsix` file provided by your team.

---

## 3. Configuration

### 3.1 OpenEdge runtime

HCK delegates the ABL runtime path to the existing ABL extension configuration. Make sure **`abl.configuration.runtimes`** is set:

```json
// settings.json
{
  "abl.configuration.runtimes": [
    { "name": "12.2", "path": "C:/Progress/OpenEdge" }
  ],
  "abl.configuration.defaultRuntime": "12.2"
}
```

### 3.2 Database connections

**Project scope** — `openedge-project.json` at the root of your project:

```json
{
  "dbConnections": [
    {
      "name": "mydb",
      "connect": "-db mydb -H dbserver -S 20001"
    }
  ]
}
```

**Workspace / User scope** — configure `openedge.abl.dbConnections` in VS Code workspace or user settings.

### 3.3 Extension settings

| Setting | Default | Description |
|---|---|---|
| `hck.httpPort` | `23003` | HTTP port used by the HCK backend server |
| `hck.ablSocketPort` | `23000` | Socket port for ABL communication |

Change these if the default ports conflict with other services on your machine.

---

## 4. Opening HCK

### Activity Bar icon
Click the HCK icon (heartbeat/pulse) in the left Activity Bar. HCK opens as a full editor tab and the backend starts automatically.

### Explorer context menu
Right-click any file in the Explorer panel → **🏥 HCK - Health Check Kit**. HCK opens in the context of the project that file belongs to.

### Command palette
`Ctrl+Shift+P` → type `HCK` → select **🏥 HCK - Health Check Kit**.

> **First launch note:** The backend spawns an OpenEdge ABL process and connects to your databases. This can take 5–15 seconds depending on your environment.

### Quick Actions sidebar
The **Quick Actions** tree view (visible in the HCK Activity Bar panel) provides shortcut buttons to jump directly to specific dashboards.

---

## 5. User interface overview

```
┌─────────────────────────────────────────────────────────────────────┐
│  Database selector ──────────────────────────────── [Refresh]       │
├──────────────────────┬──────────────────────────────────────────────┤
│  Navigation sidebar  │  Dashboard content area                      │
│                      │                                              │
│  ▸ Activity          │  (selected dashboard metrics and tables)     │
│    Buffer Usage      │                                              │
│    Lock Analysis     │                                              │
│    Page Writers      │                                              │
│    Server Activity   │                                              │
│    Summary           │                                              │
│  ▸ Database Status   │                                              │
│    Area Status       │                                              │
│    Buffer Status     │                                              │
│    Checkpoints       │                                              │
│    Connections       │                                              │
│    Files             │                                              │
│    Locks             │                                              │
│    Transactions      │                                              │
│  ▸ Replication       │                                              │
│    Agents            │                                              │
│    Servers           │                                              │
│  ▸ Statistics        │                                              │
│    Table/Index Stats │                                              │
│    User I/O          │                                              │
└──────────────────────┴──────────────────────────────────────────────┘
```

Use the **database selector** at the top to switch between connected databases. Click **Refresh** to reload the current dashboard.

---

## 6. Activity monitoring

### Buffer Usage
Shows current buffer pool utilisation: hit ratio, dirty buffers, buffer reads and writes. Useful for diagnosing memory pressure.

Key columns: buffer pool name, size, hit ratio (%), reads, writes, dirty count.

### Lock Analysis
Displays active record locks: holder, lock type (share/exclusive), table, record, duration.

Use this dashboard to identify lock contention and long-running transactions holding locks.

### Page Writers
Shows page writer agent activity: pages flushed, I/O wait, cycles. Indicates whether the page writer is keeping up with dirty buffer writes.

### Server Activity
Overview of active ABL server agents and their current state: idle, busy, waiting.

### Summary
High-level activity summary combining the most important metrics from all activity dashboards on a single screen.

---

## 7. Database status

### Area Status
Lists all database storage areas with their current fill level, extent information and available space.

### Buffer Status
Detailed buffer pool status per area: allocated buffers, locked pages, read/write counts.

### Checkpoints
Checkpoint history and timing — useful for tuning checkpoint frequency and identifying I/O spikes.

### Connections
Active client connections to the database: connection type, user, start time, idle time.

### Files
Database files and extents: path, size, free space, type.

### Locks
Current lock table state: total lock entries, available entries, wait queue depth.

### Transactions
Active and recent transactions: transaction ID, user, state, duration, undo blocks used.

---

## 8. Replication monitoring

### Replication Agents
Status of all OpenEdge Replication agents: agent name, role (source/target), state, lag, last sync time.

### Replication Servers
Replication server instances: host, port, connected agents, current status, error messages if any.

---

## 9. Statistics

### Table / Index Statistics
Read/write/create/delete counts per table and index. Helps identify hot tables and missing or unused indexes.

Columns: table/index name, reads, writes, creates, deletes, last reset time.

### User I/O
Per-user I/O breakdown: logical reads, physical reads, writes per connected user. Identifies heavy hitters consuming I/O resources.

---

## 10. Multi-project workspaces

When multiple folders are open in a VS Code workspace, HCK detects all of them. Use the **project switcher** drop-down (visible in workspace mode) to select which project's databases to monitor.

Alternatively, right-click any file in the Explorer to open HCK pre-selected on that file's project.

---

## 11. Troubleshooting

### Backend fails to start
Open the **HCK Backend** output channel (*View → Output → HCK Backend*) for detailed logs.

Common causes:
- OpenEdge runtime path (`abl.configuration.runtimes`) is not configured or the path does not exist.
- The configured ports (`hck.httpPort` / `hck.ablSocketPort`) are already in use.
- The `.pl` procedure library was not built — run `npm run build-hck-pl` from the extension source.

### "No OpenEdge runtime configured"
Set `abl.configuration.runtimes` in your VS Code settings:

```json
"abl.configuration.runtimes": [
  { "name": "12.2", "path": "/usr/dlc" }
]
```

### Dashboard shows no data
- Ensure at least one `dbConnections` entry is configured (see [Database connections](#32-database-connections)).
- Click **Refresh** to force a data reload.
- Check that the connected database is running and accessible.

### Port conflicts
Change the ports in VS Code settings:
```json
"hck.httpPort": 24003,
"hck.ablSocketPort": 24000
```

### Extension not loading / blank screen
1. Reload the window: `Ctrl+Shift+P` → *Developer: Reload Window*.
2. Check the **OpenEdge HCK** output channel for errors.
3. Rebuild the extension if running from source: `npm run compile`.

---

> For a concise quick start, see [`docs/QUICKSTART.md`](QUICKSTART.md).
