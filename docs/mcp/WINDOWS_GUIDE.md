# Windows Setup Guide for MCP Server for Splunk

This lab guide shows how to set up and run the MCP Server for Splunk on Windows.

## 🚀 Quick Start (Recommended)

### 1) Clone the repository

```powershell
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```
### 2) Copy the lab environment
```powershell
cp env.lab .env
```

### 3) Install prerequisites (uv, Node.js, Python via uv)
```powershell
pwsh -File ..\..\scripts\smart-install.ps1
```

### 4) Run the server locally

```powershell
uv run mcp-server --local -d
# Updated SPLUNK_PASSWORD will be provided by instructors
```

### 5) Verify the mcp server and Splunk connection

```powershell
uv run mcp-server --test -detailed
```

<details>
<summary>View sample successful output</summary>

```bash
== MCP Server Check ==
URL: http://0.0.0.0:8003/mcp/
• MCP Server: OK ✅
• Tools: 39 | Resources: 17

-- Splunk Health --
• Status: Connected ✅
• Server: sh-i-0b8d6e25a.deslicer.splunkcloud.com
• Version: 9.3.2411.113
• Source: server_config
```
</details>

**Lab complete:** If the script returns MCP Server: OK ✅ and Splunk Health  Status: Connected ✅ you have successfully completed the set up lab.

If Splunk shows "Not connected ❌":

- Verify your `.env` file contains correct values for `SPLUNK_HOST`, `SPLUNK_PORT`, `SPLUNK_USERNAME`, `SPLUNK_PASSWORD`, `SPLUNK_SCHEME`, `SPLUNK_VERIFY_SSL`.
  ```powershell
  uv run mcp-server --setup --local -d
  ```
  
What this does:
- Installs uv (official Windows installer)
- Installs Node.js (for MCP Inspector) via WinGet (Chocolatey fallback)
- Uses uv to install a compatible Python from `.python-version` or `requires-python`
- Verifies with `uv python find`

## 📋 Prerequisites

### Required Software
- PowerShell 5.1+ or Core 7+ (built-in or via the Microsoft Store)
- Git (for cloning the repository)

### Optional Software
- Docker Desktop: full-stack deployment with containers
- Windows Terminal: improved terminal experience

## 🧰 Managed Python with uv

You don’t need a system Python. The installer uses uv to install and manage a compatible Python automatically based on `.python-version` or `pyproject.toml`’s `requires-python`.

Install uv (Windows):
```powershell
# Official installer (Recommended)
powershell -ExecutionPolicy Bypass -c "irm https://astral.sh/uv/install.ps1 | iex"

# Verify
uv --version
```

Alternate uv installations:
```powershell
# WinGet
winget install astral-sh.uv

# PyPI (pipx preferred)
pipx install uv
```

## 🛠️ Manual Setup (Alternative)

```powershell
# From repo root
git clone https://github.com/deslicer/dev1666.git
cd dev1666

# Install uv (Windows official installer)
powershell -ExecutionPolicy Bypass -c "irm https://astral.sh/uv/install.ps1 | iex"

# Ensure a Python is available via uv
uv python list || uv python install 3.11

# Prepare environment
Copy-Item env.example .env
# Edit .env with your Splunk details

# Run with FastMCP CLI
uv run fastmcp run src/server.py
```

## ✅ Verify

```powershell
uv --version
uv python find
node --version
git --version
```

## ⚠️ Troubleshooting

### Execution policy
```powershell
# Error: "execution of scripts is disabled on this system"
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### uv installation issues
```powershell
# Official installer
powershell -ExecutionPolicy Bypass -c "irm https://astral.sh/uv/install.ps1 | iex"

# Alternatives
winget install astral-sh.uv
pipx install uv
```

### uv cannot find Python
```powershell
uv python install 3.11
uv python find
```

### Node.js/NPM issues
```powershell
node --version
npm --version
winget install OpenJS.NodeJS
```

---

References:
- Installing uv on Windows: https://docs.astral.sh/uv/getting-started/installation/#__tabbed_1_2
- uv Python versions (requests, `.python-version`, `requires-python`): https://docs.astral.sh/uv/concepts/python-versions/
