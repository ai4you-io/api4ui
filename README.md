# API4UI
API4UI | Uses GitHub issues as an official bug tracker

Visual UI Builder - Create stunning user interfaces with drag-and-drop simplicity.

This repository is intended to support users by providing extra information and guidance about the VS Code extension [API4UI - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ai4you.api4ui).

## In This Article
* [Installation](#installation)
* [Documentation](#where-can-i-find-the-documentation)
* [When do you plan on releasing features?](#when-do-you-plan-on-releasing-features)
* [I want to report a bug](#i-want-to-report-a-bug)
* [I need a tailor-made solution](#i-need-a-tailor-made-solution)
* [Getting Started](#getting-started)
* [Key Features](#key-features)
* [Framework Support](#framework-support)

## Installation

### From VS Code Marketplace
1. Open VS Code
2. Go to Extensions (`Ctrl+Shift+X`)
3. Search for "API4UI"
4. Install the extension by AI4YOU

### From Command Line
```bash
code --install-extension ai4you.api4ui
```

## Where can I find the documentation?

Access comprehensive documentation through the built-in VS Code extension:
- **Command Palette**: `Ctrl+Shift+P` → "📚 Documentation"
- **Status Bar**: Click the gear icon → Documentation
- **Context Menu**: Right-click in any .cls file → Documentation

Extended online documentation will be available in the future.

## When do you plan on releasing features?

You can create an issue where you explain your idea or feature:
1. Create the issue [Open a new issue](https://github.com/ai4you-io/api4ui/issues/new)
2. Explain your feature as CLEAR as possible
3. Include use cases and examples if applicable

We prioritize features based on community feedback and enterprise requirements.

## I want to report a bug

1. Check if the issue does not already exist in [existing issues](https://github.com/ai4you-io/api4ui/issues)
2. Create the issue [Open a new issue](https://github.com/ai4you-io/api4ui/issues/new)
3. Add a reproducible case with:
   - Steps to reproduce
   - Expected behavior
   - Actual behavior
   - VS Code version and extension version
   - Sample .cls files (if applicable)

If you need assistance with troubleshooting or isolating a problem, you can request remote assistance through our [Support](mailto:info@api4ui.io) system. Remote assistance is included in enterprise support subscriptions.

## I need a tailor-made solution

Our team specialized in making VS Code extensions and native applications is here to provide you the most versatile and tailored solution for your company.

**Enterprise Services:**
- Custom API4UI components
- Framework integrations
- Training and consultation
- Priority support

Contact us at [info@api4ui.io](mailto:info@api4ui.io) for enterprise solutions.

## Getting Started

### Quick Start
1. **Install the extension** from the VS Code Marketplace
2. **Open an OpenEdge ABL project** in VS Code
3. **Create a new form**: Right-click in Explorer → API4UI toolbox → ABL → New → Form
4. **Open the visual designer**: Right-click any .cls file → "🎨 Open in API4UI designer"
5. **Start designing**: Drag and drop components from the toolbox

### Keyboard Shortcuts
- `Ctrl+Shift+F8` - Open .cls file in visual designer
- `Ctrl+Shift+F9` - Switch back to text editor from designer

### Project Setup
Initialize your project for optimal experience:
1. Use Command Palette: `Ctrl+Shift+P` → "Initialize Project Configuration"
2. Configure build paths and database connections
3. Analyze UI components: "UI Components from openedge-project.json"

## Key Features

### 🎨 Visual Designer
- **Drag-and-drop interface** for rapid UI development
- **Real-time preview** of your OpenEdge ABL forms
- **Component property editing** with live updates
- **Grid snapping** and alignment tools
- **Responsive design** support

### 🧩 Component Library (in development)
- **Rich component set** including RadButton, RadTextBox, RadForm, and more
- **Telerik, Infragistics, DevExpress** component support
- **Automatic DLL analysis** for component discovery
- **Custom component** integration
- **Theme support** with vendor-specific styling

### 🔨 Code Generation
- **Clean ABL code output** following best practices
- **Framework-specific templates** 
- **Namespace management** with build path integration
- **Method generation** (constructors, destructors, event handlers)
- **Compilation tools** with XREF, DEBUG-LIST, and LISTING support

### 🚀 Project Management
- **OpenEdge project configuration** with build paths
- **Database connection** management
- **Multi-framework support** for different development approaches
- **Build system integration** with OpenEdge compilation
- **File templates** for classes, forms, procedures, and interfaces

### 🔌 Advanced Integrations
- **MCP (Model Context Protocol) server** for external tool integration
- **DLL analysis service** for automatic component discovery
- **OpenAPI integration** for service generation
- **Database tooling** with OpenEdge database MCP server
- **Settings management** with workspace and user scopes

## Framework Support

### Standard OpenEdge ABL
Default templates without framework dependencies for pure OpenEdge development.

### Custom Frameworks
Extensible framework system allows integration of your own templates and patterns.

## System Requirements

- **VS Code**: Version 1.96.0 or higher
- **OpenEdge**: Version 11.7 or higher (12.8 recommended)
- **Operating System**: Windows, macOS, or Linux
- **Memory**: 4GB RAM minimum (8GB recommended for large projects)

## Compilation Features

The extension includes advanced compilation tools:

- **Selective compilation**: Choose XREF, DEBUG-LIST, LISTING, PREPROCESS, or STRING-XREF
- **Dynamic compilation**: Progress COMPILE statements with proper error handling
- **Output management**: Generated files (.xref, .list, .i) appear alongside source files
- **Batch operations**: Compile multiple files with consistent options

## Sample Projects

Sample projects and templates will be added to demonstrate best practices and common patterns.

## Community

- **GitHub Issues**: [Report bugs and request features](https://github.com/ai4you-io/api4ui/issues)
- **Documentation**: Built-in extension documentation
- **Enterprise Support**: [info@api4ui.io](mailto:info@api4ui.io)

---

**AI4YOU** - Empowering developers with intelligent tools for modern application development.
