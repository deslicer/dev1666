# Lab 2a: Setup Your Personal AI Sidekick

Welcome to the AI Sidekick for Splunk hands-on lab! In this lab, you'll set up and run your own personal AI Sidekick for Splunk - a powerful, modular agent framework that integrates seamlessly with your Splunk environment.

## What You'll Build

By the end of this lab, you'll have:
- ✅ A fully functional AI Sidekick running on your machine
- ✅ Real-time connection to your Splunk environment via MCP
- ✅ Access to specialized AI agents for search, research, and administration
- ✅ A web interface to interact with your AI Sidekick
- ✅ Understanding of the modular agent architecture

## Prerequisites

- Basic familiarity with command line/terminal
- Access to a Splunk instance (local or remote)
- Internet connection for downloading dependencies
- Administrator privileges on your machine (for installing Python packages)

---

## Step 1: Clone the Repository

First, let's get the AI Sidekick project:

```bash
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
```

---

## Step 2: Configure Environment Variables

**🚀 Quick Setup (Recommended):**

Use the interactive setup script for easy configuration:

```bash
./scripts/lab/setup-env.sh
```

This script will:
- ✅ Prompt for your Google API key
- ✅ Configure MCP server URL (local or Docker)
- ✅ Set optimal model defaults
- ✅ Create your `.env` file automatically

**📋 Manual Setup (Alternative):**

If you prefer manual configuration:

1. **Copy the workshop template:**
   ```bash
   cp .env_lab .env
   ```

2. **Edit the `.env` file with your values:**
   ```bash
   # Edit with your preferred editor
   nano .env  # or code .env
   ```

3. **Required settings for the workshop:**
   ```env
   # Google ADK Configuration (Required)
   GOOGLE_GENAI_USE_VERTEXAI=False
   GOOGLE_API_KEY=your-google-ai-studio-api-key

   # MCP Server Configuration (Required)
   SPLUNK_MCP_SERVER_URL=http://localhost:8001/mcp/

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

   **Get your Google API key:**
   1. Go to [Google AI Studio](https://aistudio.google.com/)
   2. Click "Get API Key" → "Create API Key"
   3. Copy the key and replace `your-google-ai-studio-api-key`

   **MCP Server Information:**
   - The workshop assumes you have the `mcp-server-for-splunk` running on port 8001
   - Or use a provided workshop MCP server URL

4. **Save the file**

---

## Step 3: Install Prerequisites and Dependencies

Run the prerequisites script to check and install required packages:

#### For macOS/Linux/Unix:
```bash
chmod +x scripts/lab/check-prerequisites.sh
./scripts/lab/check-prerequisites.sh
```

#### For Windows:
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

---

## Step 4: Configure Lab Mode (Optional)

For workshops, you may want to use the simplified lab mode that focuses on IndexAnalyzer:

#### For macOS/Linux/Unix:
```bash
# Switch to lab mode (removes DataExplorer to avoid confusion)
./scripts/lab/switch-orchestrator-mode.sh lab

# Check current mode
./scripts/lab/switch-orchestrator-mode.sh status
```

#### For Windows:
```powershell
# Switch to lab mode (removes DataExplorer to avoid confusion)
.\scripts\lab\switch-orchestrator-mode.ps1 lab

