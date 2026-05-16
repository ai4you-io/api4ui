# OpenEdge Data Administration — User Guide

**OpenEdge Data Administration** is a VS Code extension that provides a modern data administration interface for OpenEdge databases — the equivalent of the classic Progress Data Administration tool, built natively into VS Code. It lets you browse and edit database schema, dump and load definitions and data, and run schema reports without leaving the editor.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Installation](#2-installation)
3. [Configuration](#3-configuration)
   - [OpenEdge runtime](#31-openedge-runtime)
   - [Database connections](#32-database-connections)
   - [Extension settings](#33-extension-settings)
4. [Opening Data Administration](#4-opening-data-administration)
5. [User interface overview](#5-user-interface-overview)
6. [Data Dictionary](#6-data-dictionary)
   - [Tables](#61-tables)
   - [Fields](#62-fields)
   - [Indexes](#63-indexes)
   - [Sequences](#64-sequences)
7. [Dump and Load](#7-dump-and-load)
   - [Schema definitions (.df)](#71-schema-definitions-df)
   - [Data (.d files)](#72-data-d-files)
   - [Sequence values](#73-sequence-values)
8. [Database properties](#8-database-properties)
9. [Reports](#9-reports)
10. [Multi-project workspaces](#10-multi-project-workspaces)
11. [Troubleshooting](#11-troubleshooting)

---

## 1. Prerequisites

| Requirement       | Version / Notes                                                                                                        |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **VS Code**       | 1.96 or newer                                                                                                          |
| **Node.js**       | v18 or newer — required to run the Data Administration backend server                                                  |
| **OpenEdge**      | Any supported Progress OpenEdge installation                                                                           |
| **ABL extension** | The OpenEdge ABL VS Code extension must be installed and `abl.configuration.runtimes` must point to your DLC directory |

---

## 2. Installation

### From the Marketplace

Search for **OpenEdge Data Administration** in the Extensions panel and click _Install_.

### From a `.vsix` file

```
Extensions panel → ⋯ menu → Install from VSIX…
```

Select the `.vsix` file provided by your team.

---

## 3. Configuration

### 3.1 OpenEdge runtime

Data Administration delegates the ABL runtime path to the existing ABL extension configuration. Make sure **`abl.configuration.runtimes`** is set:

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
      "connect": "-db mydb -H dbserver -S 20001"
    }
  ]
}
```

**Workspace / User scope** — configure `openedge.abl.dbConnections` in VS Code workspace or user settings:

```json
"openedge.abl.dbConnections": [
  { "connect": "-db mydb -H localhost -S 20001" }
]
```

### 3.3 Extension settings

| Setting                    | Default | Description                                              |
| -------------------------- | ------- | -------------------------------------------------------- |
| `dictionary.httpPort`      | `23005` | HTTP port used by the Data Administration backend server |
| `dictionary.ablSocketPort` | `23002` | Socket port for ABL communication                        |

Change these if the default ports conflict with other services on your machine.

---

## 4. Opening Data Administration

### Activity Bar icon

Click the **Data Administration icon** (book) in the left Activity Bar. The schema tree loads in the sidebar and the editor opens as a full tab.

### Explorer context menu

Right-click any file in the Explorer panel → **📖 Dictionary Editor**.

### Command palette

`Ctrl+Shift+P` → type `Dictionary` → select **📖 Dictionary Editor**.

### Sidebar tree view

The **Dictionary** tree in the Activity Bar shows databases and their schema objects. Click any item to open its detail editor.

> **First launch note:** The backend spawns an OpenEdge ABL process and connects to your databases. This can take 5–15 seconds depending on your environment.

---

## 5. User interface overview

```
┌──────────────────────────────────────────────────────────────────────┐
│  Database selector ─────────────────────────────────  [Refresh] [+]  │
├────────────────────┬─────────────────────────────────────────────────┤
│  Schema tree       │  Detail / Editor panel                          │
│                    │                                                 │
│  ▸ Tables          │  (selected object properties and edit form)     │
│    Customer        │                                                 │
│    Order           │                                                 │
│    …               │                                                 │
│  ▸ Sequences       │                                                 │
│                    │                                                 │
│  [Actions toolbar] │                                                 │
│  Dump / Load       │                                                 │
│  Reports           │                                                 │
└────────────────────┴─────────────────────────────────────────────────┘
```

- **Database selector** — switch between connected databases.
- **Refresh button** — reload the schema tree from the database.
- **Schema tree** — hierarchical view of all schema objects in the selected database.
- **Detail / Editor panel** — shows properties of the selected object and allows editing.
- **Actions toolbar** — access dump/load operations and reports.

---

## 6. Data Dictionary

### 6.1 Tables

**Browsing tables**
Select a database in the selector; all tables appear in the schema tree. Click a table name to open its detail view.

**Creating a table**
Click the **+** button or use the right-click context menu on the Tables node → _New Table_. Fill in the table name and properties and save.

**Editing a table**
Select a table in the tree and modify its properties in the detail panel. Changes take effect when you save.

**Deleting a table**
Right-click a table → _Delete Table_. A confirmation dialog is shown. **This permanently removes the table and all its fields and indexes.**

### 6.2 Fields

**Browsing fields**
Expand a table in the schema tree to see its fields. Click a field to see its properties: name, data type, format, label, description, initial value, mandatory flag.

**Creating a field**
Right-click the fields node under a table → _New Field_. Set at minimum the field name and data type.

**Editing a field**
Select a field; modify properties (label, format, initial value, mandatory, etc.) in the detail panel and save.

**Deleting a field**
Right-click a field → _Delete Field_. **This permanently removes the field from the table.**

### 6.3 Indexes

**Browsing indexes**
Expand a table → **Indexes** to see all indexes. Click an index to view its fields, uniqueness and primary flag.

**Creating an index**
Right-click the Indexes node → _New Index_. Add the component fields using the index editor.

**Editing an index**
Select an index; reorder or add/remove component fields in the detail panel and save.

**Deleting an index**
Right-click an index → _Delete Index_.

### 6.4 Sequences

**Browsing sequences**
The **Sequences** node at the top level of the schema tree lists all sequences. Click one to see its current value, increment, minimum, maximum and cycle settings.

**Creating a sequence**
Right-click the Sequences node → _New Sequence_.

**Editing a sequence**
Select a sequence; modify initial value, increment, min/max, and cycle flag.

**Deleting a sequence**
Right-click a sequence → _Delete Sequence_.

---

## 7. Dump and Load

### 7.1 Schema definitions (.df)

**Dump definitions**
_Actions → Dump Definitions (.df)_ — exports the full schema of the selected database (or selected tables) to a `.df` file. Choose the output path in the save dialog.

**Dump incremental definitions**
_Actions → Dump Incremental Definitions (.df)_ — generates a `.df` containing only the changes between two schema versions. Useful for applying schema migrations.

**Load definitions**
_Actions → Load Definitions (.df)_ — applies a `.df` schema file to the selected database. Select the file in the open dialog. **Review the file carefully before loading — structural changes cannot be automatically undone.**

### 7.2 Data (.d files)

**Dump data**
_Actions → Dump Data (.d files)_ — exports the contents of one or more tables to `.d` flat files. Select tables in the picker and choose the output directory.

**Load data**
_Actions → Load Data (.d files)_ — imports `.d` flat files into the database. Select the files; records are appended to the target tables.

### 7.3 Sequence values

**Dump sequence values**
_Actions → Dump Sequence Values_ — saves all current sequence counters to a file.

**Load sequence values**
_Actions → Load Sequence Values_ — restores sequence counters from a previously dumped file.

---

## 8. Database properties

_Actions → Database Properties_ — opens a read-only view of database-level properties: database name, schema holder, code page, collation, block size, and creation information.

_Actions → Database Identification Maintenance_ — edit the database description and other identification fields.

_Actions → Database Identification History_ — view the history of changes made to the database identification.

---

## 9. Reports

| Report                 | Description                                                    |
| ---------------------- | -------------------------------------------------------------- |
| **Quick Table Report** | Summary of all tables: name, CRC, number of fields and indexes |
| **Quick Field Report** | All fields across selected tables: name, type, format, label   |
| **Quick Index Report** | All indexes: name, table, unique flag, component fields        |
| **Sequence Report**    | All sequences with current values and settings                 |
| **View Report**        | SQL views defined in the database                              |
| **Trigger Report**     | Table and field triggers                                       |
| **User Report**        | Database user accounts and permissions                         |

Reports open in a separate panel and can be exported or printed.

---

## 10. Multi-project workspaces

When multiple folders are open in a VS Code workspace, Data Administration detects all of them. Use the **project switcher** drop-down (visible in workspace mode) to select which project's databases to administer.

Alternatively, right-click any file in the Explorer to open the editor pre-selected on that file's project.

---

## 11. Troubleshooting

### Backend fails to start

Open the **Dictionary Backend** output channel (_View → Output → Dictionary Backend_) for detailed logs.

Common causes:

- OpenEdge runtime path (`abl.configuration.runtimes`) is not configured or the path does not exist.
- The configured ports (`dictionary.httpPort` / `dictionary.ablSocketPort`) are already in use.
- The `.pl` procedure library was not built — run `npm run build-dictionary-pl` from the extension source.

### "No OpenEdge runtime configured"

Set `abl.configuration.runtimes` in your VS Code settings:

```json
"abl.configuration.runtimes": [
  { "name": "12.2", "path": "/usr/dlc" }
]
```

### Schema tree is empty

- Verify that `openedge-project.json` exists in the project root with at least one `dbConnections` entry.
- Click the **Refresh** button in the sidebar.
- Check that the database is running and the connection string is correct.

### Port conflicts

Change the ports in VS Code settings:

```json
"dictionary.httpPort": 24005,
"dictionary.ablSocketPort": 24002
```
