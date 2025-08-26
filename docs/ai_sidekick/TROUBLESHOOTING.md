# AI Sidekick for Splunk - Troubleshooting Guide

This guide helps you resolve common issues when setting up and running the AI Sidekick for Splunk.

## Common Issues and Solutions

### 🔴 "Connection to Splunk failed"
- Verify Splunk is running and accessible
- Check firewall settings allow port 8089
- Confirm username/password are correct
- Try disabling SSL verification for self-signed certificates

### 🔴 "MCP Server not responding"
The setup script will automatically check if the MCP server is running and provide clear instructions if it's not. If you see this error:

1. **🚨 IMPORTANT: Start the MCP server first!**

   The AI Sidekick requires the MCP (Model Context Protocol) server to communicate with Splunk.

   **📋 Easy Setup - Use the build script:**
   ```bash
   # Navigate to MCP server directory
   cd ../mcp-for-splunk

   # Run the automated build and run script
   ./scripts/build_and_run.sh
   ```

   **📖 For detailed MCP server setup, refer to the lab guide in the MCP project.**

   **🔧 Manual Setup (if build script fails):**

   #### For macOS/Linux/Unix:
   ```bash
   cd ../mcp-for-splunk
   uv run fastmcp run src/server.py --transport http --port 8003
   ```

   #### For Windows:
   ```powershell
   cd ..\mcp-for-splunk
   uv run fastmcp run src/server.py --transport http --port 8003
   ```

   **🐳 Docker Alternative (Recommended if remote Splunk fails):**

   If you're having issues with remote Splunk connections, refer to the **MCP server lab guide** for detailed Docker setup instructions with local Splunk instance.

2. **✅ Verify MCP server is running:**
   - **Local setup:** You should see: `INFO: Uvicorn running on http://0.0.0.0:8003`
   - **Docker setup:** Check containers: `docker-compose ps`
   - Test connection: `curl http://localhost:8003/health`

3. **🔍 Test MCP server tools (Optional but recommended):**

   Use MCP Inspector to verify your MCP server tools are working:

   ```bash
   # In a new terminal, navigate to MCP server directory
   cd ../mcp-for-splunk

   # Run MCP Inspector
   npx @modelcontextprotocol/inspector http://localhost:8003/mcp/
   ```

   This opens a web interface where you can:
   - ✅ See all available MCP tools
   - ✅ Test tool execution with sample queries
   - ✅ Verify Splunk connectivity
   - ✅ Debug any connection issues

4. **Then re-run the AI Sidekick setup script**
5. **Verify no other services are using port 8003**

### 🔴 "Web interface won't load"
- Confirm port 8087 is not blocked or in use
- Try accessing `http://127.0.0.1:8087` instead
- Check browser console for JavaScript errors
- Run ADK web interface manually:

  #### For macOS/Linux/Unix:
  ```bash
  cd ai-sidekick-for-splunk
  source .venv/bin/activate
  cd src
  adk web --port 8087
  ```

  #### For Windows:
  ```powershell
  cd ai-sidekick-for-splunk
  .venv\Scripts\Activate.ps1
  cd src
  adk web --port 8087
  ```

### 🔴 "Python virtual environment issues"
- Ensure Python 3.11+ is installed
- Delete `.venv` folder and re-run setup script
- On Windows, try running PowerShell as Administrator

### 🔴 "Agent responses are slow"
- Check your internet connection (for Google Search features)
- Verify Splunk server performance
- Consider using local Splunk instance for faster responses

### 🔴 "API key errors"
- Ensure you have a valid Google API key configured
- Check that the key has appropriate permissions
- Verify environment variables are set correctly

## Getting Help

### 1. Check the logs:
```bash
# View recent logs
tail -f logs/ai-sidekick.log
```

### 2. Restart services:

#### For macOS/Linux/Unix:
```bash
# Stop services
./scripts/lab/stop-lab-setup.sh
# Restart everything
./scripts/lab/start-lab-setup.sh
```

#### For Windows:
```powershell
# Stop services
.\scripts\lab\stop-lab-setup.ps1
# Restart everything
.\scripts\lab\start-lab-setup.ps1
```

### 3. Reset configuration:

#### For macOS/Linux/Unix:
```bash
# Remove existing configuration and restart
rm -f .env
./scripts/lab/start-lab-setup.sh
```

#### For Windows:
```powershell
# Remove existing configuration and restart
Remove-Item .env -ErrorAction SilentlyContinue
.\scripts\lab\start-lab-setup.ps1
```

## Platform-Specific Troubleshooting

For platform-specific issues, refer to the detailed troubleshooting sections in each platform guide:

- **Windows:** [Windows Troubleshooting](WINDOWS_GUIDE.md#troubleshooting)
- **macOS:** [macOS Troubleshooting](MACOS_GUIDE.md#troubleshooting)
- **Linux:** [Linux Troubleshooting](LINUX_GUIDE.md#troubleshooting)

## Need More Help?

If you're still experiencing issues:

1. **Check the platform-specific guides** for detailed troubleshooting steps
2. **Review the MCP server setup** to ensure it's running correctly
3. **Contact support:** opensource@deslicer.com

---

***Return to: [Main AI Sidekick Guide](../../3-setup-your-personal-ai-sidekick.md)***