# Check current mode
.\scripts\lab\switch-orchestrator-mode.ps1 status
```

**Lab Mode Benefits:**
- ✅ **Simplified agent selection** - Only IndexAnalyzer for systematic analysis
- ✅ **Eliminates confusion** - No overlap between DataExplorer and IndexAnalyzer
- ✅ **Workshop-focused** - Perfect for learning IndexAnalyzer workflow

## Step 5: Start the AI Sidekick

#### For macOS/Linux/Unix:
```bash
chmod +x scripts/lab/start-lab-setup.sh
./scripts/lab/start-lab-setup.sh
```

#### For Windows:
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

---

## Step 5: Meet Your AI Sidekick

### Understanding the Agent Architecture

Your AI Sidekick uses a **modular multi-agent architecture** with these specialized agents:

1. **🎯 Root Agent** - Main coordinator and conversation handler
2. **🔍 Search Guru** - SPL expert for search optimization and strategy
3. **🔬 Data Explorer** - Comprehensive data analysis with 5-phase workflow
4. **🧠 Researcher** - Google Search integration for current information
5. **🔧 Splunk MCP** - Direct Splunk environment access and execution

### Agent Selection

1. **In the web interface**, locate the **Agent Selection** dropdown in the top left
2. **Select "AI Sidekick for Splunk"** from the dropdown
3. The framework will automatically route your requests to the appropriate specialized agents

---

## Step 5: Example Conversations

Let's explore what your AI Sidekick can do! Try these example conversations:

### Example 1: Basic Splunk Health Check

**You:** "Check my Splunk health and show me available indexes"

**Expected Response:** The AI Sidekick will:
- Automatically delegate to the Splunk MCP agent
- Check Splunk connectivity
- List available indexes with data volume information
- Provide health recommendations

### Example 2: Search Query Optimization

**You:** "Help me optimize this SPL query: `index=pas | stats count by user | sort -count`"

**Expected Response:** The Search Guru will:
- Analyze your query for performance improvements
- Suggest optimizations (time range, field filtering, etc.)
- Provide best practices explanation
- Offer alternative approaches

### Example 3: Data Explorer Workflow

**You:** "Use data explorer to analyze index=pas"

**Expected Response:** The Data Explorer will execute a comprehensive 5-phase workflow:
1. **Phase 1: Data Collection** - Gather basic index information and samples
2. **Phase 2: Field Analysis** - Analyze field patterns and distributions
3. **Phase 3: Pattern Recognition** - Identify trends and anomalies
4. **Phase 4: Insight Generation** - Generate 5 actionable business insights
5. **Phase 5: Quality Assessment** - Validate findings and provide recommendations

### Example 4: Current Information Research

**You:** "What are the latest Splunk security advisories for version 9.4?"

**Expected Response:** The Researcher will:
- Use Google Search to find current security information
- Provide links to official Splunk security advisories
- Summarize key findings and recommendations
- Suggest next steps for security updates

### Example 5: Multi-Agent Collaboration

**You:** "Help me analyze file operations patterns in index=pas and create optimized searches"

**Expected Response:** Multiple agents will collaborate:
- **Data Explorer** performs comprehensive 5-phase analysis of file operations data
- **Search Guru** optimizes the SPL queries generated by Data Explorer
- **Splunk MCP** executes all searches and returns formatted results
- **Root Agent** coordinates the workflow and presents unified results

### 🎯 More Example Questions to Try

**Data Explorer (Comprehensive Analysis):**
```
"Use data explorer to analyze index=_internal"
"Analyze index=pas with data explorer"
"Data explorer analyze index=_audit"
```

**Search Guru (SPL Optimization & Strategy):**
```
"Help me create a search to find errors in index=_internal"
"Optimize this query: index=pas | stats count by user"
"What's the best SPL approach for analyzing failed logins?"
"Create an efficient search for monitoring system performance"
```

**Splunk MCP (Direct Operations):**
```
"Check my Splunk health and list indexes"
"Run this search: index=_internal | head 10 | table _time, component"
"Show me events from index=pas | head 20"
"List all available indexes"
```

**Researcher (Current Information):**
```
"What are the latest Splunk best practices for search optimization?"
"Research current security threats for Windows authentication"
"Find the latest Splunk security advisories"
"What's new in Splunk Enterprise 9.4?"
```

**Multi-Agent Workflows:**
```
"Analyze index=pas and optimize the searches"
"Help me investigate security patterns in my data"
"Create a complete monitoring strategy for index=_internal"
```

---

### Session Management

Your conversations are automatically saved. To start fresh:
- Click **🗑️ Clear Session** in the interface
- Or start a new session by refreshing the page

---

## Step 7: Understanding the Architecture

### Modular Design Benefits

1. **Specialized Expertise** - Each agent excels in its domain
2. **Automatic Delegation** - Framework routes tasks to appropriate agents
3. **Extensible** - Easy to add new agents and capabilities
4. **Session Persistence** - Maintains context across interactions
5. **Real-Time Integration** - Direct Splunk environment access

### MCP (Model Context Protocol) Integration

- **Real-Time Connection** - Live access to your Splunk environment
- **Session Management** - Persistent connections with automatic reconnection
- **Tool Integration** - Rich set of Splunk administration tools
- **Security** - Secure credential handling and SSL support

### Google ADK Framework

- **Multi-Agent Coordination** - Native support for agent collaboration
- **Google Search Integration** - Access to current information
- **Conversation Management** - Advanced dialog state handling
- **Tool Orchestration** - Seamless tool-to-agent integration

---

## Troubleshooting

### Common Issues and Solutions

**🔴 "Connection to Splunk failed"**
- Verify Splunk is running and accessible
- Check firewall settings allow port 8089
- Confirm username/password are correct
- Try disabling SSL verification for self-signed certificates

**🔴 "MCP Server not responding"**
The setup script will automatically check if the MCP server is running and provide clear instructions if it's not. If you see this error:

1. **🚨 IMPORTANT: Start the MCP server first!**

   The AI Sidekick requires the MCP (Model Context Protocol) server to communicate with Splunk.

   **📋 Easy Setup - Use the build script:**
   ```bash
   # Navigate to MCP server directory
   cd ../mcp-server-for-splunk

   # Run the automated build and run script
   ./scripts/build_and_run.sh
   ```

   **📖 For detailed MCP server setup, refer to the lab guide in the MCP project.**

   **🔧 Manual Setup (if build script fails):**

   #### For macOS/Linux/Unix:
   ```bash
   cd ../mcp-server-for-splunk
   uv run fastmcp run src/server.py --transport http --port 8001
   ```

   #### For Windows:
   ```powershell
   cd ..\mcp-server-for-splunk
   uv run fastmcp run src/server.py --transport http --port 8001
   ```

   **🐳 Docker Alternative (Recommended if remote Splunk fails):**

   If you're having issues with remote Splunk connections, refer to the **MCP server lab guide** for detailed Docker setup instructions with local Splunk instance.

2. **✅ Verify MCP server is running:**
   - **Local setup:** You should see: `INFO: Uvicorn running on http://0.0.0.0:8001`
   - **Docker setup:** Check containers: `docker-compose ps`
   - Test connection: `curl http://localhost:8001/health`

