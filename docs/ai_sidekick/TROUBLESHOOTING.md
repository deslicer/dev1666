# AI Sidekick for Splunk - Troubleshooting Guide

This comprehensive guide helps you resolve common issues when setting up and running the AI Sidekick for Splunk. Click on any section below to expand detailed solutions.

## Quick Issue Index

- [Connection Issues](#connection-issues) - Splunk and MCP server connectivity
- [Installation Issues](#installation-issues) - Prerequisites and dependencies
- [Web Interface Issues](#web-interface-issues) - Browser and port problems
- [Platform-Specific Issues](#platform-specific-issues) - macOS, Windows, and Linux
- [Performance Issues](#performance-issues) - Slow responses and optimization
- [Configuration Issues](#configuration-issues) - Environment variables and API keys

---

## Connection Issues

<details>
<summary><strong>🔴 "Connection to Splunk failed"</strong></summary>

**Common causes and solutions:**
- **Verify Splunk is running and accessible**
  ```bash
  # Test Splunk connectivity
  curl -k https://your-splunk-host:8089/services/server/info
  ```
- **Check firewall settings** - Ensure port 8089 is open
- **Confirm credentials** - Verify username/password are correct
- **SSL issues** - Try disabling SSL verification for self-signed certificates
- **Network connectivity** - Ensure you can reach the Splunk host

**Quick fix commands:**
```bash
# Test network connectivity
ping your-splunk-host
telnet your-splunk-host 8089
```

</details>

<details>
<summary><strong>🔴 "MCP Server not responding"</strong></summary>
**The AI Sidekick requires the MCP (Model Context Protocol) server to communicate with Splunk.**

**🚀 Quick Start:**
```bash
# Navigate to MCP server directory
cd ../mcp-for-splunk

# Run the automated build and run script
./scripts/build_and_run.sh
```

**🔧 Manual Setup (if build script fails):**

**macOS/Linux/Unix:**
```bash
cd ../mcp-for-splunk
uv run fastmcp run src/server.py --transport http --port 8003
```

**Windows:**
```powershell
cd ..\mcp-for-splunk
uv run fastmcp run src/server.py --transport http --port 8003
```

**✅ Verify MCP server is running:**
- **Local setup:** You should see: `INFO: Uvicorn running on http://0.0.0.0:8003`
- **Docker setup:** Check containers: `docker-compose ps`
- **Test connection:** `curl http://localhost:8003/health`

**🔍 Test MCP server tools (Optional):**
```bash
# Run MCP Inspector for debugging
npx @modelcontextprotocol/inspector http://localhost:8003/mcp/
```

**🔧 Common fixes:**
- Verify no other services are using port 8003
- Check if MCP server directory exists
- Ensure proper permissions on MCP server files

</details>

---

## Installation Issues

<details>
<summary><strong>🔴 "Python virtual environment issues"</strong></summary>

**Common causes:**
- Python version compatibility issues
- Permission problems
- Corrupted virtual environment

**Solutions:**
```bash
# Delete and recreate virtual environment
rm -rf .venv  # macOS/Linux
Remove-Item -Recurse -Force .venv  # Windows

# Re-run prerequisites script
./scripts/lab/check-prerequisites.sh  # macOS/Linux
.\scripts\lab\check-prerequisites.ps1  # Windows
```

**For persistent issues:**
- Ensure Python 3.11+ is installed
- On Windows, try running PowerShell as Administrator
- Check available disk space

</details>

<details>
<summary><strong>🔴 UV Package Manager Issues</strong></summary>

**Installation problems:**

**macOS/Linux:**
```bash
# Try different installation methods
curl -LsSf https://astral.sh/uv/install.sh | sh
# OR
brew install uv
# OR
pip3 install uv
```

**Windows:**
```powershell
# Try different installation methods
winget install astral-sh.uv
# OR
irm https://astral.sh/uv/install.ps1 | iex
# OR
pip install uv
```

**PATH issues:**
- Restart terminal after installation
- Check if uv is in PATH: `echo $PATH` (Unix) or `$env:PATH` (Windows)
- Add UV to PATH manually if needed

</details>

<details>
<summary><strong>🔴 Git Installation Issues</strong></summary>

**macOS:**
```bash
# Install Xcode Command Line Tools
xcode-select --install

# Verify installation
xcode-select -p
git --version
```

**Windows:**
```powershell
# Install Git
winget install Git.Git

# If PATH issues persist
$env:PATH += ";C:\Program Files\Git\bin"

# Alternative: Use Git Bash
# Search "Git Bash" in Start Menu
```

</details>

---

## Web Interface Issues

<details>
<summary><strong>🔴 "Web interface won't load"</strong></summary>
**Common causes and solutions:**

**Port conflicts:**
```bash
# Check if port 8087 is in use
lsof -i :8087  # macOS/Linux
netstat -an | findstr :8087  # Windows

# Kill process using port (if needed)
kill -9 $(lsof -ti:8087)  # macOS/Linux
```

**Browser issues:**
- Try accessing `http://127.0.0.1:8087` instead of localhost
- Check browser console for JavaScript errors (F12 → Console)
- Clear browser cache and cookies
- Try a different browser (Chrome, Firefox, Safari)

**Manual startup:**
```bash
# macOS/Linux
cd ai-sidekick-for-splunk
source .venv/bin/activate
cd src
adk web --port 8087

# Windows
cd ai-sidekick-for-splunk
.venv\Scripts\Activate.ps1
cd src
adk web --port 8087
```

</details>

<details>
<summary><strong>🔴 Port Already in Use</strong></summary>

**Find and stop conflicting processes:**

**macOS/Linux:**
```bash
# Find process using port 8087
lsof -i :8087

# Kill the process
kill -9 PID_NUMBER
```

**Windows:**
```powershell
# Find process using port 8087
netstat -ano | findstr :8087

# Kill the process
taskkill /PID PID_NUMBER /F
```

**Use alternative port:**
```bash
# Start on different port
adk web --port 8088
```

</details>

---

## Performance Issues

<details>
<summary><strong>🔴 "Agent responses are slow"</strong></summary>

**Common causes and solutions:**

**Network-related:**
- Check your internet connection (required for Google Search features)
- Verify Splunk server performance and connectivity
- Consider using local Splunk instance for faster responses

**System resources:**
```bash
# Check system resources
top  # macOS/Linux
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10  # Windows

# Check available memory
free -h  # Linux
vm_stat  # macOS
Get-WmiObject -Class Win32_OperatingSystem | Select-Object TotalVisibleMemorySize, FreePhysicalMemory  # Windows
```

**Optimization tips:**
- Close unnecessary applications
- Restart the AI Sidekick service
- Use more specific search queries to reduce processing time

</details>

---

## Configuration Issues

<details>
<summary><strong>🔴 "API key errors"</strong></summary>

**Google API Key issues:**

**Verify API key:**
```bash
# Test API key (replace YOUR_API_KEY)
curl -H "Content-Type: application/json" \
  -d '{"contents":[{"parts":[{"text":"Hello"}]}]}' \
  "https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=YOUR_API_KEY"
```

**Common fixes:**
- Ensure you have a valid Google API key from [Google AI Studio](https://aistudio.google.com/)
- Check that the key has appropriate permissions for Gemini API
- Verify environment variables are set correctly in `.env` file
- Ensure no extra spaces or quotes around the API key

**Check .env file:**
```bash
# Verify .env file contents
cat .env | grep GOOGLE_API_KEY
```

</details>

<details>
<summary><strong>🔴 Environment Variable Issues</strong></summary>

**Missing or incorrect .env file:**
```bash
# Check if .env file exists
ls -la .env

# Copy from template if missing
cp .env_lab .env  # macOS/Linux
Copy-Item .env_lab .env  # Windows
```

**Verify environment variables:**
```bash
# Check all environment variables
cat .env

# Test specific variables
echo $GOOGLE_API_KEY  # macOS/Linux
echo $env:GOOGLE_API_KEY  # Windows
```

</details>

---

## Platform-Specific Issues

<details>
<summary><strong>🍎 macOS-Specific Issues</strong></summary>

**Xcode Command Line Tools:**
```bash
# Install if missing
xcode-select --install

# Verify installation
xcode-select -p
```

**Homebrew issues:**
```bash
# Fix Homebrew PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile

# Fix permissions
sudo chown -R $(whoami) /opt/homebrew/
```

**Apple Silicon (M1/M2) compatibility:**
```bash
# Install Rosetta 2 if needed
softwareupdate --install-rosetta

# Check architecture
uname -m
```

**Firewall issues:**
```bash
# Check firewall status
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate

# Temporarily disable (not recommended for production)
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate off
```

</details>

<details>
<summary><strong>🪟 Windows-Specific Issues</strong></summary>

**PowerShell Execution Policy:**
```powershell
# Fix execution policy error
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Check current policy
Get-ExecutionPolicy -List
```

**Python PATH issues:**
```powershell
# Check Python installation
python --version
py --version

# Add Python to PATH manually
$env:PATH += ";C:\Users\$env:USERNAME\AppData\Local\Programs\Python\Python312"

# Make PATH change permanent
[Environment]::SetEnvironmentVariable("PATH", $env:PATH, [EnvironmentVariableTarget]::User)
```

**Windows Defender/Antivirus:**
- Add project folder to antivirus exclusions
- Temporarily disable real-time protection for testing

</details>

---

## General Debugging

<details>
<summary><strong>🔧 System Diagnostics</strong></summary>

**Check all prerequisites:**
```bash
# macOS/Linux
python3 --version
uv --version
node --version
git --version

# Windows
python --version
uv --version
node --version
git --version
```

**Check system information:**
```bash
# macOS
sw_vers
uname -m

# Linux
lsb_release -a
uname -a

# Windows
Get-ComputerInfo | Select WindowsProductName, WindowsVersion
$PSVersionTable.PSVersion
```

**Test network connectivity:**
```bash
# macOS/Linux
nc -zv localhost 8087
nc -zv localhost 8003

# Windows
Test-NetConnection localhost -Port 8087
Test-NetConnection localhost -Port 8003
```

</details>

<details>
<summary><strong>🔄 Reset and Restart</strong></summary>

**Complete reset procedure:**

1. **Stop all services:**
   ```bash
   # macOS/Linux
   ./scripts/lab/stop-lab-setup.sh
   
   # Windows
   .\scripts\lab\stop-lab-setup.ps1
   ```

2. **Clean environment:**
   ```bash
   # Remove virtual environment
   rm -rf .venv  # macOS/Linux
   Remove-Item -Recurse -Force .venv  # Windows
   
   # Remove configuration (optional)
   rm -f .env  # macOS/Linux
   Remove-Item .env -ErrorAction SilentlyContinue  # Windows
   ```

3. **Restart setup:**
   ```bash
   # macOS/Linux
   ./scripts/lab/check-prerequisites.sh
   
   # Windows
   .\scripts\lab\check-prerequisites.ps1
   ```

</details>

---

## Getting Additional Help

### Check Logs
```bash
# View recent logs
tail -f logs/app.log  # macOS/Linux
Get-Content logs\app.log -Tail 50  # Windows
```

### Community Support
- **GitHub Issues:** [Report bugs and get help](https://github.com/deslicer/ai-sidekick-for-splunk/issues)
- **Documentation:** [Complete documentation](https://github.com/deslicer/ai-sidekick-for-splunk/blob/main/README.md)

### Contact Support
If you're still experiencing issues after trying these solutions:
- **Email:** opensource@deslicer.com
- **Include:** System information, error messages, and steps you've tried

---

***Return to: [macOS Guide](MACOS_GUIDE.md) | [Windows Guide](WINDOWS_GUIDE.md)***
