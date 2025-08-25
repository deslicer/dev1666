# Windows Setup Guide for MCP Server for Splunk

This guide covers installing prerequisites and validating your setup on Windows.

## 1) Clone the repository

```powershell
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```

All setup scripts are in this repository under `scripts/`.

## 2) Install prerequisites

### Required Software

| Software | Version | Installation Method | Notes |
|----------|---------|-------------------|-------|
| **PowerShell** | 5.1+ or Core 7+ | Built-in or [Microsoft Store](https://aka.ms/powershell) | Required for main script |
| **Python** | 3.10+ | [Microsoft Store](https://apps.microsoft.com/store/detail/python-310/9PJPW5LDXLZ5) or [python.org](https://python.org) | Use Microsoft Store version for best PATH handling |
| **Git** | Latest | [git-scm.com](https://git-scm.com/download/win) | For cloning the repository |

### Optional Software

| Software | Purpose | Installation |
|----------|---------|--------------|
| **Docker Desktop** | Full-stack deployment | [docker.com](https://docker.com/products/docker-desktop) |
| **Node.js** | MCP Inspector testing | [nodejs.org](https://nodejs.org/) |
| **Windows Terminal** | Better terminal experience | [Microsoft Store](https://aka.ms/terminal) |

### Python Installation (Windows)

```powershell
# Option 1: Microsoft Store (Recommended)
# Search "Python" in Microsoft Store and install Python 3.11+

# Option 2: Official installer
# Download from https://python.org/downloads/
# ✅ Check "Add Python to PATH" during installation

# Option 3: Winget
winget install Python.Python.3.12

# Option 4: Chocolatey
choco install python

# Verify installation
python --version
pip --version
```

### UV Package Manager Installation (Windows)

```powershell
# Option 1: Official installer (Recommended)
irm https://astral.sh/uv/install.ps1 | iex

# Option 2: Winget
winget install astral-sh.uv

# Option 3: Pip fallback
pip install uv

# Verify installation
uv --version
```

### Install All Prerequisites (one-liner)

```powershell
# Installs Python, uv, Node.js, Docker Desktop, and Git
winget install Python.Python.3.12 astral-sh.uv OpenJS.NodeJS Docker.DockerDesktop Git.Git

# Verify installations
python --version; uv --version; node --version; docker --version; git --version
```

### Verify installations

```powershell
python --version
uv --version
git --version
node --version   # if installed
docker --version # if installed
```

### Prerequisites Verification

Use the built-in verification script to validate your environment:

```powershell
# Basic check (recommended first)
.\scripts\check-prerequisites.ps1

# Detailed output with installation paths and suggestions
.\scripts\check-prerequisites.ps1 -Detailed

# Help and usage
.\scripts\check-prerequisites.ps1 -Help
```

## 3) Validate prerequisites

From the `mcp-for-splunk` folder:

```powershell
.\scripts\check-prerequisites.ps1 -Detailed
```

## All checks pass ✅

- ***Return to: [Main Guide](../../set-up-your-mcp-server-for-splunk.md#2-prepare-your-environment)***


## Troubleshooting ⚠️

### Common Issues

#### PowerShell Execution Policy
```powershell
# Error: "execution of scripts is disabled on this system"
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

#### Python Not Found
```powershell
# Check Python installation
python --version
py --version

# Add Python to PATH (if needed)
$env:PATH += ";C:\Users\$env:USERNAME\AppData\Local\Programs\Python\Python310"
```

#### uv Installation Issues
```powershell
# Try different installation methods
winget install astral-sh.uv
# OR
pip install uv
# OR download from https://astral.sh/uv/
```

#### Docker Desktop Issues
- Ensure WSL2 is enabled: `wsl --install`
- Restart Docker Desktop after installation
- Check Docker settings: Enable "Expose daemon on tcp://localhost:2375"


#### Node.js/NPM Issues
```powershell
# Check Node.js installation
node --version
npm --version

# Install if missing
winget install OpenJS.NodeJS
```

### Debugging Commands

```powershell
# Check all prerequisites
python --version
uv --version
docker --version
node --version
git --version

# Check PowerShell version
$PSVersionTable.PSVersion

# Test Docker connectivity
docker run hello-world

# View detailed script help
.\scripts\build_and_run.ps1 -Help

# Check Windows version
Get-ComputerInfo | Select WindowsProductName, WindowsVersion
```