3. **🔍 Test MCP server tools (Optional but recommended):**

   Use MCP Inspector to verify your MCP server tools are working:

   ```bash
   # In a new terminal, navigate to MCP server directory
   cd ../mcp-server-for-splunk

   # Run MCP Inspector
   npx @modelcontextprotocol/inspector http://localhost:8001/mcp/
   ```

   This opens a web interface where you can:
   - ✅ See all available MCP tools
   - ✅ Test tool execution with sample queries
   - ✅ Verify Splunk connectivity
   - ✅ Debug any connection issues

4. **Then re-run the AI Sidekick setup script**
5. **Verify no other services are using port 8001**

**🔴 "Web interface won't load"**
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

**🔴 "Python virtual environment issues"**
- Ensure Python 3.11+ is installed
- Delete `.venv` folder and re-run setup script
- On Windows, try running PowerShell as Administrator

**🔴 "Agent responses are slow"**
- Check your internet connection (for Google Search features)
- Verify Splunk server performance
- Consider using local Splunk instance for faster responses

**🔴 "API key errors"**
- Ensure you have a valid Google API key configured
- Check that the key has appropriate permissions
- Verify environment variables are set correctly

### Getting Help

1. **Check the logs:**
   ```bash
   # View recent logs
   tail -f logs/ai-sidekick.log
   ```

2. **Restart services:**

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

3. **Reset configuration:**

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

4. **Switch orchestrator modes:**

   #### For macOS/Linux/Unix:
   ```bash
   # Switch to production mode (all agents including DataExplorer)
   ./scripts/lab/switch-orchestrator-mode.sh production

   # Switch to lab mode (IndexAnalyzer focus, no DataExplorer)
   ./scripts/lab/switch-orchestrator-mode.sh lab

   # Check current mode
   ./scripts/lab/switch-orchestrator-mode.sh status
   ```

   #### For Windows:
   ```powershell
   # Switch to production mode (all agents including DataExplorer)
   .\scripts\lab\switch-orchestrator-mode.ps1 production

   # Switch to lab mode (IndexAnalyzer focus, no DataExplorer)
   .\scripts\lab\switch-orchestrator-mode.ps1 lab

   # Check current mode
   .\scripts\lab\switch-orchestrator-mode.ps1 status
   ```

---

## Next Steps

🎉 **Congratulations!** You've successfully set up your personal AI Sidekick for Splunk!

### What You've Accomplished:
- ✅ Deployed a modular AI agent framework
- ✅ Established real-time Splunk integration
- ✅ Experienced multi-agent collaboration
- ✅ Explored advanced search and analysis capabilities

### Continue Your Journey:
- **🔗 Proceed to Lab 2:** [Create Your AI Agent](./create-your-ai-agent.md)
- **🌟 Contribute:** Add your own agents to the framework
- **🚀 Deploy:** Set up for production use in your organization
- **🤝 Connect:** Join our community for support and collaboration

### Resources:
- **GitHub Repository:** https://github.com/desclier/ai-sidekick-for-splunk
- **Documentation:** https://docs.ai-sidekick-for-splunk.com
- **Community:** https://community.ai-sidekick-for-splunk.com
- **Issues/Support:** https://github.com/desclier/ai-sidekick-for-splunk/issues

---

## Feedback

Your feedback helps us improve! Please share:
- What worked well in this lab?
- What was confusing or could be clearer?
- What additional features would you like to see?

**Share feedback:** https://forms.ai-sidekick-for-splunk.com/lab-feedback

---

*Thank you for participating in the AI Sidekick for Splunk lab! 🚀*
