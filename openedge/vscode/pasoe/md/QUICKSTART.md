# OpenEdge PASOE — Quick Start

**Manage your Progress Application Server for OpenEdge (PASOE) servers from inside VS Code.** Configure, monitor and inspect ABL applications without leaving the editor.

![ServerConfig](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_server_config.gif)
![Overview](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_overview.gif)
![Detail1](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_detail1.gif)
![Detail2](https://raw.githubusercontent.com/ai4you-io/api4ui/d1636ae2301c18e94c98314e26943b12883772bf/openedge/vscode/pasoe/vscode_pasoe_detail2.gif)

---

## Prerequisites

| Requirement | Details |
|---|---|
| **VS Code** | 1.96 or newer |
| **PASOE server** | A running Progress Application Server for OpenEdge (OEManager must be accessible) |
| **Credentials** | Server username and password (default: `tomcat` / `tomcat`) |
| **Network access** | VS Code must be able to reach the OEManager HTTP(S) port on the PASOE host |

---

## Install

Install **OpenEdge ABL - PASOE** from the VS Code Marketplace or from the `.vsix` file provided by your team.

---

## Configure a server

Open VS Code **Settings** (`Ctrl+,`) and search for `openedge-pasoe.servers`. Add one entry per server:

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
  }
]
```

You can also add and edit servers from inside the PASOE UI — see **Settings** in the sidebar.

---

## Open PASOE

Two ways to launch it:

1. **Command palette** — `Ctrl+Shift+P` → **Launch OpenEdge PASOE configuration 😎**
2. **Right-click** any file in the Explorer → select the PASOE command.

> The UI opens as a full editor tab and connects immediately to the configured servers.

---

## What you can do

- **Monitor** all configured servers and see real-time status at a glance.
- **Browse ABL applications** deployed on each server.
- **Configure** multiple servers with HTTP/HTTPS and Basic authentication.
- **Add, edit or remove** server entries directly from the UI.

---

> See [USERGUIDE.md](https://github.com/ai4you-io/api4ui/blob/main/openedge/vscode/pasoe/md/USERGUIDE.md) for a full feature reference.
