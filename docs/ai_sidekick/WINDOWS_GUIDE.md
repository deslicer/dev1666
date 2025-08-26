# Windows Setup Guide for AI Sidekick for Splunk

This guide covers setting up the AI Sidekick for Splunk on Windows systems.

## Prerequisites

- Windows 10/11 (PowerShell 5.1+ or PowerShell Core 7+)
- Administrator privileges for installing software
- Internet connection for downloading dependencies
- Access to a Splunk instance (local or remote)

## 1) Clone the Repository

```powershell
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
```

## 2) Install Prerequisites

### Required Software

| Software | Version | Installation Method | Notes |
|----------|---------|-------------------|-------|
| **PowerShell** | 5.1+ or Core 7+ | Built-in or [Microsoft Store](https://aka.ms/powershell) | Required for scripts |
| **Python** | 3.11+ | [Microsoft Store](https://apps.microsoft.com/store/detail/python-311/9NRWMJP3717K) or [python.org](https://python.org) | Use Microsoft Store version for best PATH handling |
| **Git** | Latest | [git-scm.com](https://git-scm.com/download/win) | For cloning repositories |

### Optional Software

| Software | Purpose | Installation |
|----------|---------|--------------|
| **Node.js** | MCP Inspector testing | [nodejs.org](https://nodejs.org/) |
| **Windows Terminal** | Better terminal experience | [Microsoft Store](https://aka.ms/terminal) |

### Quick Installation (Recommended)

```powershell
# Install all prerequisites using winget
winget install Python.Python.3.12 astral-sh.uv OpenJS.NodeJS Git.Git

# Verify installations
python --version; uv --version; node --version; git --version
```

### Manual Installation Steps

#### Python Installation
```powershell
# Option 1: Microsoft Store (Recommended)
# Search "Python" in Microsoft Store and install Python 3.11+

# Option 2: Official installer
# Download from https://python.org/downloads/
# ✅ Check "Add Python to PATH" during installation

# Option 3: Winget
winget install Python.Python.3.12

# Verify installation
python --version
pip --version
```

#### UV Package Manager Installation
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

## 3) Configure Environment Variables

### Quick Setup (Recommended)

Use the interactive setup script:

```powershell
.\scripts\lab\setup-env.ps1
```

This script will:
- ✅ Set up pre-configured Google API key for workshop or optionally provide your own key
- ✅ Configure MCP server URL
- ✅ Set optimal model defaults
- ✅ Create your `.env` file automatically

### Manual Setup (Alternative)

1. **Copy the workshop template:**
   ```powershell
   Copy-Item .env_lab .env
   ```

2. **Edit the `.env` file:**
   ```powershell
   # Edit with your preferred editor
   notepad .env  # or code .env
   ```

3. **Required settings for the workshop:**
   ```env
   # Google ADK Configuration (Required)
   GOOGLE_GENAI_USE_VERTEXAI=False
   GOOGLE_API_KEY=your-google-ai-studio-api-key

   # MCP Server Configuration (Required)
   SPLUNK_MCP_SERVER_URL=http://localhost:8003/mcp/

   # Splunk Connection (Required for MCP server)
   SPLUNK_HOST=dev1666-i-035e95d7e4ea1c310.splunk.show
   SPLUNK_PORT=8089
   SPLUNK_SCHEME=https
   SPLUNK_USERNAME=admin
   SPLUNK_PASSWORD=workshop-password-provided-during-session

   # Model Configuration
   BASE_MODEL=gemini-2.0-flash-exp

   # Server Configuration
   HOST=0.0.0.0
   PORT=8087
   ```

## 4) Install Dependencies

Run the prerequisites script to check and install required packages:

```powershell
.\scripts\lab\check-prerequisites.ps1
```

This script will:
- ✅ Check for Python 3.11+
- ✅ Install `uv` (fast Python package manager)
- ✅ Create virtual environment with `uv`
- ✅ Install Google ADK and required dependencies
- ✅ Test Google API key connection
- ✅ Test MCP server connectivity

## 5) Start the AI Sidekick

```powershell
.\scripts\lab\start-lab-setup.ps1
```

You should see output like:
```
🚀 AI Sidekick Setup Complete!

✅ Virtual environment activated
✅ Google ADK initialized
✅ MCP server connection verified
✅ AI agent ready

🌐 Web interface available at: http://localhost:8087

Opening web interface in your browser...
```

## 6) Access Your AI Sidekick

1. **Open your web browser** and navigate to: `http://localhost:8087`
2. **In the web interface**, locate the **Agent Selection** dropdown in the top left
3. **Select "AI Sidekick for Splunk"** from the dropdown
4. **Start chatting** with your AI Sidekick!

## Troubleshooting

### Common Windows Issues

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
$env:PATH += ";C:\Users\$env:USERNAME\AppData\Local\Programs\Python\Python312"
```

#### UV Installation Issues
```powershell
# Try different installation methods
winget install astral-sh.uv
# OR
pip install uv
# OR download from https://astral.sh/uv/
```

#### Web Interface Won't Load
```powershell
# Check if port 8087 is in use
netstat -an | findstr :8087

# Try accessing alternative URL
# http://127.0.0.1:8087

# Run ADK web interface manually
cd ai-sidekick-for-splunk
.venv\Scripts\Activate.ps1
cd src
adk web --port 8087
```

#### Virtual Environment Issues
```powershell
# Delete virtual environment and recreate
Remove-Item -Recurse -Force .venv -ErrorAction SilentlyContinue
.\scripts\lab\check-prerequisites.ps1
```

### MCP Server Connection Issues

If you see "MCP Server not responding":

1. **Start the MCP server first:**
   ```powershell
   # Navigate to MCP server directory
   cd ..\mcp-for-splunk

   # Run the automated build and run script
   .\scripts\build_and_run.ps1
   ```

2. **Manual MCP server setup (if build script fails):**
   ```powershell
   cd ..\mcp-for-splunk
   uv run fastmcp run src/server.py --transport http --port 8003
   ```

3. **Verify MCP server is running:**
   ```powershell
   # Test connection
   curl http://localhost:8003/health
   ```

### Getting Help

1. **Check the logs:**
   ```powershell
   # View recent logs
   Get-Content logs\ai-sidekick.log -Tail 50
   ```

2. **Restart services:**
   ```powershell
   # Stop services
   .\scripts\lab\stop-lab-setup.ps1
   # Restart everything
   .\scripts\lab\start-lab-setup.ps1
   ```

3. **Reset configuration:**
   ```powershell
   # Remove existing configuration and restart
   Remove-Item .env -ErrorAction SilentlyContinue
   .\scripts\lab\start-lab-setup.ps1
   ```

### Debugging Commands

```powershell
# Check all prerequisites
python --version
uv --version
node --version
git --version

# Check PowerShell version
$PSVersionTable.PSVersion

# Check Windows version
Get-ComputerInfo | Select WindowsProductName, WindowsVersion

# Test network connectivity
Test-NetConnection localhost -Port 8087
Test-NetConnection localhost -Port 8003
```

## Next Steps

🎉 **Congratulations!** You've successfully set up your AI Sidekick for Splunk on Windows!

### Continue Your Journey:
- **🔗 Return to Main Guide:** [Continue with Step 3: Configure Environment Variables](../../3-setup-your-personal-ai-sidekick.md#step-3-configure-environment-variables)
- **🔗 Proceed to Lab 4:** [Create Your AI Agent](../../4-create-your-ai-agent.md)
- **🌟 Explore:** Try the example conversations in the main guide
- **🚀 Customize:** Modify agent configurations for your use case

---

***Return to: [Main AI Sidekick Guide](../../3-setup-your-personal-ai-sidekick.md)***