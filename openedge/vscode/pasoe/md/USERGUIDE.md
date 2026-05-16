# OpenEdge PASOE — User Guide

**OpenEdge ABL - PASOE** is a VS Code extension that provides a graphical interface for configuring and monitoring Progress Application Server for OpenEdge (PASOE) servers directly within the editor.

![ServerConfig](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_server_config.gif)
![Overview](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_overview.gif)
![Detail1](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_detail1.gif)
![Detail2](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_detail2.gif)

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Installation](#2-installation)
3. [Configuration](#3-configuration)
   - [Server settings](#31-server-settings)
   - [Extension settings reference](#32-extension-settings-reference)
4. [Opening the PASOE UI](#4-opening-the-pasoe-ui)
5. [User interface overview](#5-user-interface-overview)
6. [Managing servers](#6-managing-servers)
7. [Monitoring server status](#7-monitoring-server-status)
8. [Working with ABL applications](#8-working-with-abl-applications)
9. [Troubleshooting](#9-troubleshooting)

---

## 1. Prerequisites

| Requirement | Version / Notes |
|---|---|
| **VS Code** | 1.96 or newer |
| **PASOE server** | A running Progress Application Server for OpenEdge with OEManager enabled |
| **Network access** | The VS Code host must be able to reach the OEManager HTTP(S) endpoint |

---

## 2. Installation

### From the Marketplace
Search for **OpenEdge ABL - PASOE** in the Extensions panel and click *Install*.

### From a `.vsix` file
```
Extensions panel → ⋯ menu → Install from VSIX…
```
Select the `.vsix` file provided by your team.

---

## 3. Configuration

### 3.1 Server settings

Servers are configured in VS Code settings (`Ctrl+,`) under `openedge-pasoe.servers`. Each entry is a JSON object:

```json
"openedge-pasoe.servers": [
  {
    "name": "Development Server",
    "host": "localhost",
    "port": 8810,
    "transport": "http",
    "authType": "basic",
    "username": "tomcat",
    "password": "tomcat"
  },
  {
    "name": "Production Server",
    "host": "prod.example.com",
    "port": 8843,
    "transport": "https",
    "authType": "basic",
    "username": "tomcat",
    "password": "tomcat"
  }
]
```

Settings are stored at **User** (global) scope by default, so they apply to all workspaces.

You can also manage servers from inside the PASOE UI without editing JSON directly.

### 3.2 Extension settings reference

| Setting | Type | Default | Description |
|---|---|---|---|
| `openedge-pasoe.servers` | array | Two example entries | List of PASOE server connection configurations |

Each server object has these required fields:

| Field | Type | Description |
|---|---|---|
| `name` | string | Display name shown in the server list |
| `host` | string | Hostname or IP address of the PASOE server |
| `port` | number | OEManager HTTP(S) port (typically `8810` for http, `8843` for https) |
| `transport` | `"http"` \| `"https"` | Transport protocol |
| `authType` | `"basic"` | Authentication method — use `"basic"` for HTTP Basic Authentication |
| `username` | string | Username (default: `"tomcat"`) |
| `password` | string | Password (default: `"tomcat"`) |

---

## 4. Opening the PASOE UI

### Command palette
`Ctrl+Shift+P` → type `PASOE` → select **Launch OpenEdge PASOE configuration 😎**.

### Explorer context menu
Right-click any file in the Explorer panel and select the PASOE launch command.

> Multiple panels can be open simultaneously — each is independent.

---

## 5. User interface overview

```
┌────────────────────────────────────────────────────────────────────┐
│  Server selector  ────────────────────────────────  [Settings] [+] │
├────────────────────────────────────────────────────────────────────┤
│  Server status bar  (connected / disconnected / error)             │
├────────────────────────────────────────────────────────────────────┤
│  Overview panel                                                     │
│    Server info │ Active agents │ Sessions │ Connections             │
├────────────────────────────────────────────────────────────────────┤
│  ABL Applications list                                              │
│    Name │ State │ Type │ Details                                    │
└────────────────────────────────────────────────────────────────────┘
```

- **Server selector** — drop-down to switch between configured servers.
- **Settings button** — opens the server configuration form to add/edit/delete servers.
- **Status bar** — shows current connection state and any error messages.
- **Overview panel** — high-level metrics: active agents, client sessions, connections.
- **ABL Applications list** — all deployed ABL applications on the selected server with their current state.

---

## 6. Managing servers

### Adding a server
Click the **+** button or open **Settings** in the UI and fill in the server form. The new entry is saved immediately to VS Code's global settings.

### Editing a server
Select a server from the list in **Settings**, modify the fields, and save.

### Deleting a server
Open **Settings**, select the server and click **Delete**.

### Switching servers
Use the server selector drop-down at the top of the UI to switch between configured servers. The UI reloads automatically.

---

## 7. Monitoring server status

### Connection status
The status bar at the top of the UI shows:
- ✅ **Connected** — server is reachable and credentials are accepted.
- ⚠️ **Connecting** — initial connection in progress.
- ❌ **Error** — connection failed; hover for the error message.

### Overview metrics
The overview panel shows live data fetched from OEManager:
- **Active agents** — number of ABL agent processes currently running.
- **Client sessions** — active client connections to the server.
- **Server connections** — total connections established.

> Data refreshes automatically when the panel is in focus.

---

## 8. Working with ABL applications

### Application list
All ABL applications deployed on the selected PASOE server are listed with:
- **Name** — application identifier.
- **State** — running, stopped, or error.
- **Type** — REST, SOAP, or other.

### Viewing application details
Click an application row to expand its detail view, showing configuration and runtime information.

---

## 9. Troubleshooting

### Extension output log
Open *View → Output → OpenEdge PASOE* for timestamped debug messages from the extension host.

### "Connection refused" or blank screen
- Verify `host` and `port` match the OEManager endpoint (not the ABL application port).
- Check that the PASOE server is running: `$DLC/bin/oemanager` or your administration console.
- Test connectivity: `curl http://<host>:<port>/oemanager/applications`.

### Authentication failure
- Double-check `username` and `password` in settings.
- Default OEManager credentials are `tomcat` / `tomcat` — change these in the PASOE Tomcat configuration if your site uses different values.

### Extension not loading / blank screen after launch
1. Check the **OpenEdge PASOE** output channel for errors.
2. Reload the window: `Ctrl+Shift+P` → *Developer: Reload Window*.
3. Reinstall the extension if the issue persists.


